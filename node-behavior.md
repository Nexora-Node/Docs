# Node Behavior

## Heartbeat System

The heartbeat is the core mechanism that proves a node is alive and active. Every **30 seconds**, the CLI sends a heartbeat to the backend containing the node ID, device ID, and current uptime.

```mermaid
flowchart TD
    A[CLI sends POST /node/heartbeat] --> B{Interval 20s or more?}
    B -->|No| C[Rejected - spam]
    B -->|Yes| D{Uptime delta realistic?}
    D -->|No| E[Rejected - manipulation]
    D -->|Yes| F{Node registered?}
    F -->|No| G[Rejected - unknown node]
    F -->|Yes| H[Update last_seen and uptime]
    H --> I[Calculate and credit points]
    I --> J[Return 200 OK]

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

If a heartbeat fails validation, it is rejected and no points are credited for that interval.

---

## Task Execution Lifecycle

> **Note:** Full task execution is planned for Phase 3. The current system focuses on uptime-based rewards.

```mermaid
flowchart TD
    A[Backend assigns task to node] --> B[Node receives task]
    B --> C[Node executes task locally]
    C --> D[Node submits result to backend]
    D --> E{Backend validates result}
    E -->|Valid| F[Points credited to account]
    E -->|Invalid| G[Rejected - no reward]

    style A fill:#fff,stroke:#333,color:#000
    style B fill:#fff,stroke:#333,color:#000
    style C fill:#fff,stroke:#333,color:#000
    style D fill:#fff,stroke:#333,color:#000
    style E fill:#fff,stroke:#333,color:#000
    style F fill:#fff,stroke:#333,color:#000
    style G fill:#fff,stroke:#333,color:#000
```

---

## Validation Flow

Every heartbeat goes through a full validation pipeline before any state is updated.

```mermaid
flowchart TD
    A[Heartbeat received] --> B{Node registered?}
    B -->|No| B1[Reject]
    B -->|Yes| C{Device owns node?}
    C -->|No| C1[Reject]
    C -->|Yes| D{Interval 20s or more?}
    D -->|No| D1[Reject - spam]
    D -->|Yes| E{Uptime delta realistic?}
    E -->|No| E1[Reject - manipulation]
    E -->|Yes| F{Device has 2 nodes or fewer?}
    F -->|No| F1[Reject - limit exceeded]
    F -->|Yes| G[Valid - update state and credit points]

    style A fill:#fff,stroke:#333,color:#000
    style B fill:#fff,stroke:#333,color:#000
    style B1 fill:#fff,stroke:#333,color:#000
    style C fill:#fff,stroke:#333,color:#000
    style C1 fill:#fff,stroke:#333,color:#000
    style D fill:#fff,stroke:#333,color:#000
    style D1 fill:#fff,stroke:#333,color:#000
    style E fill:#fff,stroke:#333,color:#000
    style E1 fill:#fff,stroke:#333,color:#000
    style F fill:#fff,stroke:#333,color:#000
    style F1 fill:#fff,stroke:#333,color:#000
    style G fill:#fff,stroke:#333,color:#000
```

---

## Node Lifecycle States

```mermaid
flowchart TD
    A([Start]) --> B[REGISTERED]
    B -->|CLI start| C[RUNNING]
    C -->|CLI stop| D[STOPPED]
    C -->|Heartbeat timeout| E[INACTIVE]
    D -->|CLI start| C
    E -->|CLI start| C

    style A fill:#fff,stroke:#333,color:#000
    style B fill:#fff,stroke:#333,color:#000
    style C fill:#fff,stroke:#333,color:#000
    style D fill:#fff,stroke:#333,color:#000
    style E fill:#fff,stroke:#333,color:#000
```

| State | Description |
|---|---|
| `REGISTERED` | Node has been registered but not yet started |
| `RUNNING` | Node is active and sending heartbeats |
| `STOPPED` | Node was manually stopped via CLI |
| `INACTIVE` | Node has not sent a heartbeat within the expected window |

---

## Local State Files

| File | Purpose |
|---|---|
| `~/.nexora/config.json` | User and device configuration |
| `~/.nexora/node.pid` | PID of the running node process |

The PID file is created when the node starts and removed when it stops. If the node crashes unexpectedly, you may need to delete this file manually before restarting.
