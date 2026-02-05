---
title: Queue Workers Cheat Sheet
category: Backend
last_updated: 2025-09-02
status: stable
---

# Queue Workers: Jobs, Retries & Dead-Letter-Queues

Dieses Sheet zeigt die wichtigsten Patterns für robuste Hintergrundverarbeitung — egal ob Redis, RabbitMQ oder eigene Worker.

---

## ❓ Warum überhaupt Queues?
**Lösung:** Entkopplung & Stabilität.

- Lastspitzen abfedern  
- Lange Tasks aus dem Request-Flow entfernen  
- Wiederholbare, fehlertolerante Verarbeitung  
- Garantierte Reihenfolge (FIFO)  

---

## ❓ Wie baue ich ein einfaches Producer/Consumer‑Pattern?
**Lösung:** Redis List als Queue.

```bash
# Producer
LPUSH jobs "send_email:42"

# Consumer
BRPOP jobs 0
```

---

## ❓ Wie implementiere ich Retries?
**Lösung:** Retry‑Counter im Payload.

```json
{
  "task": "send_email",
  "user": 42,
  "retries": 2
}
```

Worker‑Logik:

```text
if retries < 5:
    increment retries
    requeue()
else:
    move_to_dead_letter()
```

---

## ❓ Wie verhindere ich, dass Jobs verloren gehen?
**Lösung:** Acknowledge‑Mechanismen nutzen.

RabbitMQ:

```text
basic_ack
basic_nack
basic_reject
```

Redis (manuell):

- Job aus Queue holen  
- In „processing“ verschieben  
- Nach Erfolg löschen  

---

## ❓ Wie baue ich eine Dead‑Letter‑Queue (DLQ)?
**Lösung:** Fehlgeschlagene Jobs separat speichern.

```bash
RPUSH dlq "send_email:42:failed"
```

DLQ dient zur Analyse & manuellen Reprocessing.

---

## ❓ Wie verhindere ich Duplicate Processing?
**Lösung:** Dedup‑Key setzen.

```bash
SETNX job:lock:42 1 EX 60
```

Nur ein Worker verarbeitet den Job.

---

## ❓ Wie skaliere ich Worker horizontal?
**Lösung:** Worker sind stateless.

- Mehrere Worker → gleiche Queue  
- Keine lokalen Caches  
- Keine lokalen Locks  
- Idempotente Jobs  

---

## ❓ Wie mache ich Jobs idempotent?
**Lösung:** Gleiche Aktion mehrfach → gleicher Zustand.

Beispiele:

- E‑Mail nur senden, wenn `sent_at` leer  
- Bestellung nur einmal berechnen  
- Zahlung nur einmal buchen  

---

## ❓ Wie überwache ich Worker?
**Lösung:** Metriken & Health Checks.

- Queue‑Länge  
- Processing‑Zeit  
- Retry‑Rate  
- DLQ‑Wachstum  
- Worker‑Heartbeat  

---

## Pro-Tipp
Nutze **Visibility Timeouts** (oder TTL‑Locks), damit Jobs automatisch zurück in die Queue fallen, wenn ein Worker abstürzt.
