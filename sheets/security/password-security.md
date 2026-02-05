---
title: Password Security Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Password Security: Schutz vor Credential Theft & Account‑Übernahmen

Dieses Sheet bündelt die wichtigsten Mechaniken zur Absicherung von Passwörtern — ideal für Web‑Apps, APIs, Identity‑Provider, Enterprise‑Security und Zero‑Trust‑Architekturen.

---

## ❓ Warum Password Security?
**Lösung:** Passwörter sind der häufigste Angriffsvektor.

Angreifer nutzen:

- Credential Stuffing  
- Brute Force  
- Phishing  
- Keylogger  
- Datenbank‑Leaks  
- Passwort‑Wiederverwendung  

Password Security verhindert:

- Account‑Übernahmen  
- lateral movement  
- Identitätsdiebstahl  
- Cloud‑Kompromittierung  

---

# 🧱 Passwort‑Grundprinzipien

- niemals Klartext  
- niemals reversible Verschlüsselung  
- Hashing mit modernen Algorithmen  
- Salt + Pepper  
- Rate Limiting  
- MFA erzwingen  
- keine Wiederverwendung  

---

# 🔐 Passwort‑Hashing

Empfohlene Algorithmen:

- **argon2id** (Best Practice)  
- **bcrypt**  
- **scrypt**  

Nicht verwenden:

- SHA‑256  
- SHA‑1  
- MD5  
- PBKDF2 nur als Legacy  

Beispiel (argon2id Parameter):

- Memory: 64–256 MB  
- Iterations: 2–6  
- Parallelism: 1–4  

---

# 🧂 Salt & Pepper

### Salt
- pro Passwort einzigartig  
- zufällig  
- im Klartext speicherbar  
- verhindert Rainbow Tables  

### Pepper
- globales Secret  
- im Secret Store  
- niemals in der DB  
- schützt bei DB‑Leak  

---

# 🚫 Verbotene Passwort‑Praktiken

- Passwörter im Klartext speichern  
- reversible Verschlüsselung  
- Passwörter per E‑Mail versenden  
- Passwörter in Logs  
- Passwörter in URLs  
- Passwörter in Config Files  

---

# 🧪 Passwort‑Validierung

Regeln:

- Mindestlänge 12–14 Zeichen  
- keine Komplexitäts‑Zwangsregeln  
- Passphrase bevorzugen  
- keine häufigen Passwörter erlauben  
- HIBP‑Check (Have I Been Pwned)  

Beispiel Passphrase:

```
wolken-tanzen-auf-dem-dach
```

---

# 🛡️ Schutz vor Credential Stuffing

- MFA  
- Rate Limiting  
- IP‑Throttling  
- Device Fingerprinting  
- Bot Detection  
- Login‑Anomalieerkennung  

---

# 🧯 Schutz vor Brute Force

- Rate Limiting  
- Captcha (sparsam)  
- progressive Delays  
- Account Lockout (zeitlich begrenzt)  

---

# 🧩 Passwort‑Reset‑Sicherheit

Regeln:

- Token mit kurzer TTL (10–30 Minuten)  
- Token nur einmal gültig  
- Token nicht vorhersagbar  
- Token nicht in URLs loggen  
- keine Sicherheitsfragen  
- Reset nur per E‑Mail + MFA  

---

# 🧰 Passwort‑Änderung

- Session Rotation  
- alte Sessions invalidieren  
- Passwort‑Historie optional  
- MFA erneut anfordern  

---

# 🧭 Passwort‑Monitoring

Wichtige Signale:

- viele Fehlversuche  
- ungewöhnliche IPs  
- Login‑Versuche außerhalb Arbeitszeiten  
- HIBP‑Treffer  
- Passwort‑Reset‑Missbrauch  

---

# 🧨 Passwort‑Anti‑Patterns

- „Komplexität statt Länge“  
- „Regelmäßige Rotation für alle“  
- „Mindestens ein Sonderzeichen“  
- „Passwort per E‑Mail“  
- „Passwort im Klartext speichern“  
- „SHA‑256 ist genug“  

---

## Pro-Tipp
Password Security ist **Identitäts‑Hygiene**: Je stärker Hashing, MFA und Monitoring kombiniert werden, desto schwerer wird Credential Theft — und desto stabiler bleibt das System.
