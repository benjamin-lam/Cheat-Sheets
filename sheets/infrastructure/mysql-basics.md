---
title: MySQL Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# MySQL Basics: Queries, Indexe & Performance

Dieses Sheet bündelt die wichtigsten MySQL‑Kommandos für Setup, Debugging, Query‑Optimierung und tägliche Arbeit mit relationalen Datenbanken.

---

## ❓ Wie verbinde ich mich mit MySQL?
**Lösung:** CLI‑Login.

```bash
mysql -u root -p
```

Mit Host:

```bash
mysql -h 127.0.0.1 -u user -p
```

---

## ❓ Wie zeige ich Datenbanken & Tabellen an?
**Lösung:** SHOW‑Befehle.

```sql
SHOW DATABASES;
USE mydb;
SHOW TABLES;
DESCRIBE users;
```

---

## ❓ Wie mache ich CRUD‑Operationen?
**Lösung:** Standard‑SQL.

Select:

```sql
SELECT id, name FROM users WHERE active = 1;
```

Insert:

```sql
INSERT INTO users (name, email) VALUES ('Ben', 'ben@example.com');
```

Update:

```sql
UPDATE users SET active = 0 WHERE id = 42;
```

Delete:

```sql
DELETE FROM users WHERE id = 42;
```

---

## ❓ Wie setze ich Indexe richtig?
**Lösung:** Indexe für WHERE, JOIN, ORDER BY.

```sql
CREATE INDEX idx_users_email ON users(email);
```

Unique Index:

```sql
CREATE UNIQUE INDEX idx_users_username ON users(username);
```

---

## ❓ Wie analysiere ich Query‑Performance?
**Lösung:** EXPLAIN.

```sql
EXPLAIN SELECT * FROM users WHERE email = 'a@b.com';
```

Wichtig:

- type: ALL = schlecht  
- type: ref / const = gut  
- key: verwendeter Index  

---

## ❓ Wie finde ich langsame Queries?
**Lösung:** Slow Query Log aktivieren.

```sql
SET GLOBAL slow_query_log = 1;
SET GLOBAL long_query_time = 1;
```

---

## ❓ Wie mache ich Backups?
**Lösung:** mysqldump.

```bash
mysqldump -u root -p mydb > backup.sql
```

Restore:

```bash
mysql -u root -p mydb < backup.sql
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
START TRANSACTION;
UPDATE users SET ... WHERE id = 1;
UPDATE orders SET ... WHERE user_id = 1;
COMMIT;
```

---

## ❓ Wie optimiere ich Tabellen?
**Lösung:** ANALYZE + OPTIMIZE.

```sql
ANALYZE TABLE users;
OPTIMIZE TABLE users;
```

---

## ❓ Wie prüfe ich laufende Queries?
**Lösung:** processlist.

```sql
SHOW FULL PROCESSLIST;
```

---

## ❓ Wie setze ich sichere Defaults?
**Lösung:** Wichtige my.cnf‑Optionen.

```ini
innodb_buffer_pool_size = 1G
innodb_log_file_size = 256M
max_connections = 200
sql_mode = STRICT_ALL_TABLES
```

---

## Pro-Tipp
Nutze **Composite Indexe** (mehrere Spalten), aber immer in der richtigen Reihenfolge — MySQL nutzt sie nur von links nach rechts.
