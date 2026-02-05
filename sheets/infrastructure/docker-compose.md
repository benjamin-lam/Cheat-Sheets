---
title: Docker Compose Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Docker Compose: Multi‑Service‑Setups, Volumes & Environments

Dieses Sheet zeigt die wichtigsten Compose‑Patterns für lokale Entwicklung, CI/CD und produktionsnahe Umgebungen.

---

## ❓ Wie starte ich ein Compose‑Projekt?
**Lösung:** Standard‑Befehle.

```bash
docker compose up
docker compose up -d
docker compose down
```

---

## ❓ Wie definiere ich Services?
**Lösung:** Minimal‑Beispiel.

```yaml
services:
  api:
    build: .
    ports:
      - "8080:80"
```

---

## ❓ Wie mounte ich lokale Dateien?
**Lösung:** Volumes.

```yaml
services:
  api:
    volumes:
      - ./src:/app/src
```

---

## ❓ Wie setze ich Umgebungsvariablen?
**Lösung:** env_file oder environment.

```yaml
env_file:
  - .env
```

Oder:

```yaml
environment:
  APP_ENV: dev
  DEBUG: "true"
```

---

## ❓ Wie definiere ich Abhängigkeiten?
**Lösung:** depends_on.

```yaml
services:
  api:
    depends_on:
      - db
```

---

## ❓ Wie definiere ich eine Datenbank?
**Lösung:** Beispiel mit Postgres.

```yaml
services:
  db:
    image: postgres:16
    environment:
      POSTGRES_PASSWORD: secret
    volumes:
      - dbdata:/var/lib/postgresql/data
```

Volumes:

```yaml
volumes:
  dbdata:
```

---

## ❓ Wie definiere ich Healthchecks?
**Lösung:** healthcheck‑Block.

```yaml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:80"]
  interval: 10s
  timeout: 3s
  retries: 5
```

---

## ❓ Wie skaliere ich Services?
**Lösung:** scale.

```bash
docker compose up --scale api=3
```

---

## ❓ Wie baue ich Images neu?
**Lösung:** rebuild.

```bash
docker compose up -d --build
```

---

## ❓ Wie sehe ich Logs aller Services?
**Lösung:** logs.

```bash
docker compose logs -f
```

Nur ein Service:

```bash
docker compose logs -f api
```

---

## ❓ Wie definiere ich Netzwerke?
**Lösung:** custom networks.

```yaml
networks:
  backend:
    driver: bridge

services:
  api:
    networks:
      - backend
  db:
    networks:
      - backend
```

---

## ❓ Wie verhindere ich, dass Container neu starten?
**Lösung:** restart‑Policy.

```yaml
restart: "no"
```

Andere Optionen:

- `always`
- `on-failure`
- `unless-stopped`

---

## Pro-Tipp
Nutze `docker compose config`, um deine gesamte Compose‑Struktur zu validieren und zusammengeführt anzuzeigen — ideal für Debugging und CI.
