---
title: Identity Hardening Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Identity Hardening: Schutz von Benutzer‑, Service‑ & Maschinenidentitäten

Dieses Sheet bündelt die wichtigsten Mechaniken zur Absicherung von Identitäten — ideal für Zero‑Trust‑Architekturen, Microservices, Cloud‑Plattformen und Enterprise‑Security.

---

## ❓ Warum Identity Hardening?
**Lösung:** Identitäten sind die neue Perimeter‑Security.

Angreifer zielen auf:

- Passwörter  
- Tokens  
- API Keys  
- Zertifikate  
- Sessions  
- IAM‑Rollen  

Identity Hardening verhindert:

- Account‑Übernahmen  
- lateral movement  
- Privilege Escalation  
- Cloud‑Kompromittierung  
- API‑Missbrauch  

---

# 🧱 Benutzeridentitäten (Human Identity)

### MFA erzwingen
- Pflicht für alle Benutzer  
- bevorzugt: App‑basierte MFA  
- keine SMS‑MFA für kritische Systeme  

### Passwort‑Hygiene
- keine Wiederverwendung  
- Passwort‑Manager  
- starke Passwortrichtlinien  
- regelmäßige Rotation nur bei Verdacht  

### Session‑Sicherheit
- kurze Session‑TTL  
- Refresh Tokens sicher speichern  
- Session Binding (IP/Device)  
- automatische Logout‑Mechanismen  

### Account‑Monitoring
- ungewöhnliche Logins  
- Geolocation‑Anomalien  
- viele Fehlversuche  
- Login‑Versuche außerhalb Arbeitszeiten  

---

# 🧩 Service‑Identitäten (Machine Identity)

### mTLS
- Zertifikate statt Passwörter  
- automatische Rotation  
- SPIFFE/SPIRE für Service Identity  

### API Keys
- pro Service ein eigener Key  
- kurze TTL  
- Rotation automatisieren  
- granularer Zugriff  

### OAuth2 Client Credentials
- für serverseitige Integrationen  
- Scopes minimal halten  
- Tokens kurzlebig  

### Service‑Isolation
- kein Sharing von Credentials  
- kein globaler „service-admin“  

---

# 🐳 Container‑Identitäten

- keine statischen Secrets im Image  
- Service Account Token Projection  
- mTLS via Service Mesh  
- Pod Identity (Azure/GCP/AWS)  
- keine Root‑Container  

---

# ☸️ Kubernetes Identity Hardening

- RBAC strikt  
- keine Wildcard‑Rollen (`*`)  
- Namespaces isolieren  
- Admission Controller für Policies  
- Secrets verschlüsseln  
- Service Accounts minimal halten  

---

# 🔐 Cloud Identity Hardening

### IAM‑Grundregeln
- least privilege  
- keine Admin‑Rollen für Services  
- keine Root‑Nutzung  
- MFA für alle Benutzer  
- Rollen statt statische Keys  

### Cloud‑spezifische Mechaniken

AWS:
- IAM Roles statt Access Keys  
- STS Tokens  
- SCPs (Service Control Policies)  

Azure:
- Managed Identities  
- Conditional Access  
- Privileged Identity Management  

GCP:
- Workload Identity  
- IAM Conditions  
- VPC Service Controls  

---

# 🧰 Token‑Hardening

- kurze TTL (5–15 Minuten)  
- Refresh Tokens sicher speichern  
- Token Binding  
- Audience prüfen  
- Issuer prüfen  
- Signatur prüfen  
- keine sensiblen Daten im Token  

---

# 🧱 Secrets‑Hardening

- Secret Store verwenden  
- Rotation automatisieren  
- keine Secrets in Git  
- keine Secrets in Logs  
- dynamische Secrets bevorzugen  

---

# 🧭 Identity Monitoring

Wichtige Signale:

- ungewöhnliche Token‑Nutzung  
- viele 401/403  
- Zertifikatsfehler  
- Policy‑Verstöße  
- Login‑Anomalien  
- API Key Missbrauch  

---

# 🧪 Identity Testing

- Penetration Tests  
- Credential Stuffing Simulation  
- Phishing Simulation  
- Token Replay Tests  
- IAM Audit  
- RBAC Audit  

---

# 🧨 Identity Anti‑Patterns

- globale Admin‑Rollen  
- statische Access Keys  
- Secrets im Code  
- lange Token‑TTL  
- keine MFA  
- geteilte Service Accounts  
- „trusted internal network“  

---

## Pro-Tipp
Identity Hardening ist **Zugriffs‑Architektur**: Wer Identitäten sauber trennt, minimiert lateral movement und schützt das gesamte System.
