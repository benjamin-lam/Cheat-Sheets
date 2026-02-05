---
title: Data Protection Basics Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Data Protection Basics: Schutz sensibler Daten im gesamten Lebenszyklus

Dieses Sheet bündelt die wichtigsten Mechaniken für Datenschutz und Datensicherheit — ideal für APIs, Microservices, Cloud‑Plattformen, Datenbanken, Logs und Zero‑Trust‑Architekturen.

---

## ❓ Warum Data Protection?
**Lösung:** Daten sind das wertvollste Gut — und der häufigste Angriffspunkt.

Angreifer nutzen:

- unverschlüsselte Daten  
- offene Datenbanken  
- unsichere Backups  
- Fehlkonfigurationen  
- Datenexfiltration über APIs  
- Logs mit sensiblen Informationen  

Data Protection verhindert:

- Datenlecks  
- Compliance‑Verstöße  
- Identitätsdiebstahl  
- Reputationsschäden  
- rechtliche Konsequenzen  

---

# 🧱 Grundprinzipien

- **Data Minimization**  
- **Least Privilege**  
- **Encryption Everywhere**  
- **Secure Defaults**  
- **Need‑to‑Know Access**  
- **Zero Trust für Daten**  

---

# 🔐 Verschlüsselung

### At Rest
- AES‑256‑GCM  
- Cloud‑native Encryption (AWS KMS, Azure Key Vault, GCP KMS)  
- Datenbanken verschlüsseln  
- Backups verschlüsseln  

### In Transit
- TLS 1.2+  
- mTLS intern  
- keine unverschlüsselten Protokolle  

---

# 🧩 Datenklassifikation

### Kategorien
- öffentlich  
- intern  
- vertraulich  
- streng vertraulich  

### Regeln
- je höher die Sensitivität, desto strenger die Controls  
- Klassifikation automatisieren, wo möglich  

---

# 🗄️ Datenbanken

- TLS aktivieren  
- least privilege Accounts  
- keine shared DB‑User  
- Audit Logs aktivieren  
- Query Limits  
- keine öffentlichen Endpoints  
- automatische Backups  
- Verschlüsselung at Rest  

---

# 🧰 API‑basierte Datenzugriffe

- nur benötigte Felder zurückgeben  
- keine internen IDs  
- keine sensiblen Metadaten  
- Schema Validation  
- Rate Limiting  
- Logging ohne PII  

---

# 🧼 Datenminimierung

- nur speichern, was wirklich nötig ist  
- keine Debug‑Daten in Produktion  
- keine vollständigen Payloads loggen  
- Pseudonymisierung, wo möglich  
- Anonymisierung für Analytics  

---

# 🧯 Schutz vor Datenexfiltration

- Rate Limiting  
- IP‑Restriktionen  
- Geo‑Blocking  
- DLP (Data Loss Prevention)  
- API Gateway Logging  
- ungewöhnliche Download‑Muster erkennen  

---

# 🧱 Backups & Snapshots

- verschlüsseln  
- Zugriff minimal halten  
- Offsite‑Backups  
- Restore‑Tests regelmäßig  
- keine Produktionsdaten in Testumgebungen  

---

# ☁️ Cloud Data Protection

AWS:
- S3 Block Public Access  
- KMS Encryption  
- IAM least privilege  
- Macie für PII‑Erkennung  

Azure:
- Storage Encryption  
- Key Vault  
- Defender for Cloud  
- Private Endpoints  

GCP:
- CMEK  
- VPC Service Controls  
- Cloud DLP  
- IAM Conditions  

---

# 🧭 Logging & PII‑Schutz

### Nicht loggen
- Passwörter  
- Tokens  
- Secrets  
- personenbezogene Daten  
- vollständige Payloads  

### Log‑Hygiene
- Masking  
- Hashing  
- Truncation  
- strukturierte Logs  

---

# 🧪 Data Protection Testing

- DLP Tests  
- Pseudonymisierung prüfen  
- Backup Restore Tests  
- API Data Leakage Tests  
- Cloud Storage Exposure Tests  
- Penetration Tests  

---

# 🧨 Data Protection Anti‑Patterns

- unverschlüsselte Datenbanken  
- öffentliche Buckets  
- Logs mit PII  
- Debug‑Daten in Produktion  
- keine Backups  
- keine Restore‑Tests  
- Produktionsdaten in Dev/Test  

---

## Pro-Tipp
Data Protection ist **Daten‑Resilienz**: Wer Daten minimiert, verschlüsselt, segmentiert und überwacht, verhindert die meisten realen Sicherheitsvorfälle — bevor sie entstehen.
