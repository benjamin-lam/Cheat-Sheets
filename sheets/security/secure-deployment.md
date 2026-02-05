---
title: Secure Deployment Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Secure Deployment: Sicheres Ausrollen von Software in Cloud, Kubernetes & CI/CD

Dieses Sheet bündelt die wichtigsten Mechaniken für sichere Deployments — ideal für Microservices, Container, Cloud‑Plattformen und Zero‑Trust‑Architekturen.

---

## ❓ Warum Secure Deployment?
**Lösung:** Deployment ist ein kritischer Moment — Fehler oder Manipulationen können direkt in Produktion landen.

Secure Deployment verhindert:

- Supply‑Chain‑Angriffe  
- Deployment von manipulierten Artefakten  
- Secrets‑Leaks  
- unautorisierte Deployments  
- Konfigurationsfehler  
- Rollout von ungepatchten Images  

---

# 🚀 Deployment‑Grundprinzipien

- reproduzierbare Builds  
- signierte Artefakte  
- Zero‑Trust in der Pipeline  
- least privilege für Deploy‑Tokens  
- keine manuellen Schritte  
- keine direkten Deployments von Entwickler‑Laptops  
- Trennung von Build & Deploy  

---

# 🧱 Build‑Security

- isolierte Build‑Umgebungen  
- keine shared Runner für sensitive Projekte  
- Build‑Agenten ohne Internetzugang  
- Secrets aus Secret Store  
- SBOM erzeugen  
- Dependency Scanning  
- Container Scanning  
- signierte Builds (Sigstore/Cosign)  

---

# 🐳 Container Deployment Security

- minimalistische Base Images  
- keine Shell im Container  
- keine Secrets im Image  
- signierte Images  
- Image Policies (OPA/Gatekeeper)  
- Scanning vor Deployment  
- reproducible builds  
- Tag‑Pinning (keine „latest“)  

---

# ☸️ Kubernetes Deployment Security

- Admission Controller  
- Pod Security Standards  
- Network Policies  
- RBAC strikt  
- Secrets verschlüsseln  
- Resource Limits setzen  
- mTLS via Service Mesh  
- keine privilegierten Container  
- keine Host‑Mounts  
- Canary Deployments  
- Blue‑Green Deployments  

---

# 🔐 Secrets im Deployment

- niemals Secrets in Git  
- niemals Secrets in CI‑Logs  
- Secret Store verwenden  
- Rotation automatisieren  
- Secrets nicht als Env Vars loggen  
- Secrets nicht in Helm Charts speichern  

---

# 🧩 Deployment‑Pipelines (CI/CD)

### Pipeline‑Hardening
- least privilege für Pipeline‑Tokens  
- kein Zugriff auf Produktionsdaten  
- signierte Deployments  
- 4‑Augen‑Prinzip für kritische Deployments  
- Pipeline‑Isolation pro Projekt  
- Secrets Masking  
- keine Self‑Hosted Runner ohne Hardening  

### Deployment‑Checks
- Linting  
- Tests  
- Security Scans  
- Policy Checks  
- Infrastructure Scans (Terraform/K8s)  

---

# 🛡️ Zero‑Trust Deployment

- jede Aktion authentifizieren  
- jede Änderung signieren  
- jede Pipeline isolieren  
- jede Abhängigkeit scannen  
- jede Policy erzwingen  

---

# 🧭 Deployment Observability

Wichtige Signale:

- wer hat deployed  
- welche Version wurde deployed  
- welche Policies wurden verletzt  
- welche Images wurden verwendet  
- welche Secrets wurden geladen  
- ungewöhnliche Deployment‑Zeitpunkte  

---

# 🧪 Deployment Testing

- Canary Tests  
- Smoke Tests  
- Chaos Tests  
- Rollback Tests  
- Security Tests  
- Load Tests  

---

# 🧨 Deployment Anti‑Patterns

- Deployments von Entwickler‑Laptops  
- „latest“ Tags  
- Secrets im Repo  
- keine Tests  
- keine Scans  
- keine Signaturen  
- globale Admin‑Tokens  
- manuelle Deployments ohne Audit Trail  

---

## Pro-Tipp
Secure Deployment ist **Produktions‑Hygiene**: Je reproduzierbarer, signierter und kontrollierter ein Deployment ist, desto stabiler und sicherer bleibt die gesamte Plattform.
