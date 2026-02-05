---
title: API Gateway Patterns Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# API Gateway Patterns: Routing, Aggregation & Cross-Cutting Concerns

Dieses Sheet bündelt die wichtigsten API‑Gateway‑Konzepte für Microservices, Plattformen und verteilte Architekturen — ideal für Skalierung, Sicherheit und Vereinheitlichung.

---

## ❓ Warum ein API Gateway?
**Lösung:** zentrale Steuerung + Entkopplung.

Ein Gateway übernimmt:

- Routing  
- Authentifizierung  
- Rate Limiting  
- Caching  
- Logging & Tracing  
- Aggregation  
- Versionierung  
- Canary Releases  

Es schützt Services vor direktem Zugriff.

---

## ❓ Welche Gateway‑Typen gibt es?
**Lösung:** drei Kategorien.

### 1. Reverse Proxy (klassisch)
- NGINX  
- HAProxy  
- Envoy  

### 2. API Gateway (vollwertig)
- Kong  
- KrakenD  
- Tyk  
- Apigee  

### 3. Service Mesh Ingress
- Istio  
- Linkerd  
- Consul  

---

## ❓ Welche Routing‑Patterns gibt es?
**Lösung:** mehrere Strategien.

### Path‑Based Routing
```
/api/users → user-service
/api/orders → order-service
```

### Host‑Based Routing
```
users.example.com → user-service
orders.example.com → order-service
```

### Header‑Based Routing
```
X-Client: mobile → mobile-service
```

### Weighted Routing (Canary)
```
90% → v1
10% → v2
```

---

## ❓ Wie funktioniert Aggregation?
**Lösung:** Gateway ruft mehrere Services auf und kombiniert die Ergebnisse.

Beispiel:

```
GET /profile
→ user-service
→ orders-service
→ notifications-service
```

Vorteile:

- weniger Roundtrips  
- bessere Performance  

Nachteile:

- Gateway wird komplexer  

---

## ❓ Wie funktioniert Authentifizierung im Gateway?
**Lösung:** zentrale Kontrolle.

Typisch:

- JWT Validierung  
- OAuth2 / OpenID Connect  
- API Keys  
- mTLS  

Regel:

- Auth im Gateway  
- AuthZ im Service  

---

## ❓ Wie funktioniert Rate Limiting?
**Lösung:** Schutz vor Überlastung.

Strategien:

- Token Bucket  
- Leaky Bucket  
- Fixed Window  
- Sliding Window  

Beispiel‑Header:

```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 42
```

---

## ❓ Wie funktioniert Caching im Gateway?
**Lösung:** Response‑Caching.

Beispiele:

- GET /products → 60 Sekunden  
- GET /config → 5 Sekunden  

Regeln:

- nur idempotente Requests cachen  
- Cache‑Invalidation über TTL  

---

## ❓ Wie funktioniert Versionierung?
**Lösung:** mehrere Wege.

### URL‑Versionierung
```
/v1/users
/v2/users
```

### Header‑Versionierung
```
Accept: application/vnd.app.v2+json
```

### Routing‑Versionierung
- v1 → alter Service  
- v2 → neuer Service  

---

## ❓ Wie funktioniert Observability im Gateway?
**Lösung:** zentrale Telemetrie.

Jedes Gateway liefert:

- strukturierte Logs  
- Metriken (RPS, Errors, Latency)  
- Traces (Trace‑ID weiterreichen)  

Wichtig:

- Gateway ist der **Einstiegspunkt** für Traces  

---

## ❓ Wie funktioniert ein Service Mesh im Vergleich?
**Lösung:** Mesh = feingranulare Kontrolle.

Gateway:

- Edge‑Routing  
- Auth  
- Rate Limiting  

Mesh:

- mTLS zwischen Services  
- Retries  
- Circuit Breaker  
- Traffic Shaping  
- Observability  

Gateway + Mesh = vollständige Plattform.

---

## ❓ Wie mache ich Canary Releases?
**Lösung:** Traffic‑Splitting.

Beispiel:

```
80% → v1
20% → v2
```

Kriterien:

- Header  
- Cookies  
- User‑ID  
- Random Weight  

---

## ❓ Wie mache ich Zero‑Downtime Deployments?
**Lösung:** Blue‑Green oder Rolling.

Gateway entscheidet:

- welche Version aktiv ist  
- wann umgeschaltet wird  

---

## Pro-Tipp
Ein API Gateway ist **die Frontline deiner Plattform** — je klarer Routing, Auth und Observability definiert sind, desto stabiler und kontrollierbarer wird das Gesamtsystem.
