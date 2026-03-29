# Key Features

## CLI Node

The Nexora CLI is a lightweight Python-based command-line tool that runs on any platform — Linux, Windows, VPS, or Android (Termux). It handles everything from registration to heartbeat transmission.

Key characteristics:
- No GUI required
- Runs in the background as a daemon process
- Minimal resource usage (no computation, just network calls)
- Stores state locally in `~/.nexora/`

---

## Task Execution System

Nodes can be assigned tasks by the network. Tasks are lightweight units of work that contribute to the network's operation. The task system is designed to be:

- **Non-intensive** — tasks do not require significant CPU or memory
- **Verifiable** — results are validated by the backend before rewards are credited
- **Optional** — uptime alone is sufficient to earn points; tasks provide additional earning opportunities

> **Note:** The full task marketplace is planned for Phase 3. In the current version, uptime tracking is the primary reward mechanism.

---

## Uptime Tracking

Every node sends a heartbeat signal to the backend every **30 seconds**. The backend:

1. Records the timestamp of each heartbeat
2. Calculates the uptime delta since the last valid heartbeat
3. Validates the delta against expected ranges
4. Credits points proportional to validated uptime

Uptime is measured in seconds and converted to points at a rate of **1 point per minute**.

---

## Reward System

Points are earned passively through uptime and activity. They accumulate in the user's account and can be claimed at any time.

- Points are calculated server-side to prevent manipulation
- Claimed points are tracked separately from total earned
- The claim mechanism is designed to support future token conversion

---

## Referral System

Every user receives a unique referral code upon registration. Sharing this code with others earns the referrer bonus points when the referred user becomes active.

- Referral codes are required to register (no open registration without a code)
- This keeps the network invite-only and reduces spam
- Referral rewards are distributed automatically

---

## Anti-Cheat System

Nexora includes a multi-layer anti-cheat system to ensure fair reward distribution:

- **Max 2 nodes per device** — enforced via device fingerprinting
- **Heartbeat spam detection** — minimum 20 seconds between heartbeats
- **Uptime validation** — unrealistic uptime jumps are rejected
- **Advanced detection** — behavioral analysis for suspicious patterns

Violations result in warnings, reward reductions, or shadow bans depending on severity.
