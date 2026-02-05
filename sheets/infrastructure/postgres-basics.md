---
title: PostgreSQL Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# PostgreSQL Basics: Queries, Extensions & Performance

Dieses Sheet bündelt die wichtigsten PostgreSQL‑Kommandos für Setup, Debugging, Indexing und Performance‑Analyse — ideal für produktionsnahe Systeme.

---

## ❓ Wie verbinde ich mich mit PostgreSQL?
**Lösung:** psql‑CLI.

```bash
psql -U postgres
psql -h 127.0.0.1 -U user -d mydb
```

---

## ❓ Wie zeige ich Datenbanken, Tabellen & Spalten an?
**Lösung:** Meta‑Commands.

```sql
\l        -- Datenbanken
\c mydb   -- wechseln
\d        -- Tabellen
\d users  -- Tabellenstruktur
```

---

## ❓ Wie mache ich CRUD‑Operationen?
**Lösung:** Standard‑SQL.

Select:

```sql
SELECT id, name FROM users WHERE active = true;
```

Insert:

```sql
INSERT INTO users (name, email) VALUES ('Ben', 'ben@example.com');
```

Update:

```sql
UPDATE users SET active = false WHERE id = 42;
```

Delete:

```sql
DELETE FROM users WHERE id = 42;
```

---

## ❓ Wie setze ich Indexe richtig?
**Lösung:** B‑Tree für Gleichheit, GIN/GiST für JSON & Fulltext.

```sql
CREATE INDEX idx_users_email ON users(email);
```

GIN‑Index für JSONB:

```sql
CREATE INDEX idx_data_json ON events USING GIN (payload);
```

Fulltext:

```sql
CREATE INDEX idx_ft_body ON posts USING GIN (to_tsvector('english', body));
```

---

## ❓ Wie analysiere ich Query‑Performance?
**Lösung:** EXPLAIN (ANALYZE).

```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'a@b.com';
```

Wichtig:

- Seq Scan = kein Index  
- Index Scan = gut  
- Bitmap Heap Scan = große Trefferlisten  

---

## ❓ Wie finde ich langsame Queries?
**Lösung:** pg_stat_statements.

Aktivieren:

```sql
CREATE EXTENSION pg_stat_statements;
```

Abfragen:

```sql
SELECT query, calls, total_time
FROM pg_stat_statements
ORDER BY total_time DESC
LIMIT 10;
```

---

## ❓ Wie mache ich Backups?
**Lösung:** pg_dump.

```bash
pg_dump -U postgres mydb > backup.sql
```

Restore:

```bash
psql -U postgres mydb < backup.sql
```

---

## ❓ Wie setze ich Foreign Keys?
**Lösung:** Referenzielle Integrität.

```sql
ALTER TABLE orders
ADD CONSTRAINT fk_user
FOREIGN KEY (user_id) REFERENCES users(id);
```

---

## ❓ Wie verhindere ich Deadlocks?
**Lösung:** Konsistente Reihenfolge + kurze Transaktionen.

```sql
BEGIN;
UPDATE users SET ... WHERE id = 1;
UPDATE orders SET ... WHERE user_id = 1;
COMMIT;
```

---

## ❓ Wie optimiere ich Tabellen?
**Lösung:** VACUUM & ANALYZE.

```sql
VACUUM ANALYZE;
```

Autovacuum ist standardmäßig aktiv.

---

## ❓ Wie prüfe ich laufende Queries?
**Lösung:** pg_stat_activity.

```sql
SELECT pid, state, query
FROM pg_stat_activity;
```

Kill:

```sql
SELECT pg_terminate_backend(<pid>);
```

---

## ❓ Wie setze ich sichere Defaults?
**Lösung:** postgresql.conf.

```ini
shared_buffers = 1GB
work_mem = 64MB
maintenance_work_mem = 256MB
max_connections = 200
effective_cache_size = 3GB
```

---

## Pro-Tipp
Nutze **CTEs sparsam** — in PostgreSQL werden sie standardmäßig materialisiert und können Queries verlangsamen. Seit PG 12 kann der Planner sie aber optimieren, wenn `NOT MATERIALIZED` gesetzt wird.
