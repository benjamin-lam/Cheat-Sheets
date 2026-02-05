---
title: Markdown Syntax Cheat Sheet
category: Tooling
last_updated: 2025-09-02
status: stable
---

# Markdown Syntax: Struktur, Formatierung & technische Dokumentation

Dieses Sheet zeigt die wichtigsten Markdown‑Elemente für technische Dokumentation, READMEs, Wikis und Cheat Sheets — kompakt, klar und praxistauglich.

---

## ❓ Wie schreibe ich Überschriften?
**Lösung:** `#` bestimmt die Ebene.

```markdown
# H1 – Titel
## H2 – Abschnitt
### H3 – Unterabschnitt
```

---

## ❓ Wie formatiere ich Text?
**Lösung:** Standard‑Inline‑Formatierungen.

```markdown
**fett**
*kursiv*
~~durchgestrichen~~
`inline code`
```

---

## ❓ Wie erstelle ich Codeblöcke?
**Lösung:** Dreifache Backticks + Sprache.

```markdown
```bash
npm install
```
```

---

## ❓ Wie mache ich Listen?
**Lösung:** Ungeordnet oder geordnet.

```markdown
- Punkt A
- Punkt B
  - Unterpunkt

1. Schritt
2. Schritt
```

---

## ❓ Wie setze ich Links & Bilder?
**Lösung:** Inline‑Syntax.

```markdown
[Linktext](https://example.com)

![Alt-Text](image.png)
```

---

## ❓ Wie erstelle ich Tabellen?
**Lösung:** Pipes + Trennlinie.

```markdown
| Name  | Wert |
|-------|------|
| CPU   | 4    |
| RAM   | 16GB |
```

---

## ❓ Wie mache ich Zitate?
**Lösung:** `>` am Zeilenanfang.

```markdown
> Dies ist ein Zitat.
```

---

## ❓ Wie mache ich horizontale Trennlinien?
**Lösung:** Drei oder mehr `-` oder `*`.

```markdown
---
```

---

## ❓ Wie markiere ich TODOs oder Checklisten?
**Lösung:** GitHub‑kompatible Checkboxen.

```markdown
- [ ] Offen
- [x] Erledigt
```

---

## ❓ Wie hebe ich wichtige Hinweise hervor?
**Lösung:** Info‑Blöcke (GitHub‑Flavored Markdown).

```markdown
> **Hinweis:** Dies ist wichtig.
> **Warnung:** Vorsicht bei Änderungen.
```

---

## ❓ Wie strukturiere ich technische Dokumentation?
**Lösung:** Klare, wiederkehrende Muster.

Empfohlen:

```markdown
# Titel
## Zweck
## Installation
## Beispiele
## API
## Troubleshooting
```

---

## ❓ Wie schreibe ich Markdown für GitHub READMEs?
**Lösung:** Nutze Badges, klare Struktur & Beispiele.

```markdown
# Projektname

![Build](https://img.shields.io/badge/build-passing-brightgreen)

## Features
- Schnell
- Modular
- Dokumentiert

## Installation
```bash
npm install
```

---

## Pro-Tipp
Markdown wird mächtig, wenn du es **konsequent** nutzt: klare Überschriften, kurze Abschnitte, viele Beispiele und Codeblöcke für alles Technische.
