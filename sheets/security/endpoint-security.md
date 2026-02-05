---
title: Endpoint Security Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Endpoint Security: Schutz von Geräten, Workstations & Entwicklerumgebungen

Dieses Sheet bündelt die wichtigsten Mechaniken zur Absicherung von Endgeräten — ideal für Entwickler‑Laptops, Admin‑Workstations, Cloud‑Zugänge, Remote‑Arbeit und Zero‑Trust‑Architekturen.

---

## ❓ Warum Endpoint Security?
**Lösung:** Der einfachste Weg ins Unternehmen führt über kompromittierte Endgeräte.

Angreifer nutzen:

- Malware  
- Ransomware  
- Keylogger  
- Phishing  
- gestohlene Browser‑Sessions  
- unsichere Entwickler‑Setups  
- unverschlüsselte Geräte  

Endpoint Security verhindert:

- Credential Theft  
- lateral movement  
- Supply‑Chain‑Angriffe  
- Cloud‑Kompromittierung  
- Datenexfiltration  

---

# 🧱 Grundprinzipien

- **Zero Trust**  
- **Least Privilege**  
- **Device Hardening**  
- **Secure Defaults**  
- **Isolation**  
- **Monitoring**  

---

# 💻 Betriebssystem‑Hardening

### Windows
- Defender aktivieren  
- SmartScreen aktivieren  
- Credential Guard  
- Application Control (WDAC)  
- BitLocker  
- automatische Updates  

### macOS
- FileVault  
- Gatekeeper  
- XProtect  
- automatische Updates  
- keine Admin‑Accounts  

### Linux
- Firewall aktivieren  
- AppArmor / SELinux  
- automatische Updates  
- SSH Hardening  
- noexec /tmp  

---

# 🔐 Zugriffssicherheit

- MFA überall  
- Passwort‑Manager  
- SSH Keys statt Passwörter  
- keine globalen Admin‑Rechte  
- Just‑in‑Time Privilege Elevation  
- keine geteilten Accounts  

---

# 🧰 Entwickler‑Workstation Security

- Dev‑Container statt lokale Toolchains  
- keine Secrets lokal speichern  
- keine Cloud Keys lokal speichern  
- Browser‑Isolation für Admin‑Portale  
- VPN oder Zero‑Trust Access  
- sichere Browser‑Extensions  
- keine lokalen DBs mit Produktionsdaten  

---

# 🛡️ Malware‑Schutz

- EDR/XDR aktivieren  
- Echtzeitschutz  
- heuristische Analyse  
- regelmäßige Scans  
- USB‑Geräte blockieren oder einschränken  

---

# 🧩 Browser‑Security

- Passwort‑Manager statt Browser‑Speicher  
- keine unsicheren Extensions  
- automatische Updates  
- Isolation für kritische Portale  
- Cookies löschen bei Logout  
- kein LocalStorage für Tokens  

---

# ☁️ Cloud‑Zugriffssicherheit

- Conditional Access  
- Device Compliance Checks  
- IP‑ und Geo‑Restriktionen  
- MFA erzwingen  
- keine persistenten Sessions  
- Browser‑Isolation für Admin‑Portale  

---

# 🧯 Schutz vor Phishing

- E‑Mail‑Filter  
- Link‑Scanning  
- Attachment‑Scanning  
- Anti‑Impersonation  
- Schulungen  
- Browser‑Warnungen aktivieren  

---

# 🧱 Netzwerk‑Sicherheit für Endpoints

- Firewall aktiv  
- DNS‑Filter  
- VPN oder Zero‑Trust Access  
- keine offenen Ports  
- keine lokalen Server  
- keine öffentlichen Hotspots ohne Schutz  

---

# 🔒 Geräteschutz

- Festplattenverschlüsselung  
- automatisches Sperren  
- Remote‑Wipe  
- Device Inventory  
- Compliance Policies  
- keine privaten Geräte für Admin‑Zugänge  

---

# 🧭 Monitoring & Logging

- EDR/XDR Telemetrie  
- Login‑Anomalien  
- ungewöhnliche Prozesse  
- Browser‑Session‑Missbrauch  
- USB‑Events  
- Policy‑Verstöße  

---

# 🧪 Endpoint Security Testing

- Malware Simulation  
- Phishing Simulation  
- Credential Theft Tests  
- Browser Security Tests  
- Device Compliance Checks  

---

# 🧨 Endpoint Security Anti‑Patterns

- Entwickler als lokale Admins  
- unverschlüsselte Laptops  
- keine Updates  
- keine EDR/XDR  
- private Geräte für Firmenzugänge  
- Secrets lokal speichern  
- Browser‑Sessions für Admin‑Portale  

---

## Pro-Tipp
Endpoint Security ist **Zugangs‑Resilienz**: Wer die Geräte schützt, schützt die Identitäten — und damit das gesamte Unternehmen.
