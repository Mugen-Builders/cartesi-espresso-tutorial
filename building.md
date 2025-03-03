# Running with a Dev Environment

Dev environment in this guide refers to the **Cartesi Rollups Node v2** and **Espresso Dev Node** running on your local machine.

We have two approaches to run your application in the dev environment:

1. Run your app using Rollups Node v2 [Guide Coming Soon]
2. Run your app using Nonodo [Rapid Prototyping Tool]



## Running app using Rollups Node v2
[Coming Soon] This section will cover building and running your app using Rollups Node v2 in tandem with Espresso Dev Node.

:::note

 Rollups Node v2 is available for testing with a full Testnet environment. You'll need machine snapshot image that can be generated from steps shown below in the Nonodo section. After that, follow the [testnet guide](./testnet.md) to run your app. 

:::

## Running app using Nonodo 

For development and rapid prototyping of your app in your local machine, it is recommended that you use `Nonodo` for simulating Espresso inputs.

With it you can skip a lot of the setup and send EIP-712 messages directly to the node using the `nonce` and `submit` endpoints that will be running on `localhost:8080/nonce` and `localhost:8080/submit`

### Start Nonodo
On your terminal, start **Nonodo** environment using the command:

```bash
nonodo
```

### Build and Run your App

In another terminal tab, create and build a new Cartesi dApp using the following commands:

### 1. **Python**

```bash
cartesi create my-dapp --template python --branch prerelease/sdk-12
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
cartesi create my-dapp --template rust --branch prerelease/sdk-12
cd my-dapp
cartesi build
```

- Run the Cartesi Machine Locally on bare metal using the command;

```bash
cartesi-machine --network --flash-drive=label:root,filename:.cartesi/image.ext2 --env=ROLLUP_HTTP_SERVER_URL=http://10.0.2.2:5004 -- /opt/cartesi/dapp/dapp
```

### 3. **Golang**

```bash
cartesi create my-dapp --template go --branch prerelease/sdk-12
cd my-dapp
cartesi build
```

- Run the Cartesi Machine Locally on bare metal using the command;

```bash
cartesi-machine --network --flash-drive=label:root,filename:.cartesi/image.ext2 --env=ROLLUP_HTTP_SERVER_URL=http://10.0.2.2:5004 -- /opt/cartesi/dapp/dapp
```

### 4. **Javascript**

```bash
cartesi create my-dapp --template javascript --branch prerelease/sdk-12
cd my-dapp
cartesi build
```

- Run the Cartesi Machine Locally on bare metal using the command;

```bash
cartesi-machine --network --flash-drive=label:root,filename:.cartesi/image.ext2 \
--volume=.:/mnt --env=ROLLUP_HTTP_SERVER_URL=http://10.0.2.2:5004 --workdir=/opt/cartesi/dapp -- node index
```

Your app is now ready to receive inputs, you can follow the steps in [send inputs](./interacting.md) section.