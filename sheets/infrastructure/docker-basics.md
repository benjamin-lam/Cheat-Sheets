---
title: Docker Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Docker Basics: Images, Container & Compose

Dieses Sheet zeigt die wichtigsten Docker‑Kommandos und Patterns für lokale Entwicklung, CI/CD und Deployment.

---

## ❓ Wie baue ich ein Docker‑Image?
**Lösung:** `docker build`.

```bash
docker build -t myapp:latest .
```

---

## ❓ Wie starte ich einen Container?
**Lösung:** `docker run`.

```bash
docker run -p 8080:80 myapp:latest
```

Detached:

```bash
docker run -d myapp:latest
```

---

## ❓ Wie liste ich Container & Images auf?
**Lösung:** ps & images.

```bash
docker ps
docker ps -a
docker images
```

---

## ❓ Wie stoppe und lösche ich Container?
**Lösung:** stop & rm.

```bash
docker stop myapp
docker rm myapp
```

Alle Container löschen:

```bash
docker rm -f $(docker ps -aq)
```

---

## ❓ Wie lösche ich ungenutzte Images?
**Lösung:** prune.

```bash
docker image prune -a
```

---

## ❓ Wie öffne ich eine Shell im Container?
**Lösung:** exec.

```bash
docker exec -it myapp bash
```

---

## ❓ Wie sehe ich Logs?
**Lösung:** logs.

```bash
docker logs -f myapp
```

---

## ❓ Wie definiere ich ein Dockerfile?
**Lösung:** Minimal‑Beispiel.

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["npm", "start"]
```

---

## ❓ Wie nutze ich Docker Compose?
**Lösung:** `docker compose up`.

```yaml
services:
  api:
    build: .
    ports:
      - "8080:80"
```

Starten:

```bash
docker compose up -d
```

---

## ❓ Wie aktualisiere ich Services?
**Lösung:** rebuild.

```bash
docker compose up -d --build
```

---

## ❓ Wie mounte ich lokale Dateien?
**Lösung:** Volumes.

```yaml
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
  APP_ENV: prod
```

---

## ❓ Wie prüfe ich Netzwerk & Ports?
**Lösung:** inspect.

```bash
docker inspect myapp
```

---

## Pro-Tipp
Nutze Multi‑Stage‑Builds, um Images klein zu halten — besonders bei Go, Node und PHP.
