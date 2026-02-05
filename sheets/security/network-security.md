---
title: Network Security Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Network Security: Schutz von Datenflüssen, Services & Infrastruktur

Dieses Sheet bündelt die wichtigsten Mechaniken für Netzwerksicherheit — ideal für Microservices, APIs, Cloud‑Plattformen, Container‑Orchestrierung und Zero‑Trust‑Architekturen.

---

## ❓ Warum Network Security?
**Lösung:** Das Netzwerk ist kein sicherer Ort — weder intern noch extern.

Angreifer nutzen:

- offene Ports  
- schwache Firewalls  
- unsichere Protokolle  
- interne Vertrauenszonen  
- fehlende Segmentierung  
- unverschlüsselten Traffic  

Network Security verhindert:

- lateral movement  
- Datenexfiltration  
- Man‑in‑the‑Middle  
- RCE über Netzwerkpfade  
- unautorisierte Zugriffe  

---

# 🧱 Grundprinzipien

- **Zero Trust**  
- **Least Privilege**  
- **Mikrosegmentierung**  
- **TLS überall**  
- **Explizite Policies statt implizitem Vertrauen**  
- **Kein „intern ist sicher“**  

---

# 🔐 TLS / mTLS

### TLS
- Pflicht für alle externen Verbindungen  
- TLS 1.2 oder 1.3  
- keine veralteten Cipher Suites  

### mTLS
- Pflicht für Service‑zu‑Service Kommunikation  
- Identität über Zertifikate  
- Rotation automatisieren  
- SPIFFE/SPIRE für Identity  

---

# 🧩 Firewall & Access Control

### Regeln
- deny‑all default  
- nur explizit erlaubte Ports  
- nur explizit erlaubte IPs  
- Logging aktivieren  
- keine „any‑any“ Regeln  

### Netzwerk‑Firewalls
- Layer‑3/4 Kontrolle  
- IP‑basierte Policies  

### Application Firewalls (WAF)
- Schutz vor Injection  
- Schutz vor Bots  
- Schutz vor API‑Missbrauch  

---

# 🧱 Mikrosegmentierung

### Ziele
- Services voneinander isolieren  
- laterale Bewegung verhindern  
- Angriffsfläche reduzieren  

### Mechanismen
- Network Policies (Kubernetes)  
- Security Groups (Cloud)  
- VLANs / VPCs  
- Service Mesh Policies  

---

# ☁️ Cloud Network Security

AWS:
- Security Groups minimal  
- NACLs  
- Private Subnets  
- VPC Endpoints  
- kein Public S3  

Azure:
- NSGs  
- Private Endpoints  
- VNet Peering  
- Firewall Policies  

GCP:
- VPC Service Controls  
- Firewall Rules minimal  
- Private Service Connect  

---

# 🐳 Container Network Security

- Network Policies aktivieren  
- keine Host‑Network Pods  
- mTLS via Service Mesh  
- Ports minimal halten  
- keine offenen NodePorts  
- Ingress nur über Gateway  

---

# ☸️ Kubernetes Network Security

- Network Policies pro Namespace  
- Pod‑zu‑Pod Traffic einschränken  
- egress‑Regeln definieren  
- Ingress Controller absichern  
- Service Mesh für mTLS  
- API Server Zugriff beschränken  

---

# 🧰 API Network Security

- Rate Limiting  
- IP Throttling  
- Geo‑Blocking  
- Bot Detection  
- WAF vor API Gateway  
- CORS restriktiv konfigurieren  
- keine anonymen Endpoints  

---

# 🛡️ DNS Security

- DNSSEC  
- Private DNS Zonen  
- keine öffentlichen Records für interne Services  
- DNS Logging  
- Schutz vor DNS Rebinding  

---

# 🧯 Schutz vor Man‑in‑the‑Middle

- TLS erzwingen  
- Certificate Pinning (Mobile)  
- mTLS intern  
- HSTS aktivieren  
- keine unverschlüsselten Protokolle  

---

# 🧪 Network Security Testing

- Port Scans  
- Firewall Rule Audit  
- TLS Scanner  
- Kubernetes Network Policy Tests  
- Cloud Security Scans  
- Penetration Tests  

Tools:

- nmap  
- testssl.sh  
- kube‑bench  
- Trivy  
- Burp Suite  

---

# 🧨 Network Security Anti‑Patterns

- „intern ist sicher“  
- offene Ports „für später“  
- keine Network Policies  
- globale Admin‑Netzwerke  
- unverschlüsselter Traffic  
- keine TLS‑Validierung  
- NodePorts in Produktion  

---

## Pro-Tipp
Network Security ist **Bewegungs‑Kontrolle**: Je klarer definiert ist, wer mit wem sprechen darf, desto schwerer wird laterale Bewegung — und desto stabiler bleibt das gesamte System.
