---
head:
  - - meta
    - name: "twitter:title"
      content: Thirdweb | zkSync Docs
---

# Thirdweb

[Thirdweb](https://thirdweb.com) offers a suite of SDKs and tools designed for developers to easily build, deploy, and manage web3 applications. It provides straightforward access to smart contract functionalities across various blockchains.

This guide covers the basics of getting started with zkSync by using the Thirdweb SDK for React.

## Installation

To begin using the Thirdweb SDK in your React project, first, you need to install the SDK package. Open your terminal and run the following npm command:

```bash
npm install @thirdweb-dev/react
```

This command installs the Thirdweb React SDK and adds it to your project's dependencies.

## Initialization

You must initialize the SDK to interact with Thirdweb's functionalities. You will need a provider that wraps your main component and also to specify the active chain (in our case zkSync Sepolia Testnet) as well as Thirdweb Client ID.

In order to set this you need to first [Create Thirdweb Client ID](https://thirdweb.com/create-api-key).

#### Example

```javascript
import { ZksyncSepoliaTestnet } from "@thirdweb-dev/chains";
import { ThirdwebProvider } from "@thirdweb-dev/react";

function AppWithProvider() {
  return (
    <ThirdwebProvider
      activeChain={ZksyncSepoliaTestnet}
      clientId={yourThirdwebClientId}
    >
      <App />
    </ThirdwebProvider>
  );
}
```

## Interacting with a Deployed NFT Collection
Lets say you deploy an [NFT Drop Contract](https://thirdweb.com/thirdweb.eth/DropERC721) from the built-in Thirdweb contracts that you can utilize out of the box.

Once you have your contract address, you can interact with it directly through the React SDK! For instance, to claim a pre-minted NFT in the collection that you just deployed, first we need to import the necessary hooks and connect the user wallet:

```javascript
import { useAddress, useContract, useClaimNFT } from "@thirdweb-dev/react";

const connectedAddress = useAddress();
```

Then all we need to do is load the contract and claim one NFT:

```javascript
const { contract } = useContract(yourDeployedContractAddress);
const { mutate: claimNft } = useClaimNFT(contract);

claimNft({
  to: connectedAddress, 
  quantity: 1,
})
```
