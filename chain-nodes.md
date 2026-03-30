# Blockchain Node Rewards

## Overview

Nexora tracks and verifies local blockchain full nodes. If you run a Base, ETH, OP, BNB, or other supported EVM node on your machine, Nexora will detect it automatically and reward you with bonus points on top of your regular uptime earnings.

This creates a dual incentive: you help secure the blockchain network while earning extra rewards through Nexora.

---

## How It Works

```
Your Machine
├── Nexora CLI (uptime tracking)
└── Blockchain Node (op-geth, geth, etc.)
        │ RPC on localhost:8545
        ▼
Nexora Backend
├── Verify chain ID matches expected network
├── Check block number vs public RPC
├── Confirm sync lag is within threshold
└── Credit bonus points every 60 seconds
```

1. When you run `python cli/main.py start`, the CLI scans ports `8545`, `8546`, `9545`, `9546`, `7545` for local RPC endpoints
2. For each found RPC, it calls `eth_chainId` to identify the network
3. The server verifies the node is synced (block lag within threshold)
4. Bonus points are credited every ~60 seconds as long as the node stays synced

---

## Supported Networks

| Network | Chain ID | Reward Multiplier | Max Sync Lag |
|---|---|---|---|
| ETH Mainnet | 1 | 5× | 50 blocks |
| OP Mainnet | 10 | 2× | 50 blocks |
| BNB Chain | 56 | 2× | 100 blocks |
| Base Mainnet | 8453 | 3× | 50 blocks |
| Base Sepolia | 84532 | 1.5× | 100 blocks |
| ETH Sepolia | 11155111 | 1.5× | 100 blocks |
| OP Sepolia | 11155420 | 1.5× | 100 blocks |
| BNB Testnet | 97 | 1.2× | 200 blocks |

More chains will be added over time.

---

## Running a Base Node

The official Base node setup is at [github.com/base/node](https://github.com/base/node).

**Minimum requirements for Base Mainnet:**
- 16 GB RAM
- 2 TB SSD (NVMe recommended)
- 8-core CPU
- 25 Mbps+ internet

**Quick setup:**

```bash
git clone https://github.com/base/node.git
cd node
# Follow the README for your network (mainnet or sepolia)
docker compose up
```

Once running, the RPC will be available at `http://localhost:8545`. Nexora CLI will detect it automatically on next `start`.

---

## Running an ETH Node (Geth)

```bash
# Install geth
# https://geth.ethereum.org/docs/getting-started/installing-geth

geth --syncmode snap --http --http.port 8545
```

---

## Running an OP Node

```bash
# Follow official OP Stack docs
# https://docs.optimism.io/builders/node-operators/tutorials/mainnet
```

---

## Verification Anti-Cheat

The server performs these checks before crediting chain bonuses:

1. **Chain ID verification** — local RPC must return the expected chain ID
2. **Block advancement** — reported block must be higher than the last recorded block (prevents fake static nodes)
3. **Sync lag check** — node must be within the allowed block lag from the public RPC
4. **Rate limiting** — chain heartbeats are accepted at most once per 55 seconds

If your node falls out of sync, bonuses are paused until it catches up. The node status will show `unsynced`.

---

## Checking Chain Node Status

```bash
python cli/main.py status
```

Output example:
```
Node Status: RUNNING
Node ID: abc123...

Blockchain Nodes:
  Base Mainnet — port 8545 — 3.0x reward
  ETH Mainnet  — port 8546 — 5.0x reward
```

---

## API Endpoints

```
GET  /chain/supported          — List all supported chains
POST /chain/register           — Register a chain node
POST /chain/heartbeat          — Send chain heartbeat
GET  /chain/nodes/{node_id}    — Get chain nodes for a Nexora node
```
