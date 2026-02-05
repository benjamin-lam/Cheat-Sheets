---
title: Consistency Models Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Consistency Models: CAP, Eventual Consistency & Read Semantics

Dieses Sheet bündelt die wichtigsten Konsistenzmodelle für verteilte Systeme — ideal für Datenbanken, Microservices, Caches und globale Plattformen.

---

## ❓ Warum Konsistenzmodelle?
**Lösung:** Verteilte Systeme können nicht gleichzeitig perfekt konsistent, verfügbar und partitionstolerant sein.

Konsistenzmodelle definieren:

- wie aktuell Daten sind  
- wie Systeme auf Partitionen reagieren  
- wie Clients Lese‑/Schreib‑Semantik erleben  

---

## ❓ Was ist das CAP‑Theorem?
**Lösung:** Ein verteiltes System kann immer nur zwei der drei Eigenschaften gleichzeitig garantieren.

| Eigenschaft | Bedeutung |
|------------|-----------|
| Consistency | alle sehen denselben Zustand |
| Availability | System antwortet immer |
| Partition Tolerance | System funktioniert trotz Netzwerkausfällen |

Regel:

- Partition Tolerance ist in der Praxis unvermeidbar  
- Entscheidung ist **CP** oder **AP**  

---

## ❓ Was ist Strong Consistency?
**Lösung:** jeder Read sieht den neuesten Write.

Eigenschaften:

- deterministisch  
- einfach zu verstehen  
- höhere Latenz  
- weniger verfügbar  

Beispiele:

- klassische SQL‑Datenbanken  
- etcd  
- Spanner (mit TrueTime)  

---

## ❓ Was ist Eventual Consistency?
**Lösung:** irgendwann wird alles konsistent.

Eigenschaften:

- hohe Verfügbarkeit  
- niedrige Latenz  
- temporäre Inkonsistenzen möglich  

Beispiele:

- DynamoDB  
- Cassandra  
- S3  
- Kafka Consumer State  

---

## ❓ Welche schwächeren Konsistenzmodelle gibt es?
**Lösung:** mehrere Abstufungen.

### Read‑Your‑Writes Consistency
Ein Client sieht seine eigenen Writes sofort.

### Monotonic Reads
Ein Client sieht keine älteren Daten als zuvor.

### Monotonic Writes
Writes eines Clients werden in der richtigen Reihenfolge angewendet.

### Causal Consistency
Wenn A vor B passiert, sehen alle Clients A vor B.

### Session Consistency
Innerhalb einer Session → konsistent  
Über Sessions hinweg → eventual consistency  

---

## ❓ Was ist Write Consistency?
**Lösung:** wie viele Replikate müssen einen Write bestätigen?

Beispiele:

- QUORUM  
- ALL  
- ONE  

Trade‑off:

- ALL → stark, aber langsam  
- ONE → schnell, aber schwach  
- QUORUM → guter Mittelweg  

---

## ❓ Was ist Read Consistency?
**Lösung:** wie frisch müssen Reads sein?

Beispiele:

- Read from Leader → stark  
- Read from Replica → schwach  
- Read Repair → eventual consistency  

---

## ❓ Wie funktioniert Conflict Resolution?
**Lösung:** Strategien zur Auflösung konkurrierender Writes.

Typen:

- Last Write Wins (LWW)  
- Vector Clocks  
- CRDTs (Conflict‑Free Replicated Data Types)  
- Application‑Level Merging  

CRDTs ermöglichen **strong eventual consistency**.

---

## ❓ Wie mache ich Konsistenz in Microservices?
**Lösung:** Events + Retries + Idempotenz.

Strategien:

- Outbox Pattern  
- Event Sourcing  
- Saga Pattern  
- Compensating Actions  

Regel:

- Konsistenz ist **ein Prozess**, kein Zustand.  

---

## ❓ Wie mache ich globale Konsistenz?
**Lösung:** Multi‑Region‑Strategien.

Optionen:

- Active‑Active → eventual consistency  
- Active‑Passive → strong consistency  
- Geo‑Partitioning → lokale Konsistenz  

Trade‑off:

- Latenz vs. Konsistenz  

---

## ❓ Wie messe ich Konsistenz?
**Lösung:** Observability‑Signale.

- Replication Lag  
- Stale Reads  
- Divergence Rate  
- Conflict Rate  
- Consumer Lag (bei Streams)  

---

## Pro-Tipp
Konsistenz ist **ein Trade‑off, kein Idealzustand** — gute Architekturen wählen bewusst, welche Konsistenz wo nötig ist und wo nicht.
