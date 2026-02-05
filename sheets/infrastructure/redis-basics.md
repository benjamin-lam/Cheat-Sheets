---
title: Redis Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Redis Basics: Keys, TTL, Pub/Sub & Performance

Dieses Sheet bündelt die wichtigsten Redis‑Kommandos für Caching, Queues, Locking und schnelle Datenstrukturen — ideal für Backend‑Services, Microservices und High‑Performance‑Systeme.

---

## ❓ Wie verbinde ich mich mit Redis?
**Lösung:** redis‑cli.

```bash
redis-cli
redis-cli -h 127.0.0.1 -p 6379
```

---

## ❓ Wie setze und lese ich Werte?
**Lösung:** SET & GET.

```bash
SET user:42 "Ben"
GET user:42
```

Mit Ablaufzeit:

```bash
SET session:abc 123 EX 3600
```

---

## ❓ Wie prüfe ich, ob ein Key existiert?
**Lösung:** EXISTS.

```bash
EXISTS user:42
```

---

## ❓ Wie lösche ich Keys?
**Lösung:** DEL.

```bash
DEL user:42
```

Alle Keys löschen (vorsichtig!):

```bash
FLUSHALL
```

---

## ❓ Wie arbeite ich mit Listen?
**Lösung:** LPUSH, RPUSH, LPOP, RPOP.

```bash
LPUSH queue "task1"
RPUSH queue "task2"
LPOP queue
```

---

## ❓ Wie arbeite ich mit Sets?
**Lösung:** SADD, SMEMBERS.

```bash
SADD tags "php"
SADD tags "redis"
SMEMBERS tags
```

---

## ❓ Wie arbeite ich mit Hashes?
**Lösung:** HSET, HGET, HGETALL.

```bash
HSET user:42 name "Ben"
HSET user:42 email "ben@example.com"
HGETALL user:42
```

---

## ❓ Wie arbeite ich mit Sorted Sets?
**Lösung:** ZADD, ZRANGE.

```bash
ZADD leaderboard 100 "ben"
ZADD leaderboard 200 "alice"
ZRANGE leaderboard 0 -1 WITHSCORES
```

---

## ❓ Wie setze ich TTLs?
**Lösung:** EXPIRE.

```bash
EXPIRE session:abc 3600
TTL session:abc
```

---

## ❓ Wie mache ich Pub/Sub?
**Lösung:** publish & subscribe.

Subscriber:

```bash
SUBSCRIBE news
```

Publisher:

```bash
PUBLISH news "Hello world"
```

---

## ❓ Wie mache ich verteilte Locks?
**Lösung:** SET NX + EX.

```bash
SET lock:job1 "1" NX EX 30
```

Wenn der Key existiert → Lock schlägt fehl.

---

## ❓ Wie finde ich Keys?
**Lösung:** KEYS (nur für Debugging).

```bash
KEYS user:*
```

Produktiv stattdessen:

```bash
SCAN 0 MATCH user:* COUNT 100
```

---

## ❓ Wie prüfe ich Speicher & Performance?
**Lösung:** INFO.

```bash
INFO memory
INFO stats
```

---

## ❓ Wie persistiert Redis Daten?
**Lösung:** RDB & AOF.

RDB Snapshot:

```bash
SAVE
```

AOF aktivieren in redis.conf:

```ini
appendonly yes
appendfsync everysec
```

---

## Pro-Tipp
Nutze **Redis als Datenstruktur‑Server**, nicht als Key‑Value‑Dump — Listen, Sets, Sorted Sets und Hashes sind der wahre Performance‑Hebel.
