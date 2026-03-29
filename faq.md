# FAQ

## Is Nexora a mining platform?

No. Nexora does not involve mining, proof-of-work, or any heavy computation. There is no GPU required and no blockchain consensus to participate in. Nexora uses a **Proof-of-Activity** model — your node earns rewards simply by staying online and sending heartbeats. The resource usage is minimal.

---

## How do users earn rewards?

Rewards are earned through uptime. Every minute your node is running and sending valid heartbeats, you earn 1 point. Points accumulate in your account and can be claimed at any time. Additional earning opportunities (tasks, performance bonuses) are planned for future phases.

---

## Is it safe to run a Nexora node?

Yes. The Nexora CLI is open source and available on GitHub. It does not execute arbitrary code, does not access sensitive files, and only communicates with the Nexora backend API. The only data it sends is your node ID, device ID, and uptime — no personal information.

You can review the full source code at [github.com/Nexora-Node/Node](https://github.com/Nexora-Node/Node).

---

## Can I run multiple nodes?

You can run up to **2 nodes per device**. If you have multiple devices (e.g., a laptop and a VPS), each device can run up to 2 nodes independently. Attempting to run more than 2 nodes on a single device will be blocked by the backend.

---

## Do I need to keep my terminal open?

No. The node runs as a background process. Once started with `python cli/main.py start`, it continues running even if you close the terminal. On VPS environments, using `screen` or `tmux` is recommended to keep the backend running persistently.

---

## What happens if my node goes offline?

If your node stops sending heartbeats, it will eventually be marked as `INACTIVE`. No points are earned during downtime. When you restart the node, it resumes earning from that point forward. There is no penalty for going offline — you simply don't earn during that time.

---

## How do I get a referral code?

You need a referral code from an existing Nexora user to register. If you don't know anyone on the network, check the official Nexora community channels for available invite codes.

---

## When will token conversion be available?

Token integration is planned for Phase 3. There is no confirmed date. Points earned now will be convertible when the system launches. Follow the project on GitHub for announcements.

---

## Where can I get support?

- GitHub Issues: [github.com/Nexora-Node/Node/issues](https://github.com/Nexora-Node/Node/issues)
- Community channels will be announced as the network grows

---

## Is Nexora open source?

Yes. The full source code is available under the MIT License at [github.com/Nexora-Node/Node](https://github.com/Nexora-Node/Node).
