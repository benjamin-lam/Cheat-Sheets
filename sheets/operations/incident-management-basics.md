---
title: Incident Management Basics Cheat Sheet
category: Operations
last_updated: 2025-09-02
status: stable
---

# Incident Management: Detection, Response, Coordination & Recovery

Dieses Sheet bündelt die wichtigsten Grundlagen für professionelles Incident‑Management — ideal für Plattformen, Microservices, DevOps‑Teams und 24/7‑Betrieb.

---

## ❓ Was ist ein Incident?
**Lösung:** ein ungeplanter Zustand, der den normalen Betrieb beeinträchtigt.

Ein Incident ist:

- ein Ausfall  
- eine starke Degradation  
- ein Sicherheitsproblem  
- ein Datenproblem  
- ein kritischer Fehler  

Ein Incident ist **kein Bug** — er ist ein **Betriebsereignis**.

---

## ❓ Welche Incident‑Schweregrade gibt es?
**Lösung:** klare Klassifizierung.

Typisch:

| Severity | Bedeutung |
|---------|-----------|
| SEV‑1   | kompletter Ausfall, kritische Funktionen betroffen |
| SEV‑2   | starke Degradation, wichtige Funktionen betroffen |
| SEV‑3   | moderate Probleme, Workarounds möglich |
| SEV‑4   | geringfügige Störungen |

Regel:
- je klarer die Definition, desto schneller die Reaktion.

---

## ❓ Was sind die Phasen eines Incidents?
**Lösung:** fünf Schritte.

1. **Detection**  
2. **Triage**  
3. **Mitigation**  
4. **Resolution**  
5. **Postmortem**  

---

## ❓ Wie funktioniert Detection?
**Lösung:** Monitoring + Alerts.

Wichtige Signale:

- Error Rate steigt  
- Latenz steigt  
- CPU/RAM hoch  
- Queue‑Länge steigt  
- Circuit Breaker öffnet  
- Nutzer melden Probleme  

Detection muss **automatisiert** sein.

---

## ❓ Wie funktioniert Triage?
**Lösung:** schnelle Einordnung.

Fragen:

- Wie viele Nutzer betroffen?  
- Welche Funktionen betroffen?  
- Welche Systeme betroffen?  
- Ist es ein SEV‑1?  

Ziel:
- schnell entscheiden, wie ernst es ist.

---

## ❓ Wie funktioniert Mitigation?
**Lösung:** Schaden begrenzen.

Typische Maßnahmen:

- Rollback  
- Traffic reduzieren  
- Feature Flags deaktivieren  
- Cache aktivieren  
- Circuit Breaker öffnen  
- Load Shedding aktivieren  

Mitigation ist **sofort**, nicht perfekt.

---

## ❓ Wie funktioniert Resolution?
**Lösung:** Problem dauerhaft beheben.

Beispiele:

- Bugfix  
- Konfigurationsänderung  
- Infrastruktur‑Anpassung  
- Datenreparatur  

Resolution kommt **nach** Mitigation.

---

## ❓ Wie funktioniert Kommunikation während eines Incidents?
**Lösung:** klar + knapp + regelmäßig.

Rollen:

- **Incident Commander** → Koordination  
- **Communications Lead** → Updates  
- **Subject Matter Experts** → technische Analyse  

Regeln:

- alle 10–15 Minuten Updates  
- keine Spekulation  
- klare Fakten  

---

## ❓ Welche Rollen gibt es im Incident‑Management?
**Lösung:** definierte Verantwortlichkeiten.

- **Incident Commander**  
- **Tech Lead / SME**  
- **Communications Lead**  
- **Scribe**  
- **On‑Call Engineer**  

Ein Incident ohne Commander eskaliert chaotisch.

---

## ❓ Was ist ein Postmortem?
**Lösung:** Analyse nach dem Incident.

Ziele:

- Ursachen verstehen  
- Maßnahmen definieren  
- Wiederholung verhindern  
- Lernkultur stärken  

Regeln:

- **blameless**  
- faktenbasiert  
- konkrete Action Items  

---

## ❓ Was gehört in ein Postmortem?
**Lösung:** strukturierte Dokumentation.

- Zusammenfassung  
- Timeline  
- Impact  
- Root Cause  
- Detection Gaps  
- Mitigation & Resolution  
- Action Items  
- Owner & Deadlines  

---

## ❓ Wie mache ich Root Cause Analysis (RCA)?
**Lösung:** systematisch.

Methoden:

- 5 Whys  
- Fishbone Diagram  
- Event Timeline  
- Fault Tree Analysis  

Ziel:
- nicht Schuldige finden, sondern Ursachen.

---

## ❓ Wie mache ich Incident‑Readiness?
**Lösung:** Vorbereitung.

- klare Runbooks  
- On‑Call Rotation  
- regelmäßige Fire Drills  
- Chaos Engineering  
- Monitoring & Alerts  
- SLOs & Error Budgets  

---

## ❓ Wie messe ich Incident‑Performance?
**Lösung:** SRE‑Metriken.

- MTTR (Mean Time To Recovery)  
- MTTD (Mean Time To Detect)  
- MTTA (Mean Time To Acknowledge)  
- Incident Frequency  
- Error Budget Burn Rate  

---

## Pro-Tipp
Incident‑Management ist **Team‑Koordination unter Stress**: Je klarer Rollen, Prozesse und Kommunikation sind, desto schneller stabilisiert sich das System.
