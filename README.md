<p align="center">
  <img src="./logo.png" alt="Nexora Logo" width="120"/>
</p>

# Welcome to Nexora

Nexora is a distributed node network that rewards users for running lightweight nodes, maintaining uptime, and optionally securing blockchain networks — no heavy mining, no GPU required, just honest participation.

---

## What You'll Find Here

This documentation covers everything you need to know about Nexora — from getting your first node running to understanding how rewards, anti-cheat, blockchain node verification, and the referral system work.

---

## Quick Start

```bash
# 1. Clone the repo
git clone https://github.com/Nexora-Node/Node.git
cd Node

# 2. Install dependencies
pip install -r requirements.txt

# 3. Register your node (get a referral code from an existing user)
python cli/main.py register --ref YOUR_REF_CODE

# 4. Start earning
python cli/main.py start
```

The backend is already running at `https://node-production-712b.up.railway.app` — no local server setup needed.

---

## Terminology

| Term | Definition |
|---|---|
| **Node** | A running instance of the Nexora CLI on a device |
| **Heartbeat** | A periodic signal sent every ~30s to confirm the node is alive |
| **Chain Node** | A local blockchain full node (Base, ETH, OP, BNB, etc.) being tracked by Nexora |
| **Points** | Reward currency earned through uptime and chain node verification |
| **Claim** | Converting your earned points into rewards |
| **Device ID** | A unique fingerprint generated from OS, hostname, and MAC address |
| **Referral Code** | A unique single-use invite code required to register |
| **Reward Multiplier** | Bonus applied to points when running a verified blockchain node |

---

> **Note:** Nexora is actively developed. Check the [Roadmap](roadmap.md) for what's coming next.

---

*Nexora — Distributed. Verified. Rewarded.*
