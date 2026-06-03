<div align="center">

# fail2ban-telegram-alerts

[![MIT License](https://img.shields.io/badge/Licencia-MIT-green.svg)](LICENSE)
[![Shell Script](https://img.shields.io/badge/creado_con-Bash-4EAA25)]()

**Script de integración con Fail2ban que envía alertas de seguridad en tiempo real a Telegram cuando se bloquean IPs.**

</div>


---

<p align="center">🌐 <strong>También disponible en:</strong> <a href="README.md">Inglés</a></p>

---
## Características

- **Alertas en tiempo real** — Recibe notificaciones instantáneas cuando Fail2ban bloquea o desbloquea una IP
- **Monitoreo de jails** — Te notifica cuando las jails se inician o detienen
- **Integración sencilla** — Configuración directa en los archivos de acción de Fail2ban
- **Dependencias mínimas** — Solo requiere `curl` y un bot de Telegram
- **Mensajes con formato HTML** — Alertas limpias y legibles con IP y nombre de la jail

---

## Requisitos

- Fail2ban instalado y funcionando
- `curl` disponible en el sistema
- Un token de bot de Telegram (crea uno con [@BotFather](https://t.me/BotFather))
- Un ID de chat de Telegram (tu usuario o grupo)

---

## Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/x0-jonatanfp/fail2ban-telegram-alerts.git
cd fail2ban-telegram-alerts
```

### 2. Configurar el bot de Telegram

Edita `telegram.conf` con tu token y chat ID:

```bash
API_TOKEN="tu-token-del-bot"
CHAT_ID="tu-id-de-chat"
```

### 3. Instalar los scripts

```bash
sudo mkdir -p /etc/fail2ban/scripts
sudo cp telegram.sh.es /etc/fail2ban/scripts/telegram.sh
sudo chmod +x /etc/fail2ban/scripts/telegram.sh
sudo cp telegram.conf /etc/fail2ban/action.d/telegram.conf
```

### 4. Configurar Fail2ban

Añade la acción de Telegram a tu jail en `jail.local`:

```ini
[sshd]
enabled = true
action = telegram
```

O de forma global:

```ini
[DEFAULT]
action = telegram
```

### 5. Reiniciar Fail2ban

```bash
sudo systemctl restart fail2ban
```

---

## Uso

El script soporta cuatro acciones que Fail2ban ejecuta automáticamente:

| Acción | Disparo | Descripción |
|---|---|---|
| `start` | Inicio de jail | Notifica que una jail está activa |
| `stop` | Parada de jail | Notifica que una jail se ha detenido |
| `ban` | IP bloqueada | Envía alerta con la IP bloqueada y la jail |
| `unban` | IP desbloqueada | Envía alerta con la IP desbloqueada y la jail |

---

## Estructura de archivos

```
fail2ban-telegram-alerts/
├── telegram.sh.es       # Script principal (nombres de variables en español)
├── telegram.conf        # Configuración de acción para Fail2ban
├── assets/              # Recursos adicionales
└── README.es.md         # Este archivo
```

---

## Pruebas

Para probar la configuración manualmente:

```bash
sudo /etc/fail2ban/scripts/telegram.sh ban 192.168.1.100 sshd
sudo /etc/fail2ban/scripts/telegram.sh unban 192.168.1.100 sshd
```

Deberías recibir una notificación de Telegram por cada comando.
