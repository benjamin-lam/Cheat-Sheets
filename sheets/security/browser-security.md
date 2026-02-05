---
title: Browser Security Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Browser Security: Schutz vor XSS, CSRF, Clickjacking & Datenlecks

Dieses Sheet bündelt die wichtigsten Mechaniken zur Absicherung von Browser‑basierten Anwendungen — ideal für Web‑Apps, SPAs, PWAs, OAuth2/OIDC‑Flows und API‑Frontends.

---

## ❓ Warum Browser Security?
**Lösung:** Der Browser ist der gefährlichste Ausführungsort im gesamten System.

Angreifer nutzen:

- XSS  
- CSRF  
- Clickjacking  
- Token Theft  
- Session Hijacking  
- Browser‑APIs  
- unsichere CORS‑Konfigurationen  

Browser Security schützt:

- Benutzerkonten  
- Sessions  
- Tokens  
- persönliche Daten  
- Unternehmensdaten  

---

# 🧱 Grundprinzipien

- **Don’t trust the client**  
- **Output Encoding**  
- **Content Security Policy (CSP)**  
- **Secure Cookies**  
- **No Tokens in LocalStorage**  
- **Least Privilege für Browser‑APIs**  
- **Keine Inline‑Scripts**  

---

# 🛡️ Schutz vor XSS

### Output Encoding
- HTML Encoding  
- JSON Encoding  
- URL Encoding  

### CSP (Content Security Policy)
Empfohlen:

```
Content-Security-Policy: default-src 'self'; script-src 'self'; object-src 'none'
```

### Weitere Maßnahmen
- keine Inline‑Scripts  
- keine eval()‑ähnlichen Funktionen  
- DOMPurify für HTML‑Sanitizing  
- keine untrusted HTML‑Snippets  

---

# 🧯 Schutz vor CSRF

### SameSite Cookies
```
SameSite=Strict
```

### CSRF‑Tokens
- für klassische Web‑Forms  
- nicht für APIs mit Bearer Tokens  

### Kein Cookie‑basiertes Auth in APIs
- stattdessen OAuth2/OIDC + PKCE  

---

# 🪟 Schutz vor Clickjacking

### X-Frame-Options
```
X-Frame-Options: DENY
```

### oder CSP Frame Ancestors
```
Content-Security-Policy: frame-ancestors 'none'
```

---

# 🔐 Schutz vor Token Theft

### Niemals Tokens im LocalStorage
- anfällig für XSS  
- kein HttpOnly Schutz  

### Access Tokens
- nur im Memory halten  

### Refresh Tokens
- im HttpOnly Cookie  
- Rotation bei jeder Nutzung  

### Weitere Maßnahmen
- HTTPS überall  
- CSP aktivieren  
- keine Tokens in URLs  
- keine Tokens in HTML  

---

# 🧩 CORS Security

### Grundregeln
- niemals `Access-Control-Allow-Origin: *` bei Auth  
- nur spezifische Domains erlauben  
- nur benötigte Methoden erlauben  
- nur benötigte Header erlauben  

### Beispiel
```
Access-Control-Allow-Origin: https://app.example.com
Access-Control-Allow-Methods: GET, POST
Access-Control-Allow-Headers: Authorization, Content-Type
```

---

# 🧰 Browser API Hardening

### Permissions-Policy
```
Permissions-Policy: geolocation=(), microphone=(), camera=()
```

### Deaktivieren, was nicht gebraucht wird
- Kamera  
- Mikrofon  
- Geolocation  
- Payment API  
- USB API  
- Bluetooth API  

---

# 🧭 Cookie Security

- `Secure` Flag  
- `HttpOnly` Flag  
- `SameSite=Strict`  
- Domain & Path minimal halten  
- kurze TTL  

Beispiel:

```
Set-Cookie: refresh=...; HttpOnly; Secure; SameSite=Strict; Path=/auth
```

---

# 🧪 Browser Security Testing

- XSS Tests  
- CSRF Tests  
- Clickjacking Tests  
- CSP Tests  
- CORS Tests  
- Token Leakage Tests  
- OAuth2/OIDC Flow Tests  

Tools:

- Burp Suite  
- OWASP ZAP  
- CSP Evaluator  
- SecurityHeaders.com  

---

# 🧨 Browser Security Anti‑Patterns

- Tokens im LocalStorage  
- Inline‑Scripts  
- eval()  
- `Access-Control-Allow-Origin: *`  
- Cookies ohne HttpOnly  
- Cookies ohne SameSite  
- keine CSP  
- keine X-Frame-Options  
- Tokens in URLs  

---

## Pro-Tipp
Browser Security ist **Client‑seitige Resilienz**: Je weniger der Browser darf und je strenger die Policies sind, desto schwerer wird XSS, CSRF und Token Theft — und desto sicherer bleibt die gesamte Anwendung.
