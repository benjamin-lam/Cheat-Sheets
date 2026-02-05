---
title: Security Patterns Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Security Patterns: Zero‑Trust, Defense‑in‑Depth & Operational Hardening

Dieses Sheet bündelt die wichtigsten Security‑Mechaniken für moderne Plattformen — ideal für Microservices, APIs, Cloud‑Infrastruktur und verteilte Architekturen.

---

## ❓ Warum Security Patterns?
**Lösung:** Sicherheit ist kein Feature, sondern ein Systemverhalten.

Security Patterns schützen vor:

- Datenverlust  
- Account‑Übernahmen  
- Ransomware  
- Supply‑Chain‑Angriffen  
- API‑Missbrauch  
- Insider‑Risiken  

Security ist **Architektur**, nicht nur Kryptografie.

---

## ❓ Was ist Zero‑Trust?
**Lösung:** niemandem vertrauen — weder intern noch extern.

Grundprinzipien:

- **Verify Explicitly**  
- **Least Privilege Access**  
- **Assume Breach**  

Regeln:

- keine impliziten Vertrauenszonen  
- jede Anfrage authentifizieren  
- jede Aktion autorisieren  

---

## ❓ Was ist Defense‑in‑Depth?
**Lösung:** mehrere Schutzschichten.

Schichten:

- Netzwerk  
- Identität  
- API  
- Daten  
- Infrastruktur  
- Monitoring  

Je mehr Schichten, desto schwerer der Angriff.

---

## ❓ Welche Authentifizierungs‑Patterns gibt es?
**Lösung:** moderne Standards.

- OAuth2  
- OpenID Connect  
- JWT  
- mTLS  
- API Keys (für Maschinen)  

Regel:
- Menschen → OAuth2/OIDC  
- Maschinen → mTLS oder API Keys  

---

## ❓ Welche Autorisierungs‑Patterns gibt es?
**Lösung:** Rollen + Attribute.

- RBAC (Role‑Based Access Control)  
- ABAC (Attribute‑Based Access Control)  
- PBAC (Policy‑Based Access Control)  

Beispiel:

```
allow if user.role == "admin" and resource.owner == user.id
```

---

## ❓ Was ist Secrets‑Management?
**Lösung:** sichere Verwaltung sensibler Daten.

Regeln:

- niemals Secrets im Code  
- niemals Secrets in Git  
- Rotation automatisieren  
- Zugriff minimal halten  

Tools:

- HashiCorp Vault  
- AWS Secrets Manager  
- Azure Key Vault  

---

## ❓ Was ist API Security?
**Lösung:** Schutz der Schnittstellen.

Mechanismen:

- AuthN + AuthZ  
- Rate Limiting  
- Input Validation  
- Output Encoding  
- Schema Validation  
- Logging & Monitoring  

Regel:
- API ist die Angriffsfläche Nr. 1  

---

## ❓ Was ist Transport Security?
**Lösung:** sichere Kommunikation.

Regeln:

- TLS überall  
- TLS 1.2+  
- HSTS aktivieren  
- mTLS für interne Services  

---

## ❓ Was ist Data Security?
**Lösung:** Schutz gespeicherter Daten.

Mechanismen:

- Encryption at Rest  
- Encryption in Transit  
- Field‑Level Encryption  
- Tokenization  
- Hashing (bcrypt, argon2)  

---

## ❓ Was ist Input Validation?
**Lösung:** Schutz vor Injection.

Regeln:

- niemals Strings direkt in Queries  
- Prepared Statements  
- Schema Validation  
- Whitelisting statt Blacklisting  

---

## ❓ Was ist Output Encoding?
**Lösung:** Schutz vor XSS.

Beispiele:

- HTML Encoding  
- JSON Encoding  
- URL Encoding  

---

## ❓ Was ist Rate Limiting?
**Lösung:** Schutz vor Missbrauch.

Strategien:

- Token Bucket  
- Sliding Window  
- IP‑basiert  
- User‑basiert  
- API‑Key‑basiert  

---

## ❓ Was ist Threat Modeling?
**Lösung:** systematische Risikoanalyse.

Methoden:

- STRIDE  
- Attack Trees  
- Data Flow Diagrams  

Fragen:

- Was sind die Assets?  
- Wer sind die Angreifer?  
- Welche Angriffswege gibt es?  

---

## ❓ Was ist Security Logging?
**Lösung:** sicherheitsrelevante Ereignisse erfassen.

Beispiele:

- Login‑Versuche  
- Token‑Fehler  
- Policy‑Verstöße  
- Admin‑Aktionen  
- ungewöhnliche Requests  

Regel:
- Logs niemals sensitive Daten enthalten lassen  

---

## ❓ Was ist Security Monitoring?
**Lösung:** Angriffe erkennen.

Mechanismen:

- Anomaly Detection  
- SIEM  
- IDS/IPS  
- Alerting  

---

## ❓ Was ist Hardening?
**Lösung:** Angriffsfläche minimieren.

Beispiele:

- unnötige Ports schließen  
- unnötige Pakete entfernen  
- sichere Defaults  
- Read‑Only Filesystem  
- Non‑Root Containers  

---

## ❓ Was ist Supply‑Chain Security?
**Lösung:** Schutz vor Angriffen über Abhängigkeiten.

Mechanismen:

- SBOM (Software Bill of Materials)  
- Dependency Scanning  
- Signierte Container  
- Verified Builds  

---

## Pro-Tipp
Security ist **Konsequenz‑Management**: Du schützt nicht nur Systeme — du schützt die Fähigkeit, zuverlässig zu operieren.
