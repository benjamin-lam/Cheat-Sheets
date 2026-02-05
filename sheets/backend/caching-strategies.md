---
title: Caching Strategies Cheat Sheet
category: Backend
last_updated: 2025-09-02
status: stable
---

# Caching: TTL‑Design, Stampede‑Schutz & HTTP‑Optimierung

Dieses Sheet zeigt die wichtigsten Patterns für performante, skalierbare Web‑Anwendungen — von Redis bis HTTP‑Caching.

---

## ❓ Wie setze ich sinnvolle TTLs?
**Lösung:** TTL nach Datenvolatilität wählen.

- **statisch:** 24h – 7d  
- **semi‑dynamisch:** 5–60 min  
- **hoch‑dynamisch:** 5–30 sec  

```text
SET user:42:data "{...}" EX 300
```

---

## ❓ Wie verhindere ich Cache‑Stampedes?
**Lösung:** Soft‑TTL + Locking.

**Soft‑TTL Pattern:**
- Cache liefert alten Wert zurück  
- Parallel wird im Hintergrund neu generiert  

```text
value = cache.get(key)
if value.expired_soft:
    lock.acquire()
    refresh()
```

---

## ❓ Wie verhindere ich, dass viele Clients gleichzeitig regenerieren?
**Lösung:** Single‑Flight / Mutex‑Lock.

```text
SETNX lock:product:42 1 EX 5
```

Nur ein Worker regeneriert, alle anderen warten.

---

## ❓ Wie nutze ich ETag für HTTP‑Caching?
**Lösung:** Conditional Requests.

```http
ETag: "abc123"
If-None-Match: "abc123"
```

Server antwortet mit `304 Not Modified`, wenn unverändert.

---

## ❓ Wie aktiviere ich Browser‑Caching für statische Assets?
**Lösung:** Lange TTL + Cache‑Busting.

```nginx
location ~* \.(css|js|png|jpg|svg)$ {
    expires 30d;
    add_header Cache-Control "public";
}
```

Assets sollten versioniert sein:

```
app.9f3c1a.js
```

---

## ❓ Wie nutze ich Redis für komplexe Caching‑Patterns?
**Lösung:** Hashes + Expire.

```bash
HSET product:42 name "Laptop" price "999"
EXPIRE product:42 600
```

---

## ❓ Wie cache ich API‑Responses effizient?
**Lösung:** Key‑Design + kurze TTL.

```text
GET /api/products/42 → cache key: api:products:42
TTL: 30–120 sec
```

---

## ❓ Wie verhindere ich veraltete Daten nach Updates?
**Lösung:** Write‑Through oder Invalidation.

**Write‑Through:**
- Schreiben → DB  
- Schreiben → Cache  

**Invalidation:**
- Schreiben → DB  
- Löschen → Cache  

```text
DEL api:products:42
```

---

## Pro-Tipp
Nutze **"jitter"** (zufällige TTL‑Variation), um gleichzeitige Cache‑Invalidierungen zu vermeiden.
