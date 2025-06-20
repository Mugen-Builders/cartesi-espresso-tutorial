# Sending inputs to your dApp

## Interacting via the Dev Script

- Sending an input to your Cartesi app that leverages Espresso sequencer is an EIP-712 type input.

You can run the send command of the dev script:

```bash
./dev.sh send -a <app_address> -d <input_data_in_hex> -k <test_private_key>
```

- Sending transactions such as depositing assets(Ether, ERC20, ERC721, etc.) or generic messages through the layer 1 is done in the same way as a regular Cartesi Rollups app. You can use `cast`, the `cartesi cli` or other approaches. You can follow them here in the [docs](https://docs.cartesi.io/cartesi-rollups/1.5/development/send-requests/)

## Interacting via the Frontend Template

We have a demo example available which you can clone, and integrate into the app running on your local machine very easily. You can choose to modify this app to fit and match your ideal implementation and design.
It contains ways to send many types of input including interacting with your Cartesi app via Espresso.

### Installation

- Clone the frontend repo to your local machine:

```bash
git clone https://github.com/lynoferraz/frontend-web-cartesi-v2-rpc
```

- Install the dependencies and run in development mode:

```bash
cd frontend-web-cartesi-v2-rpc
pnpm install
pnpm dev
```

- Open your browser and navigate to the URL where your frontend app is running, you can now interact with your app running on local by signing and sending data to your app via espresso.
- To send data via Espresso, use the _“Send L2 EIP-712 Input”_ form in the Input section.
- If you are running with the testnet, remember to point to Sepolia.

## Interacting via the NPM Package

Interacting with your Cartesi dApp using the `@mugen-builders/client` npm package allows you to send data via EIP-712 or directly using signed inputs. This package simplifies the process of relaying data to Cartesi dApps, providing flexibility to work with both EIP-712 formatted data and standard inputs.
You can check the description of the function in the package's [page](https://www.npmjs.com/package/@mugen-builders/client)

### Installation

- Install the npm package by running the following command:

```bash
npm install @mugen-builders/client@0.1.2-rc1.0
```

### Usage

To integrate the package into the front-end of your dApp, use the `advanceEIP712` and `advanceInput` methods to handle both EIP-712 typed data and simple input data(which goes through the L1). Below is an example implementation:

```javascript
import { advanceInput, advanceEIP712 } from "@mugen-builders/client";

const addInput = async (_input) => {
  const provider = new ethers.providers.Web3Provider(wallet.provider);
  const signer = provider.getSigner();

  // For EIP-712 input
  let espressoInput = await advanceEIP712(
    signer,
    provider,
    dappAddress,
    _input,
    {
      cartesiNodeUrl: "http://localhost:8080",
    }
  );

  // For simple input
  let l1Input = await advanceInput(signer, dappAddress, _input, {
    inputBoxAddress: "0x58Df21fE097d4bE5dCf61e01d9ea3f6B81c2E1dB",
  });
};
```

The return of `advanceEIP712` will be the same as `advanceInput`. Both methods will return lists with reports, notices and vouchers generated from that input, allowing you to interact with your dApp using the provided data.

This simplifies interaction with your dApp, providing an easy way to handle both types of inputs.
