---
title: Security Basics Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Security Basics: Fundamentale Prinzipien moderner IT‑Sicherheit

Dieses Sheet bündelt die wichtigsten Grundprinzipien, die jedes System, jede Architektur und jedes Team verinnerlichen muss — unabhängig von Technologie, Größe oder Branche.

---

## ❓ Warum Security Basics?
**Lösung:** Ohne solide Grundlagen sind alle fortgeschrittenen Sicherheitsmaßnahmen wirkungslos.

Security Basics verhindern:

- triviale Angriffe  
- Fehlkonfigurationen  
- Datenlecks  
- Account‑Übernahmen  
- RCE durch einfache Fehler  
- Eskalation kleiner Schwachstellen  

Security Basics sind **Pflicht**, nicht Kür.

---

# 🧱 Die 5 Grundpfeiler der IT‑Sicherheit

### 1. **Confidentiality**
Nur autorisierte Personen dürfen Daten sehen.

### 2. **Integrity**
Daten dürfen nicht unbemerkt verändert werden.

### 3. **Availability**
Systeme müssen zuverlässig erreichbar sein.

### 4. **Authentication**
Wer bist du?

### 5. **Authorization**
Was darfst du?

---

# 🔐 Authentifizierung (Authentication)

- MFA überall  
- starke Passwörter  
- Passwort‑Manager  
- keine Wiederverwendung  
- sichere Login‑Flows (OAuth2/OIDC)  
- keine eigenen Auth‑Systeme bauen  

---

# 🛡️ Autorisierung (Authorization)

- least privilege  
- rollenbasierte Zugriffe  
- keine globalen Admin‑Rollen  
- Scopes für APIs  
- Service‑Identitäten trennen  

---

# 🧩 Netzwerk‑Grundsicherheit

- Firewalls  
- Zero‑Trust intern  
- Mikrosegmentierung  
- TLS überall  
- keine offenen Ports  
- keine Public Endpoints ohne Grund  

---

# 🐳 Container‑Grundsicherheit

- minimalistische Images  
- non‑root User  
- keine Shell  
- keine Secrets im Image  
- Scanning vor Deployment  

---

# ☸️ Kubernetes‑Grundsicherheit

- RBAC strikt  
- Network Policies  
- Pod Security Standards  
- Admission Controller  
- Secrets verschlüsseln  

---

# 🧰 Logging & Monitoring Basics

- zentrale Logs  
- keine sensiblen Daten loggen  
- Audit Logs aktivieren  
- Alerts für kritische Ereignisse  
- API Gateway Logs  
- Cloud Activity Logs  

---

# 🧪 Testing Basics

- Unit Tests  
- Integration Tests  
- Security Tests  
- Dependency Scanning  
- Secret Scanning  
- Infrastructure Scanning  

---

# 🔒 Secrets Basics

- Secret Store verwenden  
- keine Secrets in Git  
- keine Secrets in Logs  
- Rotation automatisieren  
- Zugriff minimal halten  

---

# 🧯 Patch & Update Basics

- regelmäßige Updates  
- CVE‑Monitoring  
- Dependency Scanning  
- Container Scanning  
- automatisierte Updates  

---

# 🧭 Secure Defaults

- alles deaktiviert, was nicht benötigt wird  
- sichere Standard‑Konfigurationen  
- keine offenen Ports  
- keine anonymen Endpoints  
- keine Debug‑Modi in Produktion  

---

# 🧨 Security Anti‑Patterns

- „Security später“  
- „Das ist nur intern“  
- „Wir haben keine Zeit“  
- globale Admin‑Rollen  
- Passwörter im Code  
- keine MFA  
- keine Logs  
- keine Updates  

---

## Pro-Tipp
Security Basics sind **Betriebssicherheit**: Wer die Grundlagen meistert, verhindert 80 % aller realen Angriffe — bevor sie überhaupt relevant werden.
