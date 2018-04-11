# Nimiq Blockchain [![Build Status](https://travis-ci.org/nimiq-network/core.svg)](https://travis-ci.org/nimiq-network/core)

**[Nimiq](https://nimiq.com/)** is a frictionless payment protocol for the web.

For a high-level introduction check out the [Nimiq White Paper](https://medium.com/nimiq-network/nimiq-a-peer-to-peer-payment-protocol-native-to-the-web-ffd324bb084).

To dive into the details of the protocol architecture check out the [Nimiq Developer Reference](https://nimiq.com/developer-reference).

## Library Demo
Check out our [Testnet](https://nimiq-testnet.com).

## Quickstart

1. Install [Node.js](https://nodejs.org) v8.0.0 or higher.
2. On Ubuntu, install `git` and `build-essential`: `sudo apt-get install -y git build-essential`.
    - On other Linux systems, install `git`, `python2.7`, `make`, `gcc` and `gcc-c++`.
    - For MacOS or Windows, [check here for git](https://git-scm.com/downloads) and [here for compilation tools](https://github.com/nodejs/node-gyp#on-mac-os-x).
3. Install yarn: `sudo npm install -g yarn`.
4. Install `gulp` globally:  `yarn global add gulp`.
5. Clone this repository: `git clone https://github.com/nimiq-network/core`.
6. Enter the core directory: `cd core`.
7. Run: `yarn`.
8. Run: `yarn build`.
9. Open `clients/browser/index.html` in your browser.

## Web Developers
### Most simple Web Application on top of the Nimiq Blockchain
A good way to get started is to have a look at [the most simple web application on top of the Nimiq Blockchain](https://demo.nimiq.com/).

### Installation for Web Developers
Follow the Quickstart guide or use our CDN:

```
<script src="https://cdn.nimiq.com/core/nimiq.js"></script>
```

### Run browser client
Open `clients/browser/index.html` in your browser.

### Build your own browser client
Just include `<script src="dist/nimiq.js"></script>` in your project.

### API
Visit the [API Documentation](https://doc.esdoc.org/github.com/nimiq-network/core/).


## Node.js client

### Run Node.js client
To run a Node.js client you will need a **publicly routable IP**, **Domain** and **SSL Certificate** (get a free one at [letsencrypt.org](https://letsencrypt.org/)). Start the client by running `clients/nodejs/nimiq`.

```bash
cd clients/nodejs/
node nimiq --host=HOSTNAME --port=PORT --cert=SSL_CERT_FILE --key=SSL_KEY_FILE [options]
```

| **Configuration** | |
| :--- | :--- |
| `--host=HOSTNAME` | Hostname of the Node.js client. |
| `--port=PORT` | Port to listen on for connections. |
| `--cert=SSL_CERT_FILE` | SSL certificate file for your domain. CN should match HOSTNAME. |
| `--key=SSL_KEY_FILE` | SSL private key file for your domain. |
| **Options** | |
| `--help` | Show usage instructions. |
| `--log[=LEVEL]` | Configure global log level. |
| `--log-tag=TAG[:LEVEL]` | Configure log level for a specific tag. |
| `--miner[=THREADS]` | Activate mining on this node with THREADS parallel threads. |
| `--passive` | Do not actively connect to the network. |
| `--rpc[=PORT]` | Start JSON-RPC server on port PORT (default: 8648). |
| `--statistics[=INTERVAL]` | Output miner statistics every INTERVAL seconds. |
| `--type=TYPE` | Configure the consensus type, one of full (default), light or nano. |
| `--wallet-seed=SEED` | Initialize wallet using SEED as a wallet seed. |
| `--wallet-address=ADDRESS` | Initialize wallet using ADDRESS as a wallet address. |

### Build binary packages for Linux distributions

After completing the steps from the [Quickstart](#quickstart), follow this steps to build a package for a Linux distribution. After building it:
- the package will be located in the `dist/` directory, 
- a [configuration](#run-node-js-client) file will be located in `/etc/nimiq/nimiq.conf`. 
- and a Systemd service will be create which you can manage with `systemctl start|stop|restart nimiq`. 

#### Debian/Ubuntu (deb package format)
After running `yarn` (from the Quickstart section):

1. Make sure you have `dpkg`, `jq` and `fakeroot` installed (if you don't, they can be easily installed with `apt`).
2. Run `yarn run build-deb`.
3. The .deb package will be located in the `dist/` directory.

Note: creating deb packages only works on Debian-based distributions (only has been extensively tested on Ubuntu).

#### Fedora/CentOS/RHEL (rpm package format)
After running `yarn` (from the Quickstart section):

1. Make sure you have `rpm-build` installed (if you don't, it can be easily installed with `yum` or `dnf`).
2. Run `yarn run build-rpm`.
3. The .rpm package will be located in the `dist/` directory.

Note: creating rpm packages only works on rpm-based distributions (only has been extensively tested on Fedora).

### Test and Build

#### Run Testsuite
- `yarn test` runs browser and Node.js tests.
- `yarn test-browser` runs the testsuite in your browser only.
- `yarn test-node` runs the testsuite in Node.js only.

#### Run ESLint
`yarn lint` runs the ESLint javascript linter.

#### Build
Executing `yarn build` concatenates all sources into `dist/{web,web-babel,web-crypto,node}.js`

## Docker

A Dockerfile is provided which allows for creating your own backbone image using the following arguments.

| Argument | Description |
| --- | --- |
| BRANCH  | Defaults to *master* but can be any available git branch  |
| PORT  | Defaults to TCP port *8080* |
| DOMAIN  | Domain to be used for hosting the backbone node  |
| KEY  | Path to an existing certificate key for the DOMAIN  |
| CRT  | Path to an existing signed certificate for the DOMAIN  |
| WALLET_SEED  | Pre-existing wallet private key  |

### Building the Docker image using the above arguments
```
docker build \
  --build-arg DOMAIN=<DOMAIN> \
  --build-arg BRANCH=<BRANCH> \
  --build-arg WALLET_SEED=<WALLET_SEED> \
  --build-arg KEY=<KEY> \
  --build-arg CRT=<CRT> \
  --build-arg PORT=<PORT> \
  -t nimiq .
```

### Running an instance of the image

`docker run -d -p 8080:8080 -v /etc/letsencrypt/:/etc/letsencrypt/ --name "nimiq" nimiq`

Note that you can override any of the arguments which were baked into the image at runtime with exception to the *BRANCH*. The -v flag here allows for mapping a local system path into the container for the purpose of using the existing *DOMAIN* certificates.

### Check status
`docker logs -f <instance_id_or_name>`

## JSON-RPC Client

Usage: `node remote.js [options] action [args]`


| **Options** | |
| :--- | :--- |
| `--host=HOST` | Define hostname or IP address of Nimiq JSON-RPC server to connect to. Defaults to local host.  |
| `--port=PORT` | Define port corresponding to HOST. Defaults to 8648. |
| `--user=USER` | Use basic authentication with username USER. The password will be prompted for. |
| **Actions** | |
| `account ADDR` | Display details for account with address ADDR. |
| `accounts` | List local accounts. |
| `block BLOCK` | Display details of block BLOCK. |
| `constant CONST [VAL]` | Display value of constant CONST. If VAL is given, overrides constant const with value VAL.|
| `mining` |  Display information on current mining settings. |
| `mining.enabled [VAL] ` | Read or change enabled state of miner. |
| `mining.threads [VAL]` | Read or change number of threads of miner. |
| `peer PEER [ACTION]` | Display details about peer PEER. If ACTION is specified, invokes the named action on the peer. Currently supported actions include: connect, disconnect, ban, unban, fail |
| `peers` | List all known peer addresses and their current connection state. |
| `transaction TX` | Display details about transaction TX. |
| `transaction BLOCK IDX` | Display details about transaction at index IDX inblock `BLOCK`. |
| `transaction.receipt TX` | Display the transaction receipt for transaction TX. |
| `transaction.send SENDER RECIPIENT VALUE FEE [DATA]` | Create, sign and send a transaction with the given properties. The sending account must be a local account. |
| `transactions ADDR [LIMIT]` | Display at most LIMIT transactions involving address ADDR. |
| `mempool` | Display mempool stats. |
| `mempool.content [INCLUDE_TX]` | Display mempool content. If INCLUDE_TX is given, full transactions instead of transaction hashes are requested. |
| `consensus.min_fee_per_byte [FEE]` | Read or change the current min fee per byte setting. |

Most actions support output either in human-readable text form (default) or as JSON by appending '.json' to the action name. Addresses may be given in user- friendly address format, hex or base64 encoded. Blocks can be specified by hash in hex or base64 format or by the height on the main chain. Transactions are understood in hex or base64 format of their hash. Peers may be given as their peer id in hex or peer address.


## Contribute

If you'd like to contribute to the development of Nimiq please follow our [Code of Conduct](/.github/CODE_OF_CONDUCT.md) and [Contributing Guidelines](/.github/CONTRIBUTING.md).

## License

This project is under the [Apache License 2.0](./LICENSE.md).