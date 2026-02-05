---
title: Python Basics Cheat Sheet
category: Tooling
last_updated: 2025-09-02
status: stable
---

# Python Basics: Skripte, Datenverarbeitung & CLI‑Tools

Dieses Sheet zeigt die wichtigsten Python‑Grundlagen für schnelle Automatisierung, Datenverarbeitung und kleine Utility‑Skripte — ideal für DevOps, Backend und Tooling.

---

## ❓ Wie führe ich ein Python‑Skript aus?
**Lösung:** Direkt oder über `python3`.

```bash
python3 script.py
```

Shebang für ausführbare Skripte:

```python
#!/usr/bin/env python3
```

---

## ❓ Wie lese ich eine Datei ein?
**Lösung:** Kontextmanager nutzen.

```python
with open("data.txt") as f:
    content = f.read()
```

Zeilenweise:

```python
for line in f:
    print(line.strip())
```

---

## ❓ Wie schreibe ich in eine Datei?
**Lösung:** Schreibmodus `"w"` oder `"a"`.

```python
with open("out.txt", "w") as f:
    f.write("Hello\n")
```

---

## ❓ Wie parse ich JSON?
**Lösung:** `json`‑Modul.

```python
import json

data = json.loads('{"user": 42}')
json_str = json.dumps(data, indent=2)
```

---

## ❓ Wie mache ich schnelle HTTP‑Requests?
**Lösung:** `requests`‑Bibliothek.

```python
import requests

r = requests.get("https://api.example.com")
print(r.status_code, r.json())
```

---

## ❓ Wie arbeite ich mit CLI‑Argumenten?
**Lösung:** `argparse` nutzen.

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--name")
args = parser.parse_args()

print("Hello", args.name)
```

---

## ❓ Wie nutze ich Listen‑Comprehensions?
**Lösung:** Kurz, schnell, pythonisch.

```python
squares = [x*x for x in range(10)]
```

Mit Filter:

```python
evens = [x for x in range(20) if x % 2 == 0]
```

---

## ❓ Wie arbeite ich mit Dictionaries?
**Lösung:** Key‑Value‑Zugriff.

```python
user = {"id": 42, "name": "Ben"}
print(user["name"])
```

Iteration:

```python
for key, value in user.items():
    print(key, value)
```

---

## ❓ Wie schreibe ich eine einfache Funktion?
**Lösung:** Standard‑Definition.

```python
def greet(name):
    return f"Hello {name}"
```

---

## ❓ Wie mache ich Fehlerbehandlung?
**Lösung:** try/except.

```python
try:
    risky()
except Exception as e:
    print("Error:", e)
```

---

## ❓ Wie installiere ich Pakete?
**Lösung:** pip.

```bash
pip install requests
pip install --upgrade pip
```

Requirements:

```bash
pip install -r requirements.txt
```

---

## ❓ Wie erstelle ich ein virtuelles Environment?
**Lösung:** venv.

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## Pro-Tipp
Nutze `pathlib` statt `os.path` — moderner, sicherer und plattformunabhängig.

```python
from pathlib import Path

p = Path("data.txt")
print(p.read_text())
```
