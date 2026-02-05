---
title: Bash Terminal Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Bash Terminal: Profi‑Einzeiler für Logs, Grep & Dateisystem

Dieses Sheet bündelt die wichtigsten Bash‑Kommandos für schnelle Analyse, Dateimanipulation und Server‑Debugging — ideal für Ops, DevOps und schnelle SSH‑Sessions.

---

## ❓ Wie finde ich Text in Dateien?
**Lösung:** `grep` mit Farben, Kontext und rekursiver Suche.

```bash
grep -R "ERROR" .
grep -Rni "timeout" /var/log
grep -R --color=auto "pattern" .
```

Kontext anzeigen:

```bash
grep -RniC 3 "fatal" .
```

---

## ❓ Wie filtere ich Logs nach Datum oder Pattern?
**Lösung:** `awk` + `grep`.

```bash
grep "2025-09-02" app.log
awk '/ERROR/ {print $0}' app.log
```

Nur Requests > 1s:

```bash
awk '$NF > 1.0 {print $0}' access.log
```

---

## ❓ Wie zeige ich die letzten Zeilen einer Datei live an?
**Lösung:** `tail -f`.

```bash
tail -f /var/log/syslog
tail -n 200 -f app.log
```

---

## ❓ Wie finde ich große Dateien?
**Lösung:** `du` + Sortierung.

```bash
du -ah . | sort -h | tail -20
```

Nur Dateien > 100MB:

```bash
find . -type f -size +100M
```

---

## ❓ Wie lösche ich Dateien nach Alter?
**Lösung:** `find` mit `-mtime`.

```bash
find /var/log -type f -mtime +30 -delete
```

---

## ❓ Wie finde ich offene Ports?
**Lösung:** `ss` (moderner als netstat).

```bash
ss -tulpen
```

---

## ❓ Wie ersetze ich Text in vielen Dateien?
**Lösung:** `sed` inline.

```bash
sed -i 's/old/new/g' *.txt
```

---

## ❓ Wie zähle ich Zeilen, Wörter oder Zeichen?
**Lösung:** `wc`.

```bash
wc -l file.txt
wc -w file.txt
wc -c file.txt
```

---

## ❓ Wie mache ich schnelle Backups?
**Lösung:** `tar` mit Kompression.

```bash
tar -czf backup.tar.gz /var/www
```

---

## ❓ Wie prüfe ich die Größe eines Ordners?
**Lösung:** `du -sh`.

```bash
du -sh /var/www
```

---

## ❓ Wie liste ich Dateien sortiert nach Datum?
**Lösung:** `ls` mit Flags.

```bash
ls -lt
ls -ltr
```

---

## ❓ Wie finde ich Prozesse?
**Lösung:** `ps` + `grep`.

```bash
ps aux | grep php
```

---

## ❓ Wie stoppe ich Prozesse?
**Lösung:** `kill` oder `pkill`.

```bash
pkill -f "php artisan queue"
kill -9 1234
```

---

## ❓ Wie mache ich schnelle Einzeiler?
**Lösung:** Pipes kombinieren.

Beispiel: Top 10 IPs im Access‑Log:

```bash
awk '{print $1}' access.log | sort | uniq -c | sort -nr | head
```

---

## Pro-Tipp
Nutze `set -euo pipefail` in Skripten, um Fehler sofort sichtbar zu machen und ungewollte Seiteneffekte zu verhindern.
