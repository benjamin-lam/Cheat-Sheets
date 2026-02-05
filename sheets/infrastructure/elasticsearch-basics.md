---
title: Elasticsearch Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Elasticsearch Basics: Indexing, Queries & Aggregations

Dieses Sheet bündelt die wichtigsten Elasticsearch‑Konzepte für Suche, Analytics, Logging und Observability — ideal für produktionsnahe Cluster.

---

## ❓ Wie teste ich, ob Elasticsearch läuft?
**Lösung:** Health‑Check.

```bash
curl -X GET http://localhost:9200
```

Cluster‑Status:

```bash
curl -X GET http://localhost:9200/_cluster/health
```

---

## ❓ Wie erstelle ich einen Index?
**Lösung:** Minimal‑Index.

```bash
curl -X PUT http://localhost:9200/users
```

Mit Mapping:

```bash
curl -X PUT http://localhost:9200/users -H "Content-Type: application/json" -d '{
  "mappings": {
    "properties": {
      "name": { "type": "text" },
      "age": { "type": "integer" },
      "created_at": { "type": "date" }
    }
  }
}'
```

---

## ❓ Wie füge ich Dokumente ein?
**Lösung:** Index API.

```bash
curl -X POST http://localhost:9200/users/_doc -H "Content-Type: application/json" -d '{
  "name": "Ben",
  "age": 42
}'
```

Mit ID:

```bash
curl -X PUT http://localhost:9200/users/_doc/1 -H "Content-Type: application/json" -d '{
  "name": "Alice"
}'
```

---

## ❓ Wie finde ich Dokumente?
**Lösung:** Match Query.

```bash
curl -X GET http://localhost:9200/users/_search -H "Content-Type: application/json" -d '{
  "query": {
    "match": { "name": "Ben" }
  }
}'
```

Exact Match:

```json
"term": { "age": 42 }
```

---

## ❓ Wie mache ich komplexe Bool‑Queries?
**Lösung:** must, should, must_not.

```bash
curl -X GET http://localhost:9200/users/_search -H "Content-Type: application/json" -d '{
  "query": {
    "bool": {
      "must": [
        { "match": { "active": true } }
      ],
      "must_not": [
        { "term": { "role": "admin" } }
      ]
    }
  }
}'
```

---

## ❓ Wie mache ich Aggregationen?
**Lösung:** group by + metrics.

```bash
curl -X GET http://localhost:9200/orders/_search -H "Content-Type: application/json" -d '{
  "size": 0,
  "aggs": {
    "total_by_user": {
      "terms": { "field": "user_id" },
      "aggs": {
        "sum_amount": { "sum": { "field": "amount" } }
      }
    }
  }
}'
```

---

## ❓ Wie aktualisiere ich Dokumente?
**Lösung:** Update API.

```bash
curl -X POST http://localhost:9200/users/_update/1 -H "Content-Type: application/json" -d '{
  "doc": { "active": false }
}'
```

---

## ❓ Wie lösche ich Dokumente?
**Lösung:** Delete API.

```bash
curl -X DELETE http://localhost:9200/users/_doc/1
```

Index löschen:

```bash
curl -X DELETE http://localhost:9200/users
```

---

## ❓ Wie finde ich langsame Queries?
**Lösung:** Profiling.

```bash
curl -X GET http://localhost:9200/users/_search -H "Content-Type: application/json" -d '{
  "profile": true,
  "query": { "match_all": {} }
}'
```

---

## ❓ Wie optimiere ich Mappings?
**Lösung:** Typen bewusst wählen.

- `keyword` für exact match, Sortierung, Aggregationen  
- `text` für Volltextsuche  
- `date` für Zeitreihen  
- `integer`, `float` für numerische Felder  

Beispiel:

```json
"status": { "type": "keyword" }
```

---

## ❓ Wie arbeite ich mit Bulk‑Operationen?
**Lösung:** Bulk API.

```bash
curl -X POST http://localhost:9200/_bulk -H "Content-Type: application/json" -d '
{ "index": { "_index": "users", "_id": 1 } }
{ "name": "Ben" }
{ "index": { "_index": "users", "_id": 2 } }
{ "name": "Alice" }
'
```

---

## ❓ Wie überwache ich Cluster‑Performance?
**Lösung:** Monitoring APIs.

Nodes:

```bash
curl -X GET http://localhost:9200/_nodes/stats
```

Indices:

```bash
curl -X GET http://localhost:9200/_stats
```

---

## Pro-Tipp
Nutze **keyword + text dual‑fields**, um sowohl Volltextsuche als auch exakte Filter zu ermöglichen:

```json
"name": {
  "type": "text",
  "fields": {
    "raw": { "type": "keyword" }
  }
}
```
