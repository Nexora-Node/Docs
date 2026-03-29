# Welcome to Nexora

Nexora is a distributed node network that rewards users for running lightweight nodes, maintaining uptime, and contributing to the network — no mining, no heavy computation, just honest participation.

---

## What You'll Find Here

This documentation covers everything you need to know about Nexora — from getting your first node running to understanding how rewards, anti-cheat, and the referral system work under the hood.

Use the sidebar to navigate between sections.

---

## Quick Start

```bash
# 1. Clone the repo
git clone https://github.com/Nexora-Node/Node.git
cd Node

# 2. Install dependencies
pip install -r requirements.txt

# 3. Seed the database (first time only)
python seed_database.py

# 4. Start the backend
cd backend && python main.py

# 5. Register your node
python cli/main.py register --ref NEXORA001

# 6. Start earning
python cli/main.py start
```

---

## Terminology

| Term | Definition |
|---|---|
| **Node** | A running instance of the Nexora CLI on a device |
| **Heartbeat** | A periodic signal sent every 30s to confirm the node is alive |
| **Points** | Reward currency earned through uptime (1 point per minute) |
| **Claim** | Converting your earned points into rewards |
| **Device ID** | A unique fingerprint generated from OS, hostname, and MAC address |
| **Referral Code** | A unique invite code required to register on the network |

---

> **Note:** Nexora is actively developed. This documentation reflects the current state of the project. Check the [Roadmap](roadmap.md) for what's coming next.

---

*Nexora — Distributed. Rewarded. Fair.*
