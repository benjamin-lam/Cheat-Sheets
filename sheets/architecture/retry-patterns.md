---
title: Retry Patterns Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Retry Patterns: Backoff, Jitter & Idempotency

Dieses Sheet bündelt die wichtigsten Retry‑Mechaniken für resiliente Systeme — ideal für Microservices, Messaging, APIs und verteilte Architekturen.

---

## ❓ Warum Retries?
**Lösung:** temporäre Fehler automatisch abfangen.

Retries helfen bei:

- Netzwerk‑Glitches  
- kurzzeitigen Timeouts  
- überlasteten Services  
- Rate Limits  
- transienten Fehlern  

Wichtig:
- **Retries lösen keine dauerhaften Fehler**  
- **Retries ohne Kontrolle zerstören Systeme**  

---

## ❓ Welche Retry‑Strategien gibt es?
**Lösung:** drei Grundformen.

### 1. Immediate Retry
- sofort erneut versuchen  
- nur für extrem leichte Operationen  
- riskant bei Lastspitzen  

### 2. Fixed Delay
- fester Abstand zwischen Versuchen  
- einfach, aber nicht optimal  

### 3. Exponential Backoff
- Wartezeit wächst exponentiell  
- Standard für resiliente Systeme  

Beispiel:

```
1s → 2s → 4s → 8s → 16s
```

---

## ❓ Was ist Jitter?
**Lösung:** Zufallsanteil zur Entlastung.

Ohne Jitter:
- alle Clients retryen gleichzeitig  
- „Retry Storm“  

Mit Jitter:
- zufällige Verzögerung  
- Last verteilt sich  

Beispiel:

```
delay = random(0, baseDelay * 2^attempt)
```

---

## ❓ Wie viele Retries sind sinnvoll?
**Lösung:** wenige, kontrollierte Versuche.

Typisch:

- 3–5 Versuche  
- maximale Gesamtdauer begrenzen  
- Timeouts pro Versuch setzen  

Regel:
- **weniger Retries → stabiler**  

---

## ❓ Welche Fehler sollten retried werden?
**Lösung:** nur temporäre Fehler.

Gute Kandidaten:

- 408 Request Timeout  
- 429 Too Many Requests  
- 500 Internal Server Error  
- 502 Bad Gateway  
- 503 Service Unavailable  
- 504 Gateway Timeout  

Keine Retries bei:

- 400 Bad Request  
- 401 Unauthorized  
- 403 Forbidden  
- 404 Not Found  

---

## ❓ Wie mache ich Idempotenz?
**Lösung:** gleiche Operation mehrfach → gleicher Zustand.

Beispiele:

- `PUT /users/42` → idempotent  
- `DELETE /orders/7` → idempotent  
- `POST /orders` → **nicht** idempotent  

Lösung für POST:

- Idempotency Keys  
- Outbox Pattern  
- dedizierte „create‑if‑not‑exists“ Endpoints  

---

## ❓ Wie mache ich Retries in Messaging?
**Lösung:** Backoff + DLQ.

Mechanismen:

- Retry Queue  
- Exponential Backoff  
- Dead Letter Queue  
- Idempotente Consumer  

Regel:
- **At‑Least‑Once Delivery → Idempotenz Pflicht**  

---

## ❓ Wie mache ich Retries in APIs?
**Lösung:** Client‑seitig + Gateway‑seitig.

Client:

- Backoff + Jitter  
- Timeouts  
- Circuit Breaker  

Gateway:

- Retry‑Budget  
- Retry‑Policy pro Route  

---

## ❓ Wie verhindere ich Retry Storms?
**Lösung:** Schutzmechanismen.

- Jitter  
- Circuit Breaker  
- Rate Limiting  
- Load Shedding  
- Retry‑Budget (max. Retries pro Zeitfenster)  

---

## ❓ Wie mache ich Observability für Retries?
**Lösung:** Metriken + Logs + Traces.

Wichtig:

- Retry Count  
- Retry Delay  
- Error Rate  
- Latency  
- DLQ‑Rate (bei Messaging)  

---

## Pro-Tipp
Retries sind **ein Skalpell, kein Hammer** — richtig eingesetzt erhöhen sie Resilienz, falsch eingesetzt zerstören sie Systeme.
