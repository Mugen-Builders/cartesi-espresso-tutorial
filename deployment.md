# Deploying your application

In the following deployment guide, we'll focus on self-hosted deployment where we'll deploy the node to [fly.io](https://fly.io) and application's smart contracts on Ethereum Sepolia testnet. We'll be using the `dev.sh` script to spreedrun the process.

Deploying a Cartesi app in production requires: 
1. Deployment of the Rollups node infrastructure to a cloud provider
2. Deployment of the smart contracts that defines your application on-chain
3. Registering and hosting the application backend on the Rollups node

:::note

Currently, the Espresso integration support is limited to Ethereum Sepolia testnet and Ethereum Mainnet.

:::



### Prerequisites
You should have a [fly.io account](https://fly.io/) and [fly CLI](https://fly.io/docs/flyctl/install/) installed to follow these steps. 

### Step:01  Deploy the node to fly.io
Go to the directory containing your project. You should create a `.env.<testnet>` file with:

```shell
CARTESI_LOG_LEVEL=info
CARTESI_AUTH_KIND=private_key
CARTESI_CONTRACTS_INPUT_BOX_ADDRESS=0xc70074BDD26d8cF983Ca6A5b89b8db52D5850051
CARTESI_CONTRACTS_AUTHORITY_FACTORY_ADDRESS=0xC7003566dD09Aa0fC0Ce201aC2769aFAe3BF0051
CARTESI_CONTRACTS_APPLICATION_FACTORY_ADDRESS=0xc7006f70875BaDe89032001262A846D3Ee160051
CARTESI_CONTRACTS_SELF_HOSTED_APPLICATION_FACTORY_ADDRESS=0xc700285Ab555eeB5201BC00CFD4b2CC8DED90051
MAIN_SEQUENCER=espresso
CARTESI_FEATURE_GRAPHQL_ENABLED=true
CARTESI_FEATURE_RPC_ENABLED=true
ESPRESSO_BASE_URL=https://query.decaf.testnet.espresso.network
ESPRESSO_NAMESPACE=55555
CARTESI_BLOCKCHAIN_HTTP_ENDPOINT=
CARTESI_BLOCKCHAIN_WS_ENDPOINT=
CARTESI_BLOCKCHAIN_ID=11155111
CARTESI_AUTH_PRIVATE_KEY=
CARTESI_DATABASE_CONNECTION=
```

Update the following variables before deployment:

- `CARTESI_BLOCKCHAIN_HTTP_ENDPOINT`: Your Sepolia RPC endpoint (e.g., Infura, Alchemy)
- `CARTESI_BLOCKCHAIN_WS_ENDPOINT`: Your Sepolia WebSocket endpoint
- `CARTESI_AUTH_PRIVATE_KEY`: Private key for contract deployments
- `CARTESI_DATABASE_CONNECTION`: Will be added after database creation in the next step


Run the following command to deploy the node with the prepared env file.

```shell
./dev.sh deploy-node --app-name <app-name> --env-file .env.<testnet>
```
The above command will:
- Create `fly.toml` configuration
- Launch fly.io app (interactive setup)
- Create Postgres database (interactive setup)
- Leave you to update the database connection in your `.env.<testnet>` file

:::note

The `--app-name` in above command is not the Cartesi dApp's name, but the name of the fly.io cloud application. We'll name the dApp in the next step.

:::

### Step:02 Deploy the app to the node

For a new deployment, you'll need to deploy the contracts and register the app to the node. You can also set the epoch length and salt for the deployment using the `--epoch-length` and `--salt` flags.

```shell
./dev.sh deploy-app --app-name <app-name> --env-file .env.<testnet> --owner <owner-address>
```

Alternatively, you can deploy an app with pre-deployed contracts.

```shell
./dev.sh deploy-app --app-name <app-name> --env-file .env.<testnet> --application-address <application-address> --consensus-address <consensus-address>
```
Your application is now deployed and registered on the Rollups node. You can start sending inputs using the methods described in the [interactions](./interacting) page.
