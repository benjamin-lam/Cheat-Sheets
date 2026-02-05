---
title: Token Hardening Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Token Hardening: Schutz von Access Tokens, Refresh Tokens & API Tokens

Dieses Sheet bündelt die wichtigsten Mechaniken zur Absicherung von Tokens — ideal für OAuth2/OIDC, APIs, Microservices, Service‑zu‑Service‑Kommunikation und Zero‑Trust‑Architekturen.

---

## ❓ Warum Token Hardening?
**Lösung:** Tokens sind digitale Schlüssel — wer sie besitzt, ist der Benutzer oder der Service.

Angreifer zielen auf:

- Token Theft  
- Token Replay  
- Token Leakage  
- Token Manipulation  
- Token Misuse  

Token Hardening verhindert:

- Account‑Übernahmen  
- API‑Missbrauch  
- lateral movement  
- Service‑Impersonation  

---

# 🧱 Token‑Grundprinzipien

- kurze Lebensdauer  
- sichere Speicherung  
- Bindung an Kontext (IP/Device)  
- Rotation bei jeder Nutzung (Refresh Tokens)  
- keine sensiblen Daten im Token  
- Signatur immer prüfen  

---

# 🔐 Access Tokens

### Eigenschaften
- kurzlebig (5–15 Minuten)  
- stateless (JWT) oder stateful (opaque)  
- nur im Memory speichern  
- niemals im LocalStorage  
- niemals im Cookie  

### Schutzmechanismen
- Audience prüfen  
- Issuer prüfen  
- Signatur prüfen  
- Token Binding  
- Scope‑basierte Autorisierung  

---

# 🔄 Refresh Tokens

### Eigenschaften
- langlebiger (Stunden bis Tage)  
- hochsensibel  
- nur im HttpOnly Cookie  
- niemals im LocalStorage  
- niemals im JS‑Memory  

### Rotation
- bei jeder Nutzung rotieren  
- altes Token sofort invalidieren  
- Replay Detection aktivieren  

### Schutzmechanismen
- Device Binding  
- IP Binding  
- MFA bei riskanten Aktionen  

---

# 🧩 ID Tokens

### Eigenschaften
- Identitätsinformationen  
- nicht für Autorisierung  
- nicht für API‑Zugriffe  
- kurze TTL  

### Schutzmechanismen
- Signatur prüfen  
- Audience prüfen  
- keine sensiblen Daten im Payload  

---

# 🔑 API Keys

### Eigenschaften
- Maschinenidentität  
- statisch oder rotierbar  
- pro Service ein eigener Key  

### Schutzmechanismen
- kurze TTL  
- Rotation automatisieren  
- Scope‑basierte Rechte  
- Rate Limiting  
- niemals im Code  
- niemals in Logs  

---

# 🐳 Service‑zu‑Service Tokens

Mechanismen:

- mTLS  
- SPIFFE/SPIRE  
- OAuth2 Client Credentials  
- JWT mit kurzer TTL  

Regeln:

- kein Sharing von Tokens  
- kein globaler „service-admin“  
- Policies pro Service  

---

# 🧯 Schutz vor Token Theft

- keine Tokens im LocalStorage  
- keine Tokens in URLs  
- keine Tokens in HTML  
- keine Tokens in Logs  
- CSP aktivieren  
- HTTPS erzwingen  
- HttpOnly Cookies für Refresh Tokens  

---

# 🛡️ Schutz vor Token Replay

- Token Binding  
- Nonces  
- Rotation bei jeder Nutzung  
- Replay Detection im Auth Server  
- mTLS für Maschinen  

---

# 🧨 Schutz vor Token Manipulation

- Signatur prüfen  
- Algorithmus erzwingen (kein `alg=none`)  
- keine unsicheren Algorithmen (HS256 nur intern)  
- Key Rotation (JWKS)  

---

# 🧭 Token Monitoring

Wichtige Signale:

- ungewöhnliche Token‑Nutzung  
- viele 401/403  
- Refresh Token Missbrauch  
- parallele Sessions aus verschiedenen Ländern  
- Token‑Fehler im Gateway  
- mTLS‑Fehler  

---

# 🧪 Token Testing

- JWT Manipulation Tests  
- Token Replay Tests  
- Token Leakage Tests  
- OAuth2/OIDC Flow Tests  
- API Key Rotation Tests  
- mTLS Identity Tests  

---

# 🧱 Token Anti‑Patterns

- Tokens im LocalStorage  
- lange TTL  
- Refresh Tokens im JS‑Memory  
- Tokens in URLs  
- Tokens in Logs  
- globale API Keys  
- kein Token Binding  
- kein Rotation‑Mechanismus  

---

## Pro-Tipp
Token Hardening ist **Identitäts‑Resilienz**: Je kürzer, gebundener und besser geschützt ein Token ist, desto schwerer wird Missbrauch — und desto stabiler bleibt das gesamte System.
