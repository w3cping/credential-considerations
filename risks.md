# Real-world identity on the web - risks and mitigations

Early DRAFT for discussion - <rbyers@chromium.org> - Sept 8, 2023


## Background

The term real-world identity (RWI) is used here to refer to a credential which is tied to properties of an individual which are difficult to reset or forge, typically because they are backed by a government-issued identity. Unlike traditional federated identity credentials such as social media credentials, a user generally cannot easily create a new RWI credential with values (name, birthdate, etc.) of their choosing. To mitigate privacy concerns, RWI credentials are generally stored in a digital "wallet" designed to blind the credential issuer from knowledge of when and where the credential is being presented (eg. using a driver's license to confirm eligibility to buy alcohol). For many credential issuers (eg. governments) this blinding is a valuable goal, reducing opposition to the wider use of their credentials.

Governments and regulators are starting to issue digital identities for their constituents. In the EU, [eiDAS 2.0](https://digital-strategy.ec.europa.eu/en/policies/eidas-regulation) is a sweeping piece of legislation that mandates by 2024 for every EU member state to make a digital identity wallet available to their citizens and require certain online companies to accept those digital identities for login. In the US and Canada, [multiple jurisdictions](https://www.aamva.org/jurisdiction-data-maps#anchorformdlmap) (i.e. state and provincial DMVs) have implemented mobile driver’s licenses with legislative activity underway in many more.

Digital wallets ("holders") are emerging as mobile applications which rely on a variety of different mechanisms for interfacing with mobile applications and websites ("verifiers"). For example [ISO-18013-7](https://www.iso.org/standard/82772.html) is being developed to enable credentials in the popular [mdoc format](https://en.wikipedia.org/wiki/Mobile_driver%27s_license) to be used online via a custom URL scheme "mdoc://", enabling websites and wallets to communicate directly over an encrypted side channel. In other applications a website may just present a QR code to be scanned by a wallet application, or rely on server-to-server communication channels to perform credential verification in ways that are entirely opaque to browsers and operating systems.

Online use of RWI promises some very real and valuable benefits, including improving the security with which users engage in online government and financial services, and protecting children from content universally considered to be adult-only through anonymous age verification. However, it also poses a unique set of long-term risks which should be considered in the design of such systems.


## Risks

Given that regulations and other forces are likely to cause a steep growth in RWI usage online over the next couple years, it's worth trying to consider what negative consequences could arise from large-scale adoption.


### Erosion of anonymity online

While usage of most government and financial services cannot generally be expected to be done anonymously, there are other tasks online for which anonymity can be valuable such as consuming journalism or organizing opposition to repressive regimes. At the same time, as browsers improve privacy, it's becoming more and more commercially valuable for ad networks to have access to reliable identities. There's some risk that normalizing the use of RWIs in activities such as consuming journalism will ultimately lead to increased tracking and potentially marginalization of those who wish to remain anonymous online by denying them access to such services.

While many wallets and issuers promise to blind issuers from credential usage, government-backed surveillance systems may already rely on overt and covert access to the infrastructure of private companies in order to track their users. Whistleblowers have shown that even democratic societies cannot rely on the assurances of their governments as to how the capabilities available to them may be used in surveillance of citizens.

### Exclusion of minority users

There are many people who prefer not to use the dominant operating systems, for example technical enthusiasts who prefer to build their own Linux environments from source, or [root their Android phones](https://liberda.nl/weblog/trust-no-client/) to ensure they have total control over the devices they own. Such usage patterns are somewhat in conflict with the security guarantees that many credential issuers require prior to provisioning credentials, so a requirement to use such credentials may exclude such users.

In addition, some people are unwilling or unable to rely on government-issued identification. Whether due to being in an at-risk demographic such as the unsheltered, out of a philosophical conviction, or just being too young, a dependence on RWI systems may place these users at risk of increasingly being excluded from larger fractions of online activity.

### Widening the use of high-assurance identity beyond user expectations

When a user has a legitimate need to use their high-assurance identity, there's a risk of that information getting used for scenarios broader than they intended. For example, using a government ID to enable consumption of content not intended for children resulting in a unique identifier being joined to the user's social media profile for the purposes of more effective ad targeting. Additionally, a security breach of a website with legitimate need for RWI could lead to greater consequences for identity theft or the trade of personal user information on the black market.

### Censorship and reduction in access to free information

There's no universal agreement on what constitutes "adult content". One person's educational material may be someone else's "adult content". Well-meaning regulations and technical mechanisms to protect children may also be used to restrict the free flow of information with a particular political agenda. Similarly, content restricted to people who can prove their citizenship or residency in one set of countries or another may further accelerate the fragmention of the web into a "splinternet", with particular implications for regimes who are interested in restricting access to information. 

### Unintended use of identity information by intermediaries

Depending on the mechanisms used for presenting identity, there's a risk of platforms using the information in ways users did not expect or intend. For example, a user using a browser API to sign into the DMV website with their driver's license likely would not expect their driver license details to be used by the browser in targeting ads to them.

### Reduction of user choice through intermediation

Depending on the mechanisms used for presenting identity, there's a risk that user-choice could be impeded by the policies of intermediaries such as operating systems and browsers. For example, through the use of dark patterns, platforms could potentially self-preference for their own identity services.

### Scaled surveilance and covert account takeover

If online accounts are increasingly tied to government real-world identity then are those accounts vulnerable to attack and takeover from any actor who gains access to the government's account signing keys or can otherwise mint government-backed credentials? Will users retain their choice of provider for the root of trust for their online identity? Will all governments protect their security infrastructure adequately, including from external state-sponsored hackers and politically motivated internal actors? Are there governments who will chose to covertly impersonate their citizens online at scale in the name of national security? 

## Potential principals for mitigations

While we should expect the debate around this topic to be very polarizing, the reality is that this is a problem of balancing competing tensions (eg. safety vs. privacy vs. openness). We should expect that any effective balance for society is going to depend on checks and balances to keep the tensions in equilibrium over time. Any rational analysis must acknowledge that we can't possibly know (nevermind agree on) the perfect balance up front. Therefore the best thing we can do now is to design-in the mechanisms which enable checks and balances that society will rely upon to continually keep the tensions in balance. With that in mind, there are some potential principles which may help enable such balance.


### Go slow and learn

Society is likely to better balance the competing tensions over time if deployment is gradual with a feedback loop which enables the design to adapt over time based on how the risks and opportunities play out in practice.


### User transparency and control

The more users can understand exactly what they're agreeing to and how to limit their exposure, the lower the risk of them being surprised or later regretting their choice. 


### Data minimization

Identity systems which are designed to enable collection of only the minimal information necessary to complete a task are less risky than those which supply additional information. For example, a website which requires a copy of the user's full driver's license for access to content universally considered to be adult-only is riskier than one which requests only a cryptographic signature proving the user is in possession of a driver's license with an age over 18 issued by one of a set of trusted authorities. Even better is if the RP is unable to learn which authority issued the credential, such as by having it signed by a trusted intermediary.


### Open dialog with a diversity of constituencies

Working in public via standards bodies such as the W3C and ISO can help in ensuring that a diversity of perspectives are taken into account in the design of any online identity system.


### Frequency minimization

Many of the above risks are greatly increased through the normalization of RWI identity presentment. If users become habituated to presenting their identity (the way they have been in responding to cookie consent dialogs), then there is much greater risk of their identity being used in ways they ultimately regret.

Online RWI identity presentment systems which are designed for relatively rare scenarios (like creating an account for government or financial services) are less risky than those designed for high-frequency operations (like daily signing into a social media product). 


### Ecosystem-wide transparency

Public dialog will be more effective when it's informed by data about real-world deployment. For example, which websites in practice have integrated support for collecting real-world identities and what is the privacy policy and business model of those websites? To what extent are users agreeing to supply their RWI on different websites in practice?


### User choice

Users being able to freely choose different options for presenting their identity helps create a natural check against the potential abuse of power of any one system. For example, a website which allows users to sign-in with their driver's license is less exposed to the above risks if users also have the choice to easily sign in with an email address instead.


### Issuer choice

Credential issuers being able to freely choose different mechanisms for having their credentials presented helps reduce the risk of an abuse of power by holders, verifiers and platforms. For example, an issuer being able to choose between multiple credential formats and wallet technologies reduces the risk of having their goals subverted due to the privacy properties of any single format or wallet application. 


### Verifier choice

Verifiers (relying-party websites) being able to choose from multiple identity systems reduces the risk that those with power in any one system will use that power to work against their goals. For example, a verifier may choose to allow users to confirm their identity both through a direct connection to known wallet applications, or via a platform/browser-provided API which may have some improved user experience properties. This choice ensures the browser and platform must offer a solution that is strictly more attractive to verifiers and issuers than direct connections to wallet applications.  


### The consequences of a failure to act are as valid as those of acting

In complex tradeoffs such as this, intractable debates may lead to inaction, and that inaction may lead to more harm than what many of the choices being debated would have led to. For this reason it's important that actors including governments, credential issuers, wallet applications, operating systems and browsers feel free to act in the best interests of their constituents despite a lack of consensus on the best course of action. Differing and often competing actions are more likely to lead to a better balance for society than the inaction that comes from waiting for total agreement.


# Related sources

- [W3C TAG Ethical web principles](https://www.w3.org/TR/ethical-web-principles/).
- [EFF - Age Verification Mandates Would Undermine Anonymity Online](https://www.eff.org/deeplinks/2023/03/age-verification-mandates-would-undermine-anonymity-online)
