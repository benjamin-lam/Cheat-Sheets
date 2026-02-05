---
title: Cryptography Basics Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Cryptography Basics: sichere Verschlüsselung, Hashing & Schlüsselverwaltung

Dieses Sheet bündelt die wichtigsten kryptografischen Grundlagen — ideal für APIs, Microservices, Cloud‑Plattformen, Identity‑Systeme und Zero‑Trust‑Architekturen.

---

## ❓ Warum Kryptografie?
**Lösung:** Kryptografie schützt Daten — im Ruhezustand, in Bewegung und in Nutzung.

Sie verhindert:

- Datenlecks  
- Token‑Manipulation  
- Identitätsdiebstahl  
- Replay‑Angriffe  
- Man‑in‑the‑Middle  
- Credential Theft  

Kryptografie ist **Vertrauens‑Infrastruktur**.

---

# 🧱 Grundbegriffe

### Verschlüsselung
Daten werden unlesbar gemacht und können nur mit einem Schlüssel entschlüsselt werden.

### Hashing
Einweg‑Transformation, nicht umkehrbar.

### Signaturen
Beweisen Integrität und Authentizität.

### Schlüsselmanagement
Sichere Verwaltung kryptografischer Schlüssel.

---

# 🔐 Symmetrische Verschlüsselung

### Empfohlen
- AES‑256‑GCM  
- AES‑128‑GCM  

### Nicht empfohlen
- AES‑CBC ohne Auth  
- DES  
- 3DES  

### Eigenschaften
- ein Schlüssel für Ver- und Entschlüsselung  
- schnell  
- ideal für Datenverschlüsselung  

---

# 🔑 Asymmetrische Verschlüsselung

### Empfohlen
- RSA‑2048+  
- RSA‑3072  
- ECC (P‑256, P‑384)  
- Ed25519  

### Eigenschaften
- zwei Schlüssel: privat + öffentlich  
- ideal für Signaturen, TLS, Token‑Signierung  

---

# 🧩 Hashing

### Empfohlen
- SHA‑256  
- SHA‑3  
- BLAKE2  

### Nicht für Passwörter geeignet
- SHA‑256  
- SHA‑1  
- MD5  

### Eigenschaften
- nicht umkehrbar  
- ideal für Integrität  

---

# 🔐 Passwort‑Hashing

### Empfohlen
- argon2id  
- bcrypt  
- scrypt  

### Eigenschaften
- langsam  
- speicherintensiv  
- schützt vor Brute Force  

---

# 🛡️ Digitale Signaturen

### Empfohlen
- RSA‑PSS  
- Ed25519  
- ECDSA (P‑256)  

### Einsatzgebiete
- JWT Signaturen  
- Code Signing  
- Container Signing  
- TLS Handshake  

---

# 🔒 TLS / HTTPS

### Empfohlene Versionen
- TLS 1.2  
- TLS 1.3  

### Unsichere Versionen
- TLS 1.0  
- TLS 1.1  
- SSLv3  

### Empfohlene Cipher Suites
- TLS_AES_256_GCM_SHA384  
- TLS_CHACHA20_POLY1305_SHA256  

---

# 🧰 Key Management

### Grundregeln
- Keys niemals im Code  
- Keys niemals in Git  
- Secret Store verwenden  
- Rotation automatisieren  
- Zugriff über IAM  
- Keys nicht loggen  

### Key‑Lebenszyklus
- Erstellung  
- Speicherung  
- Nutzung  
- Rotation  
- Revocation  
- Löschung  

---

# 🧱 JWT Security

### Empfohlen
- RS256  
- ES256  
- EdDSA (Ed25519)  

### Nicht empfohlen
- HS256 für externe Clients  
- `alg=none`  

### Regeln
- Signatur prüfen  
- Issuer prüfen  
- Audience prüfen  
- kurze TTL  

---

# 🧯 Schutz vor Replay‑Angriffen

- Nonces  
- Token Binding  
- kurze TTL  
- mTLS  
- Signaturen mit Zeitstempeln  

---

# 🧪 Kryptografisches Testing

- TLS Scanner  
- JWT Manipulation Tests  
- Hash Collision Tests  
- Key Rotation Tests  
- Certificate Validation Tests  

Tools:

- testssl.sh  
- OpenSSL  
- OPA + Rego Policies  
- Burp Suite  

---

# 🧨 Kryptografie Anti‑Patterns

- eigene Kryptografie bauen  
- veraltete Algorithmen  
- statische Schlüssel  
- keine Rotation  
- Secrets im Code  
- JWT ohne Signatur  
- TLS ohne Zertifikatsprüfung  

---

## Pro-Tipp
Kryptografie ist **Sicherheits‑Fundament**: Moderne Algorithmen + sauberes Key‑Management + kurze TTLs = robuste, zukunftssichere Systeme.
