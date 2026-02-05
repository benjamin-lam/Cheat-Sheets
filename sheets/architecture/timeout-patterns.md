---
title: Timeout Patterns Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Timeout Patterns: Latency Control, Failure Boundaries & Stability

Dieses Sheet bündelt die wichtigsten Timeout‑Mechaniken für resiliente Systeme — ideal für Microservices, APIs, Messaging und verteilte Architekturen.

---

## ❓ Warum Timeouts?
**Lösung:** um zu verhindern, dass ein langsamer Service das gesamte System blockiert.

Timeouts schützen vor:

- hängenden Requests  
- Latenz‑Kaskaden  
- Thread‑Erschöpfung  
- Connection‑Starvation  
- globalen Ausfällen  

Timeouts sind **Pflicht**, nicht optional.

---

## ❓ Welche Timeout‑Arten gibt es?
**Lösung:** drei Ebenen.

### 1. Client‑Timeout
- wie lange der Client auf eine Antwort wartet  
- verhindert hängende Requests  

### 2. Server‑Timeout
- maximale Bearbeitungszeit im Service  
- schützt Worker‑Threads  

### 3. Network‑Timeout
- Verbindungsaufbau + Lese‑Timeout  
- schützt vor Netzwerkproblemen  

---

## ❓ Wie wähle ich die richtige Timeout‑Dauer?
**Lösung:** abhängig von Latenz + SLA.

Regeln:

- Timeout = 95. oder 99. Perzentil der Latenz  
- niemals „unendlich“  
- niemals „zu großzügig“  
- pro Abhängigkeit unterschiedlich  

Beispiel:

- Redis: 5–20 ms  
- interne APIs: 100–300 ms  
- externe APIs: 500–2000 ms  

---

## ❓ Wie interagieren Timeouts mit Retries?
**Lösung:** Timeout < Retry‑Budget < Circuit‑Breaker‑Threshold.

Beispiel:

- Timeout: 200 ms  
- Retry‑Budget: 600 ms  
- Circuit‑Breaker‑Threshold: 1 s  

Regel:
- **Timeouts begrenzen Retries**  
- **Retries dürfen Timeouts nicht überfluten**  

---

## ❓ Wie interagieren Timeouts mit Circuit Breakern?
**Lösung:** Timeouts sind der wichtigste Trigger.

Timeouts erzeugen:

- Fehler  
- erhöhte Latenz  
- Circuit‑Breaker‑Öffnungen  

Regel:
- Circuit Breaker ohne Timeouts ist wertlos  

---

## ❓ Wie interagieren Timeouts mit Bulkheads?
**Lösung:** Timeouts verhindern Pool‑Blockaden.

Ohne Timeouts:

- Threads hängen  
- Pools laufen voll  
- Bulkheads verlieren Wirkung  

Mit Timeouts:

- Threads werden freigegeben  
- Pools bleiben stabil  

---

## ❓ Wie mache ich Timeouts in Microservices?
**Lösung:** pro Abhängigkeit eigene Timeouts.

Beispiel:

- DB: 50 ms  
- Cache: 10 ms  
- Payment API: 800 ms  
- Notification API: 300 ms  

Keine globalen Timeouts.

---

## ❓ Wie mache ich Timeouts in Messaging?
**Lösung:** Verarbeitung begrenzen.

Mechanismen:

- Visibility Timeout (SQS)  
- Consumer Timeout  
- Processing Deadline  

Regel:
- lange Jobs → Worker‑System  
- kurze Jobs → Queue  

---

## ❓ Wie mache ich Timeouts in HTTP‑APIs?
**Lösung:** mehrere Ebenen.

- Client Timeout  
- Server Timeout  
- Reverse Proxy Timeout  
- Gateway Timeout  

Alle müssen zusammenpassen.

---

## ❓ Wie mache ich Observability für Timeouts?
**Lösung:** Metriken + Logs + Traces.

Wichtige Metriken:

- Timeout Rate  
- Latency (P95/P99)  
- Error Rate  
- Retries  
- Circuit‑Breaker‑Open Events  

Traces zeigen:

- wo die Latenz entsteht  
- welche Abhängigkeit schuld ist  

---

## ❓ Wie erkenne ich Timeout‑Probleme?
**Lösung:** typische Symptome.

- steigende Latenz  
- steigende Retry‑Rate  
- Circuit Breaker öffnet häufig  
- Worker‑Stau  
- Pool‑Erschöpfung  

---

## Pro-Tipp
Timeouts sind **Latenz‑Sicherungen**: Sie verhindern nicht Fehler — sie verhindern, dass Fehler das System verlangsamen oder blockieren.
