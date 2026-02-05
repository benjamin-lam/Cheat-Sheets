---
title: YAML Config Cheat Sheet
category: Tooling
last_updated: 2025-09-02
status: stable
---

# YAML: Saubere Konfiguration für Docker, CI/CD & Kubernetes

Dieses Sheet zeigt die wichtigsten YAML‑Grundlagen und typische Stolperfallen — ideal für Docker Compose, GitHub Actions, Kubernetes und jede Art von deklarativer Konfiguration.

---

## ❓ Was sind die wichtigsten YAML‑Grundregeln?
**Lösung:** YAML ist whitespace‑sensitiv.

- Einrückung nur mit **Spaces**, niemals Tabs  
- Listen beginnen mit `-`  
- Key‑Value‑Paare mit `key: value`  
- Strings können unquoted, single‑quoted oder double‑quoted sein  

---

## ❓ Wie definiere ich einfache Key‑Value‑Paare?
**Lösung:** Standard‑Syntax.

```yaml
name: api-service
port: 8080
debug: true
```

---

## ❓ Wie definiere ich Listen?
**Lösung:** Mit `-` einrücken.

```yaml
servers:
  - app01
  - app02
  - app03
```

---

## ❓ Wie definiere ich verschachtelte Strukturen?
**Lösung:** Einrückung = Struktur.

```yaml
database:
  host: localhost
  port: 5432
  credentials:
    user: admin
    pass: secret
```

---

## ❓ Wie definiere ich Umgebungsvariablen (z. B. Docker Compose)?
**Lösung:** Als Liste oder Map.

Liste:

```yaml
environment:
  - APP_ENV=prod
  - DEBUG=false
```

Map:

```yaml
environment:
  APP_ENV: prod
  DEBUG: "false"
```

---

## ❓ Wie definiere ich Multi‑Line‑Strings?
**Lösung:** `|` für literal, `>` für folded.

Literal (Zeilen bleiben erhalten):

```yaml
config: |
  line 1
  line 2
```

Folded (Zeilen werden zu einem Absatz):

```yaml
message: >
  This is a long
  message that becomes
  one line.
```

---

## ❓ Wie referenziere ich Werte mehrfach?
**Lösung:** YAML‑Anchors & Aliases.

```yaml
defaults: &defaults
  retries: 3
  timeout: 30

service:
  <<: *defaults
  timeout: 60
```

---

## ❓ Wie definiere ich Docker Compose Services?
**Lösung:** Minimaler Blueprint.

```yaml
services:
  api:
    image: myapp:latest
    ports:
      - "8080:80"
    environment:
      APP_ENV: prod
```

---

## ❓ Wie definiere ich GitHub Actions Workflows?
**Lösung:** YAML‑Workflow‑Struktur.

```yaml
name: CI

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm test
```

---

## ❓ Wie definiere ich Kubernetes Manifeste?
**Lösung:** Deployment‑Beispiel.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api
spec:
  replicas: 3
  selector:
    matchLabels:
      app: api
  template:
    metadata:
      labels:
        app: api
    spec:
      containers:
        - name: api
          image: app:v1
```

---

## ❓ Wie vermeide ich typische YAML‑Fehler?
**Lösung:** Die häufigsten Stolperfallen.

- Tabs statt Spaces  
- Falsche Einrückung  
- Fehlende Anführungszeichen bei `true`, `false`, `on`, `off`  
- Unbeabsichtigte Typ‑Konvertierung  

Beispiel:

```yaml
value: "on"   # korrekt
value: on     # wird zu boolean true
```

---

## Pro-Tipp
Nutze `yamllint` oder `docker compose config` bzw. `kubectl apply --dry-run=client` für sofortige Validierung deiner YAML‑Dateien.
