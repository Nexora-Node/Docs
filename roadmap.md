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
    B --> E[Anti-Cheat Basic]
    A --> F[Device Fingerprint]
    A --> G[Heartbeat 30s]

    style A fill:#10b981,color:#fff,stroke:none
    style B fill:#10b981,color:#fff,stroke:none
    style C fill:#10b981,color:#fff,stroke:none
    style D fill:#10b981,color:#fff,stroke:none
    style E fill:#10b981,color:#fff,stroke:none
    style F fill:#10b981,color:#fff,stroke:none
    style G fill:#10b981,color:#fff,stroke:none
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

    style A fill:#2563eb,color:#fff,stroke:none
    style B fill:#2563eb,color:#fff,stroke:none
    style C fill:#f59e0b,color:#000,stroke:none
    style D fill:#f59e0b,color:#000,stroke:none
    style E fill:#f59e0b,color:#000,stroke:none
    style F fill:#f59e0b,color:#000,stroke:none
    style G fill:#f59e0b,color:#000,stroke:none
    style H fill:#f59e0b,color:#000,stroke:none
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
    A[Task Marketplace] <-->|Assign / Submit| B[Node Network]
    B --> C[Performance Score]
    C --> D[Bonus Multipliers]
    A --> E[Result Validation]
    E --> F[Advanced Anti-Cheat]
    F --> G[Behavioral Analysis]
    D --> H[Token Integration]
    H --> I[Points to Token Conversion]

    style A fill:#7c3aed,color:#fff,stroke:none
    style B fill:#7c3aed,color:#fff,stroke:none
    style H fill:#7c3aed,color:#fff,stroke:none
    style I fill:#7c3aed,color:#fff,stroke:none
    style C fill:#6b7280,color:#fff,stroke:none
    style D fill:#6b7280,color:#fff,stroke:none
    style E fill:#6b7280,color:#fff,stroke:none
    style F fill:#6b7280,color:#fff,stroke:none
    style G fill:#6b7280,color:#fff,stroke:none
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

    style A fill:#0f172a,color:#a78bfa,stroke:#7c3aed
    style B fill:#0f172a,color:#a78bfa,stroke:#7c3aed
    style C fill:#0f172a,color:#a78bfa,stroke:#7c3aed
    style D fill:#0f172a,color:#a78bfa,stroke:#7c3aed
    style E fill:#0f172a,color:#a78bfa,stroke:#7c3aed
    style F fill:#0f172a,color:#a78bfa,stroke:#7c3aed
    style G fill:#0f172a,color:#a78bfa,stroke:#7c3aed
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
    CLI Node & Backend       :done,    p1a, 2024-10, 2024-12
    Reward & Referral System :done,    p1b, 2024-10, 2024-12
    Basic Anti-Cheat         :done,    p1c, 2024-11, 2024-12

    section Phase 2 · Expansion
    VPS Deployment           :active,  p2a, 2025-01, 2025-02
    Task System v2           :active,  p2b, 2025-01, 2025-03
    Web Dashboard            :         p2c, 2025-02, 2025-04
    Public Beta              :         p2d, 2025-03, 2025-05

    section Phase 3 · Value Layer
    Task Marketplace         :         p3a, 2025-04, 2025-07
    Advanced Anti-Cheat      :         p3b, 2025-05, 2025-08
    Token Integration        :         p3c, 2025-07, 2025-09

    section Phase 4 · Ecosystem
    Developer API            :         p4a, 2025-10, 2026-01
    Decentralized Expansion  :         p4b, 2025-12, 2026-06
```

---

> **Note:** Roadmap timelines are goal-oriented, not date-bound. Phases ship when they are stable and ready. Follow the [GitHub repository](https://github.com/Nexora-Node/Node) for real-time progress updates.
