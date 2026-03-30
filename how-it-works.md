# How Nexora Works

## High-Level Architecture

```
User Device
├── Nexora CLI
│   ├── Uptime heartbeat (every ~30s)
│   └── Chain node heartbeat (every ~60s)
└── Blockchain Node (optional, Base/ETH/OP/BNB)
        │
        ▼
Nexora Backend (Railway)
├── Anti-Cheat Validator
├── Chain Node Verifier
├── Reward Engine
└── PostgreSQL Database
```

---

## Registration Flow

```
1. User gets referral code from existing user
2. CLI generates device fingerprint (OS + hostname + MAC + CPU + RAM + disk)
3. User registers → gets unique referral code for inviting others
4. Device registered → linked to user account
5. Node registered → gets node_id + node_token for authentication
```

---

## Heartbeat Flow

Every ~30 seconds (with random jitter to avoid detection):

```
CLI sends POST /node/heartbeat
    node_id, node_token, device_id, uptime
        │
        ▼
Backend validates:
    1. Token authentication
    2. Node exists and is active
    3. Rate limit (≥ 20s since last heartbeat)
    4. Suspicious behavior analysis
    5. Uptime regression check
        │
        ▼
Points calculated:
    raw = uptime_delta / 60
    adjusted = raw × (node_score / 100)
        │
        ▼
User balance updated in PostgreSQL
```

---

## Chain Node Flow

Every ~60 seconds (when a local blockchain node is detected):

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
    3. Sync lag check vs public RPC
        │
        ▼
Bonus points = chain_multiplier × 0.5
        │
        ▼
User balance updated
```

---

## Proof-of-Activity Model

Nexora uses **Proof-of-Activity (PoA)**:

- No computation required
- Rewards honest, consistent uptime
- Chain node verification adds a second layer — you must actually run the blockchain node, not just claim to

For chain nodes specifically, the server independently queries the public RPC to verify your node's sync status. You cannot fake this.

---

## Configuration Storage

The CLI stores state in `~/.nexora/`:

```
~/.nexora/
├── config.json      — user, device, referral code, api_url
├── node_info.json   — active node_id and node_token
└── chain_info.json  — detected chain nodes
```

Do not manually edit these files.
