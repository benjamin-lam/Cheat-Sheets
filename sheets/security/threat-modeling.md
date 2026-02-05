---
title: Threat Modeling Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Threat Modeling: systematische Analyse von Risiken & Angriffsflächen

Dieses Sheet bündelt die wichtigsten Methoden, Schritte und Denkmodelle für Threat Modeling — ideal für APIs, Microservices, Cloud‑Infrastruktur und Zero‑Trust‑Architekturen.

---

## ❓ Was ist Threat Modeling?
**Lösung:** eine strukturierte Methode, um Angriffe, Risiken und Schwachstellen frühzeitig zu erkennen — bevor sie ausgenutzt werden.

Threat Modeling beantwortet vier Fragen:

1. **Was bauen wir?**  
2. **Was kann schiefgehen?**  
3. **Was tun wir dagegen?**  
4. **Haben wir genug getan?**

---

## ❓ Warum Threat Modeling?
**Lösung:** Sicherheit wird planbar.

Threat Modeling hilft:

- Risiken sichtbar machen  
- Architekturfehler früh erkennen  
- Prioritäten setzen  
- Security‑Kosten senken  
- Compliance erfüllen  
- Zero‑Trust sauber implementieren  

---

## ❓ Welche Methoden gibt es?
**Lösung:** vier etablierte Ansätze.

### 1. STRIDE
Microsoft‑Modell für Bedrohungskategorien:

- **S**poofing  
- **T**ampering  
- **R**epudiation  
- **I**nformation Disclosure  
- **D**enial of Service  
- **E**levation of Privilege  

### 2. Attack Trees
Angriffe als Baumstruktur modellieren.

### 3. DFD‑basiertes Modeling
Data Flow Diagrams → Angriffsflächen sichtbar machen.

### 4. PASTA (Process for Attack Simulation and Threat Analysis)
risikobasierter, prozessorientierter Ansatz.

---

## ❓ Was sind die Schritte eines Threat Models?
**Lösung:** fünf Phasen.

### 1. Scope definieren
- Systemgrenzen  
- Assets  
- Nutzergruppen  
- Integrationen  

### 2. Architektur modellieren
- Data Flow Diagram  
- Komponenten  
- Trust Boundaries  
- Datenklassifikation  

### 3. Bedrohungen identifizieren
- STRIDE anwenden  
- Angriffswege analysieren  
- Missbrauchsszenarien definieren  

### 4. Risiken bewerten
- Eintrittswahrscheinlichkeit  
- Impact  
- Priorisierung  

### 5. Maßnahmen definieren
- technische Controls  
- organisatorische Controls  
- Policies  
- Monitoring  

---

## ❓ Was sind typische Angriffsflächen?
**Lösung:** überall, wo Daten fließen.

- APIs  
- AuthN/AuthZ  
- Secrets  
- Datenbanken  
- Message Queues  
- Cloud‑Rollen  
- CI/CD  
- Third‑Party Services  
- Admin‑Interfaces  

---

## ❓ Wie sieht ein Data Flow Diagram (DFD) aus?

Komponenten:

- Prozesse  
- Datenflüsse  
- Datenquellen  
- Datensenken  
- Trust Boundaries  

Beispiel:

```
User → API Gateway → Service → DB
             ↑
         Auth Service
```

---

## ❓ Wie wende ich STRIDE an?
**Lösung:** pro Komponente + pro Datenfluss.

Beispiel für eine API:

- **Spoofing:** gestohlene Tokens  
- **Tampering:** manipulierte Payloads  
- **Repudiation:** fehlende Audit Logs  
- **Information Disclosure:** zu viele Daten im Response  
- **DoS:** keine Rate Limits  
- **Elevation of Privilege:** fehlende Autorisierung  

---

## ❓ Wie priorisiere ich Risiken?
**Lösung:** Impact × Wahrscheinlichkeit.

Typische Kategorien:

- High  
- Medium  
- Low  

Regeln:

- High → sofortige Maßnahmen  
- Medium → zeitnah beheben  
- Low → dokumentieren  

---

## ❓ Welche Maßnahmen gehören in ein Threat Model?
**Lösung:** technische + organisatorische Controls.

Technische:

- AuthN/AuthZ  
- Rate Limiting  
- Input Validation  
- Encryption  
- Secrets Management  
- Network Policies  
- mTLS  
- Logging & Monitoring  

Organisatorische:

- Runbooks  
- On‑Call  
- Security Reviews  
- Code Reviews  

---

## ❓ Wie integriere ich Threat Modeling in den Entwicklungsprozess?
**Lösung:** kontinuierlich statt einmalig.

- bei neuen Features  
- bei Architekturänderungen  
- bei neuen Integrationen  
- bei neuen Datenflüssen  
- bei neuen Bedrohungen  

---

## ❓ Wie mache ich Threat Modeling in Microservices?
**Lösung:** pro Service + pro Schnittstelle.

Regeln:

- jeder Service hat eigenes Threat Model  
- Trust Boundaries klar definieren  
- Service‑Identität (mTLS)  
- Policies pro Service  
- keine impliziten Vertrauenszonen  

---

## ❓ Wie mache ich Threat Modeling in der Cloud?
**Lösung:** Cloud‑spezifische Risiken berücksichtigen.

Beispiele:

- IAM‑Fehlkonfigurationen  
- Public Buckets  
- offene Security Groups  
- unsichere Serverless‑Funktionen  
- unverschlüsselte Daten  

---

## ❓ Wie mache ich Threat Modeling für APIs?
**Lösung:** OWASP API Top 10 integrieren.

Fokus:

- BOLA  
- AuthN/AuthZ  
- Rate Limits  
- Input Validation  
- Schema Validation  
- Secrets  
- Logging  

---

## ❓ Wie mache ich Threat Modeling für CI/CD?
**Lösung:** Supply‑Chain‑Risiken analysieren.

Beispiele:

- manipulierte Dependencies  
- unsichere Build‑Agenten  
- fehlende Signaturen  
- Secrets in Pipelines  

---

## Pro-Tipp
Threat Modeling ist **Architektur‑Sicherheit**: Wer versteht, wie Angriffe funktionieren, baut Systeme, die Angriffe überleben.
