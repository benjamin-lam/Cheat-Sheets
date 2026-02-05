---
title: Monitoring Security Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Monitoring Security: Erkennen, Verstehen & Reagieren auf sicherheitsrelevante Ereignisse

Dieses Sheet bündelt die wichtigsten Mechaniken für sicherheitsorientiertes Monitoring — ideal für Microservices, APIs, Cloud‑Plattformen, Container, Identity‑Systeme und Zero‑Trust‑Architekturen.

---

## ❓ Warum Security Monitoring?
**Lösung:** Ohne Monitoring ist jedes System blind — Angriffe passieren unbemerkt.

Security Monitoring ermöglicht:

- frühe Erkennung von Angriffen  
- Analyse von Anomalien  
- schnelle Reaktion  
- forensische Nachvollziehbarkeit  
- Compliance‑Nachweise  

Monitoring ist **Sicherheits‑Telemetrie**.

---

# 🧱 Grundprinzipien

- **Collect everything, alert on what matters**  
- **Security‑Signale priorisieren**  
- **Zentrale Log‑Aggregation**  
- **Keine sensiblen Daten loggen**  
- **Korrelation statt Einzelereignisse**  
- **Automatisierte Alerts**  
- **Dashboards für Security‑Teams**  

---

# 🔍 Wichtige Security‑Signale

### Authentifizierung
- viele Fehlversuche  
- ungewöhnliche Login‑Orte  
- parallele Sessions  
- Login außerhalb Arbeitszeiten  
- MFA‑Fehler  

### Autorisierung
- viele 403  
- Zugriffe auf verbotene Ressourcen  
- Scope‑Missbrauch  

### API‑Missbrauch
- Rate‑Limit‑Hits  
- ungewöhnliche Traffic‑Spitzen  
- Bot‑Muster  
- Payload‑Anomalien  

### Netzwerk
- ungewöhnliche Ports  
- interne Scans  
- mTLS‑Fehler  
- DNS‑Anomalien  

### Infrastruktur
- neue Admin‑Accounts  
- unerwartete Deployments  
- Container‑Restarts  
- Node‑Anomalien  

---

# 🧰 Logging Best Practices

### Was loggen?
- Auth Events  
- Token Events  
- Policy‑Verstöße  
- API Requests (ohne sensitive Daten)  
- Fehler & Exceptions  
- Deployment Events  
- Cloud Activity Logs  

### Was nicht loggen?
- Passwörter  
- Tokens  
- Secrets  
- personenbezogene Daten  
- vollständige Payloads  

### Format
- JSON Logs  
- strukturierte Felder  
- Trace IDs  
- Correlation IDs  

---

# ☁️ Cloud Security Monitoring

AWS:
- CloudTrail  
- GuardDuty  
- IAM Access Analyzer  
- VPC Flow Logs  

Azure:
- Azure Monitor  
- Defender for Cloud  
- Activity Logs  

GCP:
- Cloud Audit Logs  
- Cloud Armor Logs  
- VPC Flow Logs  

---

# 🐳 Container & Kubernetes Monitoring

### Container
- Container Starts/Stops  
- Image Hashes  
- Policy‑Verstöße  
- Resource‑Anomalien  

### Kubernetes
- API Server Logs  
- RBAC Audit  
- Admission Controller Events  
- Pod Security Violations  
- Network Policy Violations  
- Node Health  

---

# 🧩 Identity Monitoring

- ungewöhnliche Token‑Nutzung  
- Refresh Token Missbrauch  
- viele 401/403  
- Rollenänderungen  
- neue Service Accounts  
- Zertifikatsfehler  

---

# 🛡️ SIEM & Security Analytics

### Ziele
- Korrelation  
- Anomalieerkennung  
- Threat Intelligence  
- Incident Detection  

### Beispiele
- Splunk  
- Elastic Security  
- Microsoft Sentinel  
- Wazuh  

---

# 🧪 Security Monitoring Testing

- Log Injection Tests  
- Alert Simulation  
- Incident Simulation  
- Token Replay Tests  
- API Abuse Simulation  
- Chaos Security Experiments  

---

# 🧨 Monitoring Anti‑Patterns

- keine Logs  
- Logs lokal speichern  
- Logs ohne Struktur  
- keine Alerts  
- zu viele Alerts (Alert Fatigue)  
- keine Korrelation  
- keine Dashboards  
- keine Aufbewahrungsstrategie  

---

## Pro-Tipp
Security Monitoring ist **Sichtbarkeit**: Nur wer sieht, was passiert, kann Angriffe stoppen — und Systeme wirklich verstehen.
