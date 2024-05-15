# User considerations for credential presentation on the Web

### Status of this document

An outline of the many concerns related to these areas of work, for discussion starting, and initial principles for addressing user considerations.

Editor: [Nick Doty](https://npdoty.name), <ndoty@cdt.org>

## Abstract

Many websites, some in response to legal requirements, wish to access an issued identity credential for the user, often to limit access to use of a service to people of a certain age or to confirm a legal identity. Web standards have been proposed to allow sites to request, from a user agent (browser or wallet provider) either an identity credential, or confirmation of some particular property (age, age bracket, institutional affiliation, etc.). These proposals introduce various concerns for the rights of users, including privacy and free expression online.

Separate from whether these technical mechanisms are advisable at all, or advisable for Internet or Web standardization, any proposal should directly consider the impacts on human rights (listed, non-exhaustively, below). A non-exhaustive list of principles to satisfy protection of human rights and known mechanisms to provide those protections is included.

## Privacy

There is a real danger of a papers-please web, where anonymous or pseudonymous use of online services becomes heavily restricted, and **surveillance** becomes commonplace.

* how are identity characteristics shared with origins? (minimization; control)
* what does the identity provider learn about the user's activity?
* do identities or identity properties contribute to linkability of activity between or within sites? 
* when and in what contexts will credentials (or particular credential properties such as age) be requested once available? (see Rigidity and Accountability, below)
* what information does a user have when deciding whether to share credential information? how will information be retained, used, sold or shared? (transparency; control)

Privacy is a complex, contested concept, but here would include privacy _from_ the verifier, privacy from the issuer, and even privacy from the wallet or the browser. 

### Selective disclosure

Rather than complete documents, sites should request and users should present only the particular claims necessary to satisfy a particular intended use. Protocols for issuing, requesting and presenting credentials should facilitate presentation of minimal information.

This is a specific instance of the [basic principles of data minimization](https://w3ctag.github.io/privacy-principles/#data-minimization).

See also: [abstract claims](https://www.w3.org/TR/vc-data-model/#favor-abstract-claims); [predicate proofs](https://www.w3.org/TR/vc-imp-guide/#predicates).

### Unlinkable presentations

Presenting claims or properties from a credential should not also provide a unique identifier or otherwise facilitate linking of presentation of a claim in different contexts. If presentations are linkable, there is a substantial threat of unwanted cross-context recognition.

In some cases the properties themselves are designed for linkability (like a unique government-issued ID number, or a name or address). But many claims, like age or country are not by themselves **inherently linkable**.

For any credential claims that are not inherently linkable from credentials that are designed for usage across multiple origins, presentations should be made unlinkable. Support for other capabilities, such as revocation status, should not make an otherwise unlinkable presentation linkable (see: [Revocation](#revocation-linkability), below). Specifications should define the necessary, testable requirements for presentations to be reasonably unlinkable, and identify all claims that are *inherently linkable*.  

Zero-knowledge proofs may a way to provide a signed proof of a claim from the issuer to the verifier without revealing a linkable signature between two different presentations to different verifiers.

Blind signatures may be a way to provide unlinkability of a presentation between a verifier and the issuer. (The verifier and issuer can confirm that the presented credential was issued by the issuer, but not to which holder it was issued.)

Even when designed for unlinkable presentations and without using any *inherently linkable* claims, presented information may be combined with other characteristics in order to fingerprint or identify a user. Specifications should both minimize and identify these linkability risks, and holder software should provide guidance and protection to users regarding those risks.

### In-context explanations

Credentials must only be provided when the user chooses to present them. In order for the user to have a genuine choice, the user must have an informed understanding of what they are presenting, for what reason, and the implications of doing so. As with other examples of [asking for permission on the Web](https://github.com/w3cping/adding-permissions), explanations should be provided in the context of the web site and the action the user is taking. Where browsers, wallets and other user agents are all involved in the selection and presentation of credentials, explanations must be clearly and consistently communicated throughout the ceremonial process.

Explanations should describe who is accessing identity credentials, what attributes, capabilities or inferences are accessed, for what purpose the credential is needed, and how data will be used, shared and retained. In order to ensure appropriate use of government-issued high-assurance credentials and to provide [accountability against abuse](#accountability), explanations should also include the justification for the use of credentials, a declaration of that usage and an evaluation or attestation by a reviewing authority.

> Example in-context explanation: "To sign up for this governmental program, Agency X may access, with your permission, your name and identity number in order to confirm your eligibility for the program, as required by Statute Y. This data will be used to confirm your identity, your income level and citizenship status. Data Protection Authority Z has confirmed that this is a legitimate request and that policies and technical mechanisms are in place to assure that your credentials are not used for any other purpose or shared with other parties."

This information should be consistently presented in both plain language and machine-readable format.

Where credentials can be used to recognize people (for example, where presentations are linkable or identifiable credentials are presented), prompts should explicitly indicate the tracking capability, for consumption by user agents and users, but also by researchers and regulators.

This is a specific instance of the [privacy principles of transparency](https://w3ctag.github.io/privacy-principles/#transparency).

### Voluntary presentation

### Friction

### No phoning home

Issuers should not learn about how, when, or with what verifiers a holder uses their issued credentials.

It's likely that in some significant scenarios the wallet software will be provided by the issuer or by a very limited set of parties who have agreements with the issuer. (This is especially likely in some cases in the US with governmental control, but may apply in other scenarios as well.) So while wallets should be user agents and users should be able to choose and trust them, we should also protect against the threat that a wallet may not be trustworthy or that there may be a particular risk of collusion between wallet software and issuers.

Phoning home may also be a threat if verifiers collude with issuers. In cases of identifiable credentials, this threat cannot be prevented through technical means, but in cases of selective disclosure and unlinkable presentations, it can be.

Phoning home may be a threat if the verifier has some reason to check with the issuer to verify a credential at the time that it is presented; see revocation.

## Online vs. Offline

* When a presentation/verification event happens, do either the holder or the verifier need to be online (aside from the connectivity *between* the holder and the verifier)?
* If so, who else do they need to communicate with?  What does that party learn about the transaction?
* What happens to the transaction of the remote parties are unavailable?

## Revocation

* how (if ever) are credentials revoked?
* what organizational process governs the revocation?
* what kinds of delays are inherent in revocation?
* What happens to the system when revocation information (or confirmation of non-revocation) is not available?
* To whom is revocation information made available? (Does every service I've authenticated with learn when my driver's license is revoked or my legal name is changed?)

### Revocation support should not create linkability {#revocation-linkability}

For unlinkable presentations -- especially important for maintaining the privacy protection of selective disclosure -- revocation-checking should not introduce an identifier that is linkable between different origins.

> Example: Some revocation methods, like [Bitstring Status Lists](https://www.w3.org/TR/vc-bitstring-status-list/), should not be used in unlinkable presentations or other presentations with selective disclosure. (See [Unnecessary Correlation](https://w3c.github.io/vc-bitstring-status-list/#unnecessary-correlation).)

### Extended validity times

For selective disclosure uses, validity, expiry or revocation caching times must be significant, such that neither the holder nor the verifier reveals the pattern of when credentials are used. (Extended validity also enables offline presentation and verification.)

## In-Person Presentation

* While we're talking mainly about web-based transactions, are there opportunities to use the same mechanism for in-person presentation (e.g., proving age during a purchase)?
* What are the protocol differences to be aware of during an in-person presentation?

## Free expression

* who may be excluded from online services by this technology and requirements? 
* who will be discouraged from browsing or communicating by an age or credential requirement? (chilling effects)

Privacy risks also have free expression implications here: who will be restricted from speaking or accessing information on the Web when there is a risk that a government-issued identity may be linked to that reading or writing?

## Bias and efficacy

* how effective for the specific use cases are age verification or identity attribution presentation technologies? if they aren't fully effective, what is the trade-off between their harms and efficacy?
* what bias may be present? 
* how is remediation handled, when an estimate or presented characteristic is incorrect?

## Rigidity

* if age-gating or identity credentials are in use, to what level will they be required, and what are the impacts for people who do not have the technology or credentials, or are unwilling to use them? (discrimination)
* will normal people be required to enroll in these systems?  to present them in certain contexts?
* will a verifier be obliged to offer this form of identification/verification?  will the verifier be able to offer other forms of verification?
* even if not formally mandatory, what social/economic/cultural pressures push in their direction?
* what sort of pushback is available to people who do not participate?

Access to high-assurance identity credentials presents risks of **discrimination** (either by facilitating intentional explicit discrimination, or through inaccuracies, biases or unequal levels of adoption); and of **exclusion** of people who do not have credentials, don't wish to present them online, or are excluded because of something about them (their age or immigration status, for example).

## Consolidation

* to what extent do these systems rely on centralized providers?
* how can an origin reliably accept attestations or credentials from a wide range of providers, rather than just 1 or 2?
* is any part of the system governed by tightly controlled intellectual property, in the form of patents, trade secrets, etc, that would limit the ability of the public to engage with the system without negotiating with the holder of the IP?
* how much does the scheme depend on the user carrying a device or software bundle that is deliberately designed to treat the user themselves as an adversary?
* Is it possible to create a compliant implementation that actually interoperates with the deployed ecosystem, or are their points of cryptographic control that will be used to prohibit interoperability with user-controlled devices?

## Accountability

* how will abuse of credential presentation be mitigated and addressed?
* To the extent that selective disclosure is possible but not always in play (e.g., a system that allows selective disclosure of only year of birth when viewing a tobacco site, but also enables a request for full identity disclosure at a banking site), how does the user know what is being requested of them, and whether it is a reasonable request for the context?
* how does the user (or their agent) know to whom they are disclosing this information?
* how will sites that improperly collect, or use credentials in abusive ways, be held accountable? (these are questions both for user agents and out-of-band accountability mechanisms)
* what kinds of use case regulations do we expect to be placed on these systems (legally/politically)? and what protocol mechanisms will be in place that support such regulations?

### Registration

To limit the large scale abuse of inappropriate solicitation of high assurance government-issued credentials, holders can confirm that the verifier has registered their use case and justification, and had it reviewed by a relevant authority.

> Example: eIDAS regulations require that verifiers register with a national regulator, identifying themseleves, their use case for identity credentials and the specific information they will request from users. Wallets are intended to limit provided information to what is documented in these registrations.
> 
> [EU Digital Identity Reform: The Good, Bad & Ugly in the eIDAS Regulation](https://epicenter.works/en/content/eu-digital-identity-reform-the-good-bad-ugly-in-the-eidas-regulation), see "Use Case Regulation".

### Reporting abuse

When solicitation of government-issued credentials is, inevitably, done inappropriately, users should have a straightforward means to report abuse.

[Registration](#registration) could include identification of how and where to report abuse, in order to facilitate both technical limitation on access and regulatory oversight.

## Alternatives

* how are these use cases being addressed today? will credential and age verification technologies replace those mechanisms, or be used in addition to them?
* what are the alternative, non-credential means to address some of these use cases (including child safety online)?

---

## Use (and abuse) cases

### age verification

### government services

### account creation / authentication

### data collection / tracking

### rate-limiting, anti-fraud

## Definitions

user, holder

relying site (or origin), verifier

attester, identity provider

remote presentation vs. in-person presentation
: Digital identity mechanisms may be used remotely (presenting to a non-local website being visited on a device) or for in-person presentation (using a mobile device to show a credential to a nearby person or device). Many of these concerns are still applicable, but in-person presentation is a very different context from the browseable web.

## Other resources

ACLU on digital driver's licenses:
https://www.aclu.org/sites/default/files/field_document/20210517-digitallicense.pdf

EFF on privacy and equity in digital identification:
https://www.eff.org/deeplinks/2020/08/digital-identification-must-be-designed-privacy-and-equity-10

CNIL on age verification:
https://www.cnil.fr/en/online-age-verification-balancing-privacy-and-protection-minors

Simone van der Hof on age assurance and the rights of children:
https://blogs.lse.ac.uk/parenting4digitalfuture/2021/11/17/age-assurance/

R Street on the First Amendment right in the US to anonymous use of the Internet:
https://www.rstreet.org/commentary/age-verification-methods-in-their-current-forms-threaten-our-first-amendment-right-to-anonymity/

Rick Byers on risks and mitigations:
https://github.com/w3cping/credential-considerations/blob/main/risks.md

## Standards venues

Relevant work is ongoing in the following, non-exhaustive, list of places:

* [Verifiable Credentials Working Group](https://www.w3.org/2017/vc/WG/)
* [WICG Digital Identities repo](https://github.com/WICG/digital-identities)
* [Credentials Community Group](https://w3c-ccg.github.io/)

## Acknowledgements

Thanks to reviewers and contributors, including:

* PING
* dkg
* ACLU
* EFF 