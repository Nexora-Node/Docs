# Node Behavior

## Heartbeat System

The heartbeat is the core mechanism that proves a node is alive and active. Every **30 seconds**, the CLI sends a heartbeat to the backend containing:

- `node_id` — the unique identifier of the node
- `device_id` — the device fingerprint
- `uptime` — total uptime in seconds since the node started

```
CLI Node
   │
   │  POST /node/heartbeat every 30s
   │  { node_id, device_id, uptime }
   ▼
Backend API
   │
   ├── Check: is heartbeat interval valid? (≥ 20s since last)
   ├── Check: is uptime delta realistic?
   ├── Check: is node registered?
   │
   ▼
Update last_seen, uptime → calculate points
```

If a heartbeat fails validation, it is rejected and no points are credited for that interval.

---

## Task Execution Lifecycle

> **Note:** Full task execution is planned for Phase 3. The current system focuses on uptime-based rewards.

When tasks are available, the lifecycle will follow this flow:

```
Backend assigns task to node
         │
         ▼
Node receives task via polling or push
         │
         ▼
Node executes task locally
         │
         ▼
Node submits result to backend
         │
         ▼
Backend validates result
         │
    ┌────┴────┐
  Valid     Invalid
    │           │
  Points     Rejected
 credited    (no reward)
```

---

## Validation Flow

Every heartbeat goes through a validation pipeline before any state is updated:

1. **Node existence check** — is this `node_id` registered?
2. **Device ownership check** — does this `device_id` own this node?
3. **Spam check** — has at least 20 seconds passed since the last heartbeat?
4. **Uptime delta check** — is the uptime increment within a realistic range?
5. **Node limit check** — does this device have ≤ 2 active nodes?

If all checks pass, the backend updates `last_seen`, increments `uptime`, and queues a points calculation.

---

## Node Lifecycle States

```
[REGISTERED] ──► [RUNNING] ──► [STOPPED]
                    │
                    │ (heartbeat timeout / no signal for extended period)
                    ▼
                [INACTIVE]
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
