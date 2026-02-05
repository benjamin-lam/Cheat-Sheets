---
title: Service Basics Cheat Sheet
category: Backend
last_updated: 2025-09-02
status: stable
---

# Service Basics: Layering, Boundaries, Contracts & Operational Reality

Dieses Sheet bündelt die wichtigsten Grundlagen für robuste, wartbare und klar abgegrenzte Services — ideal für Microservices, modulare Monolithen und verteilte Architekturen.

---

## ❓ Was ist ein Service?
**Lösung:** Eine klar abgegrenzte, verantwortungsvolle Einheit.

Ein Service hat:

- eine **klare Aufgabe**  
- eine **eindeutige Verantwortlichkeit**  
- eine **stabile API**  
- eigene **Daten**  
- eigene **Operational Reality** (Monitoring, Logs, Alerts)  

Ein Service ist kein Ordner, sondern eine **Konsequenz‑Einheit**.

---

## ❓ Wie definiere ich Service‑Boundaries?
**Lösung:** durch Verantwortung, nicht durch Technologie.

Gute Boundaries:

- ein Service = ein Geschäftsbegriff  
- keine geteilten Datenbanken  
- keine „Utility‑Services“  
- keine „Shared Models“  

Schlechte Boundaries:

- „UserService“, „OrderService“, „HelperService“  
- technische Gruppierung statt fachlicher  

---

## ❓ Wie sieht eine typische Service‑Struktur aus?
**Lösung:** Ports & Adapters.

```text
service/
  domain/
  application/
  infrastructure/
  api/
```

- **domain** → Geschäftslogik  
- **application** → Use Cases  
- **infrastructure** → DB, HTTP, Messaging  
- **api** → Controller, DTOs  

---

## ❓ Wie kommunizieren Services?
**Lösung:** über klar definierte Verträge.

Typen:

- **synchron**: REST, gRPC  
- **asynchron**: Events, Queues, Streams  

Regel:

- intern → Events bevorzugen  
- extern → APIs bevorzugen  

---

## ❓ Wie sieht ein guter API‑Contract aus?
**Lösung:** stabil, versioniert, minimal.

Beispiel:

```json
{
  "id": 42,
  "email": "ben@example.com",
  "created_at": "2025-09-02T12:00:00Z"
}
```

Schlecht:

- verschachtelte Monsterobjekte  
- interne Felder  
- unklare Typen  

---

## ❓ Wie sieht ein gutes Event aus?
**Lösung:** immutable + minimal.

```json
{
  "event": "UserRegistered",
  "version": 1,
  "timestamp": "2025-09-02T12:00:00Z",
  "data": {
    "user_id": 42,
    "email": "ben@example.com"
  }
}
```

---

## ❓ Wie mache ich Service‑Isolation?
**Lösung:** keine geteilten Daten.

Prinzipien:

- jeder Service besitzt seine Daten  
- Zugriff nur über API oder Events  
- kein „SELECT * FROM fremde_tabelle“  

---

## ❓ Wie mache ich Observability?
**Lösung:** Logs + Metrics + Traces.

Jeder Service braucht:

- strukturierte Logs  
- Metriken (RPS, Errors, Latency)  
- Traces (Trace‑ID, Span‑ID)  
- Health Checks  
- Alerts  

---

## ❓ Wie mache ich Resilience?
**Lösung:** defensive Patterns.

- Timeouts  
- Retries (mit Backoff)  
- Circuit Breaker  
- Bulkheads  
- Idempotenz  

---

## ❓ Wie deploye ich Services?
**Lösung:** unabhängig.

Ein Service sollte:

- unabhängig gebaut werden  
- unabhängig deployt werden  
- unabhängig skalieren  
- unabhängig versioniert werden  

---

## ❓ Wie teste ich Services?
**Lösung:** mehrere Ebenen.

- Unit Tests  
- Integration Tests  
- Contract Tests  
- End‑to‑End Tests  
- Chaos Tests  

---

## Pro-Tipp
Ein Service ist erst dann „gut“, wenn er **klar abgegrenzt**, **operational sichtbar** und **konsequenzfähig** ist — alles andere ist nur Code in einem Ordner.
