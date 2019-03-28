![OCKHAM-DESKTOP](https://user-images.githubusercontent.com/8069294/35097070-78c0dc40-fc46-11e7-9bb0-ad36f7182f39.png)

## Prerequisites

- Because the OCKHAM Node is recommended to be run on Ubuntu 16.04 LTS (see the [node guide](https://blog.ockham.consulting/how-to-setup-a-node-for-ock-and-a-basic-cheat-sheet-4f82910719da)), we recommend that the deployer is only run on Ubuntu 16.04 LTS also.
- User running the deployer commands must be a sudoer

## Installation

```bash
git clone https://github.com/gitockham/ock-deployer.git && cd ock-deployer
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
source ~/.profile
nvm install 8.9.1
sudo apt-get update && sudo apt-get install -y jq
```

## Detailed Guide

Follow this [full guide](https://blog.ockham.consulting/ock-deployer-setup-guide-c10825ebb0e4) to get the best out of your Bridgechain.

## Quick setup with Vagrant
Deploy a bridgechain and explorer within its own Vagrant setup. This requires vagrant version 2 and up.

1. Install Vagrant on your local computer
2. Clone the ock-deployer from our repository
```bash
$> git clone https://github.com/gitockham/ock-deployer.git && cd ock-deployer
```
3. Run the vagrant command
```bash
$> vagrant up
```
Vagrant will then reboot. Once finished, wait a further minute or so and you can access the Node and Explorer using the below URLs:

Node API (port forwarded): `http://127.0.0.1:14100/api/`
Explorer (port forwarded): `http://127.0.0.1:14200/`

## Quick setup with Docker
Deploy a bridgechain and explorer within its own Docker setup.

1. Install Docker on your local computer
2. Clone the ock-deployer from our repository
```bash
$> git clone https://github.com/gitockham/ock-deployer.git && cd ock-deployer
```
3. Build the docker image
```bash
$> docker build -f docker/Dockerfile . -t deployer
```
4. Run deployer
```bash
$> docker run -p 4100:4100 -p 4200:4200 -d deployer
```

Node API (port forwarded): `http://127.0.0.1:4100/api/`
Explorer (port forwarded): `http://127.0.0.1:4200/`


## Manual installation

### Node installation

*Note: Change <MACHINE_IP> to your Machine's IP*

```bash
./bridgechain.sh install-node --name MyTest --database ock_mytest --token MYTEST --symbol MT --node-ip <NODE_IP>
./bridgechain.sh start-node --name MyTest
```

#### Optional Parameters

    --path - Path to install Bridgechain [/home/$USER/ock-bridgechain]
    --name - Name of Bridgechain [bridgechain]
    --database - Database Name [ock_bridgechain]
    --node-ip - IP for node [0.0.0.0]
    --node-port - Port for node [4100]
    --explorer-ip - IP for explorer [127.0.0.1]
    --explorer-port - Port for explorer [4200]
    --token - Token Name [MINE]
    --symbol - Symbol for Token [M]
    --prefix - Address Prefix [M]
    --forgers - How many forgers for the network [51]
    --max-votes - Max Votes per Wallet [1]
    --blocktime - Time per block (seconds) [8]
    --transactions-per-block - Max Transaction count per Block [50]
    --reward-height-start - Block Height when Forgers receive Rewards [75600]
    --reward-per-block - How many Rewarded Tokens per Forged Block [200000000 (2)]
    --total-premine - How many tokens initially added to genesis account [2100000000000000 (21 million)]
    --max-tokens-per-account - Max amount of tokens per account [12500000000000000 (125 million)]
    --config - Path to JSON config file for install options (see below section for more information)
    --autoinstall-deps - Automatically install dependencies without prompt
    --skip-deps - Skips check for installing dependencies

*Note: Below Parameters do not work with standard wallets (with hardcoded values)*

    --fee-send - Fee for sending Transaction [10000000 (0.1)]
    --fee-vote - Fee for Vote Transaction [100000000 (1)]
    --fee-second-passphrase - Fee for Second Passphrase Transaction [500000000 (5)]
    --fee-delegate - Fee for Register Delegate Transaction [2500000000 (25)]
    --fee-multisig - Fee for Multisignature Transaction [500000000 (5)]
    --update-epoch - Set Epoch based on time the chain was created

### Explorer installation

*Note: Change <MACHINE_IP> to your Machine's IP*

```bash
./bridgechain.sh install-explorer --name MyTest --token MYTEST --explorer-ip <EXPLORER_IP> --node-ip <NODE_IP>
./bridgechain.sh start-explorer
```

#### Optional Parameters

    --path - Path to install Explorer [/home/$USER/ock-explorer]
    --name - Name of Bridgechain [bridgechain]
    --node-ip - IP for node [0.0.0.0]
    --node-port - Port for node [4100]
    --explorer-ip - IP for explorer [127.0.0.1]
    --explorer-port - Port for explorer [4200]
    --token - Token Name [MINE]
    --forgers - How many forgers for the network [51]
    --config - Path to JSON config file for install options (see below section for more information)
    --autoinstall-deps - Automatically install dependencies without prompt
    --skip-deps - Skips check for installing dependencies

## JSON Config

As mentioned in the parameters list, it's possible to pass in a JSON config file to load all properties, although they're not all required. For a full sample file, take a look [here](config.sample.json). For a small sample, see below:

```json
{
    "nodeIp": "localhost",
    "nodePort": 4100,
    "explorerIp": "1.2.3.4",
    "explorerPort": 4200
}
```

To use a config file during an install, simply use the `--config` argument. For example:

```bash
./bridgechain.sh install-node --config /path/to/config.json
```

## Security

If you discover a security vulnerability within this project, please send an e-mail to security@ockham.consulting. All security vulnerabilities will be promptly addressed.

## Credits

- [Alex Barnsley](https://github.com/alexbarnsley)
- [Brian Faust](https://github.com/faustbrian)
- [Luc Talarico](https://github.com/gitockham)
- [All Contributors](../../contributors)

## License

OCKHAM Deployer is licensed under the MIT License - see the [LICENSE](./LICENSE.md) file for details.
