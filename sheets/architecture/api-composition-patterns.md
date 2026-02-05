---
title: API Composition Patterns Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# API Composition Patterns: Aggregation, Orchestration & Federation

Dieses Sheet bündelt die wichtigsten Patterns zur Zusammensetzung von APIs — ideal für Microservices, modulare Monolithen und komplexe Plattformen.

---

## ❓ Warum API Composition?
**Lösung:** mehrere Services → ein konsistentes API‑Erlebnis.

API‑Composition löst:

- zu viele Roundtrips  
- inkonsistente Daten  
- komplexe Client‑Logik  
- Performance‑Probleme  
- fehlende Aggregation  

---

## ❓ Welche Composition‑Patterns gibt es?
**Lösung:** drei Grundformen.

### 1. API Aggregation
Ein Endpoint ruft mehrere Services auf und kombiniert die Ergebnisse.

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
- Aggregator wird komplex  

---

### 2. API Orchestration
Ein zentraler Orchestrator steuert mehrere Schritte.

Beispiel:

```
POST /checkout
→ payment-service
→ inventory-service
→ shipping-service
```

Vorteile:
- klare Prozesslogik  
- Fehlerbehandlung zentral  

Nachteile:
- Orchestrator kann zum Bottleneck werden  

---

### 3. API Federation
Mehrere Services werden unter einer einheitlichen API zusammengeführt.

Beispiele:
- GraphQL Federation  
- BFF (Backend for Frontend)  
- API Gateway Plugins  

Vorteile:
- einheitliches Schema  
- flexible Queries  

Nachteile:
- komplexe Infrastruktur  

---

## ❓ Was ist ein Backend for Frontend (BFF)?
**Lösung:** API‑Schicht pro Client‑Typ.

Beispiele:

- bff‑web  
- bff‑mobile  
- bff‑admin  

Vorteile:
- maßgeschneiderte APIs  
- weniger Logik im Client  
- bessere Performance  

---

## ❓ Was ist GraphQL Federation?
**Lösung:** mehrere GraphQL‑Schemas → ein gemeinsames Schema.

Vorteile:
- flexible Queries  
- keine Overfetching/Underfetching  
- klare Ownership pro Feld  

Nachteile:
- komplexe Resolver  
- schwieriger zu debuggen  

---

## ❓ Wie mache ich Composition in Microservices?
**Lösung:** klare Verantwortlichkeiten.

Regeln:

- Services liefern **Rohdaten**  
- BFF/Gateway aggregiert  
- keine Cross‑Service‑Joins  
- keine „Mega‑Services“  

---

## ❓ Wie mache ich Fehlerbehandlung?
**Lösung:** defensive Patterns.

Strategien:

- Partial Responses  
- Fallbacks  
- Timeouts  
- Retries  
- Circuit Breaker  

Beispiel Partial Response:

```json
{
  "user": {...},
  "orders": null,
  "errors": ["orders-service timeout"]
}
```

---

## ❓ Wie mache ich Performance‑Optimierung?
**Lösung:** mehrere Hebel.

- Caching (per Service oder global)  
- Parallelisierung von Calls  
- Batching  
- Pagination  
- CDN für statische Daten  

---

## ❓ Wie mache ich Observability?
**Lösung:** Tracing + Logging + Metrics.

Wichtig:

- Trace‑ID durch alle Services  
- Aggregator erzeugt Root‑Span  
- Fehler pro Service sichtbar  

---

## ❓ Wie mache ich Versionierung?
**Lösung:** Composition‑Schicht versionieren.

Beispiele:

```
/v1/profile
/v2/profile
```

Regel:
- Services können stabil bleiben  
- Composition‑Layer entwickelt sich weiter  

---

## Pro-Tipp
API‑Composition ist **Schnittstellen‑Architektur**: Services bleiben klein und fokussiert — die Composition‑Schicht sorgt für ein konsistentes, performantes und nutzerfreundliches API‑Erlebnis.
