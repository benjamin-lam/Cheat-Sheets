---
title: Dockerfile Basics Cheat Sheet
category: DevOps
last_updated: 2025-09-02
status: stable
---

# Dockerfile Basics: Layers, Builds, Caching & Best Practices

Dieses Sheet bündelt die wichtigsten Dockerfile‑Konzepte für reproduzierbare Builds, effiziente Images und produktionsnahe Container‑Deployments.

---

## ❓ Wie starte ich ein Dockerfile?
**Lösung:** FROM definiert das Basis‑Image.

```dockerfile
FROM node:20-alpine
```

---

## ❓ Wie kopiere ich Dateien ins Image?
**Lösung:** COPY.

```dockerfile
COPY package.json package-lock.json ./
```

---

## ❓ Wie installiere ich Dependencies?
**Lösung:** RUN.

```dockerfile
RUN npm ci
```

---

## ❓ Wie setze ich das Arbeitsverzeichnis?
**Lösung:** WORKDIR.

```dockerfile
WORKDIR /app
```

---

## ❓ Wie starte ich die Anwendung?
**Lösung:** CMD oder ENTRYPOINT.

```dockerfile
CMD ["npm", "start"]
```

ENTRYPOINT:

```dockerfile
ENTRYPOINT ["node", "server.js"]
```

---

## ❓ Wie setze ich Umgebungsvariablen?
**Lösung:** ENV.

```dockerfile
ENV NODE_ENV=production
```

---

## ❓ Wie öffne ich Ports?
**Lösung:** EXPOSE.

```dockerfile
EXPOSE 3000
```

---

## ❓ Wie mache ich Multi‑Stage Builds?
**Lösung:** Builder + Runtime.

```dockerfile
FROM node:20-alpine AS builder
WORKDIR /app
COPY . .
RUN npm ci && npm run build

FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
CMD ["node", "dist/index.js"]
```

---

## ❓ Wie reduziere ich Image‑Größe?
**Lösung:** Best Practices.

- alpine‑Images  
- Multi‑Stage Builds  
- `.dockerignore` nutzen  
- keine unnötigen Tools installieren  
- Layer minimieren  

---

## ❓ Wie nutze ich .dockerignore?
**Lösung:** unnötige Dateien ausschließen.

Beispiel:

```
node_modules
.git
.env
dist
```

---

## ❓ Wie nutze ich Build‑Args?
**Lösung:** ARG.

```dockerfile
ARG VERSION=dev
ENV APP_VERSION=$VERSION
```

Build:

```bash
docker build --build-arg VERSION=1.0 .
```

---

## ❓ Wie nutze ich Healthchecks?
**Lösung:** HEALTHCHECK.

```dockerfile
HEALTHCHECK CMD curl -f http://localhost:3000/health || exit 1
```

---

## ❓ Wie nutze ich Volumes?
**Lösung:** VOLUME.

```dockerfile
VOLUME ["/data"]
```

---

## ❓ Wie teste ich Dockerfiles?
**Lösung:** docker build + docker run.

```bash
docker build -t myapp .
docker run -p 3000:3000 myapp
```

---

## Pro-Tipp
Nutze **Multi‑Stage Builds + .dockerignore**, um Images klein, schnell und sicher zu halten — das ist der Schlüssel zu produktionsreifen Containern.
