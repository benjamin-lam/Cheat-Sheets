---
title: MongoDB Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# MongoDB Basics: Dokumente, Queries & Indexe

Dieses Sheet bündelt die wichtigsten MongoDB‑Kommandos für CRUD‑Operationen, Aggregation, Indexing und produktionsnahe Nutzung — ideal für flexible, schema‑freie Datenmodelle.

---

## ❓ Wie verbinde ich mich mit MongoDB?
**Lösung:** mongo‑Shell oder mongosh.

```bash
mongosh
mongosh "mongodb://user:pass@localhost:27017/mydb"
```

---

## ❓ Wie zeige ich Datenbanken & Collections an?
**Lösung:** show‑Befehle.

```javascript
show dbs
use mydb
show collections
```

---

## ❓ Wie füge ich Dokumente ein?
**Lösung:** insertOne / insertMany.

```javascript
db.users.insertOne({ name: "Ben", active: true })
```

Mehrere:

```javascript
db.users.insertMany([
  { name: "Alice" },
  { name: "Bob" }
])
```

---

## ❓ Wie finde ich Dokumente?
**Lösung:** find.

```javascript
db.users.find({ active: true })
```

Nur ein Dokument:

```javascript
db.users.findOne({ email: "ben@example.com" })
```

Projektion:

```javascript
db.users.find({}, { name: 1, email: 1 })
```

---

## ❓ Wie aktualisiere ich Dokumente?
**Lösung:** updateOne / updateMany.

```javascript
db.users.updateOne(
  { email: "ben@example.com" },
  { $set: { active: false } }
)
```

---

## ❓ Wie lösche ich Dokumente?
**Lösung:** deleteOne / deleteMany.

```javascript
db.users.deleteOne({ email: "ben@example.com" })
```

---

## ❓ Wie setze ich Indexe?
**Lösung:** createIndex.

```javascript
db.users.createIndex({ email: 1 })
```

Unique:

```javascript
db.users.createIndex({ username: 1 }, { unique: true })
```

Text‑Index:

```javascript
db.posts.createIndex({ body: "text" })
```

---

## ❓ Wie mache ich Aggregationen?
**Lösung:** Aggregation Pipeline.

```javascript
db.orders.aggregate([
  { $match: { status: "paid" } },
  { $group: { _id: "$userId", total: { $sum: "$amount" } } }
])
```

---

## ❓ Wie finde ich langsame Queries?
**Lösung:** explain.

```javascript
db.users.find({ email: "a@b.com" }).explain("executionStats")
```

Achte auf:

- COLLSCAN = kein Index  
- IXSCAN = gut  

---

## ❓ Wie setze ich TTL‑Indexe?
**Lösung:** expireAfterSeconds.

```javascript
db.sessions.createIndex(
  { createdAt: 1 },
  { expireAfterSeconds: 3600 }
)
```

---

## ❓ Wie mache ich Backups?
**Lösung:** mongodump / mongorestore.

```bash
mongodump --db=mydb --out=backup/
```

Restore:

```bash
mongorestore --db=mydb backup/mydb
```

---

## ❓ Wie prüfe ich Serverstatus & Performance?
**Lösung:** serverStatus.

```javascript
db.serverStatus()
```

---

## ❓ Wie arbeite ich mit Replica Sets?
**Lösung:** rs.status.

```javascript
rs.status()
```

Initialisierung:

```javascript
rs.initiate()
```

---

## Pro-Tipp
Nutze **Schema Validation** in MongoDB, um trotz NoSQL klare Strukturen und Qualitätsregeln durchzusetzen — besonders in produktionsnahen Systemen.
