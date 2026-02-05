---
title: Caching Patterns Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Caching Patterns: Performance, Consistency & Expiration

Dieses Sheet bündelt die wichtigsten Caching‑Konzepte für skalierende Systeme — ideal für APIs, Microservices, Datenbanken und High‑Traffic‑Plattformen.

---

## ❓ Warum Caching?
**Lösung:** Geschwindigkeit + Entlastung.

Caching reduziert:

- Latenz  
- Datenbank‑Load  
- Kosten  
- Time‑to‑First‑Byte  

Caching erhöht:

- Durchsatz  
- Stabilität  
- Nutzererlebnis  

---

## ❓ Welche Cache‑Typen gibt es?
**Lösung:** drei Ebenen.

- **Client‑Cache** (Browser, App)  
- **Edge‑Cache** (CDN)  
- **Server‑Cache** (Redis, Memcached)  

---

## ❓ Welche Caching‑Strategien gibt es?
**Lösung:** die wichtigsten Patterns.

### Cache Aside (Lazy Loading)
- Anwendung liest zuerst Cache  
- Wenn leer → DB lesen → Cache füllen  
- Standardpattern

```text
if cache miss → load from DB → write to cache
```

### Write Through
- Schreiben geht zuerst in den Cache  
- Cache schreibt synchron in DB  
- Konsistent, aber langsamer

### Write Back (Write Behind)
- Schreiben geht nur in Cache  
- Cache schreibt später in DB  
- Schnell, aber riskanter

### Read Through
- Cache ist Proxy zur DB  
- Cache lädt Daten selbst  
- Komplexer, aber sauber

---

## ❓ Wie setze ich TTLs?
**Lösung:** Ablaufzeiten definieren.

Beispiele:

- User Profile → 5 Minuten  
- Produktkatalog → 1 Stunde  
- Feature Flags → 30 Sekunden  
- Session Tokens → 24 Stunden  

TTL ist ein **Trade‑off zwischen Frische und Last**.

---

## ❓ Wie verhindere ich Cache Stampedes?
**Lösung:** Schutzmechanismen.

- **Mutex Locking** → nur ein Prozess lädt neu  
- **Request Coalescing** → gleiche Anfragen bündeln  
- **Stale‑While‑Revalidate** → abgelaufene Daten kurz weiter servieren  
- **Randomized TTLs** → Vermeidung synchroner Abläufe  

---

## ❓ Wie verhindere ich Cache Pollution?
**Lösung:** nur sinnvolle Daten cachen.

- keine seltenen Queries  
- keine riesigen Objekte  
- keine personalisierten Daten ohne Not  

---

## ❓ Wie mache ich Cache Invalidation?
**Lösung:** der schwierigste Teil.

Strategien:

- TTL (einfach, aber ungenau)  
- explizites Löschen (präzise, aber komplex)  
- Versionierung (sauber, aber aufwendig)  

Beispiel:

```text
product:42:v3
```

Neue Version → neuer Key.

---

## ❓ Wie strukturiere ich Cache Keys?
**Lösung:** deterministisch + eindeutig.

Beispiele:

```
user:42
product:42:v3
orders:user:42:page:1
```

Regeln:

- keine freien Strings  
- keine Sonderzeichen  
- immer Namespaces  

---

## ❓ Wie mache ich Distributed Caching?
**Lösung:** Redis Cluster oder Memcached Cluster.

Vorteile:

- horizontale Skalierung  
- Sharding  
- Replikation  
- Failover  

---

## ❓ Wie messe ich Cache‑Effizienz?
**Lösung:** Cache Hit Ratio.

Formel:

```
hits / (hits + misses)
```

Zielwerte:

- API‑Caches → > 90%  
- DB‑Caches → > 80%  
- CDN → > 95%  

---

## ❓ Wie integriere ich Caching in Microservices?
**Lösung:** pro Service eigener Cache‑Namespace.

Beispiel:

```
inventory:product:42
pricing:product:42
```

Kein globaler Cache für alle Services.

---

## Pro-Tipp
Caching ist **ein Performance‑Werkzeug, kein Wahrheits‑Speicher** — je klarer die Verantwortlichkeiten, desto stabiler das System.
