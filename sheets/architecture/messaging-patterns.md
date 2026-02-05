---
title: Messaging Patterns Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Messaging Patterns: Queues, Events, Streams & Delivery Guarantees

Dieses Sheet bündelt die wichtigsten Messaging‑Konzepte für verteilte Systeme — ideal für Microservices, Event‑Driven Architecture und skalierende Plattformen.

---

## ❓ Warum Messaging?
**Lösung:** Entkopplung + Resilienz + Skalierung.

Messaging ermöglicht:

- asynchrone Kommunikation  
- Lastverteilung  
- Retry‑Mechanismen  
- Backpressure  
- lose Kopplung  

---

## ❓ Welche Messaging‑Typen gibt es?
**Lösung:** drei Grundformen.

### 1. Message Queues (MQ)
- Punkt‑zu‑Punkt  
- Konsument zieht Nachricht  
- Beispiel: RabbitMQ, SQS  

### 2. Event Streams
- unveränderbare Log‑Struktur  
- mehrere Konsumenten lesen unabhängig  
- Beispiel: Kafka, Pulsar  

### 3. Pub/Sub
- Publisher sendet an Topic  
- Subscriber erhalten Kopien  
- Beispiel: Google Pub/Sub, Redis Streams  

---

## ❓ Welche Delivery Guarantees gibt es?
**Lösung:** drei Stufen.

| Guarantee          | Bedeutung |
|--------------------|-----------|
| At Most Once       | keine Duplikate, aber Verlust möglich |
| At Least Once      | keine Verluste, aber Duplikate möglich |
| Exactly Once       | teuer, selten, oft illusorisch |

Regel:

- **At Least Once** ist Standard  
- Idempotenz ist Pflicht  

---

## ❓ Was ist Idempotenz?
**Lösung:** gleiche Nachricht mehrfach → gleicher Zustand.

Beispiel:

```text
charge(user, amount) → NICHT idempotent
markOrderPaid(orderId) → idempotent
```

Idempotenz ist das wichtigste Messaging‑Pattern überhaupt.

---

## ❓ Wie strukturiere ich Events?
**Lösung:** minimal + versioniert.

```json
{
  "event": "OrderCreated",
  "version": 1,
  "timestamp": "2025-09-02T12:00:00Z",
  "data": {
    "order_id": 42,
    "user_id": 7,
    "total": 199.99
  }
}
```

Regeln:

- keine internen Felder  
- keine technischen IDs  
- keine riesigen Payloads  

---

## ❓ Wie mache ich Retry‑Strategien?
**Lösung:** Backoff + Dead Letter Queue.

### Exponential Backoff
- 1s → 2s → 4s → 8s → …  

### Dead Letter Queue (DLQ)
- Nachrichten, die dauerhaft fehlschlagen  
- manuelle oder automatische Analyse  

---

## ❓ Wie mache ich Ordering?
**Lösung:** Partition Keys.

Beispiel:

- alle Events eines Users → gleiche Partition  
- alle Events einer Bestellung → gleiche Partition  

Ordering ist **lokal**, nie global.

---

## ❓ Wie mache ich Backpressure?
**Lösung:** Konsumenten steuern Tempo.

Mechanismen:

- Prefetch / Consumer Window  
- Pausieren von Konsumenten  
- Queue‑Länge als Metrik  
- Autoscaling der Worker  

---

## ❓ Wie mache ich Eventual Consistency?
**Lösung:** Events + Retries + Idempotenz.

Ein System ist konsistent, wenn:

- alle Events verarbeitet wurden  
- alle Konsumenten aufgeholt haben  
- keine Duplikate schaden  

---

## ❓ Wie mache ich Outbox Pattern?
**Lösung:** DB + Outbox‑Tabelle + Polling.

Ablauf:

1. Business‑Transaktion schreibt Outbox‑Eintrag  
2. Outbox‑Worker liest Einträge  
3. Worker publiziert Event  
4. Eintrag wird markiert  

Vorteil:

- keine verlorenen Events  
- keine Dual‑Write‑Probleme  

---

## ❓ Wie mache ich Saga Pattern?
**Lösung:** verteilte Transaktionen ohne 2PC.

Typen:

- Choreography (Events)  
- Orchestration (zentraler Controller)  

Beispiel:

- Bestellung anlegen  
- Zahlung ausführen  
- Lager reservieren  
- Versand starten  

Bei Fehlern:

- Kompensations‑Events  

---

## ❓ Wie überwache ich Messaging‑Systeme?
**Lösung:** Metriken + Logs + Traces.

Wichtige Metriken:

- Queue‑Länge  
- Consumer Lag  
- Processing Time  
- Error Rate  
- DLQ‑Rate  

---

## Pro-Tipp
Messaging ist **Konsequenz‑Management**: Du bekommst Resilienz und Skalierung — aber nur, wenn Idempotenz, Versionierung und Backpressure sauber umgesetzt sind.
