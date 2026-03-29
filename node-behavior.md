# Node Behavior

## Heartbeat System

The heartbeat is the core mechanism that proves a node is alive and active. Every **30 seconds**, the CLI sends a heartbeat to the backend containing the node ID, device ID, and current uptime.

```mermaid
sequenceDiagram
    participant C as CLI Node
    participant B as Backend API
    participant D as Database

    loop Every 30 seconds
        C->>B: POST /node/heartbeat
        B->>B: Check interval is 20s or more
        B->>B: Check uptime delta is realistic
        B->>B: Check node is registered
        alt All checks pass
            B->>D: Update last_seen and uptime
            D->>B: OK
            B->>B: Calculate points
            B-->>C: 200 OK
        else Validation failed
            B-->>C: 400 Rejected
        end
    end
```

If a heartbeat fails validation, it is rejected and no points are credited for that interval.

---

## Task Execution Lifecycle

> **Note:** Full task execution is planned for Phase 3. The current system focuses on uptime-based rewards.

```mermaid
flowchart TD
    A([Backend assigns task]) --> B[Node receives task]
    B --> C[Node executes task locally]
    C --> D[Node submits result]
    D --> E{Backend validates result}
    E -->|Valid| F([Points credited])
    E -->|Invalid| G([Rejected])

    style A fill:#1e3a5f,stroke:#1e3a5f,color:#fff
    style B fill:#1e293b,stroke:#475569,color:#cbd5e1
    style C fill:#1e293b,stroke:#475569,color:#cbd5e1
    style D fill:#1e293b,stroke:#475569,color:#cbd5e1
    style E fill:#78350f,stroke:#78350f,color:#fff
    style F fill:#14532d,stroke:#14532d,color:#fff
    style G fill:#7f1d1d,stroke:#7f1d1d,color:#fff
```

---

## Validation Flow

Every heartbeat goes through a full validation pipeline before any state is updated.

```mermaid
flowchart TD
    A([Heartbeat received]) --> B{Node registered?}
    B -->|No| R1([Reject])
    B -->|Yes| C{Device owns node?}
    C -->|No| R2([Reject])
    C -->|Yes| D{Interval 20s or more?}
    D -->|No| R3([Reject - spam])
    D -->|Yes| E{Uptime delta realistic?}
    E -->|No| R4([Reject - manipulation])
    E -->|Yes| F{Device has 2 nodes or fewer?}
    F -->|No| R5([Reject - limit exceeded])
    F -->|Yes| G([Valid - update state and credit points])

    style A fill:#1e3a5f,stroke:#1e3a5f,color:#fff
    style G fill:#14532d,stroke:#14532d,color:#fff
    style R1 fill:#7f1d1d,stroke:#7f1d1d,color:#fff
    style R2 fill:#7f1d1d,stroke:#7f1d1d,color:#fff
    style R3 fill:#7f1d1d,stroke:#7f1d1d,color:#fff
    style R4 fill:#7f1d1d,stroke:#7f1d1d,color:#fff
    style R5 fill:#7f1d1d,stroke:#7f1d1d,color:#fff
    style B fill:#78350f,stroke:#78350f,color:#fff
    style C fill:#78350f,stroke:#78350f,color:#fff
    style D fill:#78350f,stroke:#78350f,color:#fff
    style E fill:#78350f,stroke:#78350f,color:#fff
    style F fill:#78350f,stroke:#78350f,color:#fff
```

---

## Node Lifecycle States

```mermaid
stateDiagram-v2
    [*] --> REGISTERED : CLI register
    REGISTERED --> RUNNING : CLI start
    RUNNING --> STOPPED : CLI stop
    RUNNING --> INACTIVE : Heartbeat timeout
    STOPPED --> RUNNING : CLI start
    INACTIVE --> RUNNING : CLI start

    note right of RUNNING
        Sending heartbeats every 30s
        Earning points continuously
    end note

    note right of INACTIVE
        No heartbeat within expected window
        No points earned during this period
    end note
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
