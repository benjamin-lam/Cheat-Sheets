---
title: Frontend Performance Cheat Sheet
category: Frontend
last_updated: 2025-09-02
status: stable
---

# Frontend Performance: Ladezeiten, Rendering & Optimierung

Dieses Sheet zeigt die wichtigsten Techniken, um Webseiten schnell, responsiv und ressourcenschonend auszuliefern — ohne Overengineering.

---

## ❓ Wie optimiere ich die Ladezeit von CSS & JS?
**Lösung:** Minimieren, bündeln, verzögern.

- CSS im `<head>` (blocking, aber notwendig)
- JS am Ende des `<body>` oder mit `defer`
- Unkritisches CSS → `media="print"` + `onload`
- Unkritisches JS → `async`

```html
<script src="app.js" defer></script>
```

---

## ❓ Wie reduziere ich Render‑Blocking‑CSS?
**Lösung:** Critical CSS inline einbetten.

```html
<style>
  /* Critical CSS */
  body { margin: 0; }
  header { height: 60px; }
</style>
<link rel="stylesheet" href="styles.css">
```

---

## ❓ Wie optimiere ich Bilder?
**Lösung:** Moderne Formate + Responsive Images.

```html
<img
  src="image.webp"
  srcset="image-800.webp 800w, image-1600.webp 1600w"
  sizes="(max-width: 800px) 100vw, 800px"
  alt="Beispielbild"
/>
```

- WebP/AVIF nutzen  
- Lazy Loading aktivieren  
- Große Bilder niemals unskaliert ausliefern  

```html
<img src="hero.webp" loading="lazy">
```

---

## ❓ Wie verbessere ich die Time‑to‑Interactive?
**Lösung:** JS reduzieren & splitten.

- Code‑Splitting  
- Tree‑Shaking  
- Unnötige Frameworks vermeiden  
- Third‑Party‑Scripts kritisch prüfen  

---

## ❓ Wie optimiere ich Fonts?
**Lösung:** Preload + Fallback.

```html
<link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin>
```

- `font-display: swap` nutzen  
- Nur benötigte Schriftschnitte laden  

```css
@font-face {
  font-family: "Inter";
  src: url("inter.woff2") format("woff2");
  font-display: swap;
}
```

---

## ❓ Wie aktiviere ich HTTP‑Caching für statische Assets?
**Lösung:** Lange TTL + Versionierung.

```nginx
location ~* \.(css|js|png|jpg|svg|woff2)$ {
    expires 30d;
    add_header Cache-Control "public, immutable";
}
```

---

## ❓ Wie erkenne ich Performance‑Probleme?
**Lösung:** Lighthouse‑Metriken.

- LCP (Largest Contentful Paint)  
- CLS (Cumulative Layout Shift)  
- FID (First Input Delay)  
- TTFB (Time to First Byte)  

---

## ❓ Wie verhindere ich Layout‑Shifts?
**Lösung:** Immer feste Größen definieren.

```html
<img src="photo.jpg" width="800" height="600">
```

Oder via CSS:

```css
img { aspect-ratio: 4 / 3; }
```

---

## ❓ Wie optimiere ich Third‑Party‑Scripts?
**Lösung:** Lazy Load + Consent.

- Analytics erst nach Consent laden  
- Chat‑Widgets verzögert laden  
- Tag‑Manager kritisch prüfen  

---

## Pro-Tipp
Performance ist kein einmaliges Projekt — nutze Monitoring (z. B. Web Vitals) und optimiere kontinuierlich.
