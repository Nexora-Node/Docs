# Reward System

## How Points Are Earned

Points are earned passively based on validated node uptime. The formula is straightforward:

```
points = uptime_seconds / 60
```

For every **1 minute** of validated uptime, you earn **1 point**.

Points are calculated and credited server-side after each valid heartbeat. The backend tracks two values per user:

| Field | Description |
|---|---|
| `points` | Current claimable balance |
| `total_earned` | Lifetime total points earned |

---

## Earning Rate Examples

| Uptime | Points Earned |
|---|---|
| 1 hour | 60 points |
| 24 hours | 1,440 points |
| 7 days | 10,080 points |
| 30 days | 43,200 points |

> **Tip:** Running your node on a VPS or always-on server gives you the best uptime and therefore the highest point earnings.

---

## Points Flow

```mermaid
flowchart TD
    A([Node sends heartbeat]) --> B{Heartbeat valid?}
    B -->|No| C([Rejected - 0 points])
    B -->|Yes| D[Calculate uptime delta]
    D --> E[points += delta / 60\ntotal_earned += delta / 60]
    E --> F[(Update database)]
    F --> G([Points available for claim])

    style A fill:#7c3aed,color:#fff,stroke:none
    style C fill:#ef4444,color:#fff,stroke:none
    style G fill:#10b981,color:#fff,stroke:none
    style B fill:#f59e0b,color:#000,stroke:none
```

---

## Claim Mechanism

```mermaid
sequenceDiagram
    participant U as User
    participant C as CLI / API
    participant B as Backend
    participant D as Database

    U->>C: POST /points/claim\n{ username }
    C->>B: Forward claim request
    B->>D: Read current points balance
    D-->>B: points = 120.5
    B->>D: Reset points to 0\nRecord claim history
    D-->>B: OK
    B-->>C: { success: true, points_claimed: 120.5 }
    C-->>U: Successfully claimed 120.50 points
```

After a successful claim:
- Your `points` balance resets to `0`
- Your `total_earned` remains unchanged (it's a lifetime counter)
- The claimed amount is recorded for reward distribution

---

## Checking Your Points

Use the CLI status command:

```bash
python cli/main.py status
```

Or query the API directly:

```
GET /points/{username}
```

Response:

```json
{
  "username": "your_username",
  "points": 120.5,
  "total_earned": 340.0
}
```

---

## Future: Points → Token Conversion

> **Note:** Token integration is planned for Phase 3. The current system uses points as an internal reward currency. Conversion rates and mechanisms will be announced when token integration is ready.

The claim system is designed with future token conversion in mind. When token integration launches, claimed points will be convertible at a defined rate.
