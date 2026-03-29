# Roadmap

Nexora is built in deliberate phases — each one expanding the network's capabilities, security, and value. This roadmap reflects our current progress and what's ahead.

---

## Overview

```mermaid
timeline
    title Nexora Development Roadmap
    section Phase 1 · Foundation
        Q4 2024 : CLI Node (Python)
               : FastAPI Backend
               : Uptime Reward System
               : Referral System
               : Basic Anti-Cheat
    section Phase 2 · Network Expansion
        Q1 2025 : Stable VPS Deployment
               : Task System v2
               : Web Dashboard
               : Public Beta
    section Phase 3 · Scaling & Value
        Q2-Q3 2025 : Task Marketplace
                  : Advanced Anti-Cheat
                  : Performance Rewards
                  : Token Integration
    section Phase 4 · Ecosystem
        Q4 2025+ : Developer API
                : Third-Party Integrations
                : Decentralized Expansion
                : Community Governance
```

---

## Phase 1 — Foundation

> ✅ Completed

The core infrastructure is live. Users can register, run nodes, earn points, and refer others.

```mermaid
graph LR
    A[CLI Node] --> B[FastAPI Backend]
    B --> C[Reward Engine]
    B --> D[Referral System]
    B --> E[Anti-Cheat]
    A --> F[Device Fingerprint]
    A --> G[Heartbeat 30s]

    style A fill:#166534,stroke:#166534,color:#fff
    style B fill:#166534,stroke:#166534,color:#fff
    style C fill:#166534,stroke:#166534,color:#fff
    style D fill:#166534,stroke:#166534,color:#fff
    style E fill:#166534,stroke:#166534,color:#fff
    style F fill:#166534,stroke:#166534,color:#fff
    style G fill:#166534,stroke:#166534,color:#fff
```

| Milestone | Status |
|---|---|
| CLI Node (Python, cross-platform) | ✅ Done |
| FastAPI backend with SQLAlchemy | ✅ Done |
| Uptime-based reward system (1 pt/min) | ✅ Done |
| Referral system with invite-only registration | ✅ Done |
| Basic anti-cheat (node limit, spam, uptime validation) | ✅ Done |
| Cross-platform support (Linux, Windows, VPS, Termux) | ✅ Done |

---

## Phase 2 — Network Expansion

> 🔄 In Progress

Stabilizing the network, improving the task system, and opening to a wider audience.

```mermaid
graph LR
    A[Production VPS] --> B[Stable Backend]
    B --> C[Task System v2]
    C --> D[Result Validation]
    B --> E[Web Dashboard]
    E --> F[Node Status UI]
    E --> G[Points UI]
    B --> H[Public Beta]

    style A fill:#1e3a5f,stroke:#1e3a5f,color:#fff
    style B fill:#1e3a5f,stroke:#1e3a5f,color:#fff
    style C fill:#1d4ed8,stroke:#1d4ed8,color:#fff
    style D fill:#1d4ed8,stroke:#1d4ed8,color:#fff
    style E fill:#1d4ed8,stroke:#1d4ed8,color:#fff
    style F fill:#1d4ed8,stroke:#1d4ed8,color:#fff
    style G fill:#1d4ed8,stroke:#1d4ed8,color:#fff
    style H fill:#1d4ed8,stroke:#1d4ed8,color:#fff
```

| Milestone | Status |
|---|---|
| Stable VPS deployment with production backend | 🔄 In Progress |
| Task system v2 (structured types, result validation) | 🔄 In Progress |
| Web dashboard (node status, points, referrals) | 🔜 Planned |
| Public beta with monitored onboarding | 🔜 Planned |
| Backend monitoring and logging | 🔜 Planned |

---

## Phase 3 — Scaling & Value Layer

> 🔜 Planned

Making the network more valuable, more resilient, and ready for token integration.

```mermaid
graph TD
    A[Task Marketplace] --> B[Node Network]
    B --> A
    B --> C[Performance Score]
    C --> D[Bonus Multipliers]
    A --> E[Result Validation]
    E --> F[Advanced Anti-Cheat]
    F --> G[Behavioral Analysis]
    D --> H[Token Integration]
    H --> I[Points to Token Conversion]

    style A fill:#3b0764,stroke:#3b0764,color:#fff
    style B fill:#3b0764,stroke:#3b0764,color:#fff
    style C fill:#4c1d95,stroke:#4c1d95,color:#fff
    style D fill:#4c1d95,stroke:#4c1d95,color:#fff
    style E fill:#4c1d95,stroke:#4c1d95,color:#fff
    style F fill:#4c1d95,stroke:#4c1d95,color:#fff
    style G fill:#4c1d95,stroke:#4c1d95,color:#fff
    style H fill:#6d28d9,stroke:#6d28d9,color:#fff
    style I fill:#6d28d9,stroke:#6d28d9,color:#fff
```

| Milestone | Status |
|---|---|
| Real task marketplace (nodes pick up meaningful tasks) | 🔜 Planned |
| Advanced anti-cheat (behavioral analysis, pattern detection) | 🔜 Planned |
| Performance-based rewards (uptime multipliers) | 🔜 Planned |
| Node reputation scoring | 🔜 Planned |
| Token integration — points-to-token conversion | 🔜 Planned |

---

## Phase 4 — Ecosystem

> 🔮 Future

Opening Nexora to third-party builders and moving toward decentralization.

```mermaid
graph TD
    A[Developer API] --> B[Third-Party Task Submitters]
    B --> C[Node Network]
    C --> D[On-Chain Reward Distribution]
    D --> E[Decentralized Node Registry]
    E --> F[Community Governance]
    F --> G[Node Operator Voting]

    style A fill:#1e1b4b,stroke:#312e81,color:#c7d2fe
    style B fill:#1e1b4b,stroke:#312e81,color:#c7d2fe
    style C fill:#1e1b4b,stroke:#312e81,color:#c7d2fe
    style D fill:#1e1b4b,stroke:#312e81,color:#c7d2fe
    style E fill:#1e1b4b,stroke:#312e81,color:#c7d2fe
    style F fill:#1e1b4b,stroke:#312e81,color:#c7d2fe
    style G fill:#1e1b4b,stroke:#312e81,color:#c7d2fe
```

| Milestone | Status |
|---|---|
| Developer API (third parties submit tasks to the network) | 🔮 Future |
| Third-party platform integrations | 🔮 Future |
| On-chain reward distribution (optional) | 🔮 Future |
| Decentralized node registry | 🔮 Future |
| Community governance for network parameters | 🔮 Future |

---

## Full Timeline at a Glance

```mermaid
gantt
    title Nexora Roadmap Timeline
    dateFormat YYYY-MM
    axisFormat %b %Y

    section Phase 1 · Foundation
    CLI Node and Backend         :done,    p1a, 2024-10, 2024-12
    Reward and Referral System   :done,    p1b, 2024-10, 2024-12
    Basic Anti-Cheat             :done,    p1c, 2024-11, 2024-12

    section Phase 2 · Expansion
    VPS Deployment               :active,  p2a, 2025-01, 2025-02
    Task System v2               :active,  p2b, 2025-01, 2025-03
    Web Dashboard                :         p2c, 2025-02, 2025-04
    Public Beta                  :         p2d, 2025-03, 2025-05

    section Phase 3 · Value Layer
    Task Marketplace             :         p3a, 2025-04, 2025-07
    Advanced Anti-Cheat          :         p3b, 2025-05, 2025-08
    Token Integration            :         p3c, 2025-07, 2025-09

    section Phase 4 · Ecosystem
    Developer API                :         p4a, 2025-10, 2026-01
    Decentralized Expansion      :         p4b, 2025-12, 2026-06
```

---

> **Note:** Roadmap timelines are goal-oriented, not date-bound. Phases ship when they are stable and ready. Follow the [GitHub repository](https://github.com/Nexora-Node/Node) for real-time progress updates.
