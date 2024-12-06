# Running on a Testnet

To run Nonodo with a full testnet setup, we must provide:

- The URL of a gateway RPC on Sepolia
- The application’s deployment address on Sepolia
- The URL for accessing Espresso’s testnet
- The Espresso block number from which to start looking for inputs; if absent, Nonodo will start looking at Espresso block 0; in practice, it is often a good idea to query Espresso’s current block height when deploying your application, and use that to appropriately specify this initial block number.

:::warning

Espresso’s testnet (called “Decaf”) only posts commitments to Sepolia, so you should not deploy your application to other testnets such as Optimism Sepolia or Arbitrum Sepolia.

:::

- Register your dApp Address

- To run on the testnet environment you will need a dApp address on the network. For this we prepared a web page where you can resgister an address for your dApp
  https://address.mugen.builders
  In the above link you can connect with your wallet and using you public key generate a **dApp address** that will be used in the command that follows.

- Start **_brunodo_** using the command with the flag with the flag that enables integration with Espresso;

```bash
brunodo \
  --rpc-url https://eth-sepolia.g.alchemy.com/v2/_NNA-xQcIATiYWv_UsRuk7BGLmrbxcvM \
  --contracts-application-address <dapp> \
  --sequencer espresso \
  --espresso-url https://query.decaf.testnet.espresso.network \
  --from-block <blocknumber>
```

## Running the Machine

- In another terminal, create and build a new Cartesi dApp using the following command:

### 1. **Python**

```bash
cartesi create my-dapp --template python
cd my-dapp
cartesi build
```

- Run the Cartesi Machine Locally on bare metal using the command;

```bash
cartesi-machine --network --flash-drive=label:root,filename:.cartesi/image.ext2 \
--volume=.:/mnt --env=ROLLUP_HTTP_SERVER_URL=http://10.0.2.2:5004 --workdir=/mnt -- python dapp.py
```

### 2. **Rust**

```bash
cartesi create my-dapp --template rust
cd my-dapp
cartesi build
```

- Run the Cartesi Machine Locally on bare metal using the command;

```bash
cartesi-machine --network --flash-drive=label:root,filename:.cartesi/image.ext2 --env=ROLLUP_HTTP_SERVER_URL=http://10.0.2.2:5004 -- /opt/cartesi/dapp/dapp
```

### 3. **Golang**

```bash
cartesi create my-dapp --template go
cd my-dapp
cartesi build
```

- Run the Cartesi Machine Locally on bare metal using the command;

```bash
cartesi-machine --network --flash-drive=label:root,filename:.cartesi/image.ext2 --env=ROLLUP_HTTP_SERVER_URL=http://10.0.2.2:5004 -- /opt/cartesi/dapp/dapp
```

### 4. **Javascript**

```bash
cartesi create my-dapp --template javascript
cd my-dapp
cartesi build
```

- Run the Cartesi Machine Locally on bare metal using the command;

```bash
cartesi-machine --network --flash-drive=label:root,filename:.cartesi/image.ext2 \
--volume=.:/mnt --env=ROLLUP_HTTP_SERVER_URL=http://10.0.2.2:5004 --workdir=/opt/cartesi/dapp -- node index
```
