---
title: Secure Configuration Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Secure Configuration: sichere Defaults für Systeme, Services & Infrastruktur

Dieses Sheet bündelt die wichtigsten Mechaniken für sichere Konfigurationen — ideal für APIs, Microservices, Container, Cloud‑Plattformen und Zero‑Trust‑Architekturen.

---

## ❓ Warum Secure Configuration?
**Lösung:** Die meisten Sicherheitsvorfälle entstehen durch Fehlkonfigurationen, nicht durch Zero‑Day‑Exploits.

Secure Configuration verhindert:

- offene Ports  
- unautorisierte Zugriffe  
- Datenlecks  
- Privilege Escalation  
- RCE durch unsichere Defaults  
- Cloud‑Exposure  

---

# 🧱 Grundprinzipien

- **Secure by Default**  
- **Least Privilege**  
- **Minimal Surface Area**  
- **Defense in Depth**  
- **Immutable Infrastructure**  
- **Configuration as Code**  
- **No Manual Changes in Production**  

---

# 🐳 Container Configuration

- minimalistische Base Images  
- keine Shell im Container  
- non‑root User  
- read‑only Filesystem  
- Health Checks definieren  
- Resource Limits setzen  
- keine Secrets im Image  
- Logging an stdout/stderr  

---

# ☸️ Kubernetes Configuration

- Pod Security Standards  
- Network Policies  
- RBAC strikt  
- Admission Controller  
- Secrets verschlüsseln  
- keine Host‑Mounts  
- keine privilegierten Container  
- Liveness/Readiness Probes  
- Resource Requests & Limits  

---

# 🔐 API Configuration

- TLS erzwingen  
- Rate Limiting  
- Schema Validation  
- Input Validation  
- sichere HTTP‑Header  
- CORS restriktiv konfigurieren  
- keine anonymen Endpoints  
- Versionierung erzwingen  

---

# 🧩 Service Configuration

- mTLS zwischen Services  
- Service‑Identität (SPIFFE/SPIRE)  
- keine globalen Admin‑Rollen  
- Secrets pro Service  
- Logging ohne sensitive Daten  
- Retry‑Strategien begrenzen  
- Timeouts definieren  

---

# 🗄️ Datenbank‑Konfiguration

- TLS aktivieren  
- least privilege Accounts  
- keine shared DB‑User  
- Audit Logs aktivieren  
- Query Limits  
- keine öffentlichen Endpoints  
- automatische Backups  
- Verschlüsselung at Rest  

---

# 🛡️ Server‑Konfiguration

Linux:

- Firewall aktivieren  
- SSH Hardening  
- sysctl Hardening  
- noexec /tmp  
- Auditd aktivieren  
- Logging zentralisieren  

Windows:

- Defender aktivieren  
- Credential Guard  
- Secure Boot  
- BitLocker  
- Application Control  

---

# ☁️ Cloud‑Konfiguration

AWS:

- IAM least privilege  
- keine Public S3 Buckets  
- Security Groups minimal  
- CloudTrail aktivieren  
- KMS für Encryption  

Azure:

- RBAC  
- Key Vault  
- NSGs  
- Defender for Cloud  

GCP:

- IAM minimal  
- VPC Service Controls  
- CMEK  
- Cloud Armor  

---

# 🧰 CI/CD‑Konfiguration

- Pipeline‑Isolation  
- Secrets Masking  
- signierte Artefakte  
- keine direkten Deployments von Laptops  
- Dependency Scanning  
- IaC Scanning  
- SBOM erzeugen  

---

# 🧪 Configuration Testing

- CIS Benchmarks  
- kube‑bench  
- docker‑bench  
- OpenSCAP  
- IaC Scanning (Checkov, tfsec)  
- Penetration Tests  

---

# 🧨 Configuration Anti‑Patterns

- „Default Settings sind schon sicher“  
- offene Ports „für später“  
- globale Admin‑Rollen  
- Secrets in Config Files  
- keine TLS‑Konfiguration  
- keine Resource Limits  
- manuelle Änderungen in Produktion  

---

## Pro-Tipp
Secure Configuration ist **präventive Stabilität**: Je sicherer die Defaults, desto weniger Angriffsfläche — und desto robuster das gesamte System.
