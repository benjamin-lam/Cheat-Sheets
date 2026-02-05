---
title: Security Headers Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Security Headers: Schutzschicht für Browser, APIs & Web‑Apps

Dieses Sheet bündelt die wichtigsten HTTP‑Security‑Header — ideal für Web‑Apps, APIs, Gateways, Reverse Proxies und CDN‑Konfigurationen.

---

## ❓ Warum Security Headers?
**Lösung:** Browser‑basierte Angriffe verhindern, bevor sie entstehen.

Security Headers schützen vor:

- XSS  
- Clickjacking  
- MIME‑Sniffing  
- Mixed Content  
- unsicheren Verbindungen  
- Datenlecks  

Security Headers sind **Low‑Effort, High‑Impact**.

---

# 🧱 Content-Security-Policy (CSP)

Der wichtigste Header gegen XSS.

Beispiel:

```
Content-Security-Policy: default-src 'self'; script-src 'self'; object-src 'none'
```

Regeln:

- `default-src 'self'`  
- keine Inline‑Scripts (`'unsafe-inline'` vermeiden)  
- keine eval‑ähnlichen Funktionen  
- Domains whitelisten  
- Reporting aktivieren  

---

# 🛡️ Strict-Transport-Security (HSTS)

Erzwingt HTTPS.

Beispiel:

```
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
```

Regeln:

- mindestens 1 Jahr  
- Subdomains einschließen  
- Preload optional  

---

# 🧯 X-Content-Type-Options

Verhindert MIME‑Sniffing.

```
X-Content-Type-Options: nosniff
```

Pflicht für:

- APIs  
- statische Assets  
- Downloads  

---

# 🪟 X-Frame-Options

Schützt vor Clickjacking.

```
X-Frame-Options: DENY
```

Optionen:

- `DENY`  
- `SAMEORIGIN`  

---

# 🧼 Referrer-Policy

Kontrolliert, welche Referrer‑Daten gesendet werden.

Empfohlen:

```
Referrer-Policy: strict-origin-when-cross-origin
```

---

# 🧩 Permissions-Policy

Kontrolliert Browser‑APIs.

Beispiel:

```
Permissions-Policy: geolocation=(), microphone=(), camera=()
```

Regeln:

- alles deaktivieren, was nicht benötigt wird  
- granular aktivieren  

---

# 🧰 Cross-Origin Resource Sharing (CORS)

Regelt, wer auf die API zugreifen darf.

Beispiel:

```
Access-Control-Allow-Origin: https://example.com
```

Regeln:

- niemals `*` für APIs mit Auth  
- nur spezifische Domains erlauben  
- nur benötigte Methoden erlauben  

---

# 🔐 Cross-Origin-Opener-Policy (COOP)

Schützt vor Cross‑Window‑Angriffen.

```
Cross-Origin-Opener-Policy: same-origin
```

---

# 🔒 Cross-Origin-Embedder-Policy (COEP)

Schützt vor unsicheren eingebetteten Ressourcen.

```
Cross-Origin-Embedder-Policy: require-corp
```

---

# 🧱 Cross-Origin-Resource-Policy (CORP)

Verhindert ungewolltes Einbetten.

```
Cross-Origin-Resource-Policy: same-origin
```

---

# 🧭 Cache-Control

Schützt sensible Daten.

Beispiel für APIs:

```
Cache-Control: no-store
```

Beispiel für statische Assets:

```
Cache-Control: public, max-age=31536000, immutable
```

---

# 🧪 Beispiel‑Header‑Set für APIs

```
Strict-Transport-Security: max-age=63072000; includeSubDomains
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Content-Security-Policy: default-src 'none'
Permissions-Policy: geolocation=(), microphone=(), camera=()
Cache-Control: no-store
```

---

# 🧪 Beispiel‑Header‑Set für Web‑Apps

```
Strict-Transport-Security: max-age=63072000; includeSubDomains
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Content-Security-Policy: default-src 'self'
Permissions-Policy: geolocation=(), microphone=(), camera=()
```

---

## Pro-Tipp
Security‑Header sind **Browser‑Firewalls**: Sie schützen dort, wo Code ausgeführt wird — im Browser deiner Nutzer.
