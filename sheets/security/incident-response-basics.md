---
title: Incident Response Basics Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Incident Response: strukturierte Reaktion auf Sicherheitsvorfälle

Dieses Sheet bündelt die wichtigsten Mechaniken für Incident Response (IR) — ideal für Plattformen, Microservices, Cloud‑Infrastruktur, Enterprise‑Security und Zero‑Trust‑Umgebungen.

---

## ❓ Warum Incident Response?
**Lösung:** Sicherheit ist nie perfekt — aber Reaktion kann es sein.

Incident Response verhindert:

- Eskalation von Angriffen  
- Datenverlust  
- Produktionsausfälle  
- Reputationsschäden  
- rechtliche Konsequenzen  

IR ist **Schadensbegrenzung + Wiederherstellung + Lernen**.

---

# 🧱 Die 6 Phasen des Incident Response

### 1. Preparation
- Runbooks  
- On‑Call‑Pläne  
- Logging & Monitoring  
- Forensik‑Tools  
- Kommunikationswege  
- Rollen & Verantwortlichkeiten  

### 2. Identification
- Alerts  
- Anomalien  
- Log‑Analysen  
- User‑Reports  
- Threat Intelligence  

Ziel: **Erkennen, dass etwas passiert ist.**

### 3. Containment
- kurzzeitig: Schaden begrenzen  
- langfristig: Ausbreitung verhindern  

Beispiele:
- Zugang sperren  
- Netzwerk isolieren  
- Tokens invalidieren  
- Services drosseln  

### 4. Eradication
- Ursache entfernen  
- Malware löschen  
- kompromittierte Accounts deaktivieren  
- Schwachstellen patchen  

### 5. Recovery
- Systeme wiederherstellen  
- Monitoring verstärken  
- schrittweise in Produktion zurückkehren  

### 6. Lessons Learned
- Root Cause Analysis  
- Prozessverbesserungen  
- zusätzliche Controls  
- Dokumentation  

---

# 🔍 Detection & Monitoring

Wichtige Signale:

- ungewöhnliche Logins  
- viele 401/403  
- Token‑Missbrauch  
- mTLS‑Fehler  
- Rate‑Limit‑Hits  
- plötzliche Traffic‑Spitzen  
- neue Admin‑Accounts  
- unerwartete Deployments  

Tools:

- SIEM  
- IDS/IPS  
- Cloud Logs  
- API Gateway Logs  
- EDR/XDR  

---

# 🛡️ Containment Strategien

### Kurzfristig
- Tokens invalidieren  
- Sessions beenden  
- API Keys rotieren  
- Netzwerkzugriff sperren  
- betroffene Services isolieren  

### Langfristig
- mTLS erzwingen  
- Policies verschärfen  
- Secrets rotieren  
- Rollen entziehen  

---

# 🧯 Forensik Basics

- Logs sichern  
- Speicherabbilder erstellen  
- Netzwerkverkehr analysieren  
- kompromittierte Artefakte isolieren  
- keine Systeme neu starten  
- keine Dateien löschen  

Ziel: **Beweise sichern, nicht zerstören.**

---

# 🧩 Kommunikation im Incident

### Intern
- Security Team  
- Engineering  
- Management  
- Legal  
- PR  

### Extern
- Kunden  
- Partner  
- Behörden (falls nötig)  

Regel:
- **klar, faktenbasiert, ohne Spekulation.**

---

# 🧰 Incident Response in der Cloud

- IAM Audit  
- CloudTrail/Activity Logs prüfen  
- Public Exposure Checks  
- Rollen entziehen  
- Access Keys rotieren  
- betroffene Ressourcen isolieren  

---

# ☸️ Incident Response in Kubernetes

- Pod isolieren  
- Node isolieren  
- Secrets rotieren  
- Admission Controller prüfen  
- RBAC Audit  
- Network Policies verschärfen  

---

# 🐳 Incident Response in Containern

- kompromittierte Container stoppen  
- Images scannen  
- signierte Images erzwingen  
- Base Images aktualisieren  
- Secrets rotieren  

---

# 🧭 Post‑Incident Verbesserungen

- zusätzliche Monitoring‑Signale  
- härtere Policies  
- bessere Tests  
- mehr Automatisierung  
- Playbooks aktualisieren  
- Schulungen durchführen  

---

# 🧨 Incident Response Anti‑Patterns

- Systeme sofort neu starten  
- Logs löschen  
- Schuldige suchen statt Ursachen  
- keine Dokumentation  
- keine Lessons Learned  
- „Das passiert uns nicht nochmal“ ohne Maßnahmen  

---

## Pro-Tipp
Incident Response ist **organisierte Resilienz**: Je klarer die Prozesse, je schneller die Reaktion und je besser die Vorbereitung, desto kleiner der Schaden — und desto stärker das System danach.
