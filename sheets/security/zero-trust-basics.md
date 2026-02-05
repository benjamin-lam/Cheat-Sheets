---
title: Zero Trust Basics Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Zero Trust Basics: Sicherheit ohne implizites Vertrauen

Dieses Sheet bündelt die wichtigsten Mechaniken des Zero‑Trust‑Modells — ideal für APIs, Microservices, Cloud‑Plattformen, Identitätssysteme, Remote‑Arbeit und moderne Unternehmensarchitekturen.

---

## ❓ Warum Zero Trust?
**Lösung:** „Intern ist sicher“ war einmal — moderne Angriffe kommen von außen, innen, über Geräte, über Sessions oder über kompromittierte Identitäten.

Zero Trust verhindert:

- lateral movement  
- Missbrauch interner Netzwerke  
- Session Hijacking  
- Identitätsdiebstahl  
- unautorisierte Zugriffe  
- Datenexfiltration  

Zero Trust ist **Identitäts‑ und Kontext‑basierte Sicherheit**.

---

# 🧱 Die 3 Grundprinzipien von Zero Trust

### 1. **Never trust, always verify**
Jede Anfrage wird geprüft — unabhängig von Netzwerk, Gerät oder Standort.

### 2. **Least privilege access**
Nur minimal notwendige Rechte, dynamisch angepasst.

### 3. **Assume breach**
Systeme werden so gebaut, als wäre der Angreifer bereits drin.

---

# 🔐 Identitäts‑Zentrierung

Zero Trust basiert auf Identität, nicht auf Netzwerkgrenzen.

### Regeln
- MFA überall  
- starke Authentifizierung  
- kurze Token‑TTL  
- Device Binding  
- Rollen & Scopes minimal halten  

### Identitätstypen
- Benutzer  
- Services  
- Maschinen  
- Workloads  
- Container  
- Serverless Functions  

---

# 🧩 Kontext‑basierte Entscheidungen

Zugriff hängt ab von:

- Identität  
- Gerät  
- Standort  
- Risiko  
- Verhalten  
- Sensitivität der Daten  

Beispiel:
- Zugriff erlaubt nur, wenn MFA + vertrauenswürdiges Gerät + bekannte IP + niedrige Risiko‑Signale.

---

# 🛡️ Netzwerk‑Unabhängigkeit

Zero Trust bedeutet:

- kein implizites Vertrauen in interne Netzwerke  
- Mikrosegmentierung  
- mTLS zwischen Services  
- API‑Gateways statt flacher Netzwerke  
- keine offenen internen Ports  

---

# 🐳 Zero Trust für Microservices

- mTLS für jeden Request  
- Service‑Identitäten (SPIFFE/SPIRE)  
- Policies pro Service  
- kein Sharing von Tokens  
- kein „Service‑Admin“  

---

# ☸️ Zero Trust für Kubernetes

- Network Policies  
- Pod Security Standards  
- Admission Controller  
- RBAC strikt  
- Secrets verschlüsseln  
- Service Mesh für mTLS  

---

# ☁️ Zero Trust in der Cloud

AWS:
- IAM least privilege  
- Conditional Access  
- Private Endpoints  
- SCPs  

Azure:
- Conditional Access  
- PIM  
- Managed Identities  
- NSGs minimal  

GCP:
- IAM Conditions  
- VPC Service Controls  
- Workload Identity  

---

# 🔐 Zero Trust für APIs

- OAuth2/OIDC  
- kurze TTL  
- Audience prüfen  
- Signatur prüfen  
- Rate Limiting  
- Schema Validation  
- keine anonymen Endpoints  

---

# 🧰 Zero Trust für Endpoints

- Device Compliance  
- EDR/XDR  
- Festplattenverschlüsselung  
- Browser‑Isolation  
- keine lokalen Admins  
- Remote‑Wipe  

---

# 🧭 Monitoring & Telemetrie

Zero Trust braucht Sichtbarkeit:

- Auth Events  
- Token‑Nutzung  
- Policy‑Verstöße  
- Netzwerk‑Anomalien  
- API‑Missbrauch  
- Cloud Activity Logs  

---

# 🧪 Zero Trust Testing

- Policy Tests  
- mTLS Tests  
- Token Replay Tests  
- Identity Abuse Simulation  
- Lateral Movement Simulation  
- Cloud IAM Audit  

---

# 🧨 Zero Trust Anti‑Patterns

- „intern ist sicher“  
- VPN als einzige Schutzmaßnahme  
- globale Admin‑Rollen  
- lange Token‑TTL  
- keine Device Compliance  
- keine Network Policies  
- keine MFA  

---

## Pro-Tipp
Zero Trust ist **dynamische Zugriffskontrolle**: Wer Identität, Kontext und Policies kombiniert, eliminiert implizites Vertrauen — und macht Angriffe extrem schwer.
