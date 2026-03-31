# NEXORA Token Reward System

## Token Allocation

| Allocation | Amount | Purpose |
|---|---|---|
| Mining Rewards | 200,000 NEXOR | Distributed to node operators over ~100 years |
| Reserve | 40,000 NEXOR | Liquidity, dev, airdrop, ecosystem |
| **Total Supply** | **240,000 NEXOR** | Fixed, non-mintable |

---

## Smooth Decay Model

Nexora uses a **5% smooth decay** every 24 days instead of a hard halving.
This keeps rewards stable and predictable for long-term miners.

### Formula

```
rate(epoch) = BASE_RATE × 0.95^epoch

BASE_RATE = 10,000 / 34,560 = 0.289352 NEXORA/min
         (10,000 NEXORA per first 24-day period ÷ 34,560 minutes)

epoch = floor(days_elapsed / 24)
```

### Why This Formula?

Using the geometric series sum to infinity:

```
Total = BASE_RATE_PER_PERIOD / (1 - decay_factor)
      = 10,000 / (1 - 0.95)
      = 10,000 / 0.05
      = 200,000 NEXORA  ✓
```

The total mining supply converges exactly to **200,000 NEXORA** over infinite time.

---

## Epoch Schedule

| Epoch | Days | Rate (NEXORA/min) | Period Emission |
|---|---|---|---|
| 0 | 0–23 | 0.289352 | 10,000 NEXORA |
| 1 | 24–47 | 0.274884 | 9,500 NEXORA |
| 2 | 48–71 | 0.261140 | 9,025 NEXORA |
| 3 | 72–95 | 0.248083 | 8,574 NEXORA |
| 10 | 240–263 | 0.174339 | 6,025 NEXORA |
| 30 | 720–743 | 0.063494 | 2,194 NEXORA |
| 60 | 1440–1463 | 0.013527 | 468 NEXORA |
| 150 | 3600–3623 | 0.000133 | 4.6 NEXORA |

Rewards never reach zero — they approach it asymptotically.
Mining stops only when `total_distributed` reaches 200,000 NEXORA.

---

## Per-Heartbeat Reward Calculation

```
uptime_delta  = current_uptime - last_uptime (seconds)
rate          = 0.289352 × 0.95^epoch        (NEXORA/min)
raw_tokens    = (uptime_delta / 60) × rate
multiplier    = node_score / 100             (0.0 – 1.0)
tokens_earned = raw_tokens × multiplier
```

**Example** (epoch 0, score 100, 30s heartbeat interval):
```
raw    = (30 / 60) × 0.289352 = 0.144676 NEXORA
earned = 0.144676 × 1.0       = 0.144676 NEXORA per heartbeat
       = 8.68 NEXORA/hour
       = 208.3 NEXORA/day  (single node, score 100)
```

---

## Node Score Multiplier

Every node starts at score 100. Violations reduce it, stable uptime increases it.

| Score | Multiplier | Status |
|---|---|---|
| 80–100 | 0.80–1.00 | Healthy |
| 50–79 | 0.50–0.79 | Reduced rewards |
| 20–49 | 0.10–0.25 | Heavily penalized |
| < 20 | 0 | Suspended |

---

## Blockchain Node Bonus

Running a verified local blockchain full node earns **bonus NEXORA** on top of uptime rewards.
The server verifies your node is actually synced before crediting bonuses.

```
bonus = chain_multiplier × 0.5 × current_rate
```

| Network | Multiplier | Bonus/heartbeat (epoch 0) |
|---|---|---|
| ETH Mainnet | 5× | 0.723 NEXORA |
| Base Mainnet | 3× | 0.434 NEXORA |
| OP Mainnet | 2× | 0.289 NEXORA |
| BNB Chain | 2× | 0.289 NEXORA |
| Base Sepolia | 1.5× | 0.217 NEXORA |

---

## Claiming NEXORA

NEXORA earned from mining is **off-chain balance** in the Nexora database.
To convert to real on-chain tokens:

1. Link your EVM wallet in the web dashboard
2. Click **Claim NEXORA**
3. Confirm the transaction in your wallet (you pay gas on Base)
4. NEXORA transfers from treasury to your wallet
5. 0.05% fee goes to DEX listing fund

**Minimum claim:** 1 NEXORA
**Fee:** 0.05% of claimed amount
**Network:** Base Mainnet

---

## Supply Progress

Check real-time supply stats:

```
GET https://node-production-712b.up.railway.app/mining/info
```

```json
{
  "current_epoch": 0,
  "current_rate_per_min": 0.28935185,
  "days_until_next_decay": 23.8,
  "total_distributed": 16.5,
  "mining_supply_cap": 200000,
  "remaining_supply": 199983.5
}
```
