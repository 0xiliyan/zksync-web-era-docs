---
head:
  - - meta
    - name: "twitter:title"
      content: Thirdweb | zkSync Docs
---

# Thirdweb

[Thirdweb](https://thirdweb.com) offers a suite of SDKs and tools designed for developers to easily build, deploy, and manage web3 applications. It provides straightforward access to smart contract functionalities across various blockchains.

This guide covers the basics of getting started with zkSync by using the Thirdweb SDK for JavaScript and TypeScript.

## Installation

To begin using the Thirdweb SDK in your project, first, you need to install the SDK package. Open your terminal and run the following npm command:

```bash
npm install @thirdweb-dev/sdk
```

This command installs the Thirdweb SDK and adds it to your project's dependencies.

## Initial Setup

### Initialization

You must initialize the SDK to interact with Thirdweb's functionalities. You will need a provider that connects to the [zkSync JSON-RPC API](https://docs.zksync.io/build/api.html) endpoint url and optionally, a signer to execute transactions. Below example shows using your wallet private key as signer.

Before initializing the SDK you need to create an [Thirdweb API Secret Key](https://thirdweb.com/create-api-key).

#### Example

```javascript
import { ThirdwebSDK } from "@thirdweb-dev/sdk";

// zkSync Era Sepolia Testnet network RPC URL
const zkSyncRpcUrl = "https://sepolia.era.zksync.dev";

// Your wallet private key
const walletPrivateKey = "yourWalletPrivateKey";

// Initializing the SDK
const sdk = ThirdwebSDK.fromPrivateKey(walletPrivateKey, zkSyncRpcUrl, {
  secretKey: "yourThirdwebSecretKey",
});

console.log("🚀 Thirdweb SDK initialized with wallet private key on zkSync Era Sepolia Testnet");
```

### Interacting with Smart Contracts

Thirdweb SDK simplifies the interaction with smart contracts by providing pre-built contract modules. These modules cover a wide range of use cases like NFTs, marketplaces, and tokens.

#### Deploying a Smart Contract

To deploy a smart contract using Thirdweb, you can use the SDK's deployer functionality. Here's how to deploy a simple ERC-721 NFT contract:

```javascript
const contract = await sdk.deployer.deployNFTCollection({
  name: "My zkSync Era Testnet NFT Collection",
  primary_sale_recipient: "walletAddressOfRecipient",
});

console.log(`NFT Collection deployed on zkSync Era Sepolia Testnet at: ${contract.address}`);
```

#### Interacting with a Deployed Contract

Once you have a contract deployed, you can interact with it directly through the SDK. For instance, to mint an NFT in the collection you deployed:

```javascript
const tx = await contract.nft.mint({
  name: "My First zkSync Testnet NFT",
  description: "This is my first zkSync Testnet NFT!",
  image: "<URL_TO_IMAGE>",
});

console.log("NFT minted on zkSync Era Sepolia Testnet: ", tx);
```
