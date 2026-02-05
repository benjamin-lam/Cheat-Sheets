---
title: Load Shedding Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Load Shedding: Überlast vermeiden, Kernfunktionen schützen & Systemkollaps verhindern

Dieses Sheet bündelt die wichtigsten Load‑Shedding‑Mechaniken für resiliente Systeme — ideal für APIs, Microservices, Gateways und hochskalierende Plattformen.

---

## ❓ Warum Load Shedding?
**Lösung:** Systeme schützen sich aktiv vor Überlast.

Load Shedding verhindert:

- Latenz‑Explosionen  
- Thread‑Erschöpfung  
- Queue‑Überlauf  
- Domino‑Ausfälle  
- Totalausfälle  

Es ist das **Notfallventil** eines Systems.

---

## ❓ Was ist Load Shedding?
**Lösung:** bewusstes Ablehnen von Requests, um das Gesamtsystem stabil zu halten.

Mechanismus:

- System erkennt Überlast  
- System lehnt neue Requests ab  
- System schützt Kernfunktionen  

---

## ❓ Welche Load‑Shedding‑Strategien gibt es?
**Lösung:** vier Hauptformen.

### 1. Hard Shedding
- sofortige Ablehnung  
- 503 Service Unavailable  
- schützt das System maximal  

### 2. Soft Shedding
- weniger wichtige Requests ablehnen  
- Priorisierung nach User, Endpoint oder Traffic‑Typ  

Beispiel:
- Premium‑User → durchlassen  
- Free‑User → ablehnen  

### 3. Queue‑Shedding
- Queue‑Länge begrenzen  
- neue Jobs ablehnen, wenn Queue voll ist  

### 4. Adaptive Shedding
- dynamisch basierend auf Latenz, CPU, Fehlerquote  

---

## ❓ Welche Signale lösen Load Shedding aus?
**Lösung:** Metriken + Schwellenwerte.

Typische Trigger:

- CPU > 80–90%  
- RAM > 80%  
- Latenz P99 steigt  
- Queue‑Länge > Threshold  
- Thread‑Pool fast voll  
- Connection‑Pool fast voll  
- Circuit Breaker öffnet häufig  

---

## ❓ Wie priorisiere ich Requests?
**Lösung:** nach Wichtigkeit.

Beispiele:

- Health Checks → höchste Priorität  
- Payment → hoch  
- Notifications → mittel  
- Analytics → niedrig  

Regel:
- unwichtige Funktionen zuerst abwerfen  

---

## ❓ Wie mache ich Load Shedding im API Gateway?
**Lösung:** Gateway ist der beste Ort.

Mechanismen:

- Rate Limiting  
- Concurrency Limits  
- Adaptive Shedding  
- Priority Routing  

Vorteil:
- Überlast wird abgefangen, bevor sie Services erreicht  

---

## ❓ Wie mache ich Load Shedding im Service?
**Lösung:** interne Schutzmechanismen.

Strategien:

- Worker‑Pool begrenzen  
- Queue‑Länge begrenzen  
- Timeouts  
- Circuit Breaker  
- Priorisierte Verarbeitung  

---

## ❓ Wie mache ich Load Shedding in Messaging?
**Lösung:** Queue‑basierte Kontrolle.

Mechanismen:

- Queue‑Länge begrenzen  
- Consumer pausieren  
- Backpressure  
- DLQ für Überlauf  

---

## ❓ Wie interagiert Load Shedding mit Retries?
**Lösung:** vorsichtig.

Regeln:

- Retries dürfen Load Shedding nicht verstärken  
- Retry‑Budget begrenzen  
- Backoff + Jitter Pflicht  

---

## ❓ Wie interagiert Load Shedding mit Circuit Breakern?
**Lösung:** perfekte Kombination.

Circuit Breaker:
- isoliert kaputte Services  

Load Shedding:
- schützt vor Überlast  

Zusammen:
- maximale Stabilität  

---

## ❓ Wie mache ich Observability für Load Shedding?
**Lösung:** Metriken + Logs.

Wichtige Metriken:

- Rejected Requests  
- Queue Length  
- CPU / RAM  
- Latency (P95/P99)  
- Error Rate  
- Retry Rate  

---

## ❓ Wie erkenne ich Load‑Shedding‑Probleme?
**Lösung:** typische Symptome.

- viele 503‑Antworten  
- steigende Latenz  
- steigende Retry‑Rate  
- Circuit Breaker öffnet häufig  
- Worker‑Stau  
- Pool‑Erschöpfung  

---

## Pro-Tipp
Load Shedding ist **kontrolliertes Verlieren**, um das System zu retten — lieber einige Requests verlieren als das gesamte System.
