# CPIP Purpose and Guidelines
## CIP-000

| CIP | Title                      | Author | Status | Type | Category | Created |
|---  |---                         |---     |---     | ---  | ---      |  ---    | 
| 000 | Contract Secured Revenue   |0xjones [@0xjones](https://twitter.com/0xjones) | Draft | Meta | CCIP |2022-05-16 

# What is a CPIP?

The Canto community employs a system called CPIP, which is an abbreviation for Canto Protocol Improvement Proposal. The primary function of this system is to provide a comprehensive report detailing a new feature or change intended for the Canto blockchain. The CPIP should present a clear and concise technical specification of the suggested feature, along with a rationale for its inclusion. The author of a CPIP bears the responsibility of garnering agreement from the community while also documenting any opposing views.

The main objective of CPIPs is to be the primary mode for introducing new features to the Canto blockchain. It is also used for collecting technical feedback from the community and documenting design decisions. Because CPIPs are saved as text files in a versioned repository, their revision history serves as the historical account of the feature proposition.

For individuals who implement the Canto blockchain, CPIPs provide an efficient way of monitoring the development of their implementation. Ideally, every implementation maintainer should enumerate the CPIPs they have implemented, thereby providing users with a convenient way to monitor the status of any given implementation or library.

## Types of CPIPs

There exist three categories of CPIPs which are as follows:

A Standards Track CPIP relates to modifications that affect most or all Canto implementations. These changes may include a revision to the network protocol, an alteration in block or transaction validity rules, proposed application standards, conventions, or any addition that has an impact on the interoperability of applications that use Canto. Standards Track CPIPs consist of a design document, an implementation, and (if necessary) an update to the formal specification. Standards Track CPIPs can be further categorized into the following:

* Core: Enhancements necessitating a consensus fork, such as changes to the consensus algorithm.
* Networking: Comprises proposed improvements to network protocol specifications.
* Interface: Encompasses improvements to client API/RPC specifications and standards, as well as specific language-level standards such as method names and contract ABIs.
* CRC: Application-level standards and conventions, including contract standards such as token standards, name registries, URI schemes, library/package formats, and wallet formats.

2. Meta CPIP: This type of CPIP pertains to a process concerning Canto or proposes a modification to a process. Process CPIPs apply to areas other than the Canto protocol itself and may propose an implementation but not to Canto's codebase. They often require community consensus and are more than recommendations. Examples include procedures, guidelines, changes to the decision-making process, and changes to the tools or environment used in Canto development.
3. Informational CPIP: This type of CPIP describes a design issue or provides general guidelines or information to the Canto community without proposing a new feature. Informational CPIPs do not necessarily represent Canto community consensus or a recommendation, so users and implementers are free to ignore them or follow their advice.

To increase the chances of success, a CPIP should focus on a single key proposal or idea. A change that affects multiple clients or defines a standard for multiple apps to use requires a CPIP, while a change to one client does not. The proposed enhancement must be a clear and complete description that represents a net improvement, with a solid proposed implementation that does not unduly complicate the protocol.

# CPIP Work Flow

## Shepherding a CPIP

To shepherd a CPIP, the parties involved in the process include the champion or CPIP author, the CPIP editors, and the Canto Core Developers. Before writing a formal CPIP, it's recommended to vet the idea with the Canto Protocol Improvement Cluster community on Telegram, and then open a discussion thread on the [Canto Commons forum](https://forum.canto.build/).

Once the idea is vetted, the author's responsibility is to present the idea to reviewers and interested parties through a CPIP and invite feedback. They should assess the interest in the CPIP relative to the work involved in implementing it and how many parties will need to conform to it. Negative community feedback may prevent the CPIP from progressing past the Draft stage.

## Core CPIPs

Core CPIPs are crucial changes that require client implementations to be considered final. Therefore, you must provide an implementation or persuade clients to implement your CPIP. To get client implementers to review your proposal, the best way is to present it on an CantoCoreDevs call. You can request to do so by linking your CPIP in a comment on an CantoCoreDevs agenda GitHub Issue. During CantoCoreDev calls, client implementers can discuss the technical merits of CPIPs, assess what other clients are implementing, and coordinate CPIP implementation for network upgrades. These calls often result in a "rough consensus" around which CPIPs should be implemented, assuming that they are technically sound and not contentious enough to cause a network split.

It is important to note that the CPIPs process and CantoCoreDevs call were not designed to handle non-technical issues, but they often become entangled in them due to the lack of other ways to address them. This puts the burden on client implementers to gauge community sentiment, which hinders the technical coordination function of CPIPs and CantoCoreDevs calls. If you are shepherding a CPIP, you can make the process of building community consensus easier by ensuring that the [Canto Commons forum](https://forum.canto.build/) thread for your CPIP includes or links to as much community discussion as possible and that various stakeholders are well-represented. As the champion, your role is to write the CPIP using the style and format described below, lead the discussions in the appropriate forums, and build community consensus around the idea.

## CPIP Process

The following is the standardization process for all CPIPs in the Canto Protocol:

![CPIP Process](https://github.com/isp/CPIPs/assets/53378653/64bb1d75-790a-4fce-8a25-d4dffc867a30)


Idea - A proposed notion that is in a pre-draft stage and is not currently monitored or recorded within the CPIP Repository.

Draft - The first formally tracked stage of a CPIP in development. A CPIP is merged by a CPIP Editor into the CPIP repository when properly formatted.

Review - Once a Draft CPIP is ready, the CPIP Author marks it as ready for Peer Review, requesting feedback and input from other community members.

Last Call - This is the final review window for a CPIP before it can move to the Final stage. A CPIP editor will assign Last Call status and set a review end date, typically 14 days later. If necessary normative changes are identified during this period, the CPIP will revert to the Review stage.

Final - This CPIP represents the final standard and is considered to be in a state of finality. Any updates to a Final CPIP should be limited to correcting errors or adding non-normative clarifications.

Stagnant - If a CPIP remains inactive for 6 months or longer during any stage of development, it will be moved to the Stagnant stage. However, a CPIP can be resurrected and moved back to its earlier status by the Authors or CPIP Editors. If not resurrected, a proposal may stay forever in this status.

Withdrawn - If the CPIP Author(s) decide to withdraw the proposed CPIP, it will be moved to the Withdrawn stage, and it can no longer be resurrected using the same CPIP number. If the idea is pursued again later, it will be considered a new proposal.

Living - A special status for CPIPs that are designed to be continually updated and not reach a state of finality. This includes most notably CPIPs that deal with Canto Improvement Proposals (CPIPs) and other similar proposals.

# How to make a successful CPIP?

Components of a Successful CPIP for Canto Every CPIP for Canto should include the following components:

Preamble - This section contains metadata about the CPIP, such as the CPIP number, a short descriptive title (limited to 44 characters), a description (limited to 140 characters), and author details in RFC 822 style headers. The title and description should not include the CPIP number.

Abstract - This section provides a technical summary of the CPIP in a concise and human-readable paragraph. It should convey the essence of the specification and enable readers to understand the proposal at a glance.

Motivation (optional) - This section is essential for CPIPs that aim to modify the Canto protocol. It should clearly explain why the current protocol specification is inadequate to address the problem that the CPIP aims to solve. However, it may be omitted if the motivation is evident.

Specification - This section describes the syntax and semantics of any new feature in detail. It should be comprehensive enough to allow for interoperable implementations across all Canto ecosystems.

Rationale - This section elaborates on the specification by explaining the motivation for the design and the reasoning behind specific design decisions. It should also describe alternative designs that were considered and any related work. Additionally, the rationale should address any objections or concerns raised during the CPIP discussions.

Backwards Compatibility (optional) - If the CPIP introduces any backwards incompatibilities, this section should describe them in detail and explain how the author proposes to deal with them.

Test Cases (optional) - For CPIPs that affect consensus changes, this section should contain test cases for implementation. Tests may either be included in the CPIP as data (e.g., input/expected output pairs) or in a separate file in the ../assets/cpip-###/<filename> directory. This section may be omitted for non-Core proposals.

Reference Implementation (optional) - This optional section contains a reference or example implementation that people can use to understand or implement the specification.

Security Considerations - This section is mandatory for all CPIPs and should discuss the security implications and considerations relevant to the proposed change. It should include information important for security discussions, surface risks, and be usable throughout the CPIP's lifecycle. Specifically, it should include security-relevant design decisions, concerns, important discussions, implementation-specific guidance and pitfalls, an outline of threats and risks, and how they are being addressed. CPIPs lacking a "Security Considerations" section will be rejected. An CPIP cannot proceed to the "Final" status without a Security Considerations discussion deemed sufficient by the reviewers.

Copyright Waiver - All CPIPs must be in the public domain, and the copyright waiver must link to the license file and include the following wording: "Copyright and related rights waived via [CC0](../LICENSE.md).

# CPIP Formats and Templates

CPIPs should be composed in [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) format and must adhere to a specified [template](../CPIP-Template.md). The beginning of each CPIP must contain an RFC 822 style header preamble enclosed by three hyphens (---), also known as "front matter" in Jekyll. The headers must be arranged in the following order:

* cpip: the CPIP number, determined by the CPIP editor
* title: a few words that describe the CPIP, not a complete sentence
* description: a single short sentence that summarizes the CPIP
* author: the author's or authors' name(s), username(s), or name(s) and email(s). Details are provided below.
* discussions-to: the URL of the official discussion thread
* status: Draft, Review, Last Call, Final, Stagnant, Withdrawn, or Living
* last-call-deadline: the date on which the last call period ends (optional field, only required when status is Last Call)
* type: Standards Track, Meta, or Informational
* category: Core, Networking, Interface, or CCIP (optional field, only required for Standards Track CPIPs)
* created: the date the CPIP was created, in the format of ISO 8601 (yyyy-mm-dd)
* requires: CPIP number(s) (optional field)
* withdrawal-reason: a sentence explaining why the CPIP was withdrawn (optional field, only required when status is Withdrawn) Headers that allow for lists must separate items with commas. Headers that require dates must always use the format of ISO 8601.

## Author header

The author header contains the names, email addresses, or usernames of the authors or owners of the CPIP. Authors who wish to remain anonymous can use only a username or a first name and a username. The author header value must have the following format:

Random J. User address@dom.ain

or less Random J. User (@username)

or less Random J. User (@username) address@dom.ain

if the email address and/or GitHub username is included, and

Random J. User

if neither the email address nor the GitHub username is given. At least one author should use a GitHub username to receive notifications on change requests and to have the ability to approve or reject them.

## Discussions-to Header

A CPIP should include a Discussions-to header that specifies the URL where the proposal is being discussed. The preferred discussion URL for Canto Protocol Improvement Proposals is a topic on the Canto Protocol Forum.

## Preamble

The type header specifies the type of CPIP, which can be Standards Track, Meta, or Informational. If the track is Standards, please include the subcategory (core, networking, interface, or CRC).

## Category Header

The category header specifies the category of the CPIP. This header is required for standards-track CPIPs only.

## Created Header

The created header records the date that the CPIP was assigned a number. Both headers should be in yyyy-mm-dd format, e.g. 2023-04-13.

## Requires Header

CPIPs may have a requires header, which indicates the CPIP numbers that this CPIP depends on. If such a dependency exists, this field is required. A requires dependency is created when the current CPIP cannot be understood or implemented without a concept or technical element from another CPIP. It's important to note that merely mentioning another CPIP does not necessarily create such a dependency.

# Linking to other CPIPs

To reference other CPIPs within a CPIP, the format CPIP-N should be used, where N is the number of the CPIP being referenced. Each referenced CPIP must be accompanied by a relative markdown link the first time it is referenced and may be accompanied by a link on subsequent references. The link must always be relative to ensure that it works in this GitHub repository, forks of this repository, the main Canto website, and mirrors of the main Canto site. For instance, to link to CPIP-1, the link would be ./cpip-1.md.

When drafting a CPIP for the Canto blockchain, it's crucial to adhere to the guidelines provided. These guidelines cover a wide range of topics, including auxiliary files, transferring ownership, the roles and responsibilities of CPIP editors, and more.

# Auxiliary Files

When including images, diagrams, and other auxiliary files in a CPIP for the Canto blockchain, it is important to follow a specific naming convention. These files should be placed in a subdirectory of the assets folder, named "cpip-N," where "N" represents the CPIP number. When linking to an image in the CPIP, it is crucial to use relative links, such as "../assets/cpip-1/image.png."

# Transferring CPIP Ownership

Ownership of CPIPs may need to be transferred to a new champion in certain situations. It is recommended that the original author remains a co-author of the transferred CPIP, although the final decision lies with the original author. A valid reason for transferring ownership could be that the original author no longer has the time or interest in updating or following through with the CPIP process, or is unreachable. However, transferring ownership due to a disagreement with the CPIP's direction is not advisable. While building consensus around a CPIP is essential, if it is not possible, a competing CPIP can be submitted.

If you are interested in taking over the ownership of a CPIP, you should send a message to both the original author and the CPIP editor. If the original author fails to respond in a timely manner, the CPIP editor will make a unilateral decision.

# CPIP Editors

The current CPIP editors are:

* Person1 (@person1)
* Person2 (@person2)

Responsibilities of a CPIP Editor Each new CPIP requires an editor to perform the following tasks:

* Review the CPIP to ensure that it is technically sound and complete. The ideas must make sense from a technical standpoint, even if they are unlikely to reach the final stage.
* Verify that the title accurately reflects the content of the CPIP.
* Check the CPIP for language errors, such as spelling, grammar, and sentence structure, as well as for GitHub-flavored Markdown and code style.
* If the CPIP is not ready, send it back to the author with specific instructions for revision.
* When the CPIP is ready for the repository, assign it a CPIP number (generally the PR number, but the decision is with the editors), merge the corresponding pull request, and notify the author of the next steps. While many developers with write access to the Canto Protocol codebase write and maintain CPIPs, the CPIP editors monitor CPIP changes and correct any structural, grammatical, spelling, or markup errors they come across. The editors' role is to manage the administrative and editorial aspects of the CPIPs and not to pass judgment on them.

# Writing Guideline

Title:

* Avoid using the word "standard" or any of its variations.
* Do not include the CPIP number in the title field of the preamble.

Description:

* The description field in the preamble should not include the word "standard" or any of its variations.
* Do not include the CPIP number in the description field of the preamble.

CPIP Numbers:

* For CPIPs under the CRC category, use the hyphenated form CRC-X, where X represents the assigned number.
* For CPIPs under any other category, use the hyphenated form CPIP-X, where X represents the assigned number.

RFC 2119 and RFC 8174:

* It is recommended for CPIPs to follow RFC 2119 and RFC 8174 for terminology.
* Include the following statement at the beginning of the Specification section: "The key words "MUST," "MUST NOT," "REQUIRED," "SHALL," "SHALL NOT," "SHOULD," "SHOULD NOT," "RECOMMENDED," "NOT RECOMMENDED," "MAY," and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 and RFC 8174."

Copyright

Copyright and related rights waived via [CC0](../LICENSE.md)


________________________________________________________________________________

**Separate documents/pages**


# Linkable CC0

Creative Commons Legal Code

CC0 1.0 Universal

CREATIVE COMMONS CORPORATION IS NOT A LAW FIRM AND DOES NOT PROVIDE

LEGAL SERVICES. DISTRIBUTION OF THIS DOCUMENT DOES NOT CREATE AN

ATTORNEY-CLIENT RELATIONSHIP. CREATIVE COMMONS PROVIDES THIS

INFORMATION ON AN "AS-IS" BASIS. CREATIVE COMMONS MAKES NO WARRANTIES

REGARDING THE USE OF THIS DOCUMENT OR THE INFORMATION OR WORKS

PROVIDED HEREUNDER, AND DISCLAIMS LIABILITY FOR DAMAGES RESULTING FROM

THE USE OF THIS DOCUMENT OR THE INFORMATION OR WORKS PROVIDED

HEREUNDER.

Statement of Purpose

The laws of most jurisdictions throughout the world automatically confer exclusive Copyright and Related Rights (defined below) upon the creator and subsequent owner(s) (each and all, an “owner”) of an original work of authorship and/or a database (each, a “Work”).

Certain owners wish to permanently relinquish those rights to a Work for the purpose of contributing to a commons of creative, cultural and scientific works (“Commons”) that the public can reliably and without fear of later claims of infringement build upon, modify, incorporate in other works, reuse and redistribute as freely as possible in any form whatsoever and for any purposes, including without limitation commercial purposes. These owners may contribute to the Commons to promote the ideal of a free culture and the further production of creative, cultural and scientific works, or to gain reputation or greater distribution for their Work in part through the use and efforts of others.

For these and/or other purposes and motivations, and without any expectation of additional consideration or compensation, the person associating CC0 with a Work (the “Affirmer”), to the extent that he or she is an owner of Copyright and Related Rights in the Work, voluntarily elects to apply CC0 to the Work and publicly distribute the Work under its terms, with knowledge of his or her Copyright and Related Rights in the Work and the meaning and intended legal effect of CC0 on those rights.

1. Copyright and Related Rights. A Work made available under CC0 may be protected by copyright and related or neighboring rights (“Copyright and Related Rights”). Copyright and Related Rights include, but are not limited to, the following:

i. the right to reproduce, adapt, distribute, perform, display, communicate, and translate a Work; ii. moral rights retained by the original author(s) and/or performer(s); iii. publicity and privacy rights pertaining to a person’s image or likeness depicted in a Work; iv. rights protecting against unfair competition in regards to a Work, subject to the limitations in paragraph 4(a), below; v. rights protecting the extraction, dissemination, use and reuse of data in a Work; vi. database rights (such as those arising under Directive 96/9/EC of the European Parliament and of the Council of 11 March 1996 on the legal protection of databases, and under any national implementation thereof, including any amended or successor version of such directive); and vii. other similar, equivalent or corresponding rights throughout the world based on applicable law or treaty, and any national implementations thereof.

1. Waiver. To the greatest extent permitted by, but not in contravention of, applicable law, Affirmer hereby overtly, fully, permanently, irrevocably and unconditionally waives, abandons, and surrenders all of Affirmer’s Copyright and Related Rights and associated claims and causes of action, whether now known or unknown (including existing as well as future claims and causes of action), in the Work (i) in all territories worldwide, (ii) for the maximum duration provided by applicable law or treaty (including future time extensions), (iii) in any current or future medium and for any number of copies, and (iv) for any purpose whatsoever, including without limitation commercial, advertising or promotional purposes (the “Waiver”). Affirmer makes the Waiver for the benefit of each member of the public at large and to the detriment of Affirmer’s heirs and successors, fully intending that such Waiver shall not be subject to revocation, rescission, cancellation, termination, or any other legal or equitable action to disrupt the quiet enjoyment of the Work by the public as contemplated by Affirmer’s express Statement of Purpose.

2. Public License Fallback. Should any part of the Waiver for any reason be judged legally invalid or ineffective under applicable law, then the Waiver shall be preserved to the maximum extent permitted taking into account Affirmer’s express Statement of Purpose. In addition, to the extent the Waiver is so judged Affirmer hereby grants to each affected person a royalty-free, non transferable, non sublicensable, non exclusive, irrevocable and unconditional license to exercise Affirmer’s Copyright and Related Rights in the Work (i) in all territories worldwide, (ii) for the maximum duration provided by applicable law or treaty (including future time extensions), (iii) in any current or future medium and for any number of copies, and (iv) for any purpose whatsoever, including without limitation commercial, advertising or promotional purposes (the “License”). The License shall be deemed effective as of the date CC0 was applied by Affirmer to the Work. Should any part of the License for any reason be judged legally invalid or ineffective under applicable law, such partial invalidity or ineffectiveness shall not invalidate the remainder of the License, and in such case Affirmer hereby affirms that he or she will not (i) exercise any of his or her remaining Copyright and Related Rights in the Work or (ii) assert any associated claims and causes of action with respect to the Work, in either case contrary to Affirmer’s express Statement of Purpose.

3. Limitations and Disclaimers.

a. No trademark or patent rights held by Affirmer are waived, abandoned, surrendered, licensed or otherwise affected by this document. b. Affirmer offers the Work as-is and makes no representations or warranties of any kind concerning the Work, express, implied, statutory or otherwise, including without limitation warranties of title, merchantability, fitness for a particular purpose, non infringement, or the absence of latent or other defects, accuracy, or the present or absence of errors, whether or not discoverable, all to the greatest extent permissible under applicable law. c. Affirmer disclaims responsibility for clearing rights of other persons that may apply to the Work or any use thereof, including without limitation any person’s Copyright and Related Rights in the Work. Further, Affirmer disclaims responsibility for obtaining any necessary consents, permissions or other rights required for any use of the Work. d. Affirmer understands and acknowledges that Creative Commons is not a party to this document and has no duty or obligation with respect to this CC0 or use of the Work.

# CPIP Template

Header:
Title - The CPIP title is a few words, not a complete sentence

Description - Description is one full (short) sentence

Author - a comma separated list of the author's or authors' name + GitHub username (in parenthesis), or name and email (in angle brackets). Example, FirstName LastName (@GitHubUsername), FirstName LastName <foo@bar.com>, FirstName (@GitHubUsername) and GitHubUsername (@GitHubUsername)

Discussions - URL

Status - Draft

Type - Standards Track, Meta, or Information

Category - Core, Networking, Interface, or ERC

Created - date created on, in ISO 8601 (yyyy-mm-dd) format

Requires - Related CPIP number(s)

## Abstract

## Motivation

## Specification

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 and RFC 8174.

## Rationale

TBD

## Backwards Compatibility

No backward compatibility issues found.

## Test Cases

## Reference Implementation

## Security Considerations

Needs discussion.

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).
	Idea - A proposed notion that is in a pre-draft stage and is not currently monitored or recorded within the CPIP Repository.

Draft - The first formally tracked stage of a CPIP in development. A CPIP is merged by a CPIP Editor into the CPIP repository when properly formatted.

Review - Once a Draft CPIP is ready, the CPIP Author marks it as ready for Peer Review, requesting feedback and input from other community members.

Last Call - This is the final review window for a CPIP before it can move to the Final stage. A CPIP editor will assign Last Call status and set a review end date, typically 14 days later. If necessary normative changes are identified during this period, the CPIP will revert to the Review stage.

Final - This CPIP represents the final standard and is considered to be in a state of finality. Any updates to a Final CPIP should be limited to correcting errors or adding non-normative clarifications.

Stagnant - If a CPIP remains inactive for 6 months or longer during any stage of development, it will be moved to the Stagnant stage. However, a CPIP can be resurrected and moved back to its earlier status by the Authors or CPIP Editors. If not resurrected, a proposal may stay forever in this status.

Withdrawn - If the CPIP Author(s) decide to withdraw the proposed CPIP, it will be moved to the Withdrawn stage, and it can no longer be resurrected using the same CPIP number. If the idea is pursued again later, it will be considered a new proposal.

Living - A special status for CPIPs that are designed to be continually updated and not reach a state of finality. This includes most notably CPIPs that deal with Canto Improvement Proposals (CPIPs) and other similar proposals.

# How to make a successful CPIP?

Components of a Successful CPIP for Canto Every CPIP for Canto should include the following components:

Preamble - This section contains metadata about the CPIP, such as the CPIP number, a short descriptive title (limited to 44 characters), a description (limited to 140 characters), and author details in RFC 822 style headers. The title and description should not include the CPIP number.

Abstract - This section provides a technical summary of the CPIP in a concise and human-readable paragraph. It should convey the essence of the specification and enable readers to understand the proposal at a glance.

Motivation (optional) - This section is essential for CPIPs that aim to modify the Canto protocol. It should clearly explain why the current protocol specification is inadequate to address the problem that the CPIP aims to solve. However, it may be omitted if the motivation is evident.

Specification - This section describes the syntax and semantics of any new feature in detail. It should be comprehensive enough to allow for interoperable implementations across all Canto ecosystems.

Rationale - This section elaborates on the specification by explaining the motivation for the design and the reasoning behind specific design decisions. It should also describe alternative designs that were considered and any related work. Additionally, the rationale should address any objections or concerns raised during the CPIP discussions.

Backwards Compatibility (optional) - If the CPIP introduces any backwards incompatibilities, this section should describe them in detail and explain how the author proposes to deal with them.

Test Cases (optional) - For CPIPs that affect consensus changes, this section should contain test cases for implementation. Tests may either be included in the CPIP as data (e.g., input/expected output pairs) or in a separate file in the ../assets/cpip-###/<filename> directory. This section may be omitted for non-Core proposals.

Reference Implementation (optional) - This optional section contains a reference or example implementation that people can use to understand or implement the specification.

Security Considerations - This section is mandatory for all CPIPs and should discuss the security implications and considerations relevant to the proposed change. It should include information important for security discussions, surface risks, and be usable throughout the CPIP's lifecycle. Specifically, it should include security-relevant design decisions, concerns, important discussions, implementation-specific guidance and pitfalls, an outline of threats and risks, and how they are being addressed. CPIPs lacking a "Security Considerations" section will be rejected. An CPIP cannot proceed to the "Final" status without a Security Considerations discussion deemed sufficient by the reviewers.

Copyright Waiver - All CPIPs must be in the public domain, and the copyright waiver must link to the license file and include the following wording: "Copyright and related rights waived via [CC0](../LICENSE.md).

# CPIP Formats and Templates

CPIPs should be composed in [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) format and must adhere to a specified template. The beginning of each CPIP must contain an RFC 822 style header preamble enclosed by three hyphens (---), also known as "front matter" in Jekyll. The headers must be arranged in the following order:

* cpip: the CPIP number, determined by the CPIP editor
* title: a few words that describe the CPIP, not a complete sentence
* description: a single short sentence that summarizes the CPIP
* author: the author's or authors' name(s), username(s), or name(s) and email(s). Details are provided below.
* discussions-to: the URL of the official discussion thread
* status: Draft, Review, Last Call, Final, Stagnant, Withdrawn, or Living
* last-call-deadline: the date on which the last call period ends (optional field, only required when status is Last Call)
* type: Standards Track, Meta, or Informational
* category: Core, Networking, Interface, or CCIP (optional field, only required for Standards Track CPIPs)
* created: the date the CPIP was created, in the format of ISO 8601 (yyyy-mm-dd)
* requires: CPIP number(s) (optional field)
* withdrawal-reason: a sentence explaining why the CPIP was withdrawn (optional field, only required when status is Withdrawn) Headers that allow for lists must separate items with commas. Headers that require dates must always use the format of ISO 8601.

## Author header

The author header contains the names, email addresses, or usernames of the authors or owners of the CPIP. Authors who wish to remain anonymous can use only a username or a first name and a username. The author header value must have the following format:

Random J. User address@dom.ain

or less Random J. User (@username)

or less Random J. User (@username) address@dom.ain

if the email address and/or GitHub username is included, and

Random J. User

if neither the email address nor the GitHub username is given. At least one author should use a GitHub username to receive notifications on change requests and to have the ability to approve or reject them.

## Discussions-to Header

A CPIP should include a Discussions-to header that specifies the URL where the proposal is being discussed. The preferred discussion URL for Canto Protocol Improvement Proposals is a topic on the Canto Protocol Forum.

## Preamble

The type header specifies the type of CPIP, which can be Standards Track, Meta, or Informational. If the track is Standards, please include the subcategory (core, networking, interface, or CRC).

## Category Header

The category header specifies the category of the CPIP. This header is required for standards-track CPIPs only.

## Created Header

The created header records the date that the CPIP was assigned a number. Both headers should be in yyyy-mm-dd format, e.g. 2023-04-13.

## Requires Header

CPIPs may have a requires header, which indicates the CPIP numbers that this CPIP depends on. If such a dependency exists, this field is required. A requires dependency is created when the current CPIP cannot be understood or implemented without a concept or technical element from another CPIP. It's important to note that merely mentioning another CPIP does not necessarily create such a dependency.

# Linking to other CPIPs

To reference other CPIPs within a CPIP, the format CPIP-N should be used, where N is the number of the CPIP being referenced. Each referenced CPIP must be accompanied by a relative markdown link the first time it is referenced and may be accompanied by a link on subsequent references. The link must always be relative to ensure that it works in this GitHub repository, forks of this repository, the main Canto website, and mirrors of the main Canto site. For instance, to link to CPIP-1, the link would be ./cpip-1.md.

When drafting a CPIP for the Canto blockchain, it's crucial to adhere to the guidelines provided. These guidelines cover a wide range of topics, including auxiliary files, transferring ownership, the roles and responsibilities of CPIP editors, and more.

# Auxiliary Files

When including images, diagrams, and other auxiliary files in a CPIP for the Canto blockchain, it is important to follow a specific naming convention. These files should be placed in a subdirectory of the assets folder, named "cpip-N," where "N" represents the CPIP number. When linking to an image in the CPIP, it is crucial to use relative links, such as "../assets/cpip-1/image.png."

# Transferring CPIP Ownership

Ownership of CPIPs may need to be transferred to a new champion in certain situations. It is recommended that the original author remains a co-author of the transferred CPIP, although the final decision lies with the original author. A valid reason for transferring ownership could be that the original author no longer has the time or interest in updating or following through with the CPIP process, or is unreachable. However, transferring ownership due to a disagreement with the CPIP's direction is not advisable. While building consensus around a CPIP is essential, if it is not possible, a competing CPIP can be submitted.

If you are interested in taking over the ownership of a CPIP, you should send a message to both the original author and the CPIP editor. If the original author fails to respond in a timely manner, the CPIP editor will make a unilateral decision.

# CPIP Editors

The current CPIP editors are:

* Person1 (@person1)
* Person2 (@person2)

Responsibilities of a CPIP Editor Each new CPIP requires an editor to perform the following tasks:

* Review the CPIP to ensure that it is technically sound and complete. The ideas must make sense from a technical standpoint, even if they are unlikely to reach the final stage.
* Verify that the title accurately reflects the content of the CPIP.
* Check the CPIP for language errors, such as spelling, grammar, and sentence structure, as well as for GitHub-flavored Markdown and code style.
* If the CPIP is not ready, send it back to the author with specific instructions for revision.
* When the CPIP is ready for the repository, assign it a CPIP number (generally the PR number, but the decision is with the editors), merge the corresponding pull request, and notify the author of the next steps. While many developers with write access to the Canto Protocol codebase write and maintain CPIPs, the CPIP editors monitor CPIP changes and correct any structural, grammatical, spelling, or markup errors they come across. The editors' role is to manage the administrative and editorial aspects of the CPIPs and not to pass judgment on them.

# Writing Guideline

Title:

* Avoid using the word "standard" or any of its variations.
* Do not include the CPIP number in the title field of the preamble.

Description:

* The description field in the preamble should not include the word "standard" or any of its variations.
* Do not include the CPIP number in the description field of the preamble.

CPIP Numbers:

* For CPIPs under the CRC category, use the hyphenated form CRC-X, where X represents the assigned number.
* For CPIPs under any other category, use the hyphenated form CPIP-X, where X represents the assigned number.

RFC 2119 and RFC 8174:

* It is recommended for CPIPs to follow RFC 2119 and RFC 8174 for terminology.
* Include the following statement at the beginning of the Specification section: "The key words "MUST," "MUST NOT," "REQUIRED," "SHALL," "SHALL NOT," "SHOULD," "SHOULD NOT," "RECOMMENDED," "NOT RECOMMENDED," "MAY," and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 and RFC 8174."

Copyright

Copyright and related rights waived via [CC0](../LICENSE.md)
