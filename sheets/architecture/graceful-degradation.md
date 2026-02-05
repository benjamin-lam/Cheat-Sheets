---
title: Graceful Degradation Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Graceful Degradation: Wenn Systeme unter Last kontrolliert „schlechter“ werden

Dieses Sheet bündelt die wichtigsten Mechaniken für kontrolliertes Degradieren — ideal für Microservices, APIs, Frontends und hochskalierende Plattformen.

---

## ❓ Warum Graceful Degradation?
**Lösung:** Systeme sollen unter Last oder bei Fehlern **weiter funktionieren**, nur mit reduzierter Qualität.

Graceful Degradation verhindert:

- Totalausfälle  
- Latenz‑Explosionen  
- UI‑Freeze  
- Datenverlust  
- schlechte Nutzererfahrung  

Es ist das **Notfall‑UX‑Pattern** für resiliente Systeme.

---

## ❓ Was ist Graceful Degradation?
**Lösung:** kontrolliertes Abschalten oder Vereinfachen von Funktionen, wenn das System unter Stress steht.

Beispiele:

- weniger Daten anzeigen  
- Features temporär deaktivieren  
- Fallback‑Daten nutzen  
- statische Inhalte statt dynamischer  

---

## ❓ Welche Degradations‑Strategien gibt es?
**Lösung:** vier Hauptformen.

### 1. Feature Degradation
Nicht‑kritische Features abschalten.

Beispiele:
- Empfehlungen ausblenden  
- Live‑Daten durch statische ersetzen  
- Animationen deaktivieren  

### 2. Data Degradation
Weniger oder ältere Daten anzeigen.

Beispiele:
- Pagination verkleinern  
- Cache‑Daten statt Live‑Daten  
- „Zuletzt bekannte Werte“  

### 3. UX Degradation
UI bleibt nutzbar, aber einfacher.

Beispiele:
- Skeleton Screens  
- vereinfachte Listen  
- weniger Interaktionen  

### 4. Service Degradation
Services liefern reduzierte Antworten.

Beispiele:
- nur Kernfelder zurückgeben  
- keine Aggregationen  
- keine teuren Queries  

---

## ❓ Wie erkenne ich, wann ich degradieren muss?
**Lösung:** Metriken + Schwellenwerte.

Typische Trigger:

- Latenz steigt (P95/P99)  
- CPU > 80–90%  
- Cache Hit Ratio fällt  
- Queue‑Länge steigt  
- Circuit Breaker öffnet  
- Load Shedding aktiv  

---

## ❓ Wie mache ich Graceful Degradation im Backend?
**Lösung:** Fallbacks + vereinfachte Antworten.

Beispiele:

- Fallback auf Cache  
- Fallback auf statische Daten  
- Fallback auf „minimal response“  

Minimal Response Beispiel:

```json
{
  "id": 42,
  "name": "Ben",
  "status": "unknown"
}
```

---

## ❓ Wie mache ich Graceful Degradation im Frontend?
**Lösung:** UI bleibt nutzbar, auch wenn Daten fehlen.

Beispiele:

- Skeleton Loader  
- „Zuletzt bekannte Daten“  
- „Dieses Feature ist gerade nicht verfügbar“  
- statische Inhalte statt dynamischer  

---

## ❓ Wie mache ich Graceful Degradation im API Gateway?
**Lösung:** Gateway als Schutzschicht.

Mechanismen:

- Fallback‑Responses  
- Cached Responses  
- Stale‑While‑Revalidate  
- Canary‑Rollback  

---

## ❓ Wie interagiert Graceful Degradation mit Load Shedding?
**Lösung:** perfekte Kombination.

Load Shedding:
- schützt das System  

Graceful Degradation:
- schützt die Nutzererfahrung  

Zusammen:
- stabil + nutzbar  

---

## ❓ Wie interagiert Graceful Degradation mit Circuit Breakern?
**Lösung:** Fallbacks statt Fehler.

Wenn Circuit Breaker offen:

- Fallback‑Daten  
- statische Inhalte  
- reduzierte Antworten  

---

## ❓ Wie mache ich Observability für Degradation?
**Lösung:** Metriken + Logs.

Wichtige Metriken:

- Degradation Events  
- Fallback Rate  
- Cache Hit Ratio  
- Latency  
- Error Rate  
- User Impact Score  

---

## ❓ Wie erkenne ich Degradations‑Probleme?
**Lösung:** typische Symptome.

- Nutzer sehen veraltete Daten  
- Features fehlen zu oft  
- Fallback‑Rate steigt  
- Latenz bleibt hoch trotz Degradation  
- Circuit Breaker öffnet weiterhin  

---

## Pro-Tipp
Graceful Degradation ist **kontrolliertes Weiterlaufen**: Systeme bleiben nutzbar, selbst wenn Teile ausfallen — und genau das unterscheidet robuste Plattformen von fragilen.
