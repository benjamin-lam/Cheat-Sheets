---
title: API Security Essentials Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# API Security Essentials: Schutz von Schnittstellen, Daten & Identitäten

Dieses Sheet bündelt die wichtigsten Mechaniken für sichere APIs — ideal für Microservices, Gateways, Cloud‑Plattformen, Mobile‑Backends und Zero‑Trust‑Architekturen.

---

## ❓ Warum API Security?
**Lösung:** APIs sind die häufigste Angriffsfläche moderner Systeme.

Angreifer nutzen:

- fehlende Authentifizierung  
- schwache Autorisierung  
- Injection  
- unsichere Defaults  
- Rate‑Limit‑Lücken  
- Datenexfiltration über Endpoints  

API Security verhindert:

- Account‑Übernahmen  
- Datenlecks  
- RCE  
- Privilege Escalation  
- API‑Missbrauch  

---

# 🧱 Grundprinzipien

- **Authenticate everything**  
- **Authorize every action**  
- **Validate every input**  
- **Expose minimal data**  
- **Rate limit everything**  
- **Log sicherheitsrelevante Ereignisse**  
- **Keine impliziten Vertrauenszonen**  

---

# 🔐 Authentifizierung

### Empfohlen
- OAuth2 / OIDC  
- mTLS für Maschinen  
- API Keys nur für Service‑Identitäten  

### Nicht empfohlen
- Basic Auth  
- statische Tokens  
- Session Cookies für APIs  

### Regeln
- kurze TTL  
- Signatur prüfen  
- Audience prüfen  
- Issuer prüfen  

---

# 🛡️ Autorisierung

### Prinzipien
- least privilege  
- Scope‑basierte Rechte  
- keine globalen Admin‑Rollen  
- keine impliziten Rechte  

### Beispiele
- `read:orders`  
- `write:orders`  
- `admin:orders`  

---

# 🧩 Input Validation

- JSON Schema Validation  
- Typ‑Validierung  
- maximale Payload‑Größe  
- Content‑Type prüfen  
- keine freien Strings in Queries  
- Prepared Statements  

---

# 🧼 Output Hardening

- keine sensiblen Daten im Response  
- PII minimieren  
- Fehler generisch halten  
- keine Stacktraces  
- Output Encoding  

---

# 🧯 Schutz vor Injection

- SQL → Prepared Statements  
- NoSQL → Operator‑Whitelisting  
- Command Injection → keine Shell‑Calls  
- Template Injection → sichere Engines  
- LDAP Injection → Escape + Filter  

---

# 🛑 Rate Limiting & Throttling

### Mechanismen
- globales Rate Limiting  
- pro IP  
- pro Token  
- pro Endpoint  
- Burst‑Limits  

### Ziele
- API‑Missbrauch verhindern  
- Bots drosseln  
- DoS‑Risiken reduzieren  

---

# 🧱 API Gateway Security

- AuthN/AuthZ zentral  
- Rate Limiting  
- Logging  
- mTLS  
- Schema Validation  
- WAF Integration  
- IP‑Allow/Deny Lists  

---

# 🧰 CORS Security

### Regeln
- niemals `*` bei Auth  
- nur spezifische Domains  
- nur benötigte Methoden  
- nur benötigte Header  

### Beispiel
```
Access-Control-Allow-Origin: https://app.example.com
Access-Control-Allow-Methods: GET, POST
Access-Control-Allow-Headers: Authorization, Content-Type
```

---

# 🧭 Daten‑Minimierung

- nur benötigte Felder zurückgeben  
- keine internen IDs  
- keine Debug‑Infos  
- keine sensiblen Metadaten  

---

# 🧪 API Security Testing

- OWASP API Top 10  
- Fuzzing  
- Auth Tests  
- Rate Limit Tests  
- Injection Tests  
- Broken Object Level Authorization (BOLA) Tests  
- Broken Function Level Authorization (BFLA) Tests  

Tools:

- Burp Suite  
- OWASP ZAP  
- Postman Tests  
- Schemathesis  

---

# 🧨 API Security Anti‑Patterns

- keine Auth  
- globale Admin‑Tokens  
- Tokens im LocalStorage  
- keine Rate Limits  
- Debug‑Endpoints in Produktion  
- unvalidierte Payloads  
- CORS `*`  
- sensible Daten im Response  

---

## Pro-Tipp
API Security ist **Schnittstellen‑Resilienz**: Wer Auth, Autorisierung, Validierung und Rate Limits sauber kombiniert, eliminiert 90 % aller realen API‑Angriffe.
