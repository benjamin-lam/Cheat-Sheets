---
title: API Security Checklist
category: Security
last_updated: 2025-09-02
status: stable
---

# API Security Checklist: Absicherung moderner APIs & Microservices

Diese Checkliste bündelt die wichtigsten Sicherheitsmaßnahmen für APIs — ideal für Microservices, Gateways, Serverless‑Funktionen und Zero‑Trust‑Architekturen.

---

## 🔐 Authentifizierung (AuthN)

- keine anonymen Requests  
- OAuth2 / OIDC für Benutzer  
- mTLS oder API Keys für Maschinen  
- kurze Token‑Lebensdauer (5–15 Minuten)  
- Refresh Tokens sicher speichern  
- PKCE für Public Clients  
- keine Session‑Cookies in APIs  
- Token‑Signatur prüfen  
- Token‑Issuer & Audience prüfen  

---

## 🛂 Autorisierung (AuthZ)

- RBAC oder ABAC  
- Scopes pro Endpoint  
- Least Privilege Access  
- keine impliziten Admin‑Rechte  
- keine Cross‑Service‑Sessions  
- Policies zentral definieren, dezentral ausführen  
- Ressourcen‑basierte Autorisierung (z. B. `resource.owner == user.id`)  

---

## 🔑 Secrets Management

- keine Secrets im Code  
- keine Secrets in Git  
- Secret Store verwenden (Vault, AWS Secrets Manager)  
- automatische Rotation  
- kurze TTLs  
- Service‑spezifische Secrets  
- niemals Secrets in Logs  
- TLS‑Zertifikate regelmäßig erneuern  

---

## 🔒 Transport Security

- TLS überall  
- TLS 1.2+  
- HSTS aktivieren  
- mTLS für interne Services  
- sichere Cipher Suites  
- keine unverschlüsselten internen Netzwerke  

---

## 🧱 Input Validation

- Schema Validation (JSON Schema, OpenAPI)  
- Whitelisting statt Blacklisting  
- keine freien Strings in Queries  
- Prepared Statements  
- maximale Payload‑Größe begrenzen  
- Content‑Type prüfen  

---

## 🧼 Output Encoding

- HTML Encoding  
- JSON Encoding  
- URL Encoding  
- keine sensiblen Daten im Response Body  
- Fehlerseiten ohne technische Details  

---

## 🚦 Rate Limiting & Throttling

- Token Bucket oder Sliding Window  
- Limits pro User, IP, API Key  
- separate Limits für teure Endpoints  
- Retry‑After Header setzen  
- globale Limits im Gateway  

---

## 🧨 Schutz vor Injection

- SQL Injection → Prepared Statements  
- NoSQL Injection → Operator‑Whitelisting  
- Command Injection → keine Shell‑Calls  
- Template Injection → sichere Template Engines  
- LDAP Injection → Escape + Filter  

---

## 🛡️ Schutz vor XSS

- Output Encoding  
- CSP (Content Security Policy)  
- keine untrusted HTML‑Snippets  
- keine eval()‑ähnlichen Funktionen  

---

## 🧲 Schutz vor CSRF

APIs sind meist nicht betroffen, aber:

- bei Cookies → SameSite=strict  
- CSRF‑Tokens für Web‑Forms  
- kein Cookie‑basiertes Auth in APIs  

---

## 🧯 Schutz vor SSRF

- keine offenen Redirects  
- keine unvalidierten URLs  
- interne IP‑Ranges blockieren  
- Metadata‑Endpoints schützen (z. B. AWS 169.254.169.254)  

---

## 🧱 Schutz vor RCE

- keine dynamischen Code‑Ausführungen  
- keine Shell‑Kommandos  
- sichere Deserialisierung  
- keine untrusted Plugins  

---

## 🧵 Logging & Monitoring

- Login‑Versuche  
- Token‑Fehler  
- Policy‑Verstöße  
- ungewöhnliche IP‑Muster  
- Rate‑Limit‑Hits  
- mTLS‑Fehler  
- keine sensiblen Daten loggen  

---

## 🧭 API Design & Hardening

- nur HTTPS  
- OpenAPI/Swagger definieren  
- Versionierung (v1, v2)  
- Pagination erzwingen  
- maximale Request‑Größe  
- Response‑Caching für GET  
- Idempotency Keys für POST  
- keine unnötigen Endpoints  

---

## 🧪 Testing & Scanning

- automatisierte Security‑Tests  
- Dependency Scanning  
- Static Code Analysis  
- Dynamic API Scanning  
- Penetration Tests  
- Fuzzing  

---

## 🧰 Gateway Security

- AuthN im Gateway  
- Rate Limiting im Gateway  
- Schema Validation im Gateway  
- WAF (Web Application Firewall)  
- Canary Releases  
- mTLS Termination  

---

## 🧩 Microservices Security

- Service‑Identität (SPIFFE/SPIRE)  
- mTLS zwischen Services  
- Policies pro Service  
- keine direkten DB‑Zugriffe zwischen Services  
- Secrets pro Service  
- Zero‑Trust intern  

---

## Pro-Tipp
API‑Security ist **Angriffsflächen‑Management**: Je klarer Auth, Policies, Limits und Validierungen definiert sind, desto sicherer und stabiler wird die gesamte Plattform.
