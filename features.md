# Key Features

## Lightweight CLI Node

Runs on any platform — Linux, Windows, VPS, Android (Termux). No GUI, no heavy computation.

- Sends heartbeats every ~30 seconds with random jitter
- Resumes existing node on restart (no new registration needed)
- Stores state locally in `~/.nexora/`

---

## Blockchain Node Tracking

Automatically detects and tracks local EVM blockchain nodes:

- Scans common RPC ports (8545, 8546, 9545, 9546, 7545)
- Identifies chain via `eth_chainId`
- Verifies sync status against public RPC
- Credits bonus points every ~60 seconds

Supported: Base Mainnet/Sepolia, ETH Mainnet/Sepolia, OP Mainnet/Sepolia, BNB Chain/Testnet. More chains coming.

---

## Reward Multipliers

| Node Type | Multiplier |
|---|---|
| Nexora uptime only | 1× base |
| + Base Mainnet node | +3× bonus |
| + ETH Mainnet node | +5× bonus |
| + OP Mainnet node | +2× bonus |
| + BNB Chain node | +2× bonus |

---

## Anti-Cheat System

Multi-layer protection:

- Device fingerprinting (OS + hostname + MAC + CPU + RAM + disk)
- Max 2 active nodes per device
- Max 3 active nodes per IP
- Rate limiting (min 20s between heartbeats)
- Uptime regression detection
- Perfect-timing bot detection
- Abnormal growth rate detection
- Node score system (0–100) with automatic reward reduction
- Proof-of-Work required for node registration
- Chain node block advancement verification

---

## Referral System

- Every user gets a unique referral code on registration
- Codes are **single-use** — each code can only be used once
- After use, the new user gets their own code to invite one more person
- Creates an organic invite chain

---

## Node Score System

Each node has a score (0–100, default 100):

- Decreases for: spam, suspicious behavior, uptime manipulation
- Increases for: stable long uptime (bonus per hour)
- Below 50: reduced rewards
- Below 20: node suspended

---

## Production Backend

The backend runs on Railway with PostgreSQL — data persists permanently. No local server setup needed for end users.

API: `https://node-production-712b.up.railway.app`
