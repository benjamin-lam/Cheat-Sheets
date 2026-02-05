---
title: Zero Trust Architecture Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Zero Trust Architecture: „Never Trust, Always Verify“

Dieses Sheet bündelt die wichtigsten Prinzipien, Komponenten und Mechaniken einer Zero‑Trust‑Architektur — ideal für moderne Plattformen, Microservices, Cloud‑Infrastruktur und hochregulierte Umgebungen.

---

## ❓ Was ist Zero Trust?
**Lösung:** ein Sicherheitsmodell, das davon ausgeht, dass kein Netzwerk, kein Gerät und kein Benutzer vertrauenswürdig ist — weder intern noch extern.

Grundprinzipien:

1. **Verify Explicitly**  
2. **Least Privilege Access**  
3. **Assume Breach**  

Zero Trust ersetzt das alte Modell:

> „Inside = sicher, outside = gefährlich“

durch:

> „Alles ist potenziell kompromittiert.“

---

## ❓ Warum Zero Trust?
**Lösung:** moderne Systeme sind verteilt, dynamisch und ständig Angriffen ausgesetzt.

Zero Trust schützt vor:

- lateral movement  
- Credential Theft  
- Insider Threats  
- Supply‑Chain‑Angriffen  
- API‑Missbrauch  
- Cloud‑Fehlkonfigurationen  

---

## ❓ Was sind die Kernkomponenten?
**Lösung:** fünf Bausteine.

### 1. Identity
- Benutzeridentität  
- Serviceidentität  
- Maschinenidentität  
- MFA  
- OIDC / OAuth2  
- mTLS  

### 2. Device
- Geräte‑Compliance  
- Zertifikate  
- Endpoint Security  

### 3. Network
- Mikrosegmentierung  
- kein implizites Vertrauen  
- verschlüsselte Kommunikation  

### 4. Application
- AuthN + AuthZ pro Request  
- Policy Enforcement  
- API Security  

### 5. Data
- Verschlüsselung  
- Zugriffskontrolle  
- Data Classification  

---

## ❓ Wie sieht Zero‑Trust‑Traffic aus?
**Lösung:** jeder Request wird geprüft.

Beispiel:

```
Client → Gateway → AuthN → AuthZ → Policy Check → Service → Data
```

Keine Abkürzungen. Keine „trusted zones“.

---

## ❓ Wie funktioniert Service‑zu‑Service‑Security?
**Lösung:** Identität + Policy.

Mechanismen:

- mTLS  
- SPIFFE/SPIRE  
- OPA (Open Policy Agent)  
- Service Mesh (Istio, Linkerd)  

Regel:
- kein Service darf ohne Identität kommunizieren.

---

## ❓ Wie funktioniert Mikrosegmentierung?
**Lösung:** feingranulare Isolation.

Beispiele:

- pro Service eigenes Netzwerksegment  
- pro Namespace eigene Policies  
- pro API eigene AuthZ  

Ziel:
- Angriffe bleiben lokal.

---

## ❓ Wie funktioniert Least Privilege?
**Lösung:** minimaler Zugriff.

Regeln:

- kleinste mögliche Rechte  
- kurze Token‑Lebensdauer  
- keine globalen Admin‑Rollen  
- keine geteilten Secrets  

---

## ❓ Wie funktioniert Continuous Verification?
**Lösung:** Identität + Kontext + Risiko.

Beispiele:

- ungewöhnliche IP → zusätzliche MFA  
- neues Gerät → Blockierung  
- hoher Risk Score → eingeschränkter Zugriff  

---

## ❓ Wie funktioniert Policy Enforcement?
**Lösung:** deklarative Regeln.

Beispiel (OPA/Rego):

```rego
allow {
  input.user.role == "admin"
  input.resource.type == "invoice"
  input.action == "read"
}
```

Policies sind:

- zentral definiert  
- dezentral ausgeführt  

---

## ❓ Wie funktioniert Zero‑Trust in Microservices?
**Lösung:** AuthN + AuthZ + mTLS pro Request.

Regeln:

- kein interner Traffic ohne Identität  
- kein direkter Datenbankzugriff zwischen Services  
- Policies pro Service  
- Gateway validiert Tokens  

---

## ❓ Wie funktioniert Zero‑Trust in Kubernetes?
**Lösung:** Defense‑in‑Depth.

Mechanismen:

- Network Policies  
- Pod Security Standards  
- mTLS via Service Mesh  
- RBAC  
- Secret Encryption  
- Admission Controller  

---

## ❓ Wie funktioniert Zero‑Trust in APIs?
**Lösung:** AuthN + AuthZ + Rate Limiting.

Regeln:

- keine anonymen Requests  
- keine Session‑Cookies  
- Tokens mit kurzer TTL  
- Scopes pro Endpoint  

---

## ❓ Wie mache ich Observability in Zero Trust?
**Lösung:** Audit + Monitoring + Anomalieerkennung.

Wichtige Signale:

- Policy‑Verstöße  
- ungewöhnliche Token‑Nutzung  
- mTLS‑Fehler  
- Rate‑Limit‑Hits  
- ungewöhnliche IP‑Muster  

---

## ❓ Wie erkenne ich Zero‑Trust‑Probleme?
**Lösung:** typische Symptome.

- viele 403‑Fehler  
- Token‑Fehler  
- Zertifikatsprobleme  
- Policy‑Konflikte  
- Services können nicht miteinander sprechen  

---

## Pro-Tipp
Zero Trust ist **kein Produkt**, sondern ein **Architekturprinzip**: Es verändert, wie Systeme denken, kommunizieren und sich selbst schützen.
