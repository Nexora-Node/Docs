# Node Behavior

## Heartbeat System

The heartbeat is the core mechanism that proves a node is alive and active. Every **30 seconds**, the CLI sends a heartbeat to the backend containing the node ID, device ID, and current uptime.

```mermaid
sequenceDiagram
    participant C as CLI Node
    participant B as Backend API
    participant D as Database

    loop Every 30 seconds
        C->>B: POST /node/heartbeat\n{ node_id, device_id, uptime }
        B->>B: Check interval ≥ 20s
        B->>B: Check uptime delta realistic
        B->>B: Check node registered
        alt All checks pass
            B->>D: Update last_seen + uptime
            D->>B: OK
            B->>B: Calculate points
            B-->>C: 200 OK - Heartbeat received
        else Validation failed
            B-->>C: 400 - Rejected, no points
        end
    end
```

If a heartbeat fails validation, it is rejected and no points are credited for that interval.

---

## Task Execution Lifecycle

> **Note:** Full task execution is planned for Phase 3. The current system focuses on uptime-based rewards.

```mermaid
flowchart TD
    A([Backend assigns task]) --> B[Node receives task\nvia polling or push]
    B --> C[Node executes task locally]
    C --> D[Node submits result to backend]
    D --> E{Backend validates result}
    E -->|Valid| F([Points credited to account])
    E -->|Invalid| G([Rejected - no reward])

    style A fill:#7c3aed,color:#fff,stroke:none
    style F fill:#10b981,color:#fff,stroke:none
    style G fill:#ef4444,color:#fff,stroke:none
    style E fill:#f59e0b,color:#000,stroke:none
```

---

## Validation Flow

Every heartbeat goes through a full validation pipeline before any state is updated:

```mermaid
flowchart TD
    A([Heartbeat received]) --> B{Node registered?}
    B -->|No| R1([Reject])
    B -->|Yes| C{Device owns node?}
    C -->|No| R2([Reject])
    C -->|Yes| D{Interval ≥ 20s?}
    D -->|No| R3([Reject - spam])
    D -->|Yes| E{Uptime delta realistic?}
    E -->|No| R4([Reject - manipulation])
    E -->|Yes| F{Device has ≤ 2 nodes?}
    F -->|No| R5([Reject - limit exceeded])
    F -->|Yes| G([✅ Valid - update state & credit points])

    style G fill:#10b981,color:#fff,stroke:none
    style R1 fill:#ef4444,color:#fff,stroke:none
    style R2 fill:#ef4444,color:#fff,stroke:none
    style R3 fill:#ef4444,color:#fff,stroke:none
    style R4 fill:#ef4444,color:#fff,stroke:none
    style R5 fill:#ef4444,color:#fff,stroke:none
    style A fill:#7c3aed,color:#fff,stroke:none
```

---

## Node Lifecycle States

```mermaid
stateDiagram-v2
    [*] --> REGISTERED : CLI register command
    REGISTERED --> RUNNING : CLI start command
    RUNNING --> STOPPED : CLI stop command
    RUNNING --> INACTIVE : Heartbeat timeout
    STOPPED --> RUNNING : CLI start command
    INACTIVE --> RUNNING : CLI start command

    note right of RUNNING
        Sending heartbeats every 30s
        Earning points continuously
    end note

    note right of INACTIVE
        No heartbeat received
        within expected window
        No points earned
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
