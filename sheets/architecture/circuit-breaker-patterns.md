---
title: Circuit Breaker Patterns Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Circuit Breaker Patterns: Failure Isolation, Recovery & Stability

Dieses Sheet bündelt die wichtigsten Circuit‑Breaker‑Mechaniken für resiliente Systeme — ideal für Microservices, APIs, Messaging und verteilte Architekturen.

---

## ❓ Warum Circuit Breaker?
**Lösung:** Systeme vor Kaskadenfehlern schützen.

Ein Circuit Breaker verhindert:

- endlose Retries  
- Überlastung eines kaputten Services  
- Domino‑Ausfälle  
- Latenz‑Explosionen  
- Totalausfälle  

Er ist ein **Sicherungsautomat** für Software.

---

## ❓ Welche Zustände hat ein Circuit Breaker?
**Lösung:** drei Phasen.

### 1. Closed
- alles normal  
- Requests gehen durch  
- Fehler werden gezählt  

### 2. Open
- zu viele Fehler → Circuit öffnet  
- keine Requests mehr zum Zielservice  
- sofortige Fehlerantwort  

### 3. Half‑Open
- Testphase  
- wenige Requests werden durchgelassen  
- bei Erfolg → Closed  
- bei Fehler → wieder Open  

---

## ❓ Wann öffnet ein Circuit Breaker?
**Lösung:** wenn Fehlerquote oder Latenz zu hoch ist.

Typische Trigger:

- X Fehler in Y Sekunden  
- Fehlerquote > 50%  
- Latenz > Threshold  
- Timeouts häufen sich  

---

## ❓ Welche Fehler zählen?
**Lösung:** nur echte Service‑Fehler.

Gute Kandidaten:

- Timeouts  
- 500 Internal Server Error  
- 502 Bad Gateway  
- 503 Service Unavailable  
- 504 Gateway Timeout  

Nicht zählen:

- 400 Bad Request  
- 401 Unauthorized  
- 403 Forbidden  
- 404 Not Found  

---

## ❓ Wie lange bleibt ein Circuit offen?
**Lösung:** konfigurierbare Cooldown‑Zeit.

Typisch:

- 30 Sekunden  
- 1 Minute  
- 5 Minuten  

Danach → Half‑Open.

---

## ❓ Wie funktioniert Half‑Open?
**Lösung:** vorsichtige Wiederannäherung.

Mechanismus:

- nur wenige Requests durchlassen  
- Erfolg → Circuit schließt  
- Fehler → Circuit bleibt offen  

---

## ❓ Wie kombiniere ich Circuit Breaker + Retries?
**Lösung:** sehr vorsichtig.

Regeln:

- Retries **vor** dem Circuit Breaker begrenzen  
- Circuit Breaker **nach** Retries platzieren  
- niemals unkontrollierte Retries  

---

## ❓ Wie kombiniere ich Circuit Breaker + Timeouts?
**Lösung:** Timeouts sind Pflicht.

Timeouts verhindern:

- hängende Requests  
- Latenz‑Kaskaden  
- unnötige Blockaden  

Regel:

- Timeout < Retry‑Budget < Circuit‑Breaker‑Threshold  

---

## ❓ Wie kombiniere ich Circuit Breaker + Bulkheads?
**Lösung:** Isolation auf mehreren Ebenen.

Bulkheads:

- isolieren Ressourcen  
- verhindern, dass ein Service alle Threads blockiert  

Circuit Breaker:

- isoliert Fehlerquellen  

Zusammen → maximale Resilienz.

---

## ❓ Wie mache ich Observability für Circuit Breaker?
**Lösung:** Metriken + Logs + Traces.

Wichtige Metriken:

- Open Count  
- Half‑Open Count  
- Error Rate  
- Timeout Rate  
- Latency  
- Rejected Requests  

Wichtig:

- Circuit‑Breaker‑Events loggen  
- State‑Changes sichtbar machen  

---

## ❓ Wie implementiere ich Circuit Breaker?
**Lösung:** Libraries oder Infrastruktur.

Beispiele:

- Resilience4j (Java)  
- Hystrix (Legacy)  
- Envoy  
- Istio  
- Spring Cloud  

---

## Pro-Tipp
Circuit Breaker sind **Fehler‑Sicherungen**: Sie verhindern nicht Fehler — sie verhindern, dass Fehler das gesamte System zerstören.
