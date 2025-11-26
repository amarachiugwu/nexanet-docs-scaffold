---
title: Getting Started
---

# Getting Started with NexaNet

You should have the following installed:

- [ ] Node >= 18 LTS
- [ ] Yarn or npm
- [ ] Docker (recommended for local testnet)

### 1. Clone the repo

```bash
git clone https://github.com/your-org/nexanet.git
cd nexanet
```

### 2. Install dependencies

using yarn

```bash
yarn install
```

or using npm

```bash
npm install
```

### 3. Start local testnet (docker-compose)

Your [docker-compose.yml](./docker-compose.yml) should run `nexanet-node` and `relayer` start by running:

```bash
docker-compose up --build
```

The node will expose an EVM-compatible JSON‑RPC at http://localhost:8545.

### 4. CLI quickstart

Install CLI:

```bash
npm install -g @nexanet/cli
nexanet init --url http://localhost:8545
nexanet account create --name dev
nexanet tx send --to 0x... --value 1000000000000000000
```

### 5. SDK example (JavaScript)

```javascript
import { NexaProvider, NexaWallet } from "@nexanet/sdk";

const provider = new NexaProvider("http://localhost:8545");
const wallet = NexaWallet.fromMnemonic(process.env.MNEMONIC, provider);

async function main() {
  const balance = await provider.getBalance(wallet.address);
  console.log("balance", balance.toString());
}

main();
```

### 6. Run tests

if using yarn

```bash
yarn test
```

if using npm

```bash
npm test
```
