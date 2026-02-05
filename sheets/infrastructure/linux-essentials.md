---
title: Linux Essentials Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Linux Essentials: Prozesse, Rechte & Systemdiagnose

Dieses Sheet bündelt die wichtigsten Linux‑Kommandos für Server‑Administration, Debugging und tägliche Arbeit im Terminal.

---

## ❓ Wie finde ich Systeminformationen?
**Lösung:** Hardware, Kernel, Distribution.

```bash
uname -a
lsb_release -a
cat /etc/os-release
```

CPU & RAM:

```bash
lscpu
free -h
```

---

## ❓ Wie prüfe ich Festplatten & Mounts?
**Lösung:** Speicher & Partitionen.

```bash
df -h
lsblk
mount
```

---

## ❓ Wie finde ich laufende Prozesse?
**Lösung:** ps, top, htop.

```bash
ps aux
top
htop
```

Nach Name filtern:

```bash
ps aux | grep nginx
```

---

## ❓ Wie starte/stoppe ich Services?
**Lösung:** systemd.

```bash
systemctl status nginx
systemctl restart nginx
systemctl enable nginx
```

---

## ❓ Wie prüfe ich offene Ports?
**Lösung:** ss (modern).

```bash
ss -tulpen
```

---

## ❓ Wie ändere ich Dateirechte?
**Lösung:** chmod, chown.

```bash
chmod 644 file.txt
chmod +x script.sh
chown user:group file.txt
```

---

## ❓ Wie finde ich große Dateien?
**Lösung:** du + sort.

```bash
du -ah /var | sort -h | tail -20
```

---

## ❓ Wie überwache ich Logs?
**Lösung:** tail, journalctl.

```bash
tail -f /var/log/syslog
journalctl -u nginx --since "10 min ago"
```

---

## ❓ Wie suche ich Dateien?
**Lösung:** find.

```bash
find . -name "*.log"
find /var -type f -size +100M
```

---

## ❓ Wie installiere ich Pakete?
**Lösung:** apt, yum, dnf.

Debian/Ubuntu:

```bash
apt update
apt install nginx
```

RHEL/CentOS:

```bash
yum install nginx
```

---

## ❓ Wie prüfe ich Netzwerkverbindungen?
**Lösung:** ping, traceroute, dig.

```bash
ping example.com
traceroute example.com
dig example.com
```

---

## ❓ Wie kopiere ich Dateien über SSH?
**Lösung:** scp oder rsync.

```bash
scp file.txt user@server:/tmp/
rsync -avh src/ user@server:/var/www/
```

---

## ❓ Wie plane ich Cronjobs?
**Lösung:** crontab.

```bash
crontab -e
```

Beispiel:

```cron
0 3 * * * /usr/local/bin/backup.sh
```

---

## Pro-Tipp
Nutze `journalctl -xe` für schnelle Fehlersuche — systemd liefert oft die präzisesten Hinweise.
