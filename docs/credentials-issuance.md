## Module 2: Issue Event Ticket as W3C Verifiable Credential 

Eventi App will issue tickets as digitally verifiable credentials for their consumers who purchased event tickets to enable digital trust.

Credential Issuance Service provides applications with secure methods of issuing and claiming credentials. It implements the [OpenID for Verifiable Credential Issuance - OID4VCI](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html) protocol, which provides the mechanism for Issuers to issue Verifiable Credentials to Affinidi Vault users and obtain the credentials using the OAuth 2.0 authorisation flow.

More Details on Affinidi Credential Issuance Service is available on [Affinidi Documentation](https://docs.affinidi.com/docs/affinidi-elements/credential-issuance/)

## Introduction

We will use the `Eventi` app that we generated in [Module 1](/docs/generate-app.md) and enable Affinidi Credentials Issuance Service to issue Event Tickets as digital verifiable credentials. We will dive into the Credentials Issuance feature to issue tamper-evident digital credentials, enabling trust in digital interactions through the flow of portable trusted data.

## Architecture

![Module 2 Architecture](./images/module2-architecture.png)

## What you will experience?

## Steps to complete application setup

| S.No | Content                                                                                         | Description                                                                     |
| ---- | ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| 1.   | [Install Affinidi Trust Development Kit (TDK)](#1-install-affinidi-trust-development-kit-affinidi-tdk)                               | Import the `Auth provider` and `Issuance Client` packages to easily manage credential issuance                    |
| 2.   | [Setup Credential Issuance Configuration](#2-setup-credential-issuance-configuration) | Select the **issuing wallet** and **supported schemas** for issuing ticket as Verifiable credentials                                    |
| 3.   | [Setup application frontend integration](#3-add-verifiable-credential-issuance-capability-in-the-application)                             | Add `IssueTicketVC()` function inside checkout page for Verifiable Credential issuance                        |
| 4.   | [Bind the event handlers](#4-binding-the-event-handlers)                                       | Link the user actions to issuance flow                            |
| 5.   | [Setup application backend integration ](#5-setup-application-backend-integration-with-affinidi-services)                         | Create API endpoint `/api/issuance/start` to issue Event ticket VC Offer using Affinidi TDK |
| 6.   | [Run & Test the application](#6-run-application)                                                           | Try the app with Affinidi Login & Affinidi Credentials Issuance Configuration   |

> [!IMPORTANT]
> This Module is an extension of the same Eventi App that we worked on for [**Module 1**](/docs/generate-app.md).

<hr/>

### 1. Install Affinidi Trust Development Kit (Affinidi TDK)

Let's continue with the step-by-step guide to enable the Affinidi Credentials Issuance service in the sample App.

Install below Affinidi TDK packages as dependencies on this `Eventi` application for `Affinidi Credentials Issuance Client` and `Affinidi TDK Auth provider`

```sh
npm install @affinidi-tdk/auth-provider @affinidi-tdk/credential-issuance-client
```

> [!IMPORTANT]
> Personal Access Token (PAT) is like a machine user that acts on your behalf to the Affinidi services, which was automatically generated in previous module. If the automatic generation option was not selected in previous module, PAT can be generated manually using [Affinidi CLI](https://docs.affinidi.com/dev-tools/affinidi-cli/manage-token/#affinidi-token-create-token) command.

<hr/>

### 2. Setup Credential Issuance Configuration

- To issue a Verifiable Credential, it is required to setup the **Issuance Configuration** on your project, where you select the **issuing wallet** and **supported schemas** to create a credential offer that the application can issue.

- You can easily do this using the [Affinidi Portal](https://portal.affinidi.com)

   1. Login on [Affinidi Portal](https://portal.affinidi.com)
   
   2. Open the `Wallets` menu under the `Affinidi Elements` section and click on `Create Wallet` with any name (e.g. `MyWallet`) and DID method as `did:key`. This helps to setup Organisational identity for Eventi application that is used to sign the Event Ticket Verfiable Credentials later. 
   
      For more information, refer to the [Wallets documentation](https://docs.affinidi.com/dev-tools/wallets)
   
   3. Go to `Credential Issuance Service` under the `Affinidi Elements` section.
   
   4. Click on `Create Configuration` and set the following fields:
   
      - `Name of configuration` as `myCISConfig`
      - `Issuing Wallet`: Select Wallet Created the previous step
      - `Lifetime of Credential Offer` as `600`
   
   5. Add schemas by clicking on "Add new item" under `Supported Schemas`
   
      **Schema 1** :
      
      - _Schema_ as `Manual Input`,
      - _Credential Type ID_ as `EventTicketVC`
      - _JSON Schema URL_ as `https://schema.affinidi.io/TEventTicketVCV1R0.json`
      - _JSDON-LD Context URL_ as `https://schema.affinidi.io/TEventTicketVCV1R0.jsonld`

      You should expect to see the message _Issuance configuration has been created successfully._ on the Developer portal to confirm the configuration setup is complete.

> [!TIP]
> You can create your own schema using by navigating to `Affinidi Schema Builder` under the `Services` section. For more details on `Schema Builder` refer to [Affinidi documentation](https://docs.affinidi.com/docs/affinidi-elements/schema-builder/).

> [!WARNING]
> Ensure the `NEXT_PUBLIC_CREDENTIAL_TYPE_ID` value in the application's `.env` file matches the _Credential Type ID_.

<hr/>

### 3. Add Verifiable Credential Issuance capability in the application

- On the checkout page, post purchase of the ticket, we are going to issue a ticket as Verifiable Credential.

- Open `src\components\Checkout\index.tsx` and add the below function `IssueTicketVC`(before `handlePay` event handler)

   This function performs the following tasks:
   
   1. Prepares event ticket credential data from the purchased ticket details
   2. Calls Eventi's Application API `/api/issuance/start` (we are going to create this API endpoint in the next step) to issue an **Event Ticket Credential offer URL**
   3. Generates **Affinidi Vault Claim link** from the Offer URL which can be shared with the Affinidi vault.
      

   ```javascript
   //Issue a Event Verifiable Credential by calling Application Backend API
   const IssueTicketVC = async () => {
     setIsLoading(true);
   
     //Prepare Data (the structure should match with Event Ticket VC Schema)
     //TODO - Few attributes are hardcoded, we can get this during login by updating Login PEX to request more information like name/address/phonenumber/dob etc.. https://docs.affinidi.com/docs/affinidi-vault/affinidi-vault-data/personal-information/
     const ticketCredentialData = {
       event: items.map((item: any) => {
         return {
           eventId: item.product.itemid?.toString(),
           name: item.product.name,
           location: item.product.location,
           startDate: item.product.startDate,
           endDate: item.product.endDate,
         };
       })[0],
       ticket: items.map((item: any) => {
         return {
           ticketId: item.product.itemid?.toString(),
           ticketType: item.product.name,
           seat: item.product.description,
         };
       })[0],
       createdAt: new Date(),
       attendeeAtrributes: {
         email: consumer.user.email,
         firstName: consumer.user.givenName || "John",
         lastName: consumer.user.familyName || "Doe",
         dateOfBirth: consumer.user.birthdate || "2010-10-17",
       },
       secrete: date,
     };
   
     //Call API to start VC issuance
     const response = await fetch("/api/issuance/start", {
       method: "POST",
       body: JSON.stringify({
         credentialData: ticketCredentialData,
         credentialTypeId: eventTicketVCTypeID,
         claimMode: StartIssuanceInputClaimModeEnum.FixedHolder,
       }),
       headers: {
         "Content-Type": "application/json",
       },
     });
     if (!response.ok) {
       console.log("Error in issuing credential");
       return;
     }
   
     let dataResponse = await response.json();
     console.log("dataResponse", dataResponse);
   
     setIsLoading(false);
   
     //Generate claim link to affinidi vault from offer URL
     if (dataResponse.credentialOfferUri) {
       const vaultLink = VaultUtils.buildClaimLink(
         dataResponse.credentialOfferUri
       );
       setVaultLink(vaultLink);
       setIssuanceResponse(dataResponse);
     }
     console.log("issuanceResponse", issuanceResponse);
   }
   ```

<hr/>

### 4. Binding the event handlers 

- Call the function `IssueTicketVC()` on the `handlePay` function

- Update `handlePay` event handler function by calling `IssueTicketVC()` which prepares the event ticket VC data and invoke the Affinidi Credentials Issuance Service.

```javascript
  //Event handler on successful payment
  const handlePay = () => {
    //Payment logic here
    ....

    // Call Issuance service
    IssueTicketVC();
  };
```

<hr/>

### 5. Setup Application Backend integration with Affinidi Services

Create API Endpoint `/api/issuance/start` which we have used in `IssueTicketVC()` function

Add the issuance logic in the API Handler `src\pages\api\issuance\start.ts`

```javascript
//Add VC Issuance Logic here
const { credentialTypeId, credentialData, claimMode } =
  issuanceStartSchema.parse(req.body);

const session = await getServerSession(req, res, authOptions);
const holderDid = session?.userId;

//Holder DID is required if Claim mode is FIXED_HOLDER
if (!holderDid && claimMode == StartIssuanceInputClaimModeEnum.FixedHolder) {
  res.status(400).json({
    message: "Holder DID is required in FIXED_HOLDER claim mode",
  });
  return;
}

//Prepare the data for issuance
const apiData: StartIssuanceInput = {
  claimMode,
  ...(holderDid && { holderDid }),
  data: [
    {
      credentialTypeId,
      credentialData: {
        ...credentialData,
      },
    },
  ],
};

//Initialize the Affinidi TDK with Personal Access Token(PAT) details
const authProvider = getAuthProvider();

//Initialise the Affinidi Issuance API Object
const api = new IssuanceApi(
  new Configuration({
    apiKey: authProvider.fetchProjectScopedToken.bind(authProvider),
  })
);

//Start Issuance
const issuanceResponse = await api.startIssuance(projectId, apiData);

// Reading issuance offer
const { credentialOfferUri, txCode, issuanceId, expiresIn } =
  issuanceResponse.data;

res.status(200).json({ credentialOfferUri, txCode, issuanceId, expiresIn });
```

<hr/>

### 6. Run & test the application

Run The application to experience Affinidi Credentials Issuance

Try the App with Affinidi Login & Affinidi Credential Issuance Service, by purchasing an event ticket and redeem the event ticket in your Affinidi Vault.

```sh
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result .

> Congratulations! You’ve experienced how to issue Event ticket as W3C Verifiable Credentials to the user’s Affinidi Vault. The user would now be able to manage and reuse this information without dependency on the Eventi application. In the next module, you’ll dive deeper, on how a relying application like Event access management software can request this digitally signed file from the user directly without reliance on intermediaries using Open Identity protocol (OID4VP) to establish trust that the user is the rightful owner of this ticket. You will also learn how the developer experience is simplified by Affinidi Iota Framework reducing the lines of code and effort required for applciation developers to adopt this emerging technology in their application. 


## Next Module

- [**Module 3: Building Consent-Driven Data Access for Verification**](/docs/iota-framework-verification.md)

## Move to

- [**Module 1: Generating Event Management Application from Affinidi CLI With Affinidi Login**](/docs/generate-app.md)
- [**Homepage**](/README.md)

## More Resources for Advanced Learning

- [Affinidi Documentation](https://docs.affinidi.com/docs/affinidi-elements/credential-issuance/)
- [Affinidi Credential Issuance Service](https://docs.affinidi.com/docs/affinidi-elements/credential-issuance/)
- [Affinidi Schema Builder](https://docs.affinidi.com/docs/affinidi-elements/schema-builder/)
