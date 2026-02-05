---
title: systemd Services Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# systemd: Services, Logs & Deployment

Dieses Sheet bündelt die wichtigsten Kommandos und Patterns für systemd‑basierte Deployments, Debugging und Service‑Management.

---

## ❓ Wie starte, stoppe oder restarte ich einen Service?
**Lösung:** Nutze die Standard‑Kommandos.

```bash
systemctl start myapp.service
systemctl stop myapp.service
systemctl restart myapp.service
systemctl status myapp.service
```

---

## ❓ Wie lade ich geänderte Unit‑Files neu?
**Lösung:** Nach jeder Änderung an `.service` oder `.timer`.

```bash
systemctl daemon-reload
```

---

## ❓ Wie aktiviere ich einen Service beim Booten?
**Lösung:** Enable/Disable steuert Autostart.

```bash
systemctl enable myapp.service
systemctl disable myapp.service
```

---

## ❓ Wie sehe ich Logs eines Services?
**Lösung:** journalctl bietet Filter und Live‑Ansicht.

```bash
journalctl -u myapp.service --since "10 min ago"
journalctl -u myapp.service -f
```

---

## ❓ Wie definiere ich einen eigenen Service?
**Lösung:** Minimaler Blueprint.

```ini
[Unit]
Description=My App Service
After=network.target

[Service]
ExecStart=/usr/bin/php /var/www/app/server.php
Restart=on-failure
User=www-data
WorkingDirectory=/var/www/app

[Install]
WantedBy=multi-user.target
```

---

## ❓ Wie setze ich Restart‑Policies?
**Lösung:** systemd bietet feine Kontrolle.

```ini
Restart=on-failure
RestartSec=5
StartLimitIntervalSec=60
StartLimitBurst=5
```

---

## ❓ Wie nutze ich Timer statt Cronjobs?
**Lösung:** `.timer` + `.service`.

```ini
# myjob.timer
[Timer]
OnCalendar=*-*-* 03:00:00
Persistent=true

[Install]
WantedBy=timers.target
```

---

## Pro-Tipp
Nutze `systemctl edit myapp.service` statt direkt in `/etc/systemd/system` zu schreiben – Updates bleiben konfliktfrei.
```

---

# 📄 **2. networking-tools.md**  
cURL, dig, traceroute, ss — alles kompakt.

```markdown
---
title: Networking Tools Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Networking Tools: Diagnose, DNS & Connectivity

Dieses Sheet liefert die wichtigsten Befehle für Netzwerk‑Analyse, DNS‑Debugging und HTTP‑Tests.

---

## ❓ Wie teste ich eine HTTP‑Anfrage schnell?
**Lösung:** Nutze cURL für Header, Status und Timing.

```bash
curl -I https://example.com
curl -w "@curl-format.txt" -o /dev/null -s https://example.com
```

---

## ❓ Wie prüfe ich DNS‑Einträge?
**Lösung:** dig ist der Standard.

```bash
dig example.com A
dig example.com MX
dig example.com ANY
dig +trace example.com
```

---

## ❓ Wie finde ich heraus, wohin ein Paket geht?
**Lösung:** traceroute zeigt Hops.

```bash
traceroute example.com
```

---

## ❓ Wie sehe ich offene Ports und Verbindungen?
**Lösung:** ss ist der moderne Ersatz für netstat.

```bash
ss -tulpen
ss -tn state listening
```

---

## ❓ Wie teste ich eine TCP‑Verbindung?
**Lösung:** nc (netcat) ist universell.

```bash
nc -vz example.com 443
```

---

## ❓ Wie prüfe ich DNS‑Propagation?
**Lösung:** Nutze mehrere Nameserver.

```bash
dig @1.1.1.1 example.com
dig @8.8.8.8 example.com
```

---

## Pro-Tipp
Für API‑Debugging: `curl -v` zeigt TLS‑Handshake, Redirects und Header in einem Durchlauf.
```

---

# 📄 **3. logrotate-config.md**  
Rotation, Retention, eigene Policies.

```markdown
---
title: logrotate Config Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# logrotate: Rotation, Kompression & Retention

Dieses Sheet zeigt, wie Logs automatisch rotiert, komprimiert und aufgeräumt werden – ideal für Server‑Deployments.

---

## ❓ Wie rotiere ich ein Log täglich?
**Lösung:** Minimal‑Konfiguration.

```conf
/var/log/myapp/*.log {
    daily
    rotate 14
    compress
    missingok
    notifempty
}
```

---

## ❓ Wie rotiere ich nach Dateigröße?
**Lösung:** size‑Trigger statt Zeit.

```conf
/var/log/myapp/app.log {
    size 50M
    rotate 10
    compress
}
```

---

## ❓ Wie führe ich nach der Rotation einen Befehl aus?
**Lösung:** postrotate‑Hook.

```conf
postrotate
    systemctl reload myapp.service
endscript
```

---

## ❓ Wie verhindere ich, dass leere Logs rotiert werden?
**Lösung:** `notifempty`.

```conf
notifempty
```

---

## ❓ Wie rotiere ich Logs, die nicht root gehören?
**Lösung:** user/group setzen.

```conf
create 640 www-data www-data
```

---

## ❓ Wie teste ich eine logrotate‑Konfiguration?
**Lösung:** Debug‑Modus.

```bash
logrotate -d /etc/logrotate.conf
```

---

## Pro-Tipp
Setze `delaycompress`, wenn deine App das aktuelle Logfile noch kurz nach Rotation benötigt.
