# User considerations for credentials on the Web

### Status of this document

An outline of the risks and initial principles for addressing user considerations for high-assurance or real-world identity credentials and their use on the Web.

Editors: 
* [Nick Doty](https://npdoty.name), Center for Democracy & Technology, <ndoty@cdt.org>
* Rick Byers, Google

## Abstract

Many websites, some in response to legal requirements, wish to access a government-issued or other high-assurance identity credential for the user, often to limit access to use of a service to people of a certain age or to confirm a legal identity. Web standards have been proposed to allow sites to request, from a user agent (browser or wallet provider) either an identity credential, or confirmation of some particular property (age, age bracket, institutional affiliation, etc.). These proposals introduce various concerns for the rights of users, including privacy and free expression online.

Separate from whether these technical mechanisms are advisable at all, or advisable for Internet or Web standardization, any proposal should directly consider the impacts on human rights (listed, non-exhaustively, below). A non-exhaustive list of principles to satisfy protection of human rights and known mechanisms to provide those protections is included.

## Background

Governments and regulators are starting to issue digital identities for their constituents. In the EU, [eiDAS 2.0](https://digital-strategy.ec.europa.eu/en/policies/eidas-regulation) is a sweeping piece of legislation that mandates by 2024 for every EU member state to make a digital identity wallet available to their citizens and require certain online companies to accept those digital identities for login. In the US and Canada, [multiple jurisdictions](https://www.aamva.org/jurisdiction-data-maps#anchorformdlmap) (i.e. state and provincial DMVs) have implemented mobile driver’s licenses with legislative activity underway in many more.

Digital wallets ("holders") are emerging as mobile applications which rely on a variety of different mechanisms for interfacing with mobile applications and websites ("verifiers"). For example [ISO-18013-7](https://www.iso.org/standard/82772.html) is being developed to enable credentials in the popular [mdoc format](https://en.wikipedia.org/wiki/Mobile_driver%27s_license) to be used online via a custom URL scheme "mdoc://", enabling websites and wallets to communicate directly over an encrypted side channel. In other applications a website may just present a QR code to be scanned by a wallet application, or rely on server-to-server communication channels to perform credential verification in ways that are entirely opaque to browsers and operating systems.

Online use of RWI promises some very real and valuable benefits, including improving the security with which users engage in online government and financial services, and protecting children from content universally considered to be adult-only through anonymous age verification. However, it also poses a unique set of long-term risks which should be considered in the design of such systems.

## Risks

### Invasions of privacy

There is a real danger of a papers-please web, where anonymous or pseudonymous use of online services becomes heavily restricted, and **surveillance** becomes commonplace.

While usage of some government and financial services cannot always be expected to be done anonymously, there are many tasks online for which anonymity is valuable, such as consuming journalism or political organizing. As browsers improve privacy protections, it's becoming more commercially valuable for ad networks to have access to reliable identities. Normalizing the use of RWIs in online activities could lead to increased tracking and potentially marginalization of those who wish to remain anonymous online by denying them access to such services.

Governmental or corporate surveillance could be facilitated through the presentation of real-world identity credentials, either directly or indirectly through collusion between issuers and verifiers of credentials. Assurances from governments, even in democratic jurisdictions, may not be reliable protections against surveillance of citizens.

Privacy is a complex, contested concept, but here would include privacy _from_ the verifier, privacy from the issuer, and even privacy from the wallet or the browser. 

Depending on the mechanisms used for presenting identity, there's a risk of platforms using the information in ways users did not expect or intend. For example, a user using a browser API to sign into the DMV website with their driver's license likely would not expect their driver license details to be used by the browser in targeting ads to them.

When a user has a legitimate need to use their high-assurance identity, there's a risk of that information getting used for scenarios broader than they intended. For example, using a government ID to enable consumption of content not intended for children resulting in a unique identifier being joined to the user's social media profile for the purposes of more effective ad targeting.

Some privacy-related questions to consider:

* how are identity characteristics shared with origins? (minimization; control)
* what does the identity provider learn about the user's activity?
* do identities or identity properties contribute to linkability of activity between or within sites? 
* when and in what contexts will credentials (or particular credential properties such as age) be requested once available? (see Rigidity and Accountability, below)
* what information does a user have when deciding whether to share credential information? how will information be retained, used, sold or shared? (transparency; control)

### Restrictions of free expression

Access to high-assurance identity credentials presents risks of **discrimination** (either by facilitating intentional explicit discrimination, or through inaccuracies, biases or unequal levels of adoption); and of **exclusion** of people who do not have credentials, don't wish to present them online, or are excluded because of something about them (their age or immigration status, for example).

Some people are unwilling or unable to rely on government-issued identification. Stateless people, refugees, immigrants, unsheltered people and young people all may have difficulty in accessing government-issued credentials. Dependence on RWI systems may place these users at risk of increasingly being excluded from larger fractions of online activity.

There are many people who prefer not to use the dominant operating systems or prefer to ensure they have total control over the devices they own. Such usage patterns may conflict with the security guarantees that many credential issuers will require prior to provisioning credentials, so a requirement to use such credentials may exclude such users.

There's no universal agreement on what constitutes "adult content". One person's educational material may be someone else's "adult content". Well-meaning regulations and technical mechanisms to protect children may also be used to restrict the free flow of information with a particular political agenda. Similarly, content restricted to people who can prove their citizenship or residency in one set of countries or another may further accelerate the fragmention of the web into a "splinternet", with particular implications for regimes who are interested in restricting access to information. 

* who may be excluded from online services by this technology and requirements? 
* who will be discouraged from browsing or communicating by an age or credential requirement? (chilling effects)
* how effective for the specific use cases are age verification or identity attribution presentation technologies? if they aren't fully effective, what is the trade-off between their harms and efficacy?
* what bias may be present? 
* how is remediation handled, when an estimate or presented characteristic is incorrect?
* if age-gating or identity credentials are in use, to what level will they be required, and what are the impacts for people who do not have the technology or credentials, or are unwilling to use them? (discrimination)
* will normal people be required to enroll in these systems?  to present them in certain contexts?
* will a verifier be obliged to offer this form of identification/verification?  will the verifier be able to offer other forms of verification?
* even if not formally mandatory, what social/economic/cultural pressures push in their direction?
* what sort of pushback is available to people who do not participate?

Privacy risks also have free expression implications here: who will be restricted from speaking or accessing information on the Web when there is a risk that a government-issued identity may be linked to that reading or writing?

### Consolidation

Depending on the mechanisms used for presenting identity, there's a risk that user-choice could be impeded by the policies of intermediaries (such as operating systems and browsers), issuers or verifiers. For example, platforms could potentially self-preference their own identity services, or government issuers could restrict 

* to what extent do these systems rely on centralized providers?
* how can an origin reliably accept attestations or credentials from a wide range of providers, rather than just 1 or 2?
* is any part of the system governed by tightly controlled intellectual property, in the form of patents, trade secrets, etc, that would limit the ability of the public to engage with the system without negotiating with the holder of the IP?
* how much does the scheme depend on the user carrying a device or software bundle that is deliberately designed to treat the user themselves as an adversary?
* Is it possible to create a compliant implementation that actually interoperates with the deployed ecosystem, or are their points of cryptographic control that will be used to prohibit interoperability with user-controlled devices?

### Threats to security

If online accounts are increasingly tied to government real-world identity then are those accounts vulnerable to attack and takeover from any actor who gains access to the government's account signing keys or can otherwise mint government-backed credentials? Will users retain their choice of provider for the root of trust for their online identity? Will all governments protect their security infrastructure adequately, including from external state-sponsored hackers and politically motivated internal actors? Are there governments who will chose to covertly impersonate their citizens online at scale in the name of national security? 

A security breach of a website with legitimate need for RWI could lead to greater consequences for identity theft or the trade of personal user information on illicit markets.

## Mitigations

### Process mitigations

#### Go slow and learn

Society is likely to better balance the competing tensions over time if deployment is gradual with a feedback loop which enables the design to adapt over time based on how the risks and opportunities play out in practice.

#### Open dialog with a diversity of constituencies

Working in public via standards bodies such as the W3C and ISO can help in ensuring that a diversity of perspectives are taken into account in the design of any online identity system.

#### Ecosystem-wide transparency

Public dialog will be more effective when it's informed by data about real-world deployment. For example, which websites in practice have integrated support for collecting real-world identities and what is the privacy policy and business model of those websites? To what extent are users agreeing to supply their RWI on different websites in practice?

### System design mitigations

#### Selective disclosure

Rather than complete documents, sites should request and users should present only the particular claims necessary to satisfy a particular intended use. Protocols for issuing, requesting and presenting credentials should facilitate presentation of minimal information.

This is a specific instance of the [basic principles of data minimization](https://w3ctag.github.io/privacy-principles/#data-minimization).

Identity systems which are designed to enable collection of only the minimal information necessary to complete a task are less risky than those which supply additional information. For example, a website which requires a copy of the user's full driver's license for access to content universally considered to be adult-only is riskier than one which requests only a cryptographic signature proving the user is in possession of a driver's license with an age over 18 issued by one of a set of trusted authorities. Even better is if the RP is unable to learn which authority issued the credential, such as by having it signed by a trusted intermediary.

See also: [abstract claims](https://www.w3.org/TR/vc-data-model/#favor-abstract-claims); [predicate proofs](https://www.w3.org/TR/vc-imp-guide/#predicates).

#### Unlinkable presentations

Presenting claims or properties from a credential should not also provide a unique identifier or otherwise facilitate linking of presentation of a claim in different contexts. If presentations are linkable, there is a substantial threat of unwanted cross-context recognition.

In some cases the properties themselves are designed for linkability (like a unique government-issued ID number, or a name or address). But many claims, like age or country are not by themselves **inherently linkable**.

If a credential may be used across multiple origins and contains claims that are not inherently linkable, presentations of those claims should be made unlinkable. Support for other capabilities, such as revocation status, should not make an otherwise unlinkable presentation linkable (see: [Revocation](#revocation-linkability), below). Specifications should define the necessary, testable requirements for presentations to be reasonably unlinkable, and identify all claims that are *inherently linkable*.  

Zero-knowledge proofs may a way to provide a signed proof of a claim from the issuer to the verifier without revealing a linkable signature between two different presentations to different verifiers.

Blind signatures may be a way to provide unlinkability of a presentation between a verifier and the issuer. (The verifier and issuer can confirm that the presented credential was issued by the issuer, but not to which holder it was issued.)

Even when designed for unlinkable presentations and without using any *inherently linkable* claims, presented information may be combined with other characteristics in order to fingerprint or identify a user. Specifications should both minimize and identify these linkability risks, and holder software should provide guidance and protection to users regarding those risks.

#### In-context explanations

Credentials must only be provided when the user chooses to present them. In order for the user to have a genuine choice, the user must have an informed understanding of what they are presenting, for what reason, and the implications of doing so. As with other examples of [asking for permission on the Web](https://github.com/w3cping/adding-permissions), explanations should be provided in the context of the web site and the action the user is taking. Where browsers, wallets and other user agents are all involved in the selection and presentation of credentials, explanations must be clearly and consistently communicated throughout the ceremonial process.

Explanations should describe who is accessing identity credentials, what attributes, capabilities or inferences are accessed, for what purpose the credential is needed, and how data will be used, shared and retained. In order to ensure appropriate use of government-issued high-assurance credentials and to provide [accountability against abuse](#accountability), explanations should also include the justification for the use of credentials, a declaration of that usage and an evaluation or attestation by a reviewing authority.

> Example in-context explanation: "To sign up for this governmental program, Agency X may access, with your permission, your name and identity number in order to confirm your eligibility for the program, as required by Statute Y. This data will be used to confirm your identity, your income level and citizenship status. Data Protection Authority Z has confirmed that this is a legitimate request and that policies and technical mechanisms are in place to assure that your credentials are not used for any other purpose or shared with other parties."

This information should be consistently presented in both plain language and machine-readable format.

Where credentials can be used to recognize people (for example, where presentations are linkable or identifiable credentials are presented), prompts should explicitly indicate the tracking capability, for consumption by user agents and users, but also by researchers and regulators.

This is a specific instance of the [privacy principles of transparency](https://w3ctag.github.io/privacy-principles/#transparency).

#### Voluntary presentation

#### Friction / frequency minimization

Many of the above risks are greatly increased through the normalization of RWI identity presentment. If users become habituated to presenting their identity (the way they have been in responding to cookie consent dialogs), then there is much greater risk of their identity being used in ways they ultimately regret.

Online RWI identity presentment systems which are designed for relatively rare scenarios (like creating an account for government or financial services) are less risky than those designed for high-frequency operations (like daily signing into a social media product). 

#### No phoning home

Issuers should not learn about how, when, or with what verifiers a holder uses their issued credentials.

It's likely that in some significant scenarios the wallet software will be provided by the issuer or by a very limited set of parties who have agreements with the issuer. (This is especially likely in some cases in the US with governmental control, but may apply in other scenarios as well.) So while wallets should be user agents and users should be able to choose and trust them, we should also protect against the threat that a wallet may not be trustworthy or that there may be a particular risk of collusion between wallet software and issuers.

Phoning home may also be a threat if verifiers collude with issuers. In cases of identifiable credentials, this threat cannot be prevented through technical means, but in cases of selective disclosure and unlinkable presentations, it can be.

Phoning home may be a threat if the verifier has some reason to check with the issuer to verify a credential at the time that it is presented; see revocation.

#### Revocation support should not create linkability {#revocation-linkability}

For unlinkable presentations -- especially important for maintaining the privacy protection of selective disclosure -- revocation-checking should not introduce an identifier that is linkable between different origins.

> Example: Some revocation methods, like [Bitstring Status Lists](https://www.w3.org/TR/vc-bitstring-status-list/), should not be used in unlinkable presentations or other presentations with selective disclosure. (See [Unnecessary Correlation](https://w3c.github.io/vc-bitstring-status-list/#unnecessary-correlation).)

#### Extended validity times

For selective disclosure uses, validity, expiry or revocation caching times must be significant, such that neither the holder nor the verifier reveals the pattern of when credentials are used. (Extended validity also enables offline presentation and verification.)

#### Registration of use cases

To limit the large scale abuse of inappropriate solicitation of high assurance government-issued credentials, holders can confirm that the verifier has registered their use case and justification, and had it reviewed by a relevant authority.

> Example: eIDAS regulations require that verifiers register with a national regulator, identifying themseleves, their use case for identity credentials and the specific information they will request from users. Wallets are intended to limit provided information to what is documented in these registrations.
> 
> [EU Digital Identity Reform: The Good, Bad & Ugly in the eIDAS Regulation](https://epicenter.works/en/content/eu-digital-identity-reform-the-good-bad-ugly-in-the-eidas-regulation), see "Use Case Regulation".

#### Reporting abuse

When solicitation of government-issued credentials is, inevitably, done inappropriately, users should have a straightforward means to report abuse.

[Registration](#registration) could include identification of how and where to report abuse, in order to facilitate both technical limitation on access and regulatory oversight.


---

## Additional topics and questions

### Online vs. Offline

* When a presentation/verification event happens, do either the holder or the verifier need to be online (aside from the connectivity *between* the holder and the verifier)?
* If so, who else do they need to communicate with?  What does that party learn about the transaction?
* What happens to the transaction of the remote parties are unavailable?

### Revocation

* how (if ever) are credentials revoked?
* what organizational process governs the revocation?
* what kinds of delays are inherent in revocation?
* What happens to the system when revocation information (or confirmation of non-revocation) is not available?
* To whom is revocation information made available? (Does every service I've authenticated with learn when my driver's license is revoked or my legal name is changed?)


### In-Person Presentation

* While we're talking mainly about web-based transactions, are there opportunities to use the same mechanism for in-person presentation (e.g., proving age during a purchase)?
* What are the protocol differences to be aware of during an in-person presentation?

### Accountability

* how will abuse of credential presentation be mitigated and addressed?
* To the extent that selective disclosure is possible but not always in play (e.g., a system that allows selective disclosure of only year of birth when viewing a tobacco site, but also enables a request for full identity disclosure at a banking site), how does the user know what is being requested of them, and whether it is a reasonable request for the context?
* how does the user (or their agent) know to whom they are disclosing this information?
* how will sites that improperly collect, or use credentials in abusive ways, be held accountable? (these are questions both for user agents and out-of-band accountability mechanisms)
* what kinds of use case regulations do we expect to be placed on these systems (legally/politically)? and what protocol mechanisms will be in place that support such regulations?


### Data Retention

* How will required data retention impact users in the event of a data breach?
* How will data rentention impact legal requests for information related to the purposes of the use case? E.g. Will sites be required to provide information age of users using a service?
* How will data rentention impact legal requests unrelated to the initial use cases? For example, will sites that are required to collect mDLs be subpoena'd and have this information requested for unrelated legal issues that happen on the same site? Example of this with IP addresses (that failed) was https://arstechnica.com/tech-policy/2024/02/reddit-beats-film-industry-again-wont-have-to-reveal-pirates-ip-addresses/

### Alternatives

* how are these use cases being addressed today? will credential and age verification technologies replace those mechanisms, or be used in addition to them?
* what are the alternative, non-credential means to address some of these use cases (including child safety online)?


### Use (and abuse) cases

* age verification
* government services
* account creation / authentication
* data collection / tracking
* rate-limiting, anti-fraud

## Definitions

real-world identity, government-issued identity credential, high-assurance identity credential
: The term real-world identity (RWI) is used here to refer to a credential which is tied to properties of an individual which are difficult to reset or forge, typically because they are backed by a government-issued identity. Unlike traditional federated identity credentials such as social media credentials, a user generally cannot easily create a new RWI credential with values (name, birthdate, etc.) of their choosing. To mitigate privacy concerns, RWI credentials are generally stored in a digital "wallet" designed to blind the credential issuer from knowledge of when and where the credential is being presented (eg. using a driver's license to confirm eligibility to buy alcohol). For many credential issuers (eg. governments) this blinding is a valuable goal, reducing opposition to the wider use of their credentials.

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

- [W3C TAG Ethical web principles](https://www.w3.org/TR/ethical-web-principles/).
- [EFF - Age Verification Mandates Would Undermine Anonymity Online](https://www.eff.org/deeplinks/2023/03/age-verification-mandates-would-undermine-anonymity-online)


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
