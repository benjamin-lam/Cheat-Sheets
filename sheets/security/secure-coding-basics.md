---
title: Secure Coding Basics Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Secure Coding Basics: Grundprinzipien für sichere Softwareentwicklung

Dieses Sheet bündelt die wichtigsten Prinzipien, Patterns und Anti‑Patterns für sicheres Programmieren — ideal für APIs, Microservices, Backend‑Services, Frontends und Cloud‑Plattformen.

---

## ❓ Warum Secure Coding?
**Lösung:** die meisten Sicherheitslücken entstehen durch fehlerhaften Code, nicht durch fehlende Kryptografie.

Secure Coding verhindert:

- Injection  
- XSS  
- RCE  
- Datenlecks  
- Privilege Escalation  
- Supply‑Chain‑Angriffe  

Sicherheit beginnt im Code — nicht im Firewall‑Team.

---

# 🧱 Grundprinzipien

- **Validate Input**  
- **Encode Output**  
- **Least Privilege**  
- **Fail Securely**  
- **Secure Defaults**  
- **Defense in Depth**  
- **Don’t Trust the Client**  
- **Avoid Complexity**  

---

# 🧩 Input Validation

- Whitelisting statt Blacklisting  
- JSON Schema Validation  
- maximale Payload‑Größe  
- Content‑Type prüfen  
- keine freien Strings in Queries  
- Prepared Statements  
- Regex‑Validierung für IDs, Emails, etc.  

Beispiel (Node.js):

```js
if (!/^[a-zA-Z0-9_-]{1,32}$/.test(username)) {
  throw new Error("Invalid username");
}
```

---

# 🧼 Output Encoding

- HTML Encoding  
- JSON Encoding  
- URL Encoding  
- keine untrusted HTML‑Snippets  
- keine dynamischen Templates ohne Escaping  

Beispiel (Java):

```java
String safe = StringEscapeUtils.escapeHtml4(input);
```

---

# 🧨 Schutz vor Injection

- SQL → Prepared Statements  
- NoSQL → Operator‑Whitelisting  
- Command Injection → keine Shell‑Calls  
- Template Injection → sichere Template Engines  
- LDAP Injection → Escape + Filter  

Beispiel (SQL):

```sql
SELECT * FROM users WHERE id = ?
```

---

# 🔐 Passwort‑Sicherheit

- niemals Klartext  
- Hashing: bcrypt, scrypt, argon2  
- Salt + Pepper  
- Rate Limiting bei Login  
- MFA erzwingen  

---

# 🔑 Secrets im Code vermeiden

- keine Secrets in Git  
- keine Secrets in Config Files  
- Secret Store verwenden  
- Environment Variables nur mit Vorsicht  
- Secrets niemals loggen  

---

# 🧵 Fehlerbehandlung (Fail Securely)

- keine technischen Details im Fehler  
- keine Stacktraces an den Client  
- generische Fehlermeldungen  
- Logging ohne sensitive Daten  

Beispiel:

```json
{ "error": "invalid_request" }
```

---

# 🛡️ Schutz vor XSS

- Output Encoding  
- CSP (Content Security Policy)  
- keine untrusted HTML‑Snippets  
- keine eval()‑ähnlichen Funktionen  

---

# 🧯 Schutz vor CSRF

- SameSite=strict Cookies  
- CSRF‑Tokens für Web‑Forms  
- kein Cookie‑basiertes Auth in APIs  

---

# 🧱 Schutz vor SSRF

- URL‑Whitelisting  
- interne IP‑Ranges blockieren  
- Metadata‑Endpoints schützen  
- keine offenen Redirects  

---

# 🧰 Logging & Monitoring

- Login‑Versuche  
- Token‑Fehler  
- Policy‑Verstöße  
- ungewöhnliche IP‑Muster  
- Rate‑Limit‑Hits  
- keine sensiblen Daten loggen  

---

# 🧪 Secure Testing

- Static Code Analysis  
- Dependency Scanning  
- Secret Scanning  
- Fuzzing  
- Penetration Tests  
- Unit Tests für Validierung  

---

# 🧭 Anti‑Patterns

- `eval()`  
- dynamische SQL‑Strings  
- globale Admin‑Rollen  
- unbounded Arrays/Maps  
- unbounded Retries  
- unbounded Logging  
- Debug‑Endpoints in Produktion  
- Secrets im Code  

---

## Pro-Tipp
Secure Coding ist **Qualitätssicherung**: Je sauberer der Code, desto sicherer das System — Sicherheit ist ein Nebeneffekt guter Architektur.
