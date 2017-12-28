# Setting up Development Environment

## Install Node.js

Install Node.js by your favorite method, or use Node Version Manager by following directions at https://github.com/creationix/nvm

```bash
nvm install v4
```

## Fork and Download Repositories

To develop b2x-node:

```bash
cd ~
git clone git@github.com:<yourusername>/b2x-node.git
git clone git@github.com:<yourusername>/b2x-core-lib.git
```

## Install Development Dependencies

For Ubuntu:
```bash
sudo apt-get install libzmq3-dev
sudo apt-get install build-essential
```
**Note**: Make sure that libzmq-dev is not installed, it should be removed when installing libzmq3-dev.


For Mac OS X:
```bash
brew install zeromq
```

## Install and Symlink

```bash
cd b2x-core-lib
npm install
cd ../b2x-node
npm install
```
**Note**: If you get a message about not being able to download bitcoin2x distribution, you'll need to compile bitcoin2xd from source, and setup your configuration to use that version.


We now will setup symlinks in `b2x-node` *(repeat this for any other modules you're planning on developing)*:
```bash
cd node_modules
rm -rf b2x-core-lib
ln -s ~/b2x-core-lib
rm -rf b2x-rpc
ln -s ~/b2x-rpc
```

And if you're compiling or developing segwit2x:
```bash
cd ../bin
ln -sf ~/bitcoin/src/bitcoind
```

## Run Tests

If you do not already have mocha installed:
```bash
npm install mocha -g
```

To run all test suites:
```bash
cd b2x-node
npm run regtest
npm run test
```

To run a specific unit test in watch mode:
```bash
mocha -w -R spec test/services/bitcoind.unit.js
```

To run a specific regtest:
```bash
mocha -R spec regtest/bitcoind.js
```

## Running a Development Node

To test running the node, you can setup a configuration that will specify development versions of all of the services:

```bash
cd ~
mkdir devnode
cd devnode
mkdir node_modules
touch b2x-node.json
touch package.json
```

Edit `b2x-node.json` with something similar to:
```json
{
  "network": "livenet",
  "port": 3001,
  "services": [
    "bitcoind",
    "web",
    "insight-api",
    "insight-ui",
    "<additional_service>"
  ],
  "servicesConfig": {
    "bitcoind": {
      "spawn": {
        "datadir": "/home/<youruser>/.bitcoin2x",
        "exec": "/home/<youruser>/bitcoinx/src/bitcoin2xd"
      }
    }
  }
}
```

**Note**: To install services [insight-api](https://github.com/SegwitB2X/b2x-insight-api) and [insight-ui](https://github.com/SegwitB2X/b2x-insight-ui) you'll need to clone the repositories locally.

Setup symlinks for all of the services and dependencies:

```bash
cd node_modules
ln -s ~/b2x-core-lib
ln -s ~/b2x-node
ln -s ~/insight-api
ln -s ~/insight-ui
```

Make sure that the `<datadir>/bitcoin2x.conf` has the necessary settings, for example:
```
server=1
whitelist=127.0.0.1
txindex=1
addressindex=1
timestampindex=1
spentindex=1
zmqpubrawtx=tcp://127.0.0.1:28332
zmqpubhashblock=tcp://127.0.0.1:28332
rpcallowip=127.0.0.1
rpcuser=bitcoin
rpcpassword=local321
```

From within the `devnode` directory with the configuration file, start the node:
```bash
../b2x-node/bin/b2x-node start
```