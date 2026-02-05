---
title: CLI Productivity Cheat Sheet
category: Tooling
last_updated: 2025-09-02
status: stable
---

# CLI Productivity: Moderne Tools für Geschwindigkeit & Komfort

Dieses Sheet zeigt die wichtigsten modernen CLI‑Tools, die klassische Unix‑Kommandos ersetzen oder erweitern — schneller, intuitiver und ideal für tägliche Entwicklungsarbeit.

---

## ❓ Wie finde ich Dateien schneller als mit `find`?
**Lösung:** `fd` ist schneller, einfacher und farbig.

```bash
fd config
fd -e md
fd "controller" src/
```

---

## ❓ Wie suche ich Inhalte schneller als mit `grep`?
**Lösung:** `ripgrep` (`rg`) ist der moderne Standard.

```bash
rg "TODO"
rg -i "error"
rg "function" src/
```

- ignoriert automatisch `.gitignore`  
- extrem schnell  

---

## ❓ Wie ersetze ich `cat` mit Syntax‑Highlighting?
**Lösung:** `bat` zeigt Dateien farbig und mit Pager.

```bash
bat config.yaml
bat -n app.php
```

---

## ❓ Wie navigiere ich schneller durch Verzeichnisse?
**Lösung:** `zoxide` lernt deine Bewegungen.

```bash
z project
z src
z nginx
```

Setup:

```bash
eval "$(zoxide init bash)"
```

---

## ❓ Wie verbessere ich die Dateiauswahl im Terminal?
**Lösung:** `fzf` für fuzzy search.

```bash
fzf
```

Oder kombiniert:

```bash
git ls-files | fzf
```

---

## ❓ Wie mache ich HTTP‑Requests ohne Browser?
**Lösung:** `httpie` ist lesbarer als curl.

```bash
http GET https://example.com
http POST https://api/app user=42
```

---

## ❓ Wie zeige ich Prozesse übersichtlich an?
**Lösung:** `htop` oder `btop`.

```bash
htop
btop
```

---

## ❓ Wie messe ich die Laufzeit eines Befehls?
**Lösung:** `hyperfine` für Benchmarking.

```bash
hyperfine "php script.php"
```

---

## ❓ Wie kopiere ich Dateien über SSH effizient?
**Lösung:** `rsync` mit Fortschritt.

```bash
rsync -avh --progress src/ user@server:/var/www/
```

---

## ❓ Wie mache ich schnelle JSON‑Manipulation?
**Lösung:** `jq` ist der Standard.

```bash
jq '.user.id' data.json
jq '.items[] | select(.active == true)' data.json
```

---

## Pro-Tipp
Kombiniere Tools wie `rg`, `fzf` und `bat` für interaktive Workflows — z. B. Datei suchen → anzeigen → öffnen.
