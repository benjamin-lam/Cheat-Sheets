---
title: AuthN & AuthZ Patterns Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Authentifizierung & Autorisierung: Moderne Patterns für sichere Systeme

Dieses Sheet bündelt die wichtigsten Mechaniken für Authentifizierung (AuthN) und Autorisierung (AuthZ) — ideal für APIs, Microservices, Plattformen und Zero‑Trust‑Architekturen.

---

## ❓ Was ist Authentifizierung (AuthN)?
**Lösung:** Wer bist du?

Mechanismen:

- Passwörter (mit Hashing)  
- Multi‑Factor Authentication (MFA)  
- OAuth2 / OpenID Connect  
- JWT  
- mTLS  
- API Keys (für Maschinen)  

Regel:
- Menschen → OAuth2/OIDC  
- Maschinen → mTLS oder API Keys  

---

## ❓ Was ist Autorisierung (AuthZ)?
**Lösung:** Was darfst du?

Mechanismen:

- RBAC (Role‑Based Access Control)  
- ABAC (Attribute‑Based Access Control)  
- PBAC (Policy‑Based Access Control)  
- ACLs (Access Control Lists)  

Beispiel:

```
allow if user.role == "admin" and resource.owner == user.id
```

---

## ❓ Welche AuthN‑Patterns gibt es?
**Lösung:** moderne Standards.

### OAuth2
- Delegierte Autorisierung  
- Access Tokens  
- Refresh Tokens  

### OpenID Connect
- Identitätsschicht über OAuth2  
- ID Token (JWT)  

### JWT
- selbstenthaltende Tokens  
- schnell validierbar  
- kein zentraler Speicher nötig  

### mTLS
- Maschinenidentität  
- Zertifikate statt Passwörter  

### API Keys
- einfache Maschinen‑Authentifizierung  
- rotierbar  
- eingeschränkte Rechte  

---

## ❓ Welche AuthZ‑Patterns gibt es?
**Lösung:** drei Ebenen.

### RBAC
- Rollen definieren Rechte  
- einfach, aber grob  

### ABAC
- Attribute definieren Rechte  
- flexibel, aber komplex  

### PBAC
- Policies definieren Rechte  
- deklarativ  
- ideal für Zero‑Trust  

Beispiel (OPA/Rego):

```rego
allow {
  input.user.role == "admin"
  input.resource.type == "invoice"
}
```

---

## ❓ Wie funktioniert Token‑Design?
**Lösung:** minimal + sicher.

Regeln:

- keine sensiblen Daten im Token  
- kurze TTLs  
- Signatur prüfen  
- Audience prüfen  
- Issuer prüfen  

Beispiel JWT Claims:

```
sub: "user-42"
aud: "api.example.com"
exp: 1693651200
```

---

## ❓ Wie mache ich Token‑Rotation?
**Lösung:** kurze Lebensdauer + Refresh Tokens.

Strategien:

- Access Token: 5–15 Minuten  
- Refresh Token: 1–30 Tage  
- automatische Rotation  
- sofortige Invalidierung bei Logout  

---

## ❓ Wie mache ich Maschinen‑Authentifizierung?
**Lösung:** mTLS oder API Keys.

mTLS:
- höchste Sicherheit  
- Zertifikate rotieren  

API Keys:
- einfach  
- eingeschränkte Rechte  
- rotierbar  

Regel:
- interne Services → mTLS  
- externe Integrationen → API Keys  

---

## ❓ Wie mache ich Service‑zu‑Service‑Auth?
**Lösung:** Zero‑Trust intern.

Mechanismen:

- mTLS  
- SPIFFE/SPIRE  
- Service Identity  
- OPA Policies  

Regel:
- kein „trusted internal network“  

---

## ❓ Wie mache ich Auth in Microservices?
**Lösung:** zentrale AuthN, dezentrale AuthZ.

- AuthN im Gateway  
- AuthZ im Service  
- Claims weiterreichen  
- keine Cross‑Service‑Sessions  

---

## ❓ Wie mache ich Auth in APIs?
**Lösung:** klare Standards.

- Bearer Tokens  
- OAuth2 Scopes  
- API Keys  
- mTLS  

Regel:
- niemals Session‑Cookies in APIs  

---

## ❓ Wie mache ich Auth in Frontends?
**Lösung:** OIDC + PKCE.

Mechanismus:

- Authorization Code Flow + PKCE  
- Tokens im Memory Storage  
- kein LocalStorage für Tokens  

---

## ❓ Wie mache ich Observability für Auth?
**Lösung:** Security‑relevante Signale.

Wichtige Metriken:

- Login‑Versuche  
- Token‑Fehler  
- Policy‑Verstöße  
- ungewöhnliche IPs  
- Rate‑Limit‑Hits  

---

## ❓ Wie erkenne ich Auth‑Probleme?
**Lösung:** typische Symptome.

- viele 401/403  
- viele Token‑Fehler  
- hohe Login‑Fehlerrate  
- ungewöhnliche Traffic‑Spitzen  
- abgelaufene Zertifikate  

---

## Pro-Tipp
AuthN & AuthZ sind **Identitäts‑Architektur**: Je klarer Identitäten, Tokens und Policies definiert sind, desto sicherer und kontrollierbarer wird das Gesamtsystem.
