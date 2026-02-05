---
title: Load Balancing Patterns Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Load Balancing Patterns: Routing, Algorithms & High Availability

Dieses Sheet bündelt die wichtigsten Load‑Balancing‑Konzepte für skalierende Systeme — ideal für APIs, Microservices, Datenbanken und globale Plattformen.

---

## ❓ Warum Load Balancing?
**Lösung:** gleichmäßige Lastverteilung + Ausfallsicherheit.

Load Balancing sorgt für:

- horizontale Skalierung  
- weniger Latenz  
- höhere Verfügbarkeit  
- Schutz vor Überlastung  
- Zero‑Downtime‑Deployments  

---

## ❓ Welche Load‑Balancer‑Typen gibt es?
**Lösung:** drei Ebenen.

### L4 Load Balancer (Transport Layer)
- TCP/UDP  
- schnell, simpel  
- keine HTTP‑Intelligenz  
- Beispiele: HAProxy, AWS NLB  

### L7 Load Balancer (Application Layer)
- HTTP/HTTPS  
- Routing nach Pfad, Header, Cookies  
- Caching, Auth, Rate Limiting  
- Beispiele: NGINX, Envoy, AWS ALB  

### Global Load Balancer (GSLB)
- DNS‑basiert  
- Multi‑Region Routing  
- Geo‑Routing  
- Beispiele: Cloudflare, Akamai, Route53  

---

## ❓ Welche Routing‑Algorithmen gibt es?
**Lösung:** die wichtigsten Strategien.

### Round Robin
- gleichmäßige Verteilung  
- Standard  

### Least Connections
- ideal bei langen Requests  

### IP Hash
- sticky routing  
- gut für Sessions  

### Weighted Routing
- Traffic‑Splitting  
- ideal für Canary Releases  

### Random
- einfach, überraschend effektiv  

---

## ❓ Was ist Sticky Sessions?
**Lösung:** ein Client bleibt an eine Instanz gebunden.

Mechanismen:

- Cookies  
- IP Hash  
- Session Affinity  

Regel:

- vermeiden, wenn möglich  
- stateless Services bevorzugen  

---

## ❓ Wie mache ich Health Checks?
**Lösung:** aktive Überwachung.

Typen:

- TCP Check  
- HTTP Check  
- gRPC Health Check  

Beispiel:

```
/health
/ready
/live
```

Regel:

- Liveness → Neustart  
- Readiness → Traffic stoppen  

---

## ❓ Wie mache ich Zero‑Downtime Deployments?
**Lösung:** Rolling oder Blue‑Green.

### Rolling Deployment
- Instanzen nacheinander ersetzen  
- kein Downtime  

### Blue‑Green Deployment
- zwei Umgebungen  
- Umschalten per Load Balancer  

---

## ❓ Wie mache ich Canary Releases?
**Lösung:** Traffic‑Splitting.

Beispiel:

```
95% → v1
5% → v2
```

Kriterien:

- Header  
- Cookies  
- User‑ID  
- Random Weight  

---

## ❓ Wie mache ich Failover?
**Lösung:** automatische Umschaltung.

Strategien:

- Health Checks  
- Multi‑AZ  
- Multi‑Region  
- DNS‑Failover  

---

## ❓ Wie mache ich Load Shedding?
**Lösung:** Überlast vermeiden.

Mechanismen:

- 503 zurückgeben  
- Queue‑Länge begrenzen  
- Timeouts  
- Circuit Breaker  

Ziel:

- System schützt sich selbst  

---

## ❓ Wie mache ich Observability im Load Balancer?
**Lösung:** Logs + Metrics + Traces.

Wichtige Metriken:

- RPS  
- Error Rate  
- Latency (P95/P99)  
- Active Connections  
- Dropped Requests  

---

## ❓ Wie mache ich globales Routing?
**Lösung:** GSLB + Geo‑Routing.

Strategien:

- Latency‑Based Routing  
- Geo‑Proximity  
- Weighted DNS  
- Region Failover  

Trade‑off:

- Latenz vs. Konsistenz  

---

## Pro-Tipp
Load Balancing ist **Traffic‑Management**: Je klarer Routing, Health Checks und Failover definiert sind, desto stabiler und skalierbarer wird das Gesamtsystem.
