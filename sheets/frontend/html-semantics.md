---
title: HTML Semantics Cheat Sheet
category: Frontend
last_updated: 2025-09-02
status: stable
---

# HTML Semantik: Struktur, Accessibility & SEO

Dieses Sheet zeigt die wichtigsten semantischen HTML‑Elemente und wie sie für Barrierefreiheit, SEO und klare Dokumentstruktur eingesetzt werden.

---

## ❓ Warum Semantik?
**Lösung:** Semantik verbessert:

- Accessibility (Screenreader, Navigation)
- SEO (bessere Struktur für Crawler)
- Maintainability (klarere DOM‑Struktur)
- Konsistenz über Projekte hinweg

---

## ❓ Welche strukturellen Elemente sollte ich nutzen?
**Lösung:** Die wichtigsten Layout‑Container.

```html
<header>    <!-- Kopfbereich einer Seite oder Sektion -->
<nav>       <!-- Hauptnavigation -->
<main>      <!-- Hauptinhalt der Seite -->
<section>   <!-- Thematische Abschnitte -->
<article>   <!-- Eigenständige Inhalte -->
<aside>     <!-- Ergänzende Inhalte -->
<footer>    <!-- Fußbereich -->
```

---

## ❓ Wann nutze ich <section> vs. <article>?
**Lösung:**

- **article** = eigenständiger Inhalt (Blogpost, Kommentar, Produkt)
- **section** = thematische Gruppierung innerhalb eines Artikels oder der Seite

---

## ❓ Wie strukturiere ich Überschriften korrekt?
**Lösung:** Nur ein `<h1>` pro Seite, danach hierarchisch.

```html
<h1>Seitentitel</h1>
<h2>Abschnitt</h2>
<h3>Unterabschnitt</h3>
```

Screenreader verlassen sich auf diese Hierarchie.

---

## ❓ Wie markiere ich Navigation korrekt?
**Lösung:** `<nav>` + Listen.

```html
<nav>
  <ul>
    <li><a href="/home">Home</a></li>
    <li><a href="/blog">Blog</a></li>
  </ul>
</nav>
```

---

## ❓ Wie mache ich Formulare semantisch korrekt?
**Lösung:** Labels sind Pflicht.

```html
<label for="email">E-Mail</label>
<input id="email" type="email" />
```

Optional: `<fieldset>` + `<legend>` für Gruppen.

---

## ❓ Wie markiere ich wichtige Textarten?
**Lösung:** Semantische Inline‑Elemente.

```html
<strong>Wichtig</strong>
<em>Betonung</em>
<code>inline code</code>
<mark>Hervorhebung</mark>
<time datetime="2025-09-02">2. September 2025</time>
```

---

## ❓ Wie verbessere ich SEO mit Semantik?
**Lösung:** Strukturierte Inhalte.

- `<article>` für eigenständige Inhalte  
- `<header>` + `<footer>` innerhalb von Artikeln  
- `<figure>` + `<figcaption>` für Bilder  

```html
<figure>
  <img src="diagram.png" alt="Architekturdiagramm" />
  <figcaption>Systemübersicht</figcaption>
</figure>
```

---

## ❓ Wie mache ich Tabellen barrierefrei?
**Lösung:** Header + Scope.

```html
<table>
  <thead>
    <tr>
      <th scope="col">Name</th>
      <th scope="col">Preis</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Laptop</td>
      <td>999 €</td>
    </tr>
  </tbody>
</table>
```

---

## Pro-Tipp
Nutze `aria-label`, `aria-labelledby` und `role` nur dann, wenn Semantik allein nicht reicht — nicht als Ersatz für sauberes HTML.
