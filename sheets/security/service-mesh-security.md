---
title: Service Mesh Security Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Service Mesh Security: Identität, Verschlüsselung & Policies für Microservices

Dieses Sheet bündelt die wichtigsten Sicherheitsmechaniken eines Service Mesh — ideal für Microservices, Kubernetes, Zero‑Trust‑Architekturen und hochregulierte Plattformen.

---

## ❓ Warum Service Mesh Security?
**Lösung:** Ein Service Mesh bringt Sicherheit dorthin, wo sie hingehört — in die Kommunikation zwischen Services.

Service Mesh Security ermöglicht:

- mTLS für alle Services  
- eindeutige Workload‑Identitäten  
- Zero‑Trust‑Policies  
- Traffic‑Kontrolle  
- Observability  
- sichere Service‑zu‑Service‑Kommunikation  

Es ist **Netzwerksicherheit auf Anwendungsebene**.

---

# 🧱 Kernkomponenten eines Service Mesh

### Sidecar Proxy
- interceptet Traffic  
- erzwingt mTLS  
- führt Policies aus  
- liefert Telemetrie  

### Control Plane
- verteilt Zertifikate  
- verwaltet Identitäten  
- steuert Policies  
- konfiguriert Sidecars  

### Data Plane
- tatsächlicher Traffic  
- durch Sidecars geschützt  

---

# 🔐 mTLS Everywhere

### Ziele
- Verschlüsselung  
- Authentifizierung  
- Integrität  

### Regeln
- mTLS für jeden Request  
- Zertifikate automatisch rotieren  
- keine statischen Zertifikate  
- Identität über SPIFFE/SPIRE  

### Vorteile
- kein Vertrauen in das Netzwerk  
- Schutz vor Man‑in‑the‑Middle  
- eindeutige Service‑Identitäten  

---

# 🧩 Workload Identity (SPIFFE/SPIRE)

### Eigenschaften
- eindeutige Identität pro Service  
- kryptografisch gesichert  
- automatisch verteilt  
- automatisch rotiert  

### Beispiel SPIFFE ID
```
spiffe://example.com/ns/default/sa/orders-service
```

### Vorteile
- kein Sharing von Credentials  
- kein globaler „service-admin“  
- Zero‑Trust‑Policies pro Service  

---

# 🛡️ Zero‑Trust Policies

### Prinzipien
- deny‑all default  
- explizite Allow‑Regeln  
- Identität statt IP‑Adressen  
- Kontext‑basierte Entscheidungen  

### Beispiele
- Service A darf Service B lesen  
- Service C darf nur POST auf Endpoint X  
- Service D darf nur mit mTLS kommunizieren  

---

# 🧰 Traffic Control

### Mechanismen
- Rate Limiting  
- Circuit Breaking  
- Retries  
- Timeouts  
- Fault Injection  
- Canary Deployments  
- Traffic Shifting  

### Ziele
- Stabilität  
- Resilienz  
- Schutz vor Abuse  

---

# 🐳 Service Mesh in Kubernetes

### Best Practices
- Sidecar Injection aktivieren  
- Network Policies ergänzen  
- Pod Security Standards  
- Secrets verschlüsseln  
- Admission Controller für Policies  
- Namespaces isolieren  

### Wichtige Logs
- mTLS‑Fehler  
- Policy‑Verstöße  
- ungewöhnliche Traffic‑Muster  

---

# ☁️ Cloud‑Integration

AWS:
- App Mesh  
- IAM‑basierte Identitäten  
- PrivateLink  

Azure:
- Open Service Mesh  
- Managed Identities  

GCP:
- Anthos Service Mesh  
- Workload Identity  

---

# 🧪 Service Mesh Security Testing

- mTLS Tests  
- Policy Tests  
- Identity Abuse Simulation  
- Traffic Manipulation Tests  
- Replay Tests  
- Lateral Movement Simulation  

Tools:
- istioctl  
- envoy debug tools  
- OPA/Rego  
- Chaos Mesh  

---

# 🧨 Service Mesh Anti‑Patterns

- mTLS deaktivieren  
- globale Allow‑Policies  
- statische Zertifikate  
- keine Rotation  
- Sidecars entfernen „für Performance“  
- Policies auf IP‑Basis  
- kein Monitoring  

---

## Pro-Tipp
Service Mesh Security ist **Identitäts‑basierte Netzwerksicherheit**: Wer mTLS, Workload‑Identitäten und Zero‑Trust‑Policies kombiniert, macht laterale Bewegung nahezu unmöglich — und erhöht die Resilienz der gesamten Plattform.
