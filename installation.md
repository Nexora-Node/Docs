# Installation Guide

## Requirements

| Requirement | Minimum Version |
|---|---|
| Python | 3.8+ |
| pip | Latest |
| Internet connection | Required |
| Referral code | Required for registration |

---

## Step 1 — Clone the Repository

```bash
git clone https://github.com/Nexora-Node/Node.git
cd Node
```

---

## Step 2 — Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Step 3 — Seed the Database (First-Time Setup Only)

This step is only required when setting up the backend for the first time. It creates an initial seed user with referral code `NEXORA001`.

```bash
python seed_database.py
```

---

## Step 4 — Start the Backend Server

```bash
cd backend
python main.py
```

The backend will start on `http://localhost:8000`.

You can verify it's running by visiting:
- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

---

## Step 5 — Register Your Node

```bash
python cli/main.py register --ref NEXORA001
```

You will be prompted to enter a username. The CLI will:
- Generate a unique device ID from your OS, hostname, and MAC address
- Register your user and device with the backend
- Save your configuration to `~/.nexora/config.json`

---

## Step 6 — Start Your Node

```bash
python cli/main.py start
```

Your node will start running in the background, sending heartbeats every 30 seconds.

---

## Platform-Specific Instructions

### Linux / VPS

```bash
# Install Python if needed
sudo apt update && sudo apt install python3 python3-pip

# Use screen or tmux to keep processes alive
screen -S nexora-backend
python3 backend/main.py

# Open a new screen session
screen -S nexora-node
python3 cli/main.py register --ref NEXORA001
python3 cli/main.py start
```

### Windows

```cmd
python cli/main.py register --ref NEXORA001
python cli/main.py start
```

### Android (Termux)

```bash
pkg install python
pip install -r requirements.txt
python seed_database.py

# Start backend
cd backend
python main.py &
cd ..

# Register and start node
python cli/main.py register --ref NEXORA001
python cli/main.py start
```

---

## CLI Commands Reference

| Command | Description |
|---|---|
| `register --ref CODE` | Register a new user with a referral code |
| `start` | Start the node in background mode |
| `stop` | Stop the running node |
| `status` | Show node status and current points |

---

## Troubleshooting

**"Cannot connect to server"**
Make sure the backend is running:
```bash
cd backend && python main.py
```

**"Node is already running"**
Stop the existing node first:
```bash
python cli/main.py stop
```

**"Invalid referral code"**
Use the seed code `NEXORA001` or get a valid code from an existing user.

**"Maximum 2 nodes per device allowed"**
Each device supports a maximum of 2 nodes. Stop one before starting another.

**"Heartbeat spam detected"**
Heartbeats must be at least 20 seconds apart. The CLI handles this automatically — do not modify the heartbeat interval manually.

---

> **Warning:** Do not run more than 2 nodes per device. Attempting to bypass this limit is considered a violation and may result in account penalties.
