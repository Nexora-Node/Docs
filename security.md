# Security & Fair Use

## Rules for Node Operators

Running a Nexora node comes with a set of responsibilities. These rules exist to protect the integrity of the network and ensure fair reward distribution for all participants.

### You are allowed to:

- Run 1 or 2 nodes on a single device
- Use a VPS, cloud server, or any always-on machine
- Share your referral code with genuine users
- Run the CLI on multiple different physical devices (each device is treated independently)
- Stop and restart your node as needed

### You are not allowed to:

- Run more than 2 nodes on a single device
- Modify the CLI to send fake or manipulated heartbeats
- Spoof or forge device IDs
- Create multiple accounts from the same device
- Automate referral registrations with fake users
- Use proxies or VPNs to bypass device or account limits
- Attempt to reverse-engineer or exploit the backend API

---

## Device Fingerprinting

Nexora generates a device ID from a combination of:
- Operating system information
- Hostname
- MAC address

This fingerprint is used to enforce the 2-node-per-device limit and to detect multi-account abuse. The device ID is generated locally and sent to the backend during registration.

> **Note:** The device ID is not personally identifiable information. It is a hash derived from system properties and does not contain your name, IP address, or any sensitive data.

---

## Data Stored by Nexora

| Data | Where Stored | Purpose |
|---|---|---|
| Username | Backend database | Account identification |
| Device ID (hashed) | Backend database | Node limit enforcement |
| Uptime | Backend database | Reward calculation |
| Referral relationships | Backend database | Referral reward distribution |
| Config (local) | `~/.nexora/config.json` | CLI operation |

Nexora does not collect passwords, personal information, or financial data.

---

## Responsible Disclosure

If you discover a security vulnerability in Nexora, please report it responsibly through the project's GitHub repository rather than exploiting it. The team takes security seriously and will address valid reports promptly.

---

> **Warning:** Attempting to exploit the API, manipulate reward calculations, or abuse the referral system will result in permanent account action and may be reported to relevant authorities if the abuse is significant.
