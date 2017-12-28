Segwit2x Node
============

A Segwit2x full node for building applications and services with Node.js. A node is extensible and can be configured to run additional services.

## Install

```bash
npm install -g b2x-node
b2x-node start
```

## Prerequisites

- GNU/Linux x86_32/x86_64, or OSX 64bit *(for bitcoin2xd distributed binaries)*
- Node.js v0.10, v0.12 or v4
- ZeroMQ *(libzmq3-dev for Ubuntu/Debian or zeromq on OSX)*
- ~200GB of disk storage
- ~8GB of RAM

## Configuration

b2x-node includes a Command Line Interface (CLI) for managing, configuring and interfacing with your b2x-node Node.

```bash
b2x-node create -d <bitcoin-data-dir> mynode
cd mynode
b2x-node install <service>
b2x-node install https://github.com/yourname/helloworld
```

This will create a directory with configuration files for your node and install the necessary dependencies. For more information about (and developing) services, please see the [Service Documentation](docs/services.md).

## Add-on Services

There are several add-on services available to extend the functionality of b2x-node:

- [Insight API](https://github.com/SegwitB2X/b2x-insight-api)
- [Insight UI](https://github.com/SegwitB2X/b2x-insight-ui)

## Documentation

- [Upgrade Notes](docs/upgrade.md)
- [Services](docs/services.md)
  - [Bitcoind](docs/services/bitcoind.md) - Interface to Segwit2x Core
  - [Web](docs/services/web.md) - Creates an express application over which services can expose their web/API content
- [Development Environment](docs/development.md) - Guide for setting up a development environment
- [Node](docs/node.md) - Details on the node constructor
- [Bus](docs/bus.md) - Overview of the event bus constructor
- [Release Process](docs/release.md) - Information about verifying a release and the release process.
