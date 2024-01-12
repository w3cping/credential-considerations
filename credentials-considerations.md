# User considerations for credential presentation on the Web

### Status of this document

An outline of the many concerns related to these areas of work, for discussion starting, and initial principles for addressing user considerations.

Editor: [Nick Doty](https://npdoty.name), <ndoty@cdt.org>

## Abstract

Many websites, some in response to legal requirements, wish to access an issued identity credential for the user, often to limit access to use of a service to people of a certain age or to confirm a legal identity. Web standards have been proposed to allow sites to request, from a user agent (browser or wallet provider) either an identity credential, or confirmation of some particular property (age, age bracket, institutional affiliation, etc.). These proposals introduce various concerns for the rights of users, including privacy and free expression online.

Separate from whether these technical mechanisms are advisable at all, or advisable for Internet or Web standardization, any proposal should directly consider the impacts on human rights (listed, non-exhaustively, below).

## Privacy

* how are identity characteristics shared with origins? (minimization; control)
* what does the identity provider learn about the user's activity?
* do identities or identity properties contribute to linkability of activity between or within sites? 
* when and in what contexts will credentials (or particular credential properties such as age) be requested once available? (see Rigidity and Accountability, below)
* what information does a user have when deciding whether to share credential information? how will information be retained, used, sold or shared? (transparency; control)

There is a real danger of a papers-please web, where anonymous or pseudonymous use of online services becomes heavily restricted, and **surveillance** becomes commonplace.

### Selective disclosure

Rather than complete documents, sites should request and users should present only the particular claims necessary to satisfy a particular intended use. Protocols for issuing, requesting and presenting credentials should facilitate presentation of minimal information.

This is a specific instance of the [basic principles of data minimization](https://w3ctag.github.io/privacy-principles/#data-minimization).

See also: [abstract claims](https://www.w3.org/TR/vc-data-model/#favor-abstract-claims); [predicate proofs](https://www.w3.org/TR/vc-imp-guide/#predicates).

### Unlinkable presentations

### In-context explanations

### Friction

### No phoning home

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

### Reporting abuse

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
* [WICG Identity Credential repo](https://github.com/WICG/identity-credential)
* [Credentials Community Group](https://w3c-ccg.github.io/)

## Acknowledgements

Thanks to reviewers and contributors, including:

* PING
* dkg
