# Reward System

## Base Uptime Rewards

Points are earned passively based on validated node uptime:

```
points_per_heartbeat = uptime_delta_seconds / 60 × node_score_multiplier
```

**1 point per minute** of validated uptime, adjusted by your node score (0–100).

| Uptime | Base Points |
|---|---|
| 1 hour | 60 pts |
| 24 hours | 1,440 pts |
| 7 days | 10,080 pts |
| 30 days | 43,200 pts |

---

## Node Score Multiplier

Every node has a score (0–100, default 100). Your actual points earned are:

```
adjusted_points = raw_points × (node_score / 100)
```

Scores decrease for violations and increase for stable long uptime. A node with score 80 earns 80% of base points.

---

## Blockchain Node Bonus Rewards

Running a verified local blockchain full node earns **bonus points on top of base uptime rewards**. The server verifies your node is actually synced before crediting bonuses.

| Network | Chain ID | Bonus per Heartbeat | Multiplier |
|---|---|---|---|
| ETH Mainnet | 1 | 2.5 pts | 5× |
| Base Mainnet | 8453 | 1.5 pts | 3× |
| OP Mainnet | 10 | 1.0 pts | 2× |
| BNB Chain | 56 | 1.0 pts | 2× |
| Base Sepolia | 84532 | 0.75 pts | 1.5× |
| ETH Sepolia | 11155111 | 0.75 pts | 1.5× |
| OP Sepolia | 11155420 | 0.75 pts | 1.5× |
| BNB Testnet | 97 | 0.6 pts | 1.2× |

Chain heartbeats are sent every ~60 seconds. To earn chain bonuses, your blockchain node must be within the allowed sync lag threshold.

---

## Checking Your Points

```bash
python cli/main.py status
```

Or via API:

```
GET /points/{username}
```

```json
{
  "username": "your_username",
  "points": 120.5,
  "total_earned": 340.0
}
```

---

## Claiming Points

```bash
python cli/main.py claim
```

After claiming:
- `points` balance resets to `0`
- `total_earned` remains (lifetime counter)

---

## Future: Points to Token Conversion

Token integration is planned for a future phase. Conversion rates will be announced when ready.
