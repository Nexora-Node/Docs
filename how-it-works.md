# How Nexora Works

## High-Level Architecture

Nexora is composed of three main layers that work together to validate activity and distribute rewards.

```mermaid
graph TD
    A[User Device] --> B[CLI Node]
    B --> C[Backend API]
    C --> D{Anti-Cheat Validator}
    D -->|Pass| E[Reward Engine]
    D -->|Fail| F[Rejected]
    E --> G[(Database)]
    G --> H[User Points Balance]

    style A fill:#fff,stroke:#333,color:#000
    style B fill:#fff,stroke:#333,color:#000
    style C fill:#fff,stroke:#333,color:#000
    style D fill:#fff,stroke:#333,color:#000
    style E fill:#fff,stroke:#333,color:#000
    style F fill:#fff,stroke:#333,color:#000
    style G fill:#fff,stroke:#333,color:#000
    style H fill:#fff,stroke:#333,color:#000
```

- The **CLI Node** runs on the user's device and handles registration, heartbeats, and task execution.
- The **Backend API** (FastAPI) receives node signals, validates them, and updates state.
- The **Reward Engine** calculates points based on uptime and activity, applying anti-cheat rules before crediting any rewards.

---

## Node to Backend to Reward Flow

```mermaid
flowchart TD
    A[User installs CLI] --> B[Register with referral code]
    B --> C[Node starts]
    C --> D[Send heartbeat every 30s]
    D --> E{Backend validates}
    E -->|Valid| F[Calculate points]
    E -->|Invalid| G[Heartbeat rejected]
    F --> H[Credit points to account]
    H --> I{Ready to claim?}
    I -->|Yes| J[Claim points]
    I -->|No| D

    style A fill:#fff,stroke:#333,color:#000
    style B fill:#fff,stroke:#333,color:#000
    style C fill:#fff,stroke:#333,color:#000
    style D fill:#fff,stroke:#333,color:#000
    style E fill:#fff,stroke:#333,color:#000
    style F fill:#fff,stroke:#333,color:#000
    style G fill:#fff,stroke:#333,color:#000
    style H fill:#fff,stroke:#333,color:#000
    style I fill:#fff,stroke:#333,color:#000
    style J fill:#fff,stroke:#333,color:#000
```

---

## Proof-of-Activity Explained

Nexora uses a **Proof-of-Activity (PoA)** model. Unlike Proof-of-Work (mining), PoA does not require computation. Instead, it verifies that a node is:

1. **Online** — sending regular heartbeats within expected intervals
2. **Consistent** — uptime increments are realistic and not artificially inflated
3. **Unique** — the device is not running more nodes than allowed
4. **Honest** — heartbeat timing and uptime values pass all validation checks

A node earns points simply by staying online and behaving within the rules. The longer and more consistently a node runs, the more it earns.

---

> **Tip:** Running your node on a VPS or always-on server maximizes uptime and therefore maximizes your point earnings.

---

## Configuration Storage

The CLI stores its local state in `~/.nexora/config.json`:

```json
{
  "username": "your_username",
  "device_id": "generated_device_fingerprint",
  "referral_code": "YOUR_CODE",
  "api_url": "http://backend-url:8000",
  "registered_at": "2024-01-01T00:00:00"
}
```

This file is created automatically on first registration and should not be manually edited.
