# React Workshop Guide: Master Decentralised User Profiles

Welcome to this 90-minute workshop where React developers will learn how to build secure, consent-driven applications using emerging Open Identity protocols like [OpenID for Verifiable Presentations - OID4VP](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html). These protocols transform how applications access and verify user data.

In this session, you'll work on a real-world use case: **event ticket management**. _The tickets will be issued as digitally signed data, and the relying application will verify them instantly—without needing a trusted intermediary._ The data is tamper-evident, and the open standards-based interfaces give you flexibility and choice in the tools you use.

By the end of this workshop, you'll have a solid understanding of [W3C Decentalised identifiers](https://www.w3.org/TR/did-core/) and [W3C Verifiable Credentials](https://www.w3.org/TR/vc-data-model-1.1/) technologies without blockchain and learn how to integrate them into your React applications to build more secure, user-focused experiences that work seamlessly across digital or physical channels.

For more context, [click here to read more about evolution of digital identity.](/docs/digital-identity-overview.md)

## Workshop Objective

Gain a fundamental understanding of building next-gen applications through Holistic user identity implemented via decentralised identity and W3C Verifiable Credentials. These open standards enable user-controlled, portable data exchange that enhances trust, while helping you as developer:

1. Protect user privacy
2. Enhance data minimization practices
3. Reduce trust establishment costs
4. Foster long-term trusted relationships with users
5. Improve efficiency in entitlement and eligibility checks

## What will you build?

<!--Event Ticket Management with Affinidi Trust Network -->

_If you’re eager to dive in and start building, feel free to skip this section and [get started](/workshop-module-summary) with step-by-step instructions._

You’ll build a simple event ticket management app with Next.js in under 90 minutes, integrating it with new Open Identity protocols. Using the `generate-app` feature of Affinidi CLI, you’ll quickly set up the application’s baseline code, complete with the ticket management workflow and scaffolding for seamless consumer onboarding with passwordless authentication using W3C Verifiable Credentials (VCs) — an open standard for secure, portable, digitally signed data that helps to establish transitive trust - verify once and use it anywhere. No more repeated OTPs or centralised password managers as a start and then you may add more to reduce the time and effort required to enter and verify additional information for consumer onboarding like name, phone number, age, etc.

In this process, you’ll manage user profiles with Affinidi Vault, a secure, user-friendly, confidential storage solution for digital identity data. _Post the workshop, you may try the issuance with other compatible digital identity wallets or vaults that support the same standard._ Think of it as the user's personal safe, built on open standards similar to JWT, XML, and JSON—so it doesn’t rely on any proprietary tech for the shape of the data. The Vault lets users collect, store, and share cryptographically signed data (Verifiable Credentials) in a way that machines can trust. Not only that, the mechanisms for how the data is collected in the Vault and shared from the Vault are built on Open Identity protocols [OID4VCI](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html) and [OID4VP](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html) adding additional flexibility and implementation choice of the information is exchanged between applications and the User's Vault.

For this workshop, Affinidi Vault acts as a decentralised personal data store, allowing users to control and share their identity information seamlessly. As a developer, you can focus on building your app while relying on the Vault for secure, flexible data storage and easy sharing. You’ll issue and verify event tickets as Verifiable Credentials, giving users control over their data—no need for complex systems.

With Affinidi Dev Tools and the Affinidi Trust Network, you’ll be able to integrate Decentralised Identifiers (DID), VCs, OpenId for Verifiable Credentials (OID4VCI), and OpenID for Verifiable Presentations (OID4VP) easily with few lines of code and low effort. These tools simplify credential management, and the Affinidi Iota Framework ensures secure, consent-driven data sharing between ticket holders and verifiers—all with minimal code.

The Affinidi Trust Network handles the complex trust infrastructure built with open standards, so you can focus on building and refining your app, adapting it as needed. This flexibility makes scaling easier and gives you the freedom to evolve your implementation over time.

## What will you learn?

Build React apps with Open Identity protocols, letting users control their data in a decentralized store for secure exchange and trust.

1. **Integrate Affinidi TDK to issue and verify portable digital credentials** easily without relying on intermediaries.
2. **Implement platform-agnostic instant verification** of documents to establish trust for dynamic checks using cryptographic proofs.
3. **How to use Affinidi Dev tools** like Developer Portal and CLI to leverage the interoperable trust infrastructure for productivity gains.

<!--

1. **Affinidi TDK for Decentralised Identity:** Use Affinidi TDK to issue and verify portable digital credentials without relying on central systems.

2. **Platform-Agnostic Credential Verification:** Implement cross-platform verification for instant credential authenticity and dynamic checks.

3. **Affinidi Dev Tools for Open Standards:** Easily integrate Affinidi services like Verifiable Credential Issuance and Verification into applications.
-->

<!--
- How to build a **React application with a decentralised, user-controlled personal data store** (Affinidi Vault) leveraging open standards for data models and secure data exchange enabling user-centric innovation where the application logs into the user—not the other way around.

- How to use the **Affinidi Trust Development Kit** (TDK) to build applications using **open standards for decentralised identity and verifiable credentials**, enabling digital credential issuance and verification creating portable trusted data that avoids phone home scenario.

- How to implement **platform-agnostic verification process** that can instantly confirm the credentials’ authenticity to enable dynamic eligibility checks.

- How **Affinidi Dev tools** make it easy to manage and integrate **open standards** based, managed Affinidi services like Affinidi Credential Issuance, Affindii Credential Verification, Affinidi Iota Framework among others, efficiently into your application to create interoperable data ecosystem.
-->

<!--
  - Three (3) simple steps to **issue attested credentials** to users of your application that are reusable, verifiable and secure against fraud.

  - Three (3) simple steps to **create Verification Requests** for your users to share the attested digital credentials.

  - Three (3) simple steps to **request attested credentials** for your users to prove their entitlements.
-->

## Workshop module summary

The workshop is structured into three key modules and one optional module if you finish early and have time to try out one more scenario of consent-driven data access. Even if you're new to this technology, each module is designed to take just 10-15 minutes. We understand learning something new can feel challenging, and we've made sure to keep the time manageable so you can progress comfortably at your own pace.

- [1: Setup workspace](/docs/generate-app.md)
- [2: Issue Event Ticket as Verifiable Credential](/docs/credentials-issuance.md)
- [3: Building User Consent-Driven Data Access for Instant Verification without intermediary](/docs/iota-framework-verification.md)
- [4: (Optional) Building Consent-Driven Data Access for Hyper-personal Recommendations using Zero Party Data](/docs/iota-framework-recommendation.md)

<!--
By the end of the workshop, you’ll gain practical experience in building user-centric applications leveraging open identity protocols that foster more resilient architectures—free from intermediaries. With Affinidi’s open standards-based tech stack, you can establish trusted relationships through the exchange of tamper-evident data backed by cryptographic proofs. This approach enhances user engagement while defending against misinformation and fraud. Designed to meet modern compliance standards like GDPR and DPDPA, this architecture ensures user control and data security, putting the user at the center.
-->

<!--
## What you will build?

> In this workshop, we’re starting with a [Next.js](https://nextjs.org/) app—so if you’re already familiar with React, you’ll feel right at home. We chose Next.js because it builds on React’s strengths, offering things like server-side rendering, static site generation, and file-based routing. This helps us speed up the development of a real-world-like application for the workshop, which we'll use as the baseline to learn how to integrate open identity protocols. That said, the core learnings here are framework-agnostic. So whether you’re using Next.js or another framework, these concepts about user-centric digital identity, machine-readable data, implementing transitive trust, and working with portable, cryptographically attested data to enhance security and user experience will be just as relevant.

> Next.js is simply used to expedite the workshop learning process, but if you have any suggestions or preferences for other frameworks, we’d love to hear your thoughts in the session feedback!




- [**Module 1: Generating Event Management Application(Eventi) from Affinidi CLI With Affinidi Login**](/docs/generate-app.md): Use the [Affinidi CLI](https://docs.affinidi.com/dev-tools/affinidi-cli/generate-app/) (generate app command) to kickstart your journey with Affinidi Trust Network by generating reference codes for different use-cases using different programming languages, frameworks, and IAM solutions.

  Learn to create secure and user-friendly authentication flows without relying on traditional passwords using [Affinidi Login](https://docs.affinidi.com/docs/affinidi-login/how-affinidi-login-works/)

  - Estimated time to complete the module: **5 min**

- [**Module 2: Issue Event Ticket as Verifiable Credential**](/docs/credentials-issuance.md) Dive into the Credentials Issuance feature to issue tamper-evident digital credentials, enabling trust in digital interactions through the flow of portable trusted data using [Affinidi Credential Issuance Service](/docs/credentials-issuance.md)

  - Estimated time to complete the module: **10 min**

- [**Module 3: Building Consent-Driven Data Access for Verification**](/docs/iota-framework-verification.md): Implement workflows that ensure users have full control over their data, with emphasis on secure and transparent data sharing practices using [Affinidi Iota Framework](/docs/iota-framework-recommendation.md)

  - Estimated time to complete the module: **10 min**

- [**Module 4: (Optional) Building Consent-Driven Data Access for Recommendations**](/docs/iota-framework-recommendation.md): Implement workflows that ensure users have full control over their data, with emphasis on secure and transparent data sharing practices using [Affinidi Iota Framework](/docs/iota-framework-verification.md)
  - Estimated time to complete the module: **5 min**


-->

By the end of these modules, you'll have a comprehensive understanding of how to leverage the developer tools from Affinidi Trust Network (ATN) to build robust, user-centric interoperable applications.

Here is a sneak peek into the consumer experience you will be building in the next 90 minutes, leveraging decentralised identity and verifiable credentials. Let's start with [Module 1: Setup workspace](/docs/generate-app.md).

![Affinidi ATN Workshop](/docs/images/workshop.gif)

> [!WARNING]
> This sample application are provided only as a guide to quickly explore and learn how to integrate the components of Affinidi Trust Network that reduce the effort required to add Open Identity protocols based information exchange into your application. This is NOT a Production-ready implementation. **Please don't deploy this to a production environment.**

## Food for thought

While the use case for the workshop was kept simple, push your imagination to think of how to solve real-world problems with the power of cryptographic trust that can work seamlessly across channels - digital or offline or assisted flows. For example, in Event and ticketing industry, can the use of Identity verification along with proof of ticket ownership reduce ticket fraud? how can one reimagine ticket resales with digital delegation to have audit trail of who sold the ticket to whom? Is there additional value in knowing if the visitor had also been to other events of similar type in the consumer onboarding flow to enable hyper-personal consumer experience based on better understanding of the visitor? Can we use the digital instant verification to improve physical queue management for swags by making it available through an online site where you share the proof of attendance along with your verified address to send the swag directly or engage other partners to scale the swag distribution without worrying about training of the staff or reconciliation?

## Read More

Explore our [documentation](https://docs.affinidi.com/docs/) and [labs](https://docs.affinidi.com/labs/) to learn more about Affinidi Product, Service & Frameworks

## Telemetry

Affinidi collects usage data to improve our products and services. For information on what data we collect and how we use your data, please refer to our [Privacy Notice](https://www.affinidi.com/privacy-notice).

## Feedback, Support, and Community

[Click here](https://github.com/affinidi/eventi-workshop/issues) to create a ticket and we will get on it right away. If you are facing technical or other issues, you can [Contact Support](https://share.hsforms.com/1i-4HKZRXSsmENzXtPdIG4g8oa2v).

## FAQ

### What can I develop?

You are only limited by your imagination! Affinidi Reference Applications are a toolbox with which you can build software apps for personal or commercial use.

### Is there anything I should not develop?

We only provide the tools - how you use them is largely up to you. We have no control over what you develop with our tools - but please use our tools responsibly!

We hope that you would not develop anything that contravenes any applicable laws or regulations. Your projects should also not infringe on Affinidi’s or any third party’s intellectual property (for instance, misusing other parties’ data, code, logos, etc).

### What responsibilities do I have to my end-users?

Please ensure that you have in place your own terms and conditions, privacy policies, and other safeguards to ensure that the projects you build are secure for your end users.

If you are processing personal data, please protect the privacy and other legal rights of your end-users and store their personal or sensitive information securely.

Some of our components would also require you to incorporate our end-user notices into your terms and conditions.

### Do I need to provide you with anything?

From time to time, we may request certain information from you to ensure that you are complying with the [Terms and Conditions](https://www.affinidi.com/terms-conditions).

### Can I share my developer’s account with others?

When you create a developer’s account with us, we will issue you your private login credentials. Please do not share this with anyone else, as you would be responsible for activities that happen under your account. If you have friends who are interested, ask them to sign up – let's build together!

## _Disclaimer_

_Please note that this FAQ is provided for informational purposes only and is not to be considered a legal document. For the legal terms and conditions governing your use of the Affinidi Reference Applications, please refer to our [Terms and Conditions](https://www.affinidi.com/terms-conditions)._
