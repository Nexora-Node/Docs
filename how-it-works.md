# How Nexora Works

## High-Level Architecture

```
User Device
├── Nexora CLI (python main.py start)
│   ├── Uptime heartbeat every ~30s
│   └── Chain node heartbeat every ~60s (optional)
└── Local Blockchain Node (optional — Base/ETH/OP/BNB)
        │
        ▼
Nexora Backend (Railway — FastAPI + PostgreSQL)
├── Anti-Cheat Validator
├── Proof-of-Work verifier
├── Mining Rate Engine (smooth 5% decay)
├── Chain Node Verifier (vs public RPC)
└── NEXORA Token Ledger (off-chain balance)
        │
        ▼
User Dashboard (Vercel — Next.js)
├── View NEXORA balance
├── Link EVM wallet
└── Claim NEXORA on-chain (Base network)
        │
        ▼
ClaimDistributor Contract (Base Mainnet)
├── Verify EIP-712 backend signature
├── Transfer NEXORA from treasury to user (99.95%)
└── Transfer 0.05% fee to DEX listing fund
```

---

## Registration Flow

```
1. User gets referral code from existing user
2. CLI generates device fingerprint (OS + hostname + MAC + CPU + RAM + disk)
3. CLI solves Proof-of-Work challenge (SHA256 with 3 leading zeros)
4. User registers → gets unique referral code for inviting others
5. Device registered → linked to user account
6. Node registered → gets node_id + node_token for authentication
```

---

## Heartbeat Flow

Every ~30 seconds (with random jitter ±4s to avoid pattern detection):

```
CLI sends POST /node/heartbeat
    node_id, node_token, device_id, uptime_seconds
        │
        ▼
Backend validates:
    1. Token authentication (node_token must match DB)
    2. Node exists and is active/stopped
    3. Rate limit (≥ 20s since last heartbeat)
    4. Suspicious behavior analysis (uptime jumps, timing patterns)
    5. Uptime regression check (uptime cannot go backwards)
        │
        ▼
NEXORA calculated:
    uptime_delta = current_uptime - last_uptime
    rate         = BASE_RATE × 0.95^epoch          (smooth decay)
    raw_tokens   = uptime_delta / 60 × rate
    adjusted     = raw_tokens × (node_score / 100)
        │
        ▼
User NEXORA balance updated in PostgreSQL
total_distributed counter incremented (capped at 200,000)
```

---

## Chain Node Flow

Every ~60 seconds when a local blockchain node is detected:

```
CLI detects local RPC on port 8545/8546/...
    │
    ▼
CLI sends POST /chain/heartbeat
    chain_node_id, node_id, node_token, local_block
        │
        ▼
Backend validates:
    1. Token authentication
    2. Block must be advancing (anti-fake-node)
    3. Sync lag check vs public RPC (must be within threshold)
        │
        ▼
Bonus tokens = chain_multiplier × 0.5 × current_rate
        │
        ▼
User NEXORA balance updated
```

---

## Claim Flow (On-Chain)

```
User opens web dashboard → clicks "Claim NEXORA"
    │
    ▼
Frontend calls POST /tokens/prepare-claim
    │
    ▼
Backend:
    1. Checks user has ≥ 1 NEXORA available
    2. Checks wallet is linked
    3. Generates EIP-712 voucher signed by backend signer key
    4. Returns: amount, nonce, deadline (5 min TTL), v/r/s signature
        │
        ▼
Frontend submits tx to ClaimDistributor contract (user pays gas)
    contract.claim(amount, nonce, deadline, v, r, s)
        │
        ▼
Contract:
    1. Verifies EIP-712 signature matches backend signer
    2. Marks nonce as used (prevents replay)
    3. Transfers (amount × 99.95%) NEXORA from treasury to user wallet
    4. Transfers (amount × 0.05%) NEXORA to DEX listing fund wallet
        │
        ▼
Frontend calls POST /tokens/confirm-claim
Backend deducts claimed amount from user's off-chain balance
```

---

## Proof-of-Activity Model

Nexora uses **Proof-of-Activity (PoA)**:

- No GPU or heavy computation required
- Rewards honest, consistent uptime
- Chain node verification adds a second layer — you must actually run the blockchain node
- Server independently queries public RPC to verify sync status — cannot be faked

---

## Configuration Storage

The CLI stores state in `~/.nexora/`:

```
~/.nexora/
├── config.json      — username, device_id, referral_code, node_token
├── node_info.json   — active node_id and node_token (kept on stop for resume)
├── node.log         — live heartbeat log
└── chain_info.json  — detected chain nodes
```
