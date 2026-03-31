# Introduction

## What is Nexora?

Nexora is a distributed node network where users run lightweight CLI-based nodes and earn **NEXORA tokens** based on uptime and contribution to the network. Optionally, users who run local blockchain full nodes (Base, ETH, OP, BNB) earn significantly higher rewards for helping secure those networks.

It is not a mining platform. No GPU, no heavy computation. Nexora is built around a **Proof-of-Activity** model: if your node is online and behaving honestly, you earn NEXORA.

---

## Two Ways to Earn

**1. Basic uptime node** — run the CLI, earn NEXORA passively. Works on any device (laptop, VPS, Raspberry Pi).

**2. Blockchain node operator** — run a Base/ETH/OP/BNB full node locally, earn 1.5×–5× bonus NEXORA on top of uptime rewards. The server independently verifies your node is synced.

---

## Token: NEXORA (NEXOR)

| Property | Value |
|---|---|
| Token Name | NEXORA NODE |
| Symbol | NEXOR |
| Network | Base Mainnet |
| Contract | `0xE0a4a9d3263ee93E167196954Ea4684418911E24` |
| Total Supply | 240,000 NEXOR (fixed, non-mintable) |
| Mining Allocation | 200,000 NEXOR |
| Reserve | 40,000 NEXOR |
| Decimals | 18 |

---

## How Rewards Work

NEXORA uses a **smooth 5% decay** model — rewards decrease by 5% every 24 days.
This ensures the 200,000 mining supply lasts approximately 100 years.

```
Starting rate: 0.289352 NEXORA/min (global, shared across all nodes)
Decay: ×0.95 every 24 days
Total converges to: 200,000 NEXORA
```

---

## The Problem Nexora Solves

| Problem | Nexora's Approach |
|---|---|
| High entry barrier | Lightweight CLI, works on any device |
| Energy waste | No computation — uptime-based rewards |
| Unfair distribution | Node score system, anti-cheat enforcement |
| No verification | Chain nodes verified against public RPCs |
| Bot farming | Device fingerprinting, PoW, behavioral analysis |
| Centralized rewards | On-chain claim via EIP-712 signed vouchers |

---

## Quick Start

```bash
# Install
git clone https://github.com/Nexora-Node/Node
pip install -r requirements.txt

# Register (need a referral code)
cd cli
python main.py register --ref YOUR_REFERRAL_CODE

# Start mining
python main.py start
```

The dashboard opens automatically and shows your NEXORA balance, mining rate, and node status in real-time.

---

> Nexora is in active development. The network launched with a fixed supply and smooth decay model designed for long-term sustainability.
