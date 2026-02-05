---
title: Storage Patterns Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Storage Patterns: Databases, Object Storage & Access Strategies

Dieses Sheet bündelt die wichtigsten Speicher‑Konzepte für moderne Systeme — ideal für Microservices, Plattformen, Daten‑intensive Anwendungen und skalierende Architekturen.

---

## ❓ Warum Storage Patterns?
**Lösung:** Daten sind das Rückgrat jedes Systems.

Storage Patterns helfen bei:

- Skalierung  
- Kostenkontrolle  
- Konsistenz  
- Performance  
- Sicherheit  
- Wiederherstellbarkeit  

---

## ❓ Welche Storage‑Typen gibt es?
**Lösung:** vier Grundkategorien.

### 1. Relationale Datenbanken (SQL)
- strukturierte Daten  
- ACID  
- starke Konsistenz  
- ideal für Geschäftslogik  

Beispiele: PostgreSQL, MySQL, MariaDB

### 2. NoSQL Datenbanken
- Key‑Value (Redis)  
- Document (MongoDB)  
- Column (Cassandra)  
- Graph (Neo4j)  

### 3. Object Storage
- Dateien, Blobs, Medien  
- praktisch unbegrenzt  
- günstig  
- global replizierbar  

Beispiele: S3, GCS, Azure Blob

### 4. Search Engines
- Volltextsuche  
- Analytics  
- komplexe Queries  

Beispiele: Elasticsearch, OpenSearch

---

## ❓ Wie wähle ich den richtigen Storage?
**Lösung:** nach Zugriffsmuster.

| Bedarf | Pattern |
|--------|---------|
| komplexe Transaktionen | SQL |
| flexible Dokumente | Document Store |
| massive Schreiblast | Column Store |
| globale Dateien | Object Storage |
| Suche & Analytics | Search Engine |
| extrem schnelle Reads | Key‑Value Cache |

---

## ❓ Was ist Hot, Warm & Cold Storage?
**Lösung:** Kosten vs. Zugriffsgeschwindigkeit.

### Hot Storage
- sofortiger Zugriff  
- teuer  
- z. B. SQL, Redis  

### Warm Storage
- seltener Zugriff  
- günstiger  
- z. B. Elasticsearch, S3 Standard  

### Cold Storage
- seltene Zugriffe  
- sehr günstig  
- z. B. S3 Glacier  

---

## ❓ Was ist Data Partitioning?
**Lösung:** Daten logisch trennen.

Typen:

- Range Partitioning (z. B. Datum)  
- Hash Partitioning (z. B. user_id % 4)  
- List Partitioning (z. B. Region)  

Vorteile:

- bessere Performance  
- bessere Skalierung  

---

## ❓ Was ist Sharding?
**Lösung:** Daten physisch auf mehrere Knoten verteilen.

Beispiel:

```
user_id % 4 → Shard 0–3
```

Vorteile:

- horizontale Skalierung  
- weniger Hotspots  

Nachteile:

- komplexere Queries  
- Rebalancing nötig  

---

## ❓ Wie mache ich Read Replicas?
**Lösung:** Master → Writes, Replicas → Reads.

Vorteile:

- Entlastung  
- Skalierung  

Nachteile:

- eventual consistency  

---

## ❓ Wie mache ich Write Scaling?
**Lösung:** mehrere Strategien.

- Sharding  
- Partitioning  
- Queue‑basierte Writes  
- Event Sourcing  

---

## ❓ Wie mache ich File Storage richtig?
**Lösung:** Object Storage + CDN.

Beispiel:

- Upload → S3  
- Serve → Cloudflare CDN  

Regeln:

- niemals Dateien in der DB speichern  
- URLs signieren  
- Versionierung aktivieren  

---

## ❓ Wie mache ich Backups?
**Lösung:** automatisiert + getestet.

Regeln:

- regelmäßige Snapshots  
- Point‑in‑Time Recovery  
- Restore‑Tests  
- Offsite‑Backups  

---

## ❓ Wie mache ich Disaster Recovery?
**Lösung:** Multi‑Region‑Strategien.

Optionen:

- Active‑Passive  
- Active‑Active  
- Geo‑Replication  

Wichtig:

- RPO (Recovery Point Objective)  
- RTO (Recovery Time Objective)  

---

## ❓ Wie mache ich Storage Observability?
**Lösung:** Metriken + Logs.

Wichtige Metriken:

- Query Latency  
- IOPS  
- Replication Lag  
- Storage Size  
- Error Rate  
- Cache Hit Ratio  

---

## ❓ Wie mache ich Storage Security?
**Lösung:** Defense‑in‑Depth.

- Verschlüsselung at rest  
- Verschlüsselung in transit  
- IAM Policies  
- Least Privilege  
- Audit Logs  

---

## Pro-Tipp
Storage ist **Zugriffsmuster‑Design**: Nicht die Technologie entscheidet, sondern wie Daten gelesen, geschrieben und skaliert werden müssen.
