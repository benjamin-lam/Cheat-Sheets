---
title: REST API Design Cheat Sheet
category: Backend
last_updated: 2025-09-02
status: stable
---

# REST API Design: Versionierung, Fehler & Idempotenz

Dieses Sheet fasst die wichtigsten Prinzipien für robuste, skalierbare REST‑APIs zusammen.

---

## ❓ Wie strukturiere ich Ressourcen sauber?
**Lösung:** Nutze Substantive, keine Verben.

```text
GET /users
POST /users
GET /users/{id}
PATCH /users/{id}
DELETE /users/{id}
```

---

## ❓ Wie versioniere ich APIs?
**Lösung:** Version in der URL.

```text
GET /v1/users
GET /v2/users
```

---

## ❓ Wie gestalte ich Fehler konsistent?
**Lösung:** Einheitliches JSON‑Format.

```json
{
  "error": "invalid_request",
  "message": "Email is required",
  "status": 400
}
```

---

## ❓ Wie implementiere ich Pagination?
**Lösung:** Limit/Offset oder Cursor.

```text
GET /users?limit=20&offset=40
GET /users?cursor=eyJpZCI6IDEwMH0=
```

---

## ❓ Wie mache ich PUT und DELETE idempotent?
**Lösung:** Gleiche Anfrage → gleicher Zustand.

```text
PUT /users/10     # ersetzt Ressource
DELETE /users/10  # mehrfach erlaubt
```

---

## ❓ Wie dokumentiere ich APIs sauber?
**Lösung:** OpenAPI/Swagger nutzen.

```yaml
openapi: 3.0.0
paths:
  /users:
    get:
      summary: List users
```

---

## ❓ Wie sichere ich APIs ab?
**Lösung:** Auth + Rate Limiting + Validation.

- Bearer Tokens / JWT  
- Input Validation  
- Throttling  
- CORS‑Regeln  

---

## ❓ Wie verbessere ich Caching & Performance?
**Lösung:** ETag + Conditional Requests.

```text
ETag: "abc123"
If-None-Match: "abc123"
```

---

## Pro-Tipp
Nutze konsistente Naming‑Konventionen und dokumentiere jede Response‑Struktur — das reduziert Support‑Aufwand massiv.
