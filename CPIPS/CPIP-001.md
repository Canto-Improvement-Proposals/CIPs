# Contract Secured Revenue
## CIP-001

| CIP | Title                      | Author | Status | Type | Category | Created |
|---  |---                         |---     |---     | ---  | ---      |  ---    | 
| 001 | Contract Secured Revenue   |Zak Cole (@0xzak), Scott Lewis (@scott_lew_is) | Draft | Standards Track | Core | 2022-08-29 


# Simple Summary

A modified version of EIP-1559 that maintains the benefits of transient congestion management and provides a novel economic mechanism that allows contract creators to receive a portion of the gas fees consumed by their contracts within a given block.

This document is a work-in-progress. If you would like to contribute, please submit a pull request in the appropriate repository.

# Abstract

We present a novel economic mechanism which modifies EIP-1559 to distribute a portion of the total base fee (an amount that would otherwise be burnt) to the deployers of the contracts that consume gas within a given block. This provides a protocol-level subsidy for developers and those responsible for attracting significant network activity. Our goal is to implement the CSR protocol with as few changes as possible to the existing EIP-1559 specification while also providing a simple and flexible user experience.

# Specification
The Accountant exists on the protocol layer and should be implemented as a Cosmos SDK module. As these processes will be responsible for maintaining significant portions of the network state, it must be implemented on the consensus-layer.  

On the application layer, the CSR program functions as a series of smart contracts responsible for generating and maintaining a registry of eligible contract addresses. As a contract creator, participation is on an opt-in basis. Should a contract creator choose to deploy a CSR enabled contract, they must integrate support for the CSR Turnstile, described in the section below. Upon deployment of a CSR enabled contract, the contract creator is minted a CSR NFT. This NFT acts as a claim ticket for all future fees accrued. 

## Turnstile
`Turnstile.sol` is a smart contract that registers other smart contracts on behalf of Accountant.

To opt-in to the CSR program and mint the CSR NFT, contract deployment transactions must call the `register` function on `Turnstile.sol` to append the newly deployed contract address to the Accountant’s registry.

The register defaults to minting a new NFT as the `beneficiary` and sending that NFT to `fromAddr`, but the function can be called to assign an existing NFT as the beneficiary or send newly minted NFT to another address.

The `beneficiary` is the NFT to which accrued fees are distributed.

```
turnstile.register(nftID = None, nftRecipient = None)

## not specifying an existing `nftID` as beneficiary triggers the default case of minting a new NFT to `msg.sender`. 

if nftID == None:


    Mint an NFT with the next unused nftID 
    Send the NFT to `nftRecipient` if specified or fromAddr if an nftRecipient is None.
    Add key value pair of (contract address: next available nftID) to registry


else:

## Making an existing NFT the beneficiary of a newly deployed contract


        add a key value pair (contractAddress:nftID) to registry

turnstile.deploy(the smart contract, nftID = None, nftRecipient = None)

## deploy is a helper function that lets devs easily use 
turnstile.register in their deployment transaction.

deploy contract onchain
call turnstile.register(nftID, nftRecipient)


```



## Accountant

When a given transaction is sealed within a block, the protocol parses the transaction data for ‘toAddr` and then finds the nftID beneficiaries, where they exist in the register, and accrues 20% of the burnt base fee to those nftIDs. This fee total is claimable at any time by the owner of the NFT. When the owner withdraws the accrued gas from the burnt `base_fee`, they may specify a withdrawal amount, less than or equal to available balance, defaulting to available balance, and a receiving address that is different from their own address to which the withdrawal amount is sent. If no address is specified when calling withdraw, the owner of the NFT receives the accrued fees. The accrued balance after withdrawal is set to zero.

## Cosmos Data Structures
The Cosmos (client) side stores the following data structure in state:
```protobuf
message CSR {
    // Contracts is the list of all EVM address that are registered to this NFT
    repeated string contracts = 1;
    // The NFT id which this CSR corresponds to
    uint64 id = 2;
    // The total number of transactions for this CSR NFT
    uint64 txs = 3;
    // The cumulative revenue for this CSR NFT
    string revenue = 4 [
        (gogoproto.customtype) = "github.com/cosmos/cosmos-sdk/types.Int",
        (gogoproto.nullable) = false
    ];
}
```

## Cosmos Event Handling
The `x/csr` module (client side) is designed to handle 2 types of state transitions: `Register` and `Assign`. These state-transitions are triggered through a set of methods on the Turnstile smart contract. Each of these methods emits an event that is subsequently parsed in the csr module’s PostTxProcessing hook.

The PostTxProcessing hook implements EvmHooks.PostTxProcessing. The EVM hook allows users to utilize the Turnstile smart contract to register and assign smart contracts to a CSR NFT + distribute transaction fees for contracts that are already registered to some NFT. After each successful EVM transaction, the PostTxProcessing hook will check if any of the events emitted in the tx originate from the Turnstile address. If some event does exist, the event handler will process and update state accordingly. At the very end of the hook, the hook will check if the `To` address in the tx belongs to any NFT currently in state. If so, the fees will be split and distributed to the Turnstile Address / NFT.

```go
func (h Hooks) PostTxProcessing(ctx sdk.Context, msg core.Message, receipt *ethtypes.Receipt) error {
	// Check if the csr module has been enabled
	params := h.k.GetParams(ctx)
	if !params.EnableCsr {
		return nil
	}

	// Check and process turnstile events if applicable
	h.processEvents(ctx, receipt)

	// Grab contract to check which NFT it belongs to
	contract := msg.To()
	if contract == nil {
		return nil
	}

	nftID, foundNFT := h.k.GetNFTByContract(ctx, contract.String())
	if !foundNFT {
		return nil
	}

	csr, found := h.k.GetCSR(ctx, nftID)
	if !found {
		return sdkerrors.Wrapf(ErrNonexistentCSR, "EVMHook::PostTxProcessing the NFT ID was found but the CSR was not.")
	}

	// Calculate fees to be distributed = intFloor(GasUsed * GasPrice * csrShares)
	fee := sdk.NewIntFromUint64(receipt.GasUsed).Mul(sdk.NewIntFromBigInt(msg.GasPrice()))
	csrFee := sdk.NewDecFromInt(fee).Mul(params.CsrShares).TruncateInt()
	evmDenom := h.k.evmKeeper.GetParams(ctx).EvmDenom
	csrFees := sdk.Coins{{Denom: evmDenom, Amount: csrFee}}

	// Send fees from fee collector to module account before distribution
	err := h.k.bankKeeper.SendCoinsFromModuleToModule(ctx, h.k.FeeCollectorName, types.ModuleName, csrFees)
	if err != nil {
		return sdkerrors.Wrapf(ErrFeeDistribution, "EVMHook::PostTxProcessing failed to distribute fees from fee collector to module, %d", err)
	}

	// Get the turnstile which will receive funds for tx fees
	turnstileAddress, found := h.k.GetTurnstile(ctx)
	if !found {
		return sdkerrors.Wrapf(ErrContractDeployments, "Keeper::ProcessEvents the turnstile contract has not been found.")
	}

	// Distribute fees to turnstile contract by NFT ID distributeFees(amount, nftID)
	amount := csrFee.BigInt()
	_, err = h.k.CallMethod(ctx, "distributeFees", contracts.TurnstileContract, types.ModuleAddress, &turnstileAddress, amount, new(big.Int).SetUint64(nftID))
	if err != nil {
		return sdkerrors.Wrapf(ErrFeeDistribution, "EVMHook::PostTxProcessing failed to distribute fees from module account to turnstile, %d", err)
	}

	// Update TX count for this NFT
	csr.Txs += 1
	// Update the cumulative revenue accumulated by this NFT
	csr.Revenue = csr.Revenue.Add(csrFee)

	// Store updated CSR
	h.k.SetCSR(ctx, *csr)

	return nil
}
```
Events are processed as follows:
```go
func (h Hooks) processEvents(ctx sdk.Context, receipt *ethtypes.Receipt) {
	// Get the turnstile address from which state transition events are emitted
	turnstileAddress, found := h.k.GetTurnstile(ctx)
	if !found {
		panic(sdkerrors.Wrapf(ErrContractDeployments, "Keeper::ProcessEvents the turnstile contract has not been found."))
	}

	for _, log := range receipt.Logs {
		if len(log.Topics) == 0 {
			continue
		}

		// Only process events that originate from the Turnstile contract
		eventID := log.Topics[0]
		if log.Address == turnstileAddress {
			event, err := TurnstileContract.EventByID(eventID)
			if err != nil {
				h.k.Logger(ctx).Error(err.Error())
			}

			// switch and process based on the turnstile event type
			switch event.Name {
			case types.TurnstileEventRegister:
				err = h.k.RegisterEvent(ctx, log.Data)
			case types.TurnstileEventUpdate:
				err = h.k.UpdateEvent(ctx, log.Data)
			}
			if err != nil {
				h.k.Logger(ctx).Error(err.Error())
			}
		}
	}
}
```
The code body for how a `Register` event will be handled is below:
```go
func (k Keeper) RegisterEvent(ctx sdk.Context, data []byte) error {
	var event types.RegisterCSREvent
	// Unpack the data
	err := TurnstileContract.UnpackIntoInterface(&event, types.TurnstileEventRegister, data)
	if err != nil {
		return err
	}

	// Validate that the contract entered can be registered
	err = k.ValidateContract(ctx, event.SmartContract)
	if err != nil {
		return err
	}

	// Check that the receiver account exists in the evm store
	if acct := k.evmKeeper.GetAccount(ctx, event.Recipient); acct == nil {
		return sdkerrors.Wrapf(ErrNonexistentAcct, "EventHandler::RegisterEvent: account does not exist: %s", event.Recipient)
	}

	// Check if this token ID has already been registered
	nftID := event.TokenId.Uint64()
	_, found := k.GetCSR(ctx, nftID)
	if found {
		return sdkerrors.Wrapf(ErrDuplicateNFTID, "EventHandler::RegisterEvent: this NFT id has already been registered")
	}

	// Create CSR object and perform stateless validation
	csr := types.NewCSR(
		[]string{event.SmartContract.String()},
		nftID,
	)
	if err := csr.Validate(); err != nil {
		return err
	}

	// Set the CSR in the store
	k.SetCSR(ctx, csr)

	return nil
}
```

# Future Upgrades
Add a split between first called contract and underlying protocols called during the transaction


