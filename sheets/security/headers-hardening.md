---
title: HTTP Security Headers Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# HTTP Security Headers: Hardening für moderne Web‑Apps

Dieses Sheet zeigt die wichtigsten Security‑Header, um Browser‑Angriffsflächen zu reduzieren und Standards wie OWASP ASVS einzuhalten.

---

## ❓ Wie verhindere ich MIME‑Sniffing?
**Lösung:** Browser dürfen den MIME‑Type nicht raten.

```http
X-Content-Type-Options: nosniff
```

---

## ❓ Wie verhindere ich Clickjacking?
**Lösung:** Seite darf nicht in fremden Frames geladen werden.

```http
X-Frame-Options: SAMEORIGIN
```

Alternative (moderner):

```http
Content-Security-Policy: frame-ancestors 'self';
```

---

## ❓ Wie aktiviere ich HSTS (HTTPS erzwingen)?
**Lösung:** Browser merken sich HTTPS für die Domain.

```http
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
```

**Achtung:** preload ist irreversibel, erst testen.

---

## ❓ Wie verhindere ich Referrer‑Leaks?
**Lösung:** Minimale Weitergabe von Referrer‑Daten.

```http
Referrer-Policy: strict-origin-when-cross-origin
```

---

## ❓ Wie kontrolliere ich Browser‑Features granular?
**Lösung:** Permissions‑Policy (ehemals Feature‑Policy).

```http
Permissions-Policy: geolocation=(), microphone=(), camera=()
```

Blockiert Zugriff auf kritische APIs.

---

## ❓ Wie verhindere ich Mixed Content?
**Lösung:** Browser blockieren HTTP‑Ressourcen auf HTTPS‑Seiten.

```http
Content-Security-Policy: upgrade-insecure-requests;
```

---

## ❓ Wie setze ich eine sichere Content‑Security‑Policy?
**Lösung:** Minimale, sichere Basis‑CSP.

```http
Content-Security-Policy:
    default-src 'self';
    script-src 'self';
    style-src 'self';
    img-src 'self' data:;
    object-src 'none';
    base-uri 'self';
    frame-ancestors 'self';
```

---

## ❓ Wie verhindere ich, dass Cookies gestohlen werden?
**Lösung:** Sichere Cookie‑Flags.

```http
Set-Cookie: session=abc123; HttpOnly; Secure; SameSite=Lax
```

---

## ❓ Wie verhindere ich, dass die Seite in unsicheren Kontexten läuft?
**Lösung:** Require‑HTTPS‑Kontext.

```http
Content-Security-Policy: block-all-mixed-content;
```

---

## ❓ Wie verhindere ich, dass Browser alte Versionen cachen?
**Lösung:** No‑Cache‑Header für sensible Inhalte.

```http
Cache-Control: no-store, no-cache, must-revalidate
Pragma: no-cache
```

---

## Pro-Tipp
Setze Security‑Header **serverseitig**, nicht per JavaScript — Browser laden JS erst *nachdem* die Header wirken sollten.
