---
title: Supply Chain Security Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Supply Chain Security: Schutz vor Angriffen über Abhängigkeiten, Builds & Deployments

Dieses Sheet bündelt die wichtigsten Mechaniken zur Absicherung der Software‑Lieferkette — ideal für Microservices, CI/CD, Container, Cloud‑Plattformen und Open‑Source‑Ökosysteme.

---

## ❓ Was ist Supply Chain Security?
**Lösung:** Schutz vor Angriffen, die nicht direkt das eigene System angreifen, sondern die Komponenten, aus denen es besteht.

Angriffsflächen:

- Dependencies  
- Container Images  
- Build‑Systeme  
- CI/CD‑Pipelines  
- Package Registries  
- Entwickler‑Workstations  
- Secrets in Repos  

Supply‑Chain‑Angriffe sind **hochwirksam**, weil sie viele Systeme gleichzeitig kompromittieren.

---

## ❓ Warum ist Supply Chain Security wichtig?
**Lösung:** moderne Software ist ein Ökosystem aus Drittkomponenten.

Risiken:

- manipulierte Libraries  
- bösartige Updates  
- kompromittierte Build‑Server  
- gestohlene Signierschlüssel  
- Dependency Confusion  
- Typosquatting  

Ein einziger Angriff kann tausende Systeme treffen.

---

# 🧩 Dependency Security

- nur vertrauenswürdige Quellen  
- Versions‑Pinning (`package-lock.json`, `go.sum`, `Cargo.lock`)  
- keine „latest“ Versionen  
- regelmäßige Updates  
- Dependency Scanning (SCA)  
- SBOM erzeugen  
- keine unmaintained Libraries  

Tools:

- Dependabot  
- Snyk  
- Trivy  
- OWASP Dependency Check  

---

# 🐳 Container Supply Chain Security

- minimalistische Base Images  
- signierte Images (Cosign, Notary)  
- SBOM im Image  
- keine Secrets im Image  
- Scanning vor Deployment  
- reproduzierbare Builds  
- Image Policies (z. B. Gatekeeper)  

---

# 🧰 Build System Security

- isolierte Build‑Umgebungen  
- keine shared Runner für sensitive Projekte  
- Build‑Agenten ohne Internetzugang  
- signierte Artefakte  
- reproducible builds  
- Build‑Logs schützen  
- keine Secrets in Build‑Logs  

---

# 🚀 CI/CD Pipeline Security

- least privilege für Pipeline‑Tokens  
- Secrets aus Secret Store  
- kein Zugriff auf Produktionsdaten  
- signierte Deployments  
- 4‑Augen‑Prinzip für kritische Deployments  
- Pipeline‑Isolation pro Projekt  
- keine Self‑Hosted Runner ohne Hardening  

---

# 🔐 Signing & Verification

- Code Signing  
- Container Signing  
- Commit Signing (GPG, SSH)  
- Verified Commits erzwingen  
- Sigstore / Cosign für Container  
- Verifikation im Deployment erzwingen  

---

# 📦 Package Registry Security

- private Registries für interne Pakete  
- keine direkten Downloads aus dem Internet im Build  
- Dependency Confusion verhindern (Namespace‑Schutz)  
- Typosquatting vermeiden  
- Versions‑Freeze für kritische Komponenten  

---

# 🧱 Developer Workstation Security

- MFA überall  
- SSH Keys statt Passwörter  
- keine globalen Admin‑Rechte  
- Festplattenverschlüsselung  
- sichere Browser‑Extensions  
- isolierte Dev‑Container  
- keine Secrets lokal speichern  

---

# 🧪 Testing & Scanning

- Static Code Analysis  
- Dependency Scanning  
- Container Scanning  
- IaC Scanning (Terraform, Kubernetes)  
- Secret Scanning (GitLeaks, TruffleHog)  
- regelmäßige Penetration Tests  

---

# 🧭 SBOM (Software Bill of Materials)

Ein SBOM listet alle Komponenten eines Systems auf.

Vorteile:

- Transparenz  
- Compliance  
- schnelle Reaktion bei CVEs  
- reproduzierbare Builds  

Standards:

- SPDX  
- CycloneDX  

---

# 🛡️ Zero‑Trust für die Supply Chain

- jede Komponente verifizieren  
- jede Aktion authentifizieren  
- jede Pipeline isolieren  
- jede Abhängigkeit scannen  
- jede Änderung signieren  

---

## Pro-Tipp
Supply‑Chain‑Security ist **Vertrauens‑Management**: Du schützt nicht nur deinen Code — du schützt alles, worauf dein Code baut.
