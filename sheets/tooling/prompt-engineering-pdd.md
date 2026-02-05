---
title: Prompt Engineering & PDD Cheat Sheet
category: Tooling
last_updated: 2025-09-02
status: stable
---

# Prompt Engineering & PDD: Struktur, Qualität & Reproduzierbarkeit

Dieses Sheet zeigt die wichtigsten Techniken für Prompt Driven Development (PDD) — ein Ansatz, bei dem KI‑Systeme als deterministische Werkzeuge in klaren, reproduzierbaren Pipelines eingesetzt werden.

---

## ❓ Was ist Prompt Driven Development (PDD)?
**Lösung:** Ein systematischer Ansatz, bei dem Prompts wie Code behandelt werden:

- deterministisch  
- versioniert  
- modular  
- testbar  
- reproduzierbar  

Prompts sind **Spezifikationen**, nicht Chat‑Nachrichten.

---

## ❓ Wie strukturiere ich einen guten Prompt?
**Lösung:** Die 5‑Schichten‑Struktur.

1. **Rolle** – „Du bist ein erfahrener …“  
2. **Ziel** – Was soll erzeugt werden  
3. **Kontext** – Domain, Einschränkungen, Beispiele  
4. **Regeln** – Format, Stil, Output‑Form  
5. **Input** – Daten, die verarbeitet werden sollen  

Beispiel:

```text
du bist ein erfahrener PHP-Architekt.
Ziel: Erstelle eine robuste Repository-Klasse.
Regeln: PSR-12, keine Kommentare, nur Code.
Input: UserRepository benötigt findByEmail().
```

---

## ❓ Wie mache ich Prompts reproduzierbar?
**Lösung:** Immer deterministische Vorgaben:

- feste Rollen  
- feste Output‑Formate  
- keine offenen Fragen  
- keine „kreativen“ Freiheiten  

Beispiel:

```text
Output: Nur JSON, keine Erklärungen.
```

---

## ❓ Wie verhindere ich Halluzinationen?
**Lösung:** Constraints + Beispiele.

```text
Wenn du etwas nicht weißt, gib null zurück.
```

Oder:

```text
Hier sind 3 Beispiele. Folge exakt diesem Muster.
```

---

## ❓ Wie baue ich modulare Prompt‑Bausteine?
**Lösung:** Prompt‑Snippets wie Code‑Snippets behandeln.

- `role.prompt`  
- `style.prompt`  
- `format.prompt`  
- `validation.prompt`  

Diese können kombiniert werden:

```text
@include role.backend-architect
@include format.php-class
@include rules.no-comments
```

---

## ❓ Wie teste ich Prompts?
**Lösung:** Golden‑Master‑Testing.

- Input → Prompt → Output  
- Output wird gespeichert  
- Änderungen am Prompt → Diff prüfen  

Ideal für CI‑Pipelines.

---

## ❓ Wie definiere ich Output‑Formate klar?
**Lösung:** Immer explizit.

```text
Output: Nur Markdown.
```

Oder:

```text
Output: Nur Codeblock, Sprache: yaml.
```

---

## ❓ Wie nutze ich PDD für Code‑Generierung?
**Lösung:** Prompts als Spezifikation.

Beispiel:

```text
du bist ein erfahrener Laravel-Architekt.
Ziel: Erstelle ein Policy-Template.
Regeln: PSR-12, keine Kommentare.
Input: Model = Invoice.
```

---

## ❓ Wie nutze ich PDD für Analyse & Refactoring?
**Lösung:** KI als statisches Analysewerkzeug.

```text
Analysiere diesen Code.
Finde Verstöße gegen SOLID.
Output: JSON mit violations[].
```

---

## ❓ Wie baue ich KI‑Pipelines?
**Lösung:** Mehrere Prompts als Schritte.

1. Analyse  
2. Strukturierung  
3. Generierung  
4. Validierung  
5. Optimierung  

Jeder Schritt ist deterministisch.

---

## Pro-Tipp
Behandle Prompts wie Code: versionieren, testen, reviewen — und niemals „aus dem Bauch heraus“ schreiben.
