---
title: Hardening Patterns Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Hardening Patterns: Angriffsfläche minimieren & sichere Defaults etablieren

Dieses Sheet bündelt die wichtigsten Hardening‑Mechaniken für APIs, Microservices, Container, Server, Cloud‑Infrastruktur und CI/CD‑Pipelines.

---

## ❓ Was ist Hardening?
**Lösung:** systematische Reduktion der Angriffsfläche durch sichere Defaults, Isolation und Minimierung.

Hardening bedeutet:

- weniger Angriffsfläche  
- weniger unnötige Funktionen  
- weniger unnötige Ports  
- weniger unnötige Berechtigungen  
- weniger unnötige Software  

Hardening ist **präventive Sicherheit**.

---

## ❓ Warum Hardening?
**Lösung:** die meisten Angriffe nutzen Fehlkonfigurationen.

Hardening schützt vor:

- RCE  
- Privilege Escalation  
- Supply‑Chain‑Angriffen  
- Container‑Breakouts  
- Credential Theft  
- lateral movement  

---

# 🧱 System‑Hardening

- unnötige Pakete entfernen  
- unnötige Dienste deaktivieren  
- Firewall aktivieren  
- SSH absichern (kein root login, nur Keys)  
- sichere Defaults für Kernel‑Parameter  
- Logging aktivieren  
- Auditd aktivieren  

---

# 🐳 Container‑Hardening

- minimalistische Base Images (distroless, alpine)  
- keine Shell im Container  
- non‑root User  
- read‑only Filesystem  
- seccomp Profile  
- AppArmor / SELinux  
- keine Secrets im Image  
- Health Checks definieren  

---

# ☸️ Kubernetes‑Hardening

- Pod Security Standards  
- Network Policies  
- RBAC strikt  
- Admission Controller  
- Secret Encryption at Rest  
- keine privilegierten Container  
- keine Host‑Mounts  
- Resource Limits setzen  
- mTLS via Service Mesh  

---

# 🔐 API‑Hardening

- TLS erzwingen  
- Rate Limiting  
- Schema Validation  
- Input Validation  
- Output Encoding  
- sichere HTTP‑Header  
- keine unnötigen Endpoints  
- Versionierung erzwingen  
- Idempotency Keys  

---

# 🧩 Microservices‑Hardening

- mTLS zwischen Services  
- Service‑Identität (SPIFFE/SPIRE)  
- Policies pro Service  
- keine direkten DB‑Zugriffe zwischen Services  
- Secrets pro Service  
- keine impliziten Vertrauenszonen  

---

# 🗄️ Datenbank‑Hardening

- least privilege Accounts  
- keine shared DB‑User  
- TLS aktivieren  
- Audit Logs aktivieren  
- Query Limits  
- Prepared Statements erzwingen  
- keine öffentlichen DB‑Endpoints  

---

# 🧰 CI/CD‑Hardening

- Build‑Agent isolieren  
- keine Secrets im Repo  
- Secrets Masking  
- signierte Builds  
- Dependency Scanning  
- SBOM erzeugen  
- keine shared Runner für sensitive Projekte  
- Zugriff auf Deploy‑Keys minimieren  

---

# 🛡️ Netzwerk‑Hardening

- Mikrosegmentierung  
- Zero‑Trust intern  
- Firewall Regeln minimal halten  
- keine offenen Ports  
- IDS/IPS  
- DDoS‑Schutz  
- DNSSEC  

---

# 🔒 Betriebssystem‑Hardening

Linux:

- sysctl Hardening  
- noexec /tmp  
- read‑only root FS  
- Passwort‑Policy  
- Auditd  
- SSH Hardening  

Windows:

- Defender aktivieren  
- Credential Guard  
- Application Control  
- Secure Boot  
- BitLocker  

---

# 🧯 Cloud‑Hardening

AWS:

- IAM least privilege  
- keine Public S3 Buckets  
- Security Groups minimal  
- KMS für Encryption  
- CloudTrail aktivieren  

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

# 🧪 Hardening‑Testing

- CIS Benchmarks  
- kube‑bench  
- docker‑bench  
- Lynis  
- OpenSCAP  
- Penetration Tests  

---

# 🧭 Hardening‑Philosophie

- sichere Defaults  
- minimale Rechte  
- minimale Software  
- minimale Angriffsfläche  
- maximale Isolation  

Hardening ist **Architektur**, nicht nur Konfiguration.

---

## Pro-Tipp
Hardening ist **präventive Resilienz**: Je weniger Angriffsfläche ein System bietet, desto weniger muss es im Ernstfall verteidigen.
