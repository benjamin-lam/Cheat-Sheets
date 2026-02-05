---
title: Secrets Management Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Secrets Management: sichere Verwaltung von Tokens, Passwörtern & Schlüsseln

Dieses Sheet bündelt die wichtigsten Mechaniken für modernes Secrets‑Management — ideal für Microservices, Cloud‑Infrastruktur, CI/CD‑Pipelines und Zero‑Trust‑Architekturen.

---

## ❓ Warum Secrets Management?
**Lösung:** Secrets sind der Generalschlüssel zu Systemen.

Schlechte Verwaltung führt zu:

- Account‑Übernahmen  
- Datenlecks  
- Supply‑Chain‑Angriffen  
- Infrastruktur‑Kompromittierung  
- Compliance‑Verstößen  

Secrets müssen **zentralisiert, verschlüsselt, rotierbar und auditierbar** sein.

---

## ❓ Was sind Secrets?
**Lösung:** alles, was Zugang gewährt.

Beispiele:

- API Keys  
- Datenbank‑Passwörter  
- OAuth2 Client Secrets  
- JWT Signing Keys  
- SSH Keys  
- TLS Zertifikate  
- Encryption Keys  
- Cloud Credentials  

---

## ❓ Was sind die Grundprinzipien?
**Lösung:** vier Regeln.

1. **Never store secrets in code**  
2. **Never store secrets in Git**  
3. **Rotate secrets regularly**  
4. **Least Privilege Access**  

---

## ❓ Welche Tools gibt es?
**Lösung:** moderne Secret Stores.

### HashiCorp Vault
- dynamische Secrets  
- PKI  
- Leasing & Rotation  
- Audit Logs  

### AWS Secrets Manager
- automatische Rotation  
- IAM‑Integration  

### Azure Key Vault
- zentraler Secret Store  
- RBAC‑Integration  

### Kubernetes Secrets (mit Vorsicht)
- Base64 ≠ Verschlüsselung  
- nur mit Encryption‑at‑Rest + RBAC  

---

## ❓ Wie speichere ich Secrets sicher?
**Lösung:** verschlüsselt + zentral.

Regeln:

- Encryption at Rest  
- Encryption in Transit  
- Zugriff über IAM  
- niemals in Umgebungsvariablen loggen  
- niemals in Crash Dumps  

---

## ❓ Wie gebe ich Secrets an Services weiter?
**Lösung:** über sichere Mechanismen.

Optionen:

- Secret Injection (Sidecar)  
- Environment Variables (mit Vorsicht)  
- Filesystem Mounts  
- Service Mesh Identity  
- Vault Agent  

Regel:
- Secrets niemals im Container‑Image speichern  

---

## ❓ Wie mache ich Secret Rotation?
**Lösung:** automatisiert + ohne Downtime.

Strategien:

- regelmäßige Rotation (z. B. alle 30 Tage)  
- sofortige Rotation bei Verdacht  
- Blue‑Green Rotation (alt + neu parallel)  
- dynamische Secrets (Vault)  

---

## ❓ Was sind dynamische Secrets?
**Lösung:** kurzlebige, automatisch generierte Zugangsdaten.

Beispiele:

- DB‑Credentials mit TTL 1 Stunde  
- Cloud‑Credentials mit TTL 15 Minuten  

Vorteile:

- kein Leaken von Langzeit‑Secrets  
- automatische Revocation  
- Auditierbarkeit  

---

## ❓ Wie mache ich Secrets in CI/CD?
**Lösung:** niemals Secrets im Repo.

Regeln:

- Secret Store Integration  
- kein `echo $SECRET` in Logs  
- Masking aktivieren  
- Build‑Agent isolieren  
- kurzlebige Tokens verwenden  

---

## ❓ Wie mache ich Secrets in Kubernetes?
**Lösung:** Defense‑in‑Depth.

Regeln:

- Encryption at Rest aktivieren  
- RBAC strikt konfigurieren  
- Secrets nicht in ConfigMaps  
- Secret‑Mounts statt Env Vars  
- Service Account Token Projection  

---

## ❓ Wie mache ich Secrets in Microservices?
**Lösung:** pro Service eigene Secrets.

Regeln:

- keine globalen Secrets  
- kein Teilen von DB‑Passwörtern  
- kein Teilen von API Keys  
- Rotation pro Service  

---

## ❓ Wie mache ich Observability für Secrets?
**Lösung:** Audit Logs + Anomalieerkennung.

Wichtige Signale:

- ungewöhnliche Zugriffe  
- Zugriffe außerhalb der Arbeitszeit  
- fehlgeschlagene Zugriffe  
- plötzliche Rotation  
- Nutzung abgelaufener Tokens  

---

## ❓ Wie erkenne ich Secret‑Leaks?
**Lösung:** automatisierte Scans.

Tools:

- GitLeaks  
- TruffleHog  
- GitHub Secret Scanning  
- CI‑Scanner  

Symptome:

- unerwartete API‑Calls  
- ungewöhnliche IPs  
- plötzliche Kostenexplosion (Cloud)  

---

## Pro-Tipp
Secrets‑Management ist **Identitäts‑Hygiene**: Je kürzer die Lebensdauer, je klarer die Zugriffsregeln und je besser die Rotation, desto sicherer das Gesamtsystem.
