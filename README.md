<div align="center">

# fail2ban-telegram-alerts

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Shell Script](https://img.shields.io/badge/built_with-Bash-4EAA25)]()

**Fail2ban integration script that sends real-time security alerts to Telegram when IPs are blocked.**

</div>


---

<p align="center">🌐 <strong>Also available in:</strong> <a href="README.es.md">Spanish</a></p>

---
## Features

- **Real-time Telegram alerts** — Receive instant notifications when Fail2ban bans or unbans an IP
- **Jail monitoring** — Get notified when jails start or stop
- **Simple integration** — Drop-in configuration for Fail2ban action files
- **Minimal dependencies** — Only requires `curl` and a Telegram bot
- **HTML formatted messages** — Clean, readable alerts with IP and jail information

---

## Requirements

- Fail2ban installed and running
- `curl` available on the system
- A Telegram bot token (create one with [@BotFather](https://t.me/BotFather))
- A Telegram chat ID (your user or group)

---

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/x0-jonatanfp/fail2ban-telegram-alerts.git
cd fail2ban-telegram-alerts
```

### 2. Configure your Telegram bot

Edit `telegram.conf` and set your bot token and chat ID:

```bash
API_TOKEN="your-telegram-bot-token"
CHAT_ID="your-chat-id"
```

### 3. Install the scripts

```bash
sudo mkdir -p /etc/fail2ban/scripts
sudo cp telegram.sh.es /etc/fail2ban/scripts/telegram.sh
sudo chmod +x /etc/fail2ban/scripts/telegram.sh
sudo cp telegram.conf /etc/fail2ban/action.d/telegram.conf
```

### 4. Configure Fail2ban

Add the Telegram action to your jail configuration:

```ini
[sshd]
[🇪🇸 Español](README.es.md)
enabled = true
action = telegram
```

Or add it globally in `jail.local`:

```ini
[DEFAULT]
[🇪🇸 Español](README.es.md)
action = telegram
```

### 5. Restart Fail2ban

```bash
sudo systemctl restart fail2ban
```

---

## Usage

The script supports four actions that Fail2ban triggers automatically:

| Action | Trigger | Description |
|---|---|---|
| `start` | Jail starts | Notifies that a jail is now active |
| `stop` | Jail stops | Notifies that a jail has been stopped |
| `ban` | IP is blocked | Sends alert with the blocked IP and jail name |
| `unban` | IP is unblocked | Sends alert with the unblocked IP and jail name |

---

## File structure

```
fail2ban-telegram-alerts/
├── telegram.sh.es       # Main script (Spanish variable names)
├── telegram.conf        # Fail2ban action configuration
├── assets/              # Supporting assets
└── README.md            # This file
```

---

## Testing

To test the setup manually:

```bash
sudo /etc/fail2ban/scripts/telegram.sh ban 192.168.1.100 sshd
sudo /etc/fail2ban/scripts/telegram.sh unban 192.168.1.100 sshd
```

You should receive a Telegram notification for each command.
