---
title: API Reference
---

# API Reference

This file contains the top-level RPC & SDK reference. For full generated references, integrate an OpenAPI/TypeDoc generator and link the outputs here.

## JSON-RPC Methods (examples)

### `nexa_getSequencerInfo`

**Params:** `[]`

**Result:**

```json
{
  "chainId": 1337,
  "uptime": 12345,
  "currentBlock": 123456
}
```

### `nexa_batchSubmit`

**Params:**

- `batch`: base64-encoded batch payload

**Errors:**

- `-32000` Invalid batch format
- `-32001` DA submission failed

## SDK: Provider

```typescript
interface NexaProvider {
  getBalance(address: string): Promise<BigNumber>;
  sendTransaction(rawTx: string): Promise<string>;
  getSequencerInfo(): Promise<SequencerInfo>;
}
```

## Example: contract deployment via SDK

```typescript
const receipt = await sdk.deployContract(compiledAbi, bytecode, {
  from: wallet.address,
});
console.log("deployed at", receipt.contractAddress);
```
