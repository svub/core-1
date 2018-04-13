# Nimiq Blockchain [![Build Status](https://travis-ci.org/nimiq-network/core.svg)](https://travis-ci.org/nimiq-network/core)

**[Nimiq](https://nimiq.com/)** is a frictionless payment protocol for the web.

## Resources

- [Nimiq White Paper](https://medium.com/nimiq-network/nimiq-a-peer-to-peer-payment-protocol-native-to-the-web-ffd324bb084): High-level introduction of the Nimiq payment protocol.
- [Nimiq Developer Reference](https://nimiq.com/developer-reference): Details of the protocol architecture.
- [API Documentation](https://doc.esdoc.org/github.com/nimiq-network/core/).
- [JSON-RPC Client](doc/json-rpc-client.md): Usage instructions for the Nimiq JSON-RPC Client.
- [Docker Documentation](doc/docker.md): Instuctions on setting up a Nimiq Node using Docker.

## Demo
Check out our [Testnet](https://nimiq-testnet.com).

## Quickstart

1. Install [Node.js](https://nodejs.org) v8.0.0 or higher.
2. On Ubuntu and Debian, install `git` and `build-essential`: `sudo apt-get install -y git build-essential`.
    - On other Linux systems, install `git`, `python2.7`, `make`, `gcc` and `gcc-c++`.
    - For MacOS or Windows, [check here for git](https://git-scm.com/downloads) and [here for compilation tools](https://github.com/nodejs/node-gyp#on-mac-os-x).
3. Install yarn: `sudo npm install -g yarn`.
4. Install `gulp` globally:  `yarn global add gulp`.
5. Clone this repository: `git clone https://github.com/nimiq-network/core`.
6. Build the project: `cd core && yarn && yarn build`.
7. Open `clients/browser/index.html` in your browser.

## Web Developers
### Simple Web Application on top of Nimiq
A good way to get started is to have a look at [the most simple web application on top of the Nimiq Blockchain](https://demo.nimiq.com/).

### Getting Started
Follow the [Quickstart](#quickstart) guide or make use of our CDN:

```
<script src="https://cdn.nimiq.com/core/nimiq.js"></script>
```

## Browser client

Open `clients/browser/index.html` in your browser or include `<script src="dist/nimiq.js"></script>` in your project.

## Node.js client

### Run Node.js client
To run a Node.js client you will need a **publicly routable IP**, **Domain**, and **SSL Certificate** (get a free certificate at [letsencrypt.org](https://letsencrypt.org/)). Start the client by running `clients/nodejs/nimiq` with the respective [configuration](doc/configuration.md).

### Build binary packages for Linux distributions

After completing the [Quickstart](#quickstart), follow the steps below to build a Linux package. After the build process:
- the package will be located in the `dist/` directory, 
- once the package has been installed,
    - a [configuration](#run-node-js-client) file will be located in `/etc/nimiq/nimiq.conf` and
    - a `systemd` service will be avialable which you can manage with `systemctl start|stop|restart nimiq`. 

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

## Contribute

If you'd like to contribute to the development of Nimiq please follow our [Code of Conduct](/.github/CODE_OF_CONDUCT.md) and [Contributing Guidelines](/.github/CONTRIBUTING.md).

## License

This project is under the [Apache License 2.0](./LICENSE.md).
