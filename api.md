# API Overview

The Nexora backend exposes a RESTful API built with FastAPI. All endpoints accept and return JSON.

**Base URL:** `http://your-backend:8000`

Interactive documentation is available at:
- Swagger UI: `/docs`
- ReDoc: `/redoc`

---

## User Endpoints

### Register User

`POST /user/register`

Register a new user with a referral code.

**Request:**
```json
{
  "username": "alice",
  "referral_code": "NEXORA001"
}
```

**Response:**
```json
{
  "id": 1,
  "username": "alice",
  "referral_code": "ABC12345",
  "invited_by": "NEXORA001",
  "points": 0.0,
  "total_earned": 0.0,
  "created_at": "2024-01-01T00:00:00"
}
```

---

## Node Endpoints

### Register Node

`POST /node/register`

Register a new node for a device.

**Request:**
```json
{
  "device_id": "abc123def456",
  "system": "Linux-5.15.0-x86_64",
  "hostname": "my-vps"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Node registered successfully",
  "node_id": "node789xyz"
}
```

---

### Send Heartbeat

`POST /node/heartbeat`

Send a heartbeat signal from a running node.

**Request:**
```json
{
  "node_id": "node789xyz",
  "device_id": "abc123def456",
  "uptime": 3600.5
}
```

**Response:**
```json
{
  "success": true,
  "message": "Heartbeat received"
}
```

> **Note:** Heartbeats must be sent at least 20 seconds apart. The CLI handles this automatically.

---

### Get Node Status

`GET /node/status/{device_id}`

Get the status of all nodes registered to a device.

**Response:**
```json
[
  {
    "node_id": "node789xyz",
    "device_id": "abc123def456",
    "uptime": 3600.5,
    "last_seen": "2024-01-01T01:00:00",
    "status": "active"
  }
]
```

---

## Points Endpoints

### Get Points

`GET /points/{username}`

Retrieve the current points balance for a user.

**Response:**
```json
{
  "username": "alice",
  "points": 120.5,
  "total_earned": 340.0
}
```

---

### Claim Points

`POST /points/claim`

Claim the current points balance.

**Request:**
```json
{
  "username": "alice"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Successfully claimed 120.50 points",
  "points_claimed": 120.5
}
```

---

## Database Schema Reference

### Users

| Column | Type | Description |
|---|---|---|
| `id` | Integer | Primary key |
| `username` | String(50) | Unique username |
| `referral_code` | String(20) | User's unique referral code |
| `invited_by` | String(20) | Referral code of the inviter |
| `points` | Float | Current claimable balance |
| `total_earned` | Float | Lifetime points earned |
| `created_at` | DateTime | Registration timestamp |

### Devices

| Column | Type | Description |
|---|---|---|
| `id` | Integer | Primary key |
| `device_id` | String(64) | Unique device fingerprint |
| `user_id` | Integer | Foreign key to users |
| `created_at` | DateTime | Registration timestamp |

### Nodes

| Column | Type | Description |
|---|---|---|
| `id` | Integer | Primary key |
| `node_id` | String(64) | Unique node identifier |
| `device_id` | String(64) | Foreign key to devices |
| `uptime` | Float | Total uptime in seconds |
| `last_seen` | DateTime | Last heartbeat timestamp |
| `status` | String(20) | `active` or `stopped` |
| `created_at` | DateTime | Node start timestamp |
