---
title: System Design Basics Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# System Design Basics: Scalability, Data Flows, Caches & Trade-offs

Dieses Sheet bündelt die wichtigsten Grundlagen für das Design großer, verteilter Systeme — ideal für Microservices, Plattformen und hochskalierende Anwendungen.

---

## ❓ Was ist System Design?
**Lösung:** Die Kunst, Systeme zu bauen, die unter Last funktionieren.

System Design beantwortet:

- Wie skalieren wir?  
- Wie speichern wir Daten?  
- Wie kommunizieren Komponenten?  
- Wie verhindern wir Ausfälle?  
- Wie messen wir Verhalten?  

Es geht immer um **Trade-offs**, nie um perfekte Lösungen.

---

## ❓ Was sind die wichtigsten Bausteine?
**Lösung:** die Grundkomponenten verteilter Systeme.

- Load Balancer  
- API Gateways  
- Caches  
- Message Queues  
- Databases  
- Object Storage  
- Search Engines  
- Stream Processing  
- CDNs  
- Monitoring & Logging  

---

## ❓ Wie skaliert man Systeme?
**Lösung:** horizontal > vertikal.

Vertikal:

- größere Maschine  
- begrenzter Nutzen  

Horizontal:

- mehr Instanzen  
- Load Balancing  
- Stateless Services  

---

## ❓ Was ist ein Cache?
**Lösung:** schneller Speicher für häufige Daten.

Typen:

- In‑Memory (Redis, Memcached)  
- CDN (Cloudflare, Akamai)  
- Application Cache  

Strategien:

- Cache Aside  
- Write Through  
- Write Back  

---

## ❓ Was ist ein Load Balancer?
**Lösung:** verteilt Traffic.

Typen:

- L4 (TCP)  
- L7 (HTTP)  

Strategien:

- Round Robin  
- Least Connections  
- IP Hash  

---

## ❓ Was ist ein Message Queue System?
**Lösung:** asynchrone Kommunikation.

Beispiele:

- RabbitMQ  
- Kafka  
- SQS  

Vorteile:

- Entkopplung  
- Resilienz  
- Backpressure  

---

## ❓ Was ist ein CDN?
**Lösung:** global verteilte Caches.

Vorteile:

- weniger Latenz  
- weniger Origin‑Load  
- DDoS‑Schutz  

---

## ❓ Wie speichert man Daten?
**Lösung:** je nach Zugriffsmuster.

Optionen:

- Relationale DBs  
- NoSQL (Key‑Value, Document, Column)  
- Search Engines (Elasticsearch)  
- Object Storage (S3)  
- Time Series DBs (Prometheus)  

---

## ❓ Wie designe ich eine API unter Last?
**Lösung:** defensive Patterns.

- Rate Limiting  
- Caching  
- Pagination  
- Idempotenz  
- Bulk Endpoints  
- Circuit Breaker  

---

## ❓ Wie mache ich Datenkonsistenz?
**Lösung:** CAP‑Trade-offs.

- Consistency  
- Availability  
- Partition Tolerance  

Typische Strategien:

- Eventual Consistency  
- Strong Consistency  
- Read‑Your‑Writes  

---

## ❓ Wie mache ich Observability?
**Lösung:** Logs + Metrics + Traces.

Jedes System braucht:

- strukturierte Logs  
- Metriken (RPS, Errors, Latency)  
- Traces (Trace‑ID, Span‑ID)  
- Dashboards  
- Alerts  

---

## ❓ Wie mache ich Resilience?
**Lösung:** defensive Architektur.

- Timeouts  
- Retries (mit Backoff)  
- Circuit Breaker  
- Bulkheads  
- Load Shedding  
- Graceful Degradation  

---

## ❓ Wie mache ich High Availability?
**Lösung:** Redundanz + Failover.

- mehrere Instanzen  
- mehrere Zonen  
- mehrere Regionen  
- automatische Wiederherstellung  

---

## ❓ Wie mache ich ein System „operational ready“?
**Lösung:** Operational Reality.

Ein System ist erst fertig, wenn es:

- Logs schreibt  
- Metriken liefert  
- Traces erzeugt  
- Health Checks hat  
- Alerts definiert  
- Dashboards besitzt  
- Backups & Restore getestet sind  

---

## Pro-Tipp
System Design ist **Trade-off‑Design**: Jede Entscheidung erzeugt Konsequenzen — gute Systeme machen diese sichtbar, steuerbar und messbar.
