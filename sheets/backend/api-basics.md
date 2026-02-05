---
title: API Basics Cheat Sheet
category: Backend
last_updated: 2025-09-02
status: stable
---

# API Basics: REST, HTTP, Status Codes & Best Practices

Dieses Sheet bündelt die wichtigsten Grundlagen für moderne Backend‑APIs — ideal für Microservices, Web‑Apps und Integrationen.

---

## ❓ Was ist eine API?
**Lösung:** Schnittstelle zwischen Systemen.

APIs ermöglichen:

- Daten abrufen  
- Aktionen ausführen  
- Systeme integrieren  
- Microservices verbinden  

Typen:

- REST  
- GraphQL  
- gRPC  
- Webhooks  

---

## ❓ Wie funktioniert REST?
**Lösung:** Ressourcen + HTTP‑Methoden.

Typische Methoden:

| Methode | Bedeutung |
|--------|-----------|
| GET    | lesen |
| POST   | erstellen |
| PUT    | ersetzen |
| PATCH  | teilweise aktualisieren |
| DELETE | löschen |

---

## ❓ Wie sehen typische Endpoints aus?
**Lösung:** Ressourcenorientiert.

Beispiele:

```
GET /users
GET /users/42
POST /users
PATCH /users/42
DELETE /users/42
```

---

## ❓ Welche HTTP‑Statuscodes sind wichtig?
**Lösung:** die wichtigsten Kategorien.

| Code | Bedeutung |
|------|-----------|
| 200  | OK |
| 201  | Created |
| 204  | No Content |
| 400  | Bad Request |
| 401  | Unauthorized |
| 403  | Forbidden |
| 404  | Not Found |
| 409  | Conflict |
| 422  | Unprocessable Entity |
| 500  | Server Error |

---

## ❓ Wie sollten API‑Responses aussehen?
**Lösung:** JSON + klare Struktur.

```json
{
  "id": 42,
  "name": "Ben",
  "created_at": "2025-09-02T12:00:00Z"
}
```

Fehler:

```json
{
  "error": "User not found",
  "code": "USER_NOT_FOUND"
}
```

---

## ❓ Wie mache ich Pagination?
**Lösung:** limit + offset oder cursor.

Beispiel:

```
GET /users?limit=20&offset=40
```

Cursor‑basiert:

```
GET /users?cursor=abc123
```

---

## ❓ Wie mache ich Filtering & Sorting?
**Lösung:** Query‑Parameter.

```
GET /orders?status=paid&sort=-created_at
```

---

## ❓ Wie mache ich Authentifizierung?
**Lösung:** Tokens.

Typisch:

- Bearer Token  
- JWT  
- API Keys  
- OAuth2  

Beispiel:

```
Authorization: Bearer <token>
```

---

## ❓ Wie mache ich Rate Limiting?
**Lösung:** Header + Limits.

Beispiel‑Header:

```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 42
X-RateLimit-Reset: 1693650000
```

---

## ❓ Wie dokumentiere ich APIs?
**Lösung:** OpenAPI / Swagger.

Beispiel:

```yaml
paths:
  /users:
    get:
      summary: List users
      responses:
        "200":
          description: OK
```

---

## ❓ Wie teste ich APIs?
**Lösung:** Tools.

- curl  
- Postman  
- Insomnia  
- k6 (Load Testing)  
- Jest / PHPUnit / Go test  

---

## ❓ Wie versioniere ich APIs?
**Lösung:** URL oder Header.

URL‑Versionierung:

```
GET /v1/users
```

Header‑Versionierung:

```
Accept: application/vnd.myapp.v2+json
```

---

## Pro-Tipp
Nutze **klare Ressourcen, konsistente Statuscodes und saubere Fehlerobjekte** — APIs werden erst dadurch stabil, verständlich und integrationsfreundlich.
