# Referral System

## How Referrals Work

Every user who registers on Nexora receives a unique referral code. This code can be shared with others to invite them to the network.

Registration on Nexora is **invite-only** — a valid referral code is required to create an account. This keeps the network quality high and reduces spam and bot registrations.

---

## Registration Flow

```mermaid
sequenceDiagram
    participant R as Referrer
    participant N as New User
    participant B as Backend API

    R->>N: Shares referral code
    N->>B: POST /user/register with referral code
    B->>B: Validate referral code exists
    B->>B: Check code is not suspended
    alt Valid code
        B->>B: Create user account
        B->>B: Record referral relationship
        B-->>N: Account created with new referral code
    else Invalid code
        B-->>N: 400 Invalid referral code
    end
    Note over B,R: Referrer earns bonus when new user becomes active
```

---

## Referral Reward Flow

```mermaid
flowchart TD
    A([Referred user runs node]) --> B[Referred user earns points]
    B --> C[Backend detects active referral]
    C --> D[Calculate referral bonus]
    D --> E([Bonus credited to referrer])

    style A fill:#1e3a5f,stroke:#1e3a5f,color:#fff
    style B fill:#1e293b,stroke:#475569,color:#cbd5e1
    style C fill:#1e293b,stroke:#475569,color:#cbd5e1
    style D fill:#1e293b,stroke:#475569,color:#cbd5e1
    style E fill:#14532d,stroke:#14532d,color:#fff
```

---

## Referral Code Details

- Each user gets exactly one referral code, generated at registration
- Referral codes are unique across the network
- The relationship between referrer and referred is stored permanently
- You can find your referral code using `python cli/main.py status`

---

## Reward Distribution

When a referred user earns points through uptime, a portion is credited to the referrer as a bonus. This incentivizes users to invite genuine, active participants rather than inactive accounts.

> **Note:** Exact referral reward rates will be published as the reward system matures. The current implementation records the referral relationship and is designed to support bonus distribution.

---

## Referral Rules

- You cannot refer yourself
- Referral codes from suspended accounts are invalidated
- Coordinated fake referral chains are detected by the anti-cheat system and penalized
- There is no limit on how many people you can refer

---

> **Tip:** The best way to maximize referral rewards is to invite users who will actually run their nodes consistently. Inactive referrals generate no bonus for the referrer.
