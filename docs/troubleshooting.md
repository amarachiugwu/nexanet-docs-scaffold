---
title: Troubleshooting
---

# Troubleshooting & Error Guide

This page lists common problems, root causes, and fixes.

## Common errors

### `ERR_DA_SUBMIT_FAILED`

**Symptoms:** Relayer logs show `failed to submit to DA: 502`.

**Explanation:** The chosen Data Availability provider is down or responded with 5xx.

**Fix:**

1. Check DA provider health: `curl https://da.example/health`.
2. Switch DA provider in `nexanet-config.yaml` to `local` or `ipfs`.
3. Restart relayer.

### `ERR_EXECUTION_REVERT` / transaction reverted

**Symptoms:** `eth_getTransactionReceipt` shows `status: 0` and `revertReason`.

**Explanation:** Contract execution triggered a revert. Could be insufficient gas, failing require, or bad input.

**Fix:**

- Re-run the transaction locally with the `TRACE` flag on the `executor`.
- Check the revert reason: `provider.call(tx, blockNumber)` to get reason string.

### `ERR_SYNC_LAG`

**Symptoms:** Node reports `syncLag > 200` blocks.

**Explanation:** Node cannot catch up due to slow disk, CPU, or network.

**Fix:**

- Increase resources (CPU/memory).
- Wipe data and resync from snapshot: `nexanet snapshot restore snapshot-2025-11-01.tar.gz`.

## How to collect useful debug data

- Node logs (`/var/log/nexanet/node.log`)
- Dumped state: `nexanet dump-state --block <n>`
- RPC trace: Enable `TRACE` level for `executor`

## FAQs

- **Q:** Why is my transaction pending?

  - **A:** Could be mempool policy. Check `sequencer/mempool_size` and gas price.

- **Q:** How do I run a full node vs sequencer?
  - **A:** Use `nexanet --role executor` or `--role sequencer`.
