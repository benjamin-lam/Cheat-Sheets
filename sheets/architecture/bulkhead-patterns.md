---
title: Bulkhead Patterns Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Bulkhead Patterns: Isolation, Containment & Failure Boundaries

Dieses Sheet bündelt die wichtigsten Bulkhead‑Mechaniken für resiliente Systeme — ideal für Microservices, APIs, Worker‑Pools und verteilte Architekturen.

---

## ❓ Warum Bulkheads?
**Lösung:** Fehler isolieren, bevor sie das gesamte System zerstören.

Bulkheads verhindern:

- Thread‑Erschöpfung  
- Connection‑Erschöpfung  
- Domino‑Ausfälle  
- Latenz‑Kaskaden  
- globale Systemblockaden  

Bulkheads sind **Brandabschnitte** für Software.

---

## ❓ Welche Bulkhead‑Typen gibt es?
**Lösung:** zwei Hauptformen.

### 1. Thread‑Pool Isolation
Jede Abhängigkeit bekommt einen eigenen Pool.

Beispiel:

- DB‑Pool  
- Cache‑Pool  
- Payment‑Pool  
- External‑API‑Pool  

Vorteil:
- ein langsamer Service blockiert nicht alle Threads  

---

### 2. Connection‑Pool Isolation
Jede Ressource hat eigene Verbindungen.

Beispiel:

- PostgreSQL Pool  
- Redis Pool  
- Kafka Producer Pool  

Vorteil:
- kein „Connection Starvation“  

---

## ❓ Wie sieht ein Bulkhead‑Diagramm aus?

```text
Service
 ├── DB Pool (max 20)
 ├── Redis Pool (max 10)
 ├── External API Pool (max 5)
 └── Worker Pool (max 8)
```

Jede Abhängigkeit ist isoliert.

---

## ❓ Wie dimensioniere ich Bulkheads?
**Lösung:** nach Last + Latenz.

Regeln:

- kleine Pools für langsame Abhängigkeiten  
- größere Pools für schnelle Abhängigkeiten  
- niemals „unbounded“ Pools  
- Timeouts pro Pool setzen  

---

## ❓ Wie interagieren Bulkheads mit Circuit Breakern?
**Lösung:** perfekte Kombination.

Bulkheads:
- verhindern Ressourcenerschöpfung  

Circuit Breaker:
- verhindern Kaskadenfehler  

Zusammen:
- maximale Isolation  
- kontrollierte Wiederherstellung  

---

## ❓ Wie interagieren Bulkheads mit Retries?
**Lösung:** vorsichtig.

Regeln:

- Retries dürfen Pools nicht überfluten  
- Retry‑Budget pro Pool  
- Backoff + Jitter Pflicht  

---

## ❓ Wie interagieren Bulkheads mit Timeouts?
**Lösung:** Timeouts sind Pflicht.

Timeouts verhindern:

- hängende Threads  
- blockierte Pools  
- Latenz‑Explosionen  

Regel:
- Timeout < Retry‑Budget < Circuit‑Breaker‑Threshold  

---

## ❓ Wie mache ich Bulkheads in Microservices?
**Lösung:** Isolation auf mehreren Ebenen.

- pro Service eigener DB‑Pool  
- pro Service eigener Cache‑Pool  
- pro Service eigener Worker‑Pool  
- pro Service eigene Rate Limits  

Kein globaler Pool für alle Services.

---

## ❓ Wie mache ich Bulkheads in Worker‑Systemen?
**Lösung:** Queue‑basierte Isolation.

Beispiel:

- queue‑email → worker‑email  
- queue‑billing → worker‑billing  
- queue‑analytics → worker‑analytics  

Vorteil:
- ein langsamer Jobtyp blockiert nicht alle anderen  

---

## ❓ Wie mache ich Observability für Bulkheads?
**Lösung:** Metriken + Logs.

Wichtige Metriken:

- Pool Size  
- Pool Utilization  
- Queue Length  
- Rejected Tasks  
- Timeout Rate  
- Latency  

---

## ❓ Wie erkenne ich Bulkhead‑Probleme?
**Lösung:** typische Symptome.

- steigende Latenz  
- steigende Timeout‑Rate  
- „Pool exhausted“ Fehler  
- Worker‑Stau  
- ungleichmäßige Lastverteilung  

---

## Pro-Tipp
Bulkheads sind **Ressourcen‑Sicherungen**: Sie verhindern nicht Fehler — sie verhindern, dass Fehler alle Ressourcen auffressen.
