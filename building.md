# Running with a Dev Environment

Dev environment in this guide refers to the **Cartesi Rollups Node v2** and **Espresso Dev Node** running on your local machine.

We have two approaches to run your application in the dev environment:

1. Run your app using Rollups Node v2 
2. Run your app using Nonodo [Rapid Prototyping Tool]



## Running app using Rollups Node v2
This section will cover building and running your app using Rollups Node v2 in tandem with Espresso Dev Node.

### Create your application template
```bash
cartesi create <my-app-name> --template <language> --branch prerelease/sdk-12
```
You can pick any of the languages supported by Cartesi rollups. Make the changes to the template as per your application requirements.

### Build your application
```bash
cd <my-app-name>
cartesi build
```
If successful, you should see the image snapshot file in the `.cartesi` directory.

### Setup and run Dev Environment

Download the `dev` script and setup the environment:
```bash
curl -fsSL https://raw.githubusercontent.com/prototyp3-dev/node-recipes/feature/v2-alpha/dev.sh -o dev.sh && chmod +x dev.sh && ./dev.sh setup
```

Start development environment (with Espresso sequencer):
```bash
./dev.sh start
```
Deploy the application and the consensus contract:
```
./dev.sh deploy
```
To stop the environment, run:
```
./dev.sh stop
```
You can now interact with your application by sending inputs to the node. Follow the steps in [send inputs](./interacting.md) section.


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