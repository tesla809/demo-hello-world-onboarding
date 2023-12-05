# demo-hello-world-onboarding

Onboarding and integrating Lit Protocol

## How to approach

- short files limited to one thing
- keep them to under 20 - 30 lines of code
- name them well
- describe TypeScript overview quickly
- Don't assume much. Just assume they know how to code.
- Have overall objective: integrate Lit as an embedded wallet
- Have estimated time to learn
- Describe TypeScript schemas
- File structure -> where Lit goes -> types / schema overview
  -> describe the flow via tests
  -> connecting to Lit
  -> types for Lit / description
  -> add logic for components

Key Concept:
Decentralized Key Management Network with Automations.

Lit Protocol provides encryption which can be used for access control, digital signatures, and programmable wallets as-a-service.

Big Picture:
Wallets as a service that make it easier to onboard, manage, automate and include external data. Automations allow for purely decentralized back-ends.

Decentralized trust increases resiliency, ease of use, and overall utility.

Emergence of Concepts:  
-> Cryptography -> Public Key Encryption
-> Secure Enclaves -> Multi-Party Computation
-> Threshold Cryptography -> Distributed Key Generation
-> Programmable Key Pairs
-> Multi-Party Comptuation Wallet
-> Chronicle, Ethereum Based Network
-> Lit Actions aka Decentralizaed Automation
-> Decentralized signing, encryption
-> Decentralized authentication
-> Decentralized Back-end -> Decentralized Wallet-as-a-service
This would be great as a picture.

See: https://developer.litprotocol.com/v3/sdk/authentication/session-sigs/auth-methods/overview

## Lit Protocol Overview

Lit Protocol is a network of decentralized nodes for private key generation, signing and encryption. Through decentralization, we can create reslient applications without a single point of failure. This is similar to how the internet was designed, resilence through decentralization.

## Using Lit for easier web2 to web3 onboarding

Using Lit Protocol's embedded onboarding gives users the ability to easily integrate web3 wallets without plugins, seed phrases, or complex methods of maintenence. Just sign-in like a regular website. This allows for a safer and easier experience.

Lit Protocol also allows for Lit Actions, automated methods similar to IFTT (If this, then that) or Zapier. They give wallets logic to automate any abitrary action between web2 and web3. Think of them as middleware to automate wallet. If wallets were browsers, Lit Actions are like JavaScript to add interactivity to stores of value.

Lit Actions allows to bring off-chain data into web3, like weather updates, financial data, and more. By linking external data to wallets, value can be allocated based on real world data.

## Lit Protocol From a Techincal Perspective

Lit decentralizes [public key cryptography](https://developer.litprotocol.com/v3/resources/glossary/#public-key-cryptography) through the use of secure [multi-party computation](https://developer.litprotocol.com/v3/resources/glossary/#multi-party-computation-mpc) and [threshold signature schemes](https://en.wikipedia.org/wiki/Threshold_cryptosystem) (MPC + TSS). This operates on a When run across a distributed network of nodes called the "Lit Network". The Lit software runs on top of it and supports the secure management of persistent cryptographic keys for signing, encryption, and compute.

This network allows for [Programmable Key Pairs](https://developer.litprotocol.com/v2/pkp/intro/). Programmable Key Pairs are distributed key-pairs that break up a private key and share it across the network. No one node has the complete key. This allows for greater security, resilence and robustness, much like the internet.

Functionally, each Programmable Key Pair is a wallet. The private key lives on the Lit Network. These wallets are called multi party computation (MPC) wallets since using them invovles computation across the entire network.

Wallets essentially are public/private keys, where the approval of assets are confirmed via the "signing" with a private key.

Lit Actions operate on top of the Lit Network. Lit Actions are JavaScript functions which act like permissionless rules which automate the signing using Programmable Key Pair. They can be made immutable by storing them on the InterPlanetary File System (IPFS), a distributed storage network.

## Overall Objective

We will be integrating Lit Protocol's embedded wallet. This onboarding tutorial that will help you get familar with the basics of Lit Protocol's methods.

We will be building a UI that can allow for multi-factor authentication using email, phone number, discord and various other forms of social logins. This can be customnized and placed in your application as needed.

Simply, we will understand how to create a better experience for users that give them the convienence of web2 while being web3.

From a technical perspective, we will cover an file structure, the basics of TypeScript for those not familar, and testing.

We will first set up our project, go over TypeScript types, describe Lit Actions types, review their schema (how the data is commonly structured). Then we will use test driven development to create our files. First, ee will give a simple overview of testing. Next, we will create the tests, which describes our aims. Our tests will be clear, and have comments in them to further explain.

Then, we write the code in the appropriate file.

Our files will be as small as possible, with each one serving to keep the objective as small as possible. This avoids large file sizes, keeps our code clean, and is easier to follow. Additionally, we will use JSDocs standard to comment the code in a clear, simple English.

## Pre-Requisites

### Basic Skills

We assume that the developer understands JavaScript, React and the basics of the command line. Familarity with TypeScript is great, however not necessary.

Beyond that, we will cover what is needed to the level of depth that is useful for our goal: creating an multi-factor authentication for an wallet using Lit Protocol.

### Machine Setup

We will assume the developer is working with:

- UNIX based system: Linux or MacOS
- VSCode or your favorite editor
- Node v16 and higher

## Big Picture View - Directory Overview

To get a big picture overview, our file structure will end up looking like this.

[] EDIT THIS AT THE END

```bash
.
├── README.md
├── app
│   └── router.options.ts
├── app.vue
├── assets
│   └── css
│       └── tailwind.css
├── components
│   ├── app-header.vue
│   ├── app-main.vue
│   ├── auto-height-textarea.vue
│   ├── form-input.vue
│   ├── form-select.vue
│   ├── holder.vue
│   ├── issuer.vue
│   └── verifier.vue
├── lit
│   └── lit.ts
├── lit_actions
│   ├── globa.d.ts
│   ├── src
│   │   ├── alwaysverified.action.ts
│   │   ├── main.action.ts
│   │   ├── types.ts
│   │   ├── verify-signature.ts
│   │   ├── verifyzk.action.ts
│   │   └── youtubeviewcount.action.ts
│   ├── test
│   │   ├── alwaysverified.t.action.mjs
│   │   ├── data
│   │   │   └── proof.json
│   │   ├── foo.t.action.mjs
│   │   ├── main.t.action.mjs
│   │   ├── verifyzk.t.action.mjs
│   │   └── youtubeviewcount.t.action.mjs
│   ├── tsconfig.json
│   └── utils.mjs
├── nuxt.config.ts
├── package.json
├── public
│   └── favicon.ico
├── scripts
│   └── mintGrantBurn.ts
├── tailwind.config.js
├── tsconfig.json
├── typechain
│   ├── Airdrop.d.ts
├── usecase
│   ├── Airdrop.json
├── web3
│   ├── hex.ts
│   ├── keepContract.ts
│   └── web3.ts
├── yarn.lock
```

### Project Setup

- For this project we will be using:
  - React, front end UI
  - JavaScript / TypeScript
  - Tailwind.css, styliing
  - Yarn, package manager
  - NodeJS, runtime environment
  - Lit Protocol for embededed wallets

We are using `zsh` as the shell for the command line, however, it is not necessary.

Check your system for NodeJS:

```bash
node -v
```

> :bulb: **_NOTE:_**
> If you do not have NodeJS, you can install `nvm` also known as node version manager. It allows you to install and manage different versions of NodeJS.
> This is handy when working with tooling that requires other versions of NodeJS. You can vist [nvm's github repo](https://github.com/nvm-sh/nvm) to learn more.

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
```

Let's set up our directory. Navigate to an empty directory (folder) in your machine.

```bash
cd Desktop
```

Create a directory to hold your project:

```bash
mkdir lit-protocol
```

Create your React directory with `create-react-app`

```bash
npx create-react-app lit-protocol-embedded-wallet
```

If you have a Mac based machine, add this line of code to your `.gitignore` file. This will ignore the `.DS_Store` file from when you commit files to github.

```bash
# Mac based file system
.DS_Store
```

Create the directory structure. This will be where the files will be placed.

```bash
cd lit-protocol-embedded-wallet
cd src
mkdir components
mkdir tests
mkdir lit
mkdir lit_actions
```

### Installing Packages

Now that we have our directory structure set up, let's install the appropriate packages.

```bash
yarn add @lit-protocol/lit-node-client @lit-protocol/constants @lit-protocol/types @lit-protocol/pkp-ethers @lit-protocol/auth-helpers ethers prettier eslint eslint-config-prettier eslint-config-next eslint @stytch/nextjs
```

## Overview of Each Package

### Ethers

`EthersJS` is a library to connect to Ethereum Virtual Machine based networks. Ethereum is a decentralized programmable blockchain network, which allows for the transfer of value through digital assets through a distributed ledger. Like the internet, Ethereum is a public network allowing for anyone to participate and create or use applications built on top of it. These applications are called dApps or decentralzied applications.

`EthersJS` makes it easy to interact with these types of networks via code.

### @lit-protocol/lit-node-client

This SDK package allows you to connect to the Lit Network. You can learn more about it on the installation section of the [Lit Protocol Docs](https://developer.litprotocol.com/v3/sdk/installation).

### @lit-protocol/pkp-ethers

To write to the blockchain, the `LitContracts` instance must be created with a `ethers.Signer` that is authorized to sign transactions using the PKP.

The `@lit-protocol/pkp-ethers` package provides a convenient class, `PKPEthersWallet`, which can be used as a signer.

### @lit-protocol/lit-auth-client

The `@lit-protocol/lit-auth-client` package allows for Social logins.

It offers users a convenient way to authenticate with Lit Protocol by leveraging their existing social accounts. Currently, Lit Protocol supports Google and Discord OAuth.

### @lit-protocol/auth-helpers

Authentication methods are ways of asigning Programmable Key Pairs (PKP) to a specific account resource. This requires individuals to authenticate before performing operations requiring a PKP.

This is a powerful feature of the Lit network as it means users can sign up for a wallet the same way they sign up for other types of digital resources, thus lowering the barrier to accessing web3 enabled applications.

### @lit-protocol/constants

This [submodule](https://github.com/LIT-Protocol/js-sdk/tree/master/packages/constants) exports various modules, constants, interfaces, enums, errors, utilities that are being used in Lit Protocol.

Constants like various Ethereum virtual machine (EVM) and Cosmos based networks for production and testing.

### @lit-protocol/types

See the description of [@lit-protocol/pkp-ethers](https://developer.litprotocol.com/v2/pkp/usage).

With PKPs, you can build secure, customizable MPC wallets that offer intuitive onboarding experiences without the pain of private key management.

The `@lit-protocol/pkp-ethers` package provides a familiar wallet interface that makes it easy to sign data, send transactions, and handle Ethereum JSON RPC requests using PKPs.

### React

React lets you build user interfaces out of individual pieces called components. Then combine them into entire screens, pages, and apps.

### Tailwind CSS

Tailwind CSS is a utility-first CSS framework for rapidly building custom user interfaces. It is a highly customizable, low-level CSS framework that gives you all of the building blocks you need to build bespoke designs without any annoying opinionated styles you have to fight to override.

### Prettier and ESLint

ESLint helps you find and fix common problems with your JavaScript code.

Prettier is an opinionated code formatter to help structure your code when you save it.

These two tools help you create cleaner and structured code

### @stytch/react @stytch/vanilla-js

Stytch will help us with your authentication and add authenticate Google and Discord.

## Setting up Lit

Let's connect to the network with the following code.

First, let's move to the appropriate folder.

```bash
cd lit
```

Next, let's create the file. This will be written in TypeScript. However, we will describe enough TypeScript and the file to make it understandable.

```bash
touch lit.ts
```

Open the file in your text editor. If you have VSCode, you can run. If the command does not work, follow [these instructions](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line).

```bash
code .
```

## Writing Our Lit Base Code

We start by importing our `@lit-protocol` packages. These will help us connect to the next and authenticate with 3rd party services.

```typescript
// src/lit/lit.ts
// helps us connect to the lit network
import { LitNodeClient } from "@lit-protocol/lit-node-client";
// a submodule with handy constants
import { AuthMethodType, ProviderType } from "@lit-protocol/constants";
// TypeScript type definitions
import {
  AuthCallbackParams,
  AuthMethod,
  GetSessionSigsProps,
  IRelayPKP,
  ProviderOptions,
  SessionSigs,
} from "@lit-protocol/types";
// package to implement social log-ins
import {
  DiscordProvider,
  GoogleProvider,
  EthWalletProvider,
  WebAuthnProvider,
  LitAuthClient,
  OtpProvider,
} from "@lit-protocol/lit-auth-client";
```

Next, we set up the development and production environments. We first add the production or testing code.

[] DOUBLE CHECK THIS TO SEE IF IT WORKS

```typescript
// src/lit/lit.ts
// environment variable

// ...
export const DOMAIN = process.env.NEXT_PUBLIC_PROD_URL || "localhost"; // production URL or localhost
export const ORIGIN =
  process.env.NEXT_PUBLIC_ENV === "production"
    ? `https://${DOMAIN}`
    : `http://${DOMAIN}:3000`;
```

In the root directory of the project, create a `.env` file.

Run the command:

```bash
cd ..
touch .env
```

Then in the `.env` file, add the following:

```bash
# Environment variables.
NEXT_PUBLIC_PROD_URL=YOUR PROD URL
#Development port
NEXT_PUBLIC_ENV=production
```

Now we connect to the network:

```typescript
// src/lit/lit.ts
// client.connect() will return a promise that resolves when you are connected to the Lit Network.
const client = new LitJsSdk.LitNodeClient({
  litNetwork: "cayenne",
});

class Lit {
  private litNodeClient;
  async connect() {
    await client.connect();
    this.litNodeClient = client;
  }
}
export default new Lit();
```

Now, we connect to the authentication client:

```typescript
// src/lit/lit.ts
//  connect to the Authentication Client
export const litAuthClient: LitAuthClient = new LitAuthClient({
  litRelayConfig: {
    // relayUrl: 'http://localhost:3001',
    relayApiKey: "test-api-key",
  },
  litOtpConfig: {
    baseUrl: "https://auth-api.litgateway.com",
    port: "443",
    startRoute: "/api/otp/start",
    checkRoute: "/api/otp/check",
  },
  litNodeClient,
});
```

Next, we create a function that validates which provider we are using for sign-in. The term "Provider" is a design pattern name which allows for the implementation of different services with the same interface.

For those unfamilar with TypeScript, the parameter `provider: string` means that it expects a `string` type, and returns a `boolean` type.

The function returns a `array` that must `.include` the passed through string.

The functions use the `export` keyword, since we will eventually use these in another file and to keep our structure modular.

```typescript
// src/lit/lit.ts
// ...
/**
 * Validate provider
 */
export function isSocialLoginSupported(provider: string): boolean {
  return ["google", "discord"].includes(provider);
}
```

### Authentication

To sign-in an application, we must next authenticate the validity of the user credentials. This is ensure that the user's correct identity.

#### Sign-in Providers Methods

Next, we now create the sign in with Google function. For those unfamilar with TypeScript, `signInWithGoogle` takes in a string called `redirectUri` and returns a `Promise` of type `void`. Types in TypeScript allow for better documentation and error correction prior to runtime to avoid costly errors.

We then create a variable called `googleProvider` from the `LitAuthClient` method on the `@lit-protocol/lit-auth-client"` package. It is of type `GoogleProvider` which means it has properties specific to that implementation of the Provider pattern.

```typescript
// src/lit/lit.ts
/**
 * Redirect to Lit login
 */
export async function signInWithGoogle(redirectUri: string): Promise<void> {
  const googleProvider = litAuthClient.initProvider<GoogleProvider>(
    ProviderType.Google,
    { redirectUri }
  );
  await googleProvider.signIn();
}
```

To sign-in an application, we must next authenticate the validity of the user credentials. This is ensure that the user's correct identity.

To do this, we initalize the `litAuthClient` with the `.initProvider` of type `<GoogleProvider>.

```typescript
// src/lit/lit.ts
/**
 * Get auth method object from redirect
 */
export async function authenticateWithGoogle(
  redirectUri: string
): Promise<AuthMethod | undefined> {
  const googleProvider = litAuthClient.initProvider<GoogleProvider>(
    ProviderType.Google,
    { redirectUri }
  );
  const authMethod = await googleProvider.authenticate();
  return authMethod;
}
```

We then follow the same pattern for the other forms of social login.
The only difference here is the type of provider used. Notice, for this we are using Discord.

```typescript
// src/lit/lit.ts
/**
 * Redirect to Lit login
 */
export async function signInWithDiscord(redirectUri: string): Promise<void> {
  const discordProvider = litAuthClient.initProvider<DiscordProvider>(
    ProviderType.Discord,
    { redirectUri }
  );
  await discordProvider.signIn();
}
```

The logic is the same for the authentication with Discord.

```typescript
/**
 * Get auth method object from redirect
 */
export async function authenticateWithDiscord(
  redirectUri: string
): Promise<AuthMethod | undefined> {
  const discordProvider = litAuthClient.initProvider<DiscordProvider>(
    ProviderType.Discord,
    { redirectUri }
  );
  const authMethod = await discordProvider.authenticate();
  return authMethod;
}
```

Next we authenticate with an Ethereum wallet.

We follow the same pattern here. The inital logic is the same with some small differences. We take two parameters `address?` as a `string`, with `?` making the parameter an optional parameter.

The same with `signMessage?` as with a unnamed function that takes in a `message` in the form of a `string`. The function returns a `Promise` as a `string`. The `authenticateWithEthWallet` itself returns a `Promise` of type `<AuthMethod>` or `undefined` if not exisiting.

Inside the function we are initalizing the `litAuthClient`'s `initProvider` with a type of `<EthWalletProvider>`. It recieves two parameters, `ProviderType.EthWallet` and an object with the where `ORIGIN` indicates the production type and `DOMAIN` the destination site, `localhost` or `URI.`

We follow up by authenticating the wallet and returning that `authMethod`.

```typescript
// src/lit/lit.ts
/**
 * Get auth method object by signing a message with an Ethereum wallet
 */
export async function authenticateWithEthWallet(
  address?: string,
  signMessage?: (message: string) => Promise<string>
): Promise<AuthMethod | undefined> {
  const ethWalletProvider = litAuthClient.initProvider<EthWalletProvider>(
    ProviderType.EthWallet,
    {
      domain: DOMAIN,
      origin: ORIGIN,
    }
  );
  const authMethod = await ethWalletProvider.authenticate({
    address,
    signMessage,
  });
  return authMethod;
}
```

We follow the same logic fo the WebAuth standard, which allows servers to register and authenticate users using public key cryptography instead of a password. You can check the overview of the [WebAuth standard here](https://webauthn.guide/).

```typescript
// src/lit/lit.ts
/**
 * Get auth method object by authenticating with a WebAuthn credential
 */
export async function authenticateWithWebAuthn(): Promise<
  AuthMethod | undefined
> {
  let provider = litAuthClient.getProvider(ProviderType.WebAuthn);
  if (!provider) {
    provider = litAuthClient.initProvider<WebAuthnProvider>(
      ProviderType.WebAuthn
    );
  }
  const authMethod = await provider.authenticate();
  return authMethod;
}
```

This function takes in an email or phone number as a string. The `otpProvider` takes in the provider type of `<OtpProvider>`.

It takes the parameter and `unknown` from `ProviderOptions` constants.

```typescript
// src/lit/lit.ts
//...
/**
 * Send OTP code to user
 */
export async function sendOTPCode(emailOrPhone: string) {
  const otpProvider = litAuthClient.initProvider<OtpProvider>(
    ProviderType.Otp,
    {
      userId: emailOrPhone,
    } as unknown as ProviderOptions
  );
  const status = await otpProvider.sendOtpCode();
  return status;
}
```

Stytch offers options to customize the auth experience in any way you need, like a combination of like Email Magic Links, Embeddable Magic Links, Passwords, OAuth, OTP, TOTP, Mobile Biometrics, Passkeys, WebAuthn, and Web3.

The `authenticateWithStytch` method works like a normal API, where you pass in an `accessToken` and `userId`. The rest of teh code works in a similar fashion to the others.

```typescript
// src/lit/lit.ts
/**
 * Get auth method object by validating Stytch JWT
 */
export async function authenticateWithStytch(
  accessToken: string,
  userId?: string
) {
  const provider = litAuthClient.initProvider(ProviderType.StytchOtp, {
    appId: process.env.NEXT_PUBLIC_STYTCH_PROJECT_ID,
  });
  // @ts-ignore
  const authMethod = await provider?.authenticate({ accessToken, userId });
  return authMethod;
}
```

The pattern is the same for `discordProvider` as it is with `googleProvider`. The only difference is the reference to the provider.

```typescript
// src/lit/lit.ts
/**
 * Get auth method object from redirect
 */
export async function authenticateWithDiscord(
  redirectUri: string
): Promise<AuthMethod | undefined> {
  const discordProvider = litAuthClient.initProvider<DiscordProvider>(
    ProviderType.Discord,
    { redirectUri }
  );
  const authMethod = await discordProvider.authenticate();
  return authMethod;
}
```

In order to authenticate with an Ethereum wallet, we have to consider the `address` and `signedMessage` types.

```typescript
// src/lit/lit.ts
/**
 * Get auth method object by signing a message with an Ethereum wallet
 */
export async function authenticateWithEthWallet(
  address?: string,
  signMessage?: (message: string) => Promise<string>
): Promise<AuthMethod | undefined> {
  const ethWalletProvider = litAuthClient.initProvider<EthWalletProvider>(
    ProviderType.EthWallet,
    {
      domain: DOMAIN,
      origin: ORIGIN,
    }
  );
  const authMethod = await ethWalletProvider.authenticate({
    address,
    signMessage,
  });
  return authMethod;
}
```

Next, we create the authentication methods for the various providers we set up.

```typescript
// src/lit/lit.ts
/**
 * Get auth method object by validating the OTP code
 */
export async function authenticateWithOTP(
  code: string
): Promise<AuthMethod | undefined> {
  const otpProvider = litAuthClient.getProvider(ProviderType.Otp);
  const authMethod = await otpProvider?.authenticate({ code });
  return authMethod;
}
```

Next, we create the authentication methods for the various providers we set up.

```typescript
// src/lit/lit.ts
/**
 * Get auth method object by validating Stytch JWT
 */
export async function authenticateWithStytch(
  accessToken: string,
  userId?: string
) {
  const provider = litAuthClient.initProvider(ProviderType.StytchOtp, {
    appId: process.env.NEXT_PUBLIC_STYTCH_PROJECT_ID,
  });
  // @ts-ignore
  const authMethod = await provider?.authenticate({ accessToken, userId });
  return authMethod;
}
```

Prior to authenticating with WebAuth, we must first register it. To do so, we mint a Programmable Key Pair by sending a valid WebAuthn credential generated by your browser to the Lit Relay server.

Let's highlight the unique aspects of this piece of code. The `registerWebAuthn()` return the a `Promise` of the type `Promise<IRelayPKP>`.

Let's breakdown `<IRelayPKP>`, `I` is shorthand for Interface. An interface in TypeScript is used to "shape" the structure of data and give them a name. This prevents errors related to passing in the wrong types of code.

The `RelayPKP` refers to the relay node operated by Lit Protocol to subsidize the creation of Programmable Key Pairs. These Programmable Key Pairs are used to sign and encrypt arbitrary logic in a decentralized manner and are key part of the network.

The Lit Relay server allows for oAuth or WebAuth to generate a Lit-powered Multi-Party Computation (MPC) wallet, all without a single seed phrase in sight. The Lit Relay Server takes care of the PKP minting request and the linking of the distributed key pair to the service, all in a gasless manner for the end user.

You can learn more about minting a PKP using the [Lit Relayer via the docs](https://developer.litprotocol.com/v3/sdk/wallets/minting/#mint-via-webauthn).

```typescript
/**
 * Register new WebAuthn credential
 */
export async function registerWebAuthn(): Promise<IRelayPKP> {
  const provider = litAuthClient.initProvider<WebAuthnProvider>(
    ProviderType.WebAuthn
  );
  // Register new WebAuthn credential
  const options = await provider.register();

  // Verify registration and mint PKP through relay server
  const txHash = await provider.verifyAndMintPKPThroughRelayer(options);
  const response = await provider.relay.pollRequestUntilTerminalState(txHash);
  if (response.status !== "Succeeded") {
    throw new Error("Minting failed");
  }
  const newPKP: IRelayPKP = {
    tokenId: response.pkpTokenId,
    publicKey: response.pkpPublicKey,
    ethAddress: response.pkpEthAddress,
  };
  return newPKP;
}
```

### Minting PKPs

A Session Key is an encryption and decryption key that is randomly generated to ensure the security of a communications session between a user and another computer or between two computers.

Lit Protocol uses Programmable Key Pairs to create these session keys.

The `getSessionSigs()` function will try to create a session key for you and store it in local storage. You can use any wallet or auth method to generate session signatures with the `getSessionSigs()` function from the Lit SDK.

You can also generate the session key yourself using `generateSessionKeyPair()` function and store it however you like. You can then pass the generated session key to `getSessionSigs()` as the `sessionKey` param.

```typescript
/**
 * Generate session sigs for given params
 */
export async function getSessionSigs({
  pkpPublicKey,
  authMethod,
  sessionSigsParams,
}: {
  pkpPublicKey: string;
  authMethod: AuthMethod;
  sessionSigsParams: GetSessionSigsProps;
}): Promise<SessionSigs> {
  // const provider = getProviderByAuthMethod(authMethod);
  // if (provider) {
  //   const sessionSigs = await provider.getSessionSigs({
  //     pkpPublicKey,
  //     authMethod,
  //     sessionSigsParams,
  //   });
  //   return sessionSigs;
  // } else {
  //   throw new Error(
  //     `Provider not found for auth method type ${authMethod.authMethodType}`
  //   );
  // }
  await litNodeClient.connect();

  const authNeededCallback = async (params: AuthCallbackParams) => {
    const response = await litNodeClient.signSessionKey({
      statement: params.statement,
      authMethods: [authMethod],
      pkpPublicKey: pkpPublicKey,
      expiration: params.expiration,
      resources: params.resources,
      chainId: 1,
    });
    return response.authSig;
  };

  const sessionSigs = await litNodeClient.getSessionSigs({
    ...sessionSigsParams,
    authNeededCallback,
  });

  return sessionSigs;
}
```

Finally, once we minted the Programmable Key Pair and registered it with the WebAuth service.

```typescript
// src/lit/lit.ts
/**
 * Get auth method object by authenticating with a WebAuthn credential
 */
export async function authenticateWithWebAuthn(): Promise<
  AuthMethod | undefined
> {
  let provider = litAuthClient.getProvider(ProviderType.WebAuthn);
  if (!provider) {
    provider = litAuthClient.initProvider<WebAuthnProvider>(
      ProviderType.WebAuthn
    );
  }
  const authMethod = await provider.authenticate();
  return authMethod;
}
```

---

## Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
