---
title: OWASP Basics Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# OWASP Basics: Die wichtigsten Web‑ und API‑Sicherheitsrisiken

Dieses Sheet bündelt die zentralen OWASP‑Konzepte — ideal für APIs, Microservices, Web‑Apps und Cloud‑Plattformen.

---

## ❓ Was ist OWASP?
**Lösung:** eine offene, gemeinnützige Organisation, die Best Practices für Web‑ und API‑Sicherheit definiert.

OWASP liefert:

- Risiko‑Kataloge  
- Best Practices  
- Tools  
- Security‑Guidelines  

Die wichtigsten Projekte:

- OWASP Top 10 (Web)  
- OWASP API Security Top 10  
- OWASP ASVS  
- OWASP Cheat Sheets  

---

# 🧱 OWASP Top 10 (Web)

Die zehn häufigsten Web‑Sicherheitsrisiken.

### 1. Broken Access Control
- fehlende Autorisierung  
- horizontale/vertikale Rechteausweitung  

### 2. Cryptographic Failures
- unsichere Verschlüsselung  
- Klartext‑Daten  

### 3. Injection
- SQL Injection  
- NoSQL Injection  
- Command Injection  

### 4. Insecure Design
- fehlende Sicherheitsarchitektur  
- keine Threat Models  

### 5. Security Misconfiguration
- offene Ports  
- Standardpasswörter  
- unsichere Defaults  

### 6. Vulnerable & Outdated Components
- alte Libraries  
- ungepatchte Systeme  

### 7. Identification & Authentication Failures
- schwache Auth  
- fehlende MFA  
- Session‑Probleme  

### 8. Software & Data Integrity Failures
- unsichere CI/CD  
- Supply‑Chain‑Risiken  

### 9. Security Logging & Monitoring Failures
- fehlende Logs  
- keine Alerts  

### 10. Server‑Side Request Forgery (SSRF)
- unvalidierte URLs  
- Zugriff auf interne Systeme  

---

# 🔌 OWASP API Security Top 10

Die zehn häufigsten API‑Risiken.

### 1. Broken Object Level Authorization (BOLA)
- Zugriff auf fremde Ressourcen  
- häufigster API‑Fehler  

### 2. Broken Authentication
- schwache Token  
- fehlende Validierung  

### 3. Broken Object Property Level Authorization
- Zugriff auf Felder, die nicht erlaubt sind  

### 4. Unrestricted Resource Consumption
- keine Limits  
- DoS‑Risiken  

### 5. Broken Function Level Authorization
- Admin‑Funktionen ohne Schutz  

### 6. Unrestricted Access to Sensitive Business Flows
- kritische Abläufe ohne Schutz  

### 7. Server‑Side Request Forgery (SSRF)
- unvalidierte URLs  

### 8. Security Misconfiguration
- unsichere Defaults  
- fehlende Header  

### 9. Improper Inventory Management
- unbekannte APIs  
- alte Versionen  

### 10. Unsafe Consumption of APIs
- blindes Vertrauen in externe APIs  

---

# 🧰 OWASP ASVS (Application Security Verification Standard)

Ein Sicherheitsstandard für Web‑Apps.

Level:

- **L1**: Basis  
- **L2**: Standard für Unternehmen  
- **L3**: Hochsicherheit  

ASVS deckt ab:

- AuthN  
- AuthZ  
- Session Security  
- Input Validation  
- Cryptography  
- Error Handling  
- Logging  
- Data Protection  

---

# 🧪 OWASP Testing Guide

Wichtige Testbereiche:

- AuthN Tests  
- AuthZ Tests  
- Input Validation Tests  
- Business Logic Tests  
- API Tests  
- Cryptography Tests  

---

# 🧩 OWASP Cheat Sheets

Empfehlenswerte Sheets:

- Authentication Cheat Sheet  
- Authorization Cheat Sheet  
- Input Validation Cheat Sheet  
- Logging Cheat Sheet  
- Secure Headers Cheat Sheet  
- Docker Security Cheat Sheet  
- Kubernetes Security Cheat Sheet  

---

# 🛡️ Wichtige OWASP‑Header

- `Content-Security-Policy`  
- `Strict-Transport-Security`  
- `X-Content-Type-Options: nosniff`  
- `X-Frame-Options: DENY`  
- `Referrer-Policy`  
- `Permissions-Policy`  

---

# 🧭 Wie OWASP in der Praxis hilft

OWASP liefert:

- klare Prioritäten  
- reproduzierbare Standards  
- gemeinsame Sprache zwischen Dev, Ops & Security  
- Basis für Audits & Compliance  

---

## Pro-Tipp
OWASP ist **Sicherheits‑Grundbildung**: Wer OWASP versteht, baut automatisch sicherere APIs, Services und Plattformen.
