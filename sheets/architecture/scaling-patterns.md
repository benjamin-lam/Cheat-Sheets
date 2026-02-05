---
title: Scaling Patterns Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Scaling Patterns: Vertical, Horizontal, Sharding & Statelessness

Dieses Sheet bündelt die wichtigsten Skalierungs‑Konzepte für moderne Plattformen — ideal für APIs, Microservices, Datenbanken und High‑Traffic‑Systeme.

---

## ❓ Warum Skalierung?
**Lösung:** Systeme müssen unter Last stabil bleiben.

Skalierung verbessert:

- Durchsatz  
- Latenz  
- Resilienz  
- Kostenkontrolle  
- Nutzererlebnis  

---

## ❓ Welche Skalierungsarten gibt es?
**Lösung:** zwei Grundformen.

### Vertikale Skalierung (Scale Up)
- größere Maschine  
- mehr CPU, RAM, IO  
- schnell, aber begrenzt  
- teuer  

### Horizontale Skalierung (Scale Out)
- mehr Instanzen  
- Load Balancing  
- stateless Services  
- praktisch unbegrenzt  

Regel: **Horizontal schlägt vertikal**.

---

## ❓ Was ist Statelessness?
**Lösung:** keine Session im Service.

Ein stateless Service:

- speichert keinen Zustand lokal  
- kann beliebig repliziert werden  
- ist ideal für Load Balancing  

State gehört in:

- Redis  
- Datenbanken  
- Object Storage  

---

## ❓ Wie skaliert man Datenbanken?
**Lösung:** drei Strategien.

### 1. Read Replicas
- Master → Writes  
- Replicas → Reads  
- eventual consistency  

### 2. Sharding
- Daten nach Schlüssel aufteilen  
- Beispiel: user_id % 4 → Shard 0–3  
- komplex, aber mächtig  

### 3. Partitioning
- Tabellen logisch trennen  
- z. B. nach Datum  

---

## ❓ Wie skaliert man APIs?
**Lösung:** Load Balancing + Caching.

Mechanismen:

- Round Robin  
- Least Connections  
- IP Hash  
- Weighted Routing  

Zusätzlich:

- CDN für statische Assets  
- API‑Caching  
- Rate Limiting  

---

## ❓ Wie skaliert man Queues?
**Lösung:** Consumer‑Scaling.

- mehr Worker  
- Prefetch‑Tuning  
- Backpressure  
- DLQ‑Monitoring  

---

## ❓ Wie skaliert man Event Streams?
**Lösung:** Partitionen.

Kafka:

- mehr Partitionen → mehr Parallelität  
- Partition Key → Ordering  

---

## ❓ Wie skaliert man Storage?
**Lösung:** Object Storage + CDN.

- S3  
- GCS  
- Azure Blob  

Vorteile:

- praktisch unbegrenzt  
- günstig  
- global replizierbar  

---

## ❓ Wie skaliert man Suchsysteme?
**Lösung:** Elasticsearch‑Cluster.

- Shards  
- Replicas  
- Node‑Rollen (Master, Data, Ingest)  

---

## ❓ Wie skaliert man Microservices?
**Lösung:** pro Service unabhängig.

Jeder Service:

- eigener Deployment‑Plan  
- eigene Skalierungsregeln  
- eigene Datenbank  
- eigene Observability  

---

## ❓ Wie skaliert man Hintergrundjobs?
**Lösung:** Worker‑Pools.

- Queue‑Länge → Autoscaling  
- CPU‑Last → Autoscaling  
- Timeouts → Schutzmechanismus  

---

## ❓ Wie skaliert man global?
**Lösung:** Multi‑Region‑Architektur.

Strategien:

- Active‑Active  
- Active‑Passive  
- Geo‑Routing  
- Edge‑Caching  

Trade‑off:

- Latenz vs. Konsistenz  

---

## ❓ Wie messe ich Skalierungsbedarf?
**Lösung:** Metriken.

Wichtig:

- CPU / RAM  
- RPS  
- Error Rate  
- Latency (P95/P99)  
- Queue‑Länge  
- DB‑Connections  
- Cache Hit Ratio  

---

## Pro-Tipp
Skalierung ist **Bottleneck‑Management**: Du skalierst nicht das System, sondern die Engstellen — und jede Engstelle hat andere Konsequenzen.
