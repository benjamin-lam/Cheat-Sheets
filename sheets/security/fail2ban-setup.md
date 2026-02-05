---
title: Fail2Ban Setup Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Fail2Ban: Schutz vor Brute-Force & Bots

Dieses Sheet zeigt, wie du SSH, Apache, Nginx und eigene Logs mit Fail2Ban absicherst.

---

## ❓ Wie installiere und starte ich Fail2Ban?
**Lösung:** Standardinstallation + Aktivierung.

```bash
sudo apt install fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

---

## ❓ Wie aktiviere ich den SSH-Schutz?
**Lösung:** jail.local anlegen.

```ini
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 5
bantime = 1h
```

---

## ❓ Wie sehe ich aktive Bans?
**Lösung:** Status-Abfrage.

```bash
fail2ban-client status sshd
```

---

## ❓ Wie entbanne ich eine IP?
**Lösung:** Unban-Befehl.

```bash
fail2ban-client set sshd unbanip 192.168.1.10
```

---

## ❓ Wie schütze ich Apache oder Nginx?
**Lösung:** Access-Log als Quelle.

```ini
[nginx-404]
enabled  = true
port     = http,https
filter   = nginx-404
logpath  = /var/log/nginx/access.log
maxretry = 20
findtime = 60
bantime  = 10m
```

---

## ❓ Wie definiere ich eigene Filter?
**Lösung:** Regex in `/etc/fail2ban/filter.d/myapp.conf`.

```ini
[Definition]
failregex = ^<HOST> .* "POST /login" .* 401
ignoreregex =
```

---

## ❓ Wie teste ich einen Filter?
**Lösung:** fail2ban-regex.

```bash
fail2ban-regex /var/log/myapp.log /etc/fail2ban/filter.d/myapp.conf
```

---

## Pro-Tipp
Setze `bantime.increment = true`, um Wiederholungstäter exponentiell länger zu sperren.
