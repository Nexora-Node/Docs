# Installation Guide

## Requirements

| Requirement | Minimum |
|---|---|
| Python | 3.8+ |
| pip | Latest |
| Internet connection | Required |
| Referral code | Required for registration |

---

## Option A — Connect to Production Server (Recommended)

The Nexora backend is already running in production. You only need the CLI.

```bash
# 1. Clone the repo
git clone https://github.com/Nexora-Node/Node.git
cd Node

# 2. Install dependencies
pip install -r requirements.txt

# 3. Register (get a referral code from an existing user)
python cli/main.py register --ref YOUR_REF_CODE

# 4. Start your node
python cli/main.py start
```

The CLI automatically connects to `https://node-production-712b.up.railway.app`.

---

## Option B — Run Your Own Backend (Self-Hosted)

### Step 1 — Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 2 — Set Up Database

For local development, SQLite is used automatically. For production, set the `DATABASE_URL` environment variable:

```bash
export DATABASE_URL=postgresql://user:password@host:5432/dbname
```

### Step 3 — Seed the Database

```bash
python seed_database.py
```

This creates the initial admin user with a random referral code. Note the referral code printed — you'll need it to register.

### Step 4 — Start the Backend

```bash
cd backend
python main.py
```

Backend starts on `http://localhost:8000`.

### Step 5 — Point CLI to Your Backend

```bash
export NEXORA_API_URL=http://localhost:8000
python cli/main.py register --ref YOUR_SEED_CODE
```

---

## CLI Commands Reference

| Command | Description |
|---|---|
| `register --ref CODE` | Register a new user with a referral code |
| `start` | Start the node (auto-detects local blockchain nodes) |
| `stop` | Stop the running node |
| `status` | Show node status, chain nodes, and current points |
| `claim` | Claim available points |
| `chains` | List all supported blockchain networks and multipliers |

---

## Platform Notes

### Linux / VPS

```bash
# Use screen or tmux to keep the node running after logout
screen -S nexora
python cli/main.py start
# Ctrl+A, D to detach
```

### Windows

```cmd
python cli/main.py register --ref YOUR_REF_CODE
python cli/main.py start
```

### Android (Termux)

```bash
pkg install python
pip install -r requirements.txt
python cli/main.py register --ref YOUR_REF_CODE
python cli/main.py start
```

---

## Troubleshooting

**"Cannot connect to server"**
Check your internet connection. The production server is at `https://node-production-712b.up.railway.app`.

**"Device not found. Register your device first."**
Run `python cli/main.py register --ref CODE` before starting.

**"Invalid referral code"**
Referral codes are single-use. Get a fresh code from an existing user.

**"Maximum 2 nodes per device allowed"**
Each device supports max 2 active nodes. Stop one before starting another.

**"Heartbeat spam detected"**
Heartbeats must be at least 20 seconds apart. Do not modify the CLI heartbeat interval.
