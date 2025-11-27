---
title: Developer Guide
---

# Developer Guide

This guide covers: environment, debugging, code structure, SDKs, running a node, deploying contracts on testnet, and writing integrations.

## Repo layout

```
/cli
/core
/executor
/sequencer
/sdk-js
/docs
/tests
```

## Setup (local dev)

1. `git clone ...`
2. `yarn install` at repo root
3. `yarn build` to compile all packages
4. `docker-compose up` to start local network

Follow the [Getting Started](getting-started.md) guide for more details.

## Running a node with debug logging

```bash
NEXANET_LOG=debug ./bin/nexanet --config ./nexanet-config.yaml
```

## Useful commands

using yarn

`yarn build` — compile packages

`yarn lint` — run linters

`yarn test` — run unit and integration tests

`yarn dev:node` — start a hot-reload dev node

or using NPM

`npm run build` — compile packages

`npm run lint` — run linters

`npm run test` — run unit and integration tests

`npm run dev:node` — start a hot-reload dev node

## SDK example

- JavaScript: `sdk-js` includes `Provider`, `Wallet`, `Contract` helpers.

- TypeScript: complete typed definitions for all RPC responses.

## Example: submit a transaction via raw JSON-RPC

```javascript
curl -X POST http://localhost:8545 -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"eth_sendRawTransaction","params":["0x..."] ,"id":1}'
```

## Debugging tips

- Enable `TRACE` logging for `executor` to see vm steps.

- Use `rpc.getTransactionReceipt` to inspect reverts and gas usage.

- Use `nexanet dump-state --block 12345` to export state to JSON.

## Local development patterns

Run unit tests in watch mode with `yarn test:watch`.

Use `docker-compose` for integration tests that rely on DA provider emulators.
