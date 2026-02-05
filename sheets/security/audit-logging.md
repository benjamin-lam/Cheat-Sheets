---
title: Audit Logging Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Audit Logging: Nachvollziehbarkeit, Integrität & forensische Sicherheit

Dieses Sheet bündelt die wichtigsten Mechaniken für Audit Logging — ideal für APIs, Microservices, Cloud‑Plattformen, Identity‑Systeme, Kubernetes und Zero‑Trust‑Architekturen.

---

## ❓ Warum Audit Logging?
**Lösung:** Ohne Audit Logs gibt es keine Beweise, keine Forensik und keine Verantwortlichkeit.

Audit Logging ermöglicht:

- Nachvollziehbarkeit sicherheitsrelevanter Aktionen  
- forensische Analyse  
- Incident Response  
- Compliance‑Nachweise  
- Erkennung von Missbrauch  

Audit Logs sind **Beweis‑Infrastruktur**.

---

# 🧱 Grundprinzipien

- **Unveränderbarkeit**  
- **Integrität**  
- **Zentrale Speicherung**  
- **Keine sensiblen Daten**  
- **Strukturierte Logs**  
- **Korrelation über Trace IDs**  
- **Retention Policies**  

---

# 🔍 Was gehört in Audit Logs?

### Authentifizierung
- Login‑Versuche  
- MFA‑Ereignisse  
- Passwort‑Änderungen  
- Token‑Ausstellung  
- Token‑Invalidierung  

### Autorisierung
- Zugriffe auf geschützte Ressourcen  
- 403‑Ereignisse  
- Scope‑Verstöße  
- Rollenänderungen  

### Datenzugriffe
- Lesen sensibler Daten  
- Schreiben/Ändern/Löschen  
- Export‑Aktionen  
- ungewöhnliche Download‑Muster  

### System‑Änderungen
- Deployments  
- Konfigurationsänderungen  
- Policy‑Änderungen  
- neue Service Accounts  
- neue Admin‑Rollen  

### Infrastruktur
- Container Starts/Stops  
- Node‑Änderungen  
- Netzwerk‑Policy‑Verstöße  
- Cloud IAM Events  

---

# 🧰 Was gehört **nicht** in Audit Logs?

- Passwörter  
- Tokens  
- Secrets  
- personenbezogene Daten  
- vollständige Payloads  
- Kreditkarteninformationen  
- Session Cookies  

---

# 🧩 Log‑Format

### Empfohlen
- JSON  
- strukturierte Felder  
- Zeitstempel in UTC  
- Trace ID  
- Correlation ID  
- User ID / Service ID  
- Aktion  
- Ergebnis (success/failure)  
- Kontext (minimal)  

Beispiel:

```json
{
  "timestamp": "2025-09-02T12:34:56Z",
  "trace_id": "abc123",
  "actor": "user:42",
  "action": "update_profile",
  "resource": "profile",
  "result": "success",
  "ip": "192.168.1.10"
}
```

---

# 🛡️ Integrität & Manipulationsschutz

- Write‑Once Storage (WORM)  
- Hash Chains  
- Signierte Logs  
- unveränderbare Buckets  
- Zugriff minimal halten  
- getrennte Rollen für Logging & Admin  

---

# ☁️ Cloud Audit Logging

AWS:
- CloudTrail  
- IAM Access Analyzer  
- S3 Object Access Logs  
- VPC Flow Logs  

Azure:
- Activity Logs  
- Azure Monitor  
- Defender for Cloud  

GCP:
- Cloud Audit Logs  
- VPC Flow Logs  
- Cloud Armor Logs  

---

# ☸️ Kubernetes Audit Logging

- API Server Audit Logs  
- RBAC Audit  
- Admission Controller Events  
- Pod Security Violations  
- Node Events  
- Network Policy Violations  

---

# 🐳 Container Audit Logging

- Container Starts/Stops  
- Image Hashes  
- Policy‑Verstöße  
- mTLS‑Fehler  
- Resource‑Anomalien  

---

# 🧭 Audit Log Retention

### Empfohlen
- 90–180 Tage für operative Logs  
- 1–7 Jahre für Compliance‑relevante Logs  

### Regeln
- verschlüsselt speichern  
- Zugriff minimal halten  
- automatisches Löschen nach Ablauf  

---

# 🧪 Audit Logging Testing

- Log Injection Tests  
- Manipulationsversuche  
- Replay Tests  
- Incident Simulation  
- Alert Simulation  
- Cloud IAM Audit  

---

# 🧨 Audit Logging Anti‑Patterns

- Logs lokal speichern  
- Logs überschreiben  
- Logs ohne Struktur  
- keine Trace IDs  
- keine Retention Policies  
- Logs mit PII  
- Logs ohne Integritätsschutz  

---

## Pro-Tipp
Audit Logging ist **Verantwortlichkeits‑Infrastruktur**: Wer sauber, strukturiert und unveränderbar loggt, kann Angriffe verstehen, Verantwortlichkeiten klären und Systeme nachhaltig verbessern.
