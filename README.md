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
Decentralized Key Management Network with Automations

Big Picture:
Wallets as a service that make it easier to onboard, manage, automate and include external data.

Distributed trust increases resiliency, ease of use, and overall utility.

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

## Lit Protocol Overview

Lit Protocol is a network of decentralized nodes for private key generation, signing and encryption. Through decentralization, we can create reslient applications without a single point of failure. This is similar to how the internet was designed, resilence through decentralization.

## Using Lit for easier web2 to web3 onboarding

- Using Lit Protocol's embedded onboarding gives users the ability to easily integrate web3 wallets without plugins, seed phrases, or complex methods of maintenence. Just sign-in like a regular website. This allows for a safer and easier experience.

- Lit Protocol also allows for Lit Actions, automated methods similar to IFTT (If this, then that) or Zapier. They give wallets logic to automate any abitrary action between web2 and web3. Think of them as middleware to automate wallet. If wallets were browsers, Lit Actions are like javascript to add interactivity to stores of value.

- Lit Actions allows to bring off-chain data into web3, like weather updates, financial data, and more. By linking external data to wallets, value can be allocated based on real world data.

## Lit Protocol From a Techincal Perspective

Lit decentralizes [public key cryptography]() through the use of secure [multi-party computation]() and [threshold signature schemes]() (MPC + TSS). This operates on a When run across a distributed network of nodes called the "Lit Network". The Lit software runs on top of it and supports the secure management of persistent cryptographic keys for signing, encryption, and compute.

This network allows for [Programmable Key Pairs](https://developer.litprotocol.com/v2/pkp/intro/). Programmable Key Pairs are distributed key-pairs that break up a private key and share it across the network. No one node has the complete key. This allows for greater security, resilence and robustness, much like the internet.

Functionally, each Programmable Key Pair is a wallet. The private key lives on the Lit Network. These wallets are called multi party computation (MPC) wallets since using them invovles computation across the entire network.

Wallets essentially are public/private keys, where the approval of assets are confirmed via the "signing" with a private key.

Lit Actions operate on top of the Lit Network. Lit Actions are JavaScript functions which act like permissionless rules which automate the signing using Programmable Key Pair. They can be made immutable by storing them on the InterPlanetary File System (IPFS), a distributed storage network.

## Overall Objective

- We will be integrating Lit Protocol's embedded wallet. This onboarding tutorial that will help you get familar with the basics of Lit Protocol's methods.

- We will be building a UI that can allow for multi-factor authentication using email, phone number, discord and various other forms of social logins. This can be customnized and placed in your application as needed.

- Simply, we will understand how to create a better experience for users that give them the convienence of web2 while being web3.

- From a technical perspective, we will cover an file structure, the basics of TypeScript for those not familar, and testing.

- We will first set up our project, go over TypeScript types, describe Lit Actions types, review their schema (how the data is commonly structured). Then we will use test driven development to create our files. First,We will give a simple overview of testing. Next, we will create the tests, which describes our aims. Our tests will be clear, and have comments in them to further explain.

- Then, we write the code in the appropriate file.

- Our files will be as small as possible, with each one serving to keep the objective as small as possible. This avoids large file sizes, keeps our code clean, and is easier to follow. Additionally, we will use JSDocs standard to comment the code in a clear, simple English.

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

If you have a Mac based machine, add this line of code to your
`.gitignore` file. This will ignore the `.DS_Store` file from when you commit files to github.

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
yarn add @lit-protocol/lit-node-client @lit-protocol/constants @lit-protocol/types @lit-protocol/pkp-ethers @lit-protocol/auth-helpers ethers
```

## Overview of Each Package

### Ethers

`EthersJS` is a library to connect to Ethereum Virtual Machine based networks. Ethereum is a decentralized programmable blockchain network, which allows for the transfer of value through digital assets through a distributed ledger. Like the internet, Ethereum is a public network allowing for anyone to participate and create or use applications built on top of it. These applications are called dApps or decentralzied applications.

`EthersJS` makes it easy to interact with these types of networks via code.

### @lit-protocol/lit-node-client

This package

### @lit-protocol/pkp-ethers

### @lit-protocol/constants

### @lit-protocol/types

See the description of [@lit-protocol/pkp-ethers](https://developer.litprotocol.com/v2/pkp/usage).

With PKPs, you can build secure, customizable MPC wallets that offer intuitive onboarding experiences without the pain of private key management.

The @lit-protocol/pkp-ethers package provides a familiar wallet interface that makes it easy to sign data, send transactions, and handle Ethereum JSON RPC requests using PKPs.

### @lit-protocol/auth-helpers

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
