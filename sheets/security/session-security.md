---
title: Session Security Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Session Security: Schutz von Benutzer‑Sessions, Tokens & Anmeldezuständen

Dieses Sheet bündelt die wichtigsten Mechaniken zur Absicherung von Sessions — ideal für Web‑Apps, APIs, OAuth2/OIDC‑Flows und Zero‑Trust‑Architekturen.

---

## ❓ Warum Session Security?
**Lösung:** Sessions sind der direkte Zugang zum Benutzerkonto.

Angreifer zielen auf:

- Session Hijacking  
- Session Fixation  
- Token Theft  
- Cookie Theft  
- Replay Attacks  

Session Security verhindert:

- Account‑Übernahmen  
- Identitätsdiebstahl  
- Missbrauch von Tokens  
- unautorisierte Aktionen  

---

# 🧱 Session‑Grundprinzipien

- kurze Lebensdauer  
- sichere Speicherung  
- Bindung an Kontext (IP/Device)  
- Rotation bei Risiko  
- sofortige Invalidierung bei Logout  
- keine sensiblen Daten im Cookie  

---

# 🍪 Cookie‑Security

### Secure Flag
- Cookies nur über HTTPS senden

```
Set-Cookie: session=...; Secure
```

### HttpOnly Flag
- schützt vor JavaScript‑Zugriff (XSS)

```
Set-Cookie: session=...; HttpOnly
```

### SameSite
- schützt vor CSRF

Empfohlen:

```
SameSite=Strict
```

### Domain & Path
- Scope minimal halten

Beispiel:

```
Domain=example.com; Path=/app
```

---

# 🔐 Session‑Storage

### Niemals Sessions im LocalStorage
- anfällig für XSS  
- kein Schutz durch HttpOnly  

### Session Cookies bevorzugen
- sicherer  
- HttpOnly  
- SameSite  

### Memory Storage für SPAs
- Tokens im Memory halten  
- Refresh Token im HttpOnly Cookie  

---

# 🔄 Session Rotation

Wann rotieren?

- nach Login  
- nach Passwortänderung  
- nach Rollenänderung  
- nach verdächtigem Verhalten  
- regelmäßig (z. B. alle 15–30 Minuten)  

Ziel:
- gestohlene Sessions wertlos machen.

---

# 🧩 Token‑basierte Sessions (OAuth2/OIDC)

### Access Tokens
- kurze TTL (5–15 Minuten)  
- niemals im Cookie speichern  
- niemals im LocalStorage speichern  
- nur im Memory halten  

### Refresh Tokens
- im HttpOnly Cookie  
- Rotation bei jeder Nutzung  
- Bindung an Device/Session  

### ID Tokens
- nur für Identität  
- nicht für Autorisierung  

---

# 🛡️ Schutz vor Session Hijacking

- HTTPS überall  
- Secure + HttpOnly Cookies  
- kurze TTL  
- Session Binding (IP/Device/Fingerprint)  
- MFA  
- Token Replay Detection  
- CSP gegen XSS  

---

# 🧯 Schutz vor Session Fixation

- Session ID nach Login rotieren  
- keine Session IDs in URLs  
- keine Session IDs in GET‑Parametern  
- Session ID nur im Cookie  

---

# 🧨 Schutz vor Token Theft

- keine Tokens im LocalStorage  
- keine Tokens in Logs  
- keine Tokens in URLs  
- keine Tokens in HTML  
- CSP aktivieren  
- mTLS für Maschinen  

---

# 🧭 Session Monitoring

Wichtige Signale:

- parallele Sessions aus verschiedenen Ländern  
- viele Login‑Versuche  
- ungewöhnliche IP‑Wechsel  
- Refresh Token Missbrauch  
- lange Sessions ohne Aktivität  

---

# 🧪 Session Testing

- Session Fixation Tests  
- Token Replay Tests  
- Cookie Security Tests  
- XSS Tests  
- CSRF Tests  
- OAuth2/OIDC Flow Tests  

---

# 🧱 Session Anti‑Patterns

- Sessions im LocalStorage  
- lange Session‑TTL  
- keine Rotation  
- Session IDs in URLs  
- globale Admin‑Sessions  
- Refresh Tokens im JS‑Storage  
- Session‑Daten im Client speichern  

---

## Pro-Tipp
Session Security ist **Identitäts‑Resilienz**: Je kürzer, gebundener und besser geschützt eine Session ist, desto schwerer wird Account‑Übernahme — und desto stabiler bleibt das System.
