---
title: Architecture Basics Cheat Sheet
category: Architecture
last_updated: 2025-09-02
status: stable
---

# Architecture Basics: Layering, Boundaries, Coupling & Consequences

Dieses Sheet bündelt die wichtigsten Architektur‑Grundlagen für moderne Software‑Systeme — ideal für Microservices, modulare Monolithen und komplexe Plattformen.

---

## ❓ Was ist Software‑Architektur?
**Lösung:** Die Summe aller Entscheidungen, die schwer zu ändern sind.

Architektur definiert:

- Strukturen  
- Verantwortlichkeiten  
- Abhängigkeiten  
- Datenflüsse  
- Konsequenzen  

Architektur ist kein Diagramm, sondern **Entscheidungsmanagement**.

---

## ❓ Was sind die wichtigsten Architektur‑Qualitäten?
**Lösung:** die „ilities“.

- Maintainability  
- Testability  
- Scalability  
- Reliability  
- Observability  
- Security  
- Evolvability  

---

## ❓ Was ist Coupling & Cohesion?
**Lösung:** zwei Grundkräfte.

- **Cohesion** → Dinge, die zusammengehören, bleiben zusammen  
- **Coupling** → Dinge, die nicht zusammengehören, werden getrennt  

Ziel:

- hohe Kohäsion  
- niedriges Kopplungsniveau  

---

## ❓ Was ist ein Modul?
**Lösung:** eine Einheit mit klarer Verantwortung.

Ein Modul hat:

- eine Aufgabe  
- eine API  
- interne Details  
- klare Grenzen  

Ein Modul ist kein Ordner, sondern eine **Konsequenz‑Einheit**.

---

## ❓ Was ist ein Layer?
**Lösung:** Abstraktionsebenen.

Typisch:

- API / Interface  
- Application / Use Cases  
- Domain / Business Logic  
- Infrastructure  

Regel:

- Abhängigkeiten gehen **nach unten**, nicht nach oben.

---

## ❓ Was ist Domain‑Driven Design (DDD)?
**Lösung:** Fachlogik im Zentrum.

Kernideen:

- Ubiquitous Language  
- Bounded Contexts  
- Aggregates  
- Entities & Value Objects  
- Domain Events  

DDD ist ein Werkzeug, kein Dogma.

---

## ❓ Was ist ein Bounded Context?
**Lösung:** ein abgeschlossener Bedeutungsraum.

Ein BC hat:

- eigene Sprache  
- eigene Modelle  
- eigene Daten  
- eigene Regeln  

BCs kommunizieren über **APIs** oder **Events**, nicht über geteilte Tabellen.

---

## ❓ Was ist ein Anti‑Corruption Layer?
**Lösung:** Schutzschicht zwischen Systemen.

Verhindert:

- Leaky Abstractions  
- Modell‑Vermischung  
- Kopplung an Fremdsysteme  

---

## ❓ Was ist ein Modularer Monolith?
**Lösung:** ein Monolith mit klaren Grenzen.

Eigenschaften:

- interne Module  
- klare APIs  
- keine Querverweise  
- keine „Shared Everything“‑Strukturen  

Vorteil:

- weniger Komplexität als Microservices  
- trotzdem klare Verantwortlichkeiten  

---

## ❓ Was sind Microservices?
**Lösung:** unabhängige, kleine Services.

Eigenschaften:

- eigene Deployments  
- eigene Daten  
- eigene Operational Reality  
- lose gekoppelt  
- event‑getrieben  

Microservices sind ein **Organisationsmodell**, kein Technik‑Trend.

---

## ❓ Wie kommunizieren Systeme?
**Lösung:** synchron oder asynchron.

Synchron:

- REST  
- gRPC  

Asynchron:

- Events  
- Queues  
- Streams  

Regel:

- intern → Events bevorzugen  
- extern → APIs bevorzugen  

---

## ❓ Was ist Event‑Driven Architecture?
**Lösung:** Systeme reagieren auf Ereignisse.

Vorteile:

- lose Kopplung  
- bessere Skalierung  
- natürliche Historie  
- Resilienz  

---

## ❓ Was ist CQRS?
**Lösung:** Commands & Queries trennen.

- Commands → ändern Zustand  
- Queries → lesen Zustand  

Optional mit Event Sourcing kombinierbar.

---

## ❓ Was ist Event Sourcing?
**Lösung:** Zustand = Summe aller Events.

Vorteile:

- perfekte Historie  
- Auditing  
- Rebuilds  
- Time Travel  

Nachteile:

- komplexer  
- Event‑Evolution nötig  

---

## ❓ Was ist eine Architektur‑Entscheidung?
**Lösung:** eine Entscheidung mit langfristigen Konsequenzen.

Dokumentiert als:

- ADR (Architecture Decision Record)  
- Kontext  
- Entscheidung  
- Alternativen  
- Konsequenzen  

---

## Pro-Tipp
Architektur ist **Konsequenz‑Management**: Jede Entscheidung erzeugt Lasten, Abhängigkeiten und Pfade — gute Architektur macht diese sichtbar, steuerbar und bewusst.
