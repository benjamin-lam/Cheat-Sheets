---
title: Hardened .htaccess Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Hardened .htaccess: Server-Sicherheit & Routing

Dieses Sheet bietet erprobte Lösungen für Apache-Server, um die Sicherheit zu erhöhen und sauberes Routing zu garantieren.

---

## ❓ Wie schütze ich sensible System-Ordner vor direktem Zugriff?
**Lösung:** Blockiere Kern-Verzeichnisse und sende einen `403 Forbidden`.

```apache
# Blockiert Zugriff auf core, content, jobs und templates
RewriteRule ^(core|content|jobs|templates)(/.*)?$ - [F,L,NC]
```

---

## ❓ Wie verhindere ich Directory Listing?
**Lösung:** Deaktiviere das automatische Directory Indexing.

```apache
Options -Indexes
```

---

## ❓ Wie erzwinge ich HTTPS und entferne gleichzeitig das "www"?
**Lösung:** Kombiniere beide Redirects, um Ketten zu vermeiden.

```apache
# Entfernt www
RewriteCond %{HTTP_HOST} ^www\.(.*)$ [NC]
RewriteRule ^(.*)$ https://%1/$1 [R=301,L]

# Erzwingt HTTPS
RewriteCond %{HTTPS} !=on
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

---

## ❓ Wie blockiere ich den Zugriff auf versteckte Dateien (.env, .git)?
**Lösung:** Nutze eine FilesMatch-Direktive.

```apache
<FilesMatch "^\.">
    Order Allow,Deny
    Deny from all
</FilesMatch>
```

---

## ❓ Wie gebe ich die llms.txt für KI-Crawler frei (CORS)?
**Lösung:** Setze einen spezifischen Header.

```apache
<Files "llms.txt">
    <IfModule mod_headers.c>
        Header set Access-Control-Allow-Origin "*"
    </IfModule>
</Files>
```

---

## ❓ Wie verhindere ich MIME‑Sniffing?
**Lösung:** Erzwinge den korrekten MIME‑Type.

```apache
Header set X-Content-Type-Options "nosniff"
```

---

## ❓ Wie verhindere ich Clickjacking?
**Lösung:** Verbiete das Einbetten in fremde Seiten.

```apache
Header always append X-Frame-Options SAMEORIGIN
```

---

## ❓ Wie verhindere ich Caching sensibler Inhalte?
**Lösung:** Setze Cache‑Kontroll‑Header.

```apache
<FilesMatch "\.(json|env|key|config)$">
    Header set Cache-Control "no-store, no-cache, must-revalidate"
</FilesMatch>
```

---

## ❓ Wie leite ich alle Requests an index.php weiter (sauberes Routing)?
**Lösung:** Klassisches Front‑Controller‑Pattern.

```apache
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^ index.php [L]
```

---

## ❓ Wie verhindere ich Hotlinking von Bildern?
**Lösung:** Blockiere fremde Domains.

```apache
RewriteEngine On
RewriteCond %{HTTP_REFERER} !^$
RewriteCond %{HTTP_REFERER} !example\.com [NC]
RewriteRule \.(jpg|jpeg|png|gif)$ - [F]
```

---

## Pro-Tipp
Teste Änderungen immer zuerst in einer Staging-Umgebung – Syntaxfehler führen sofort zu einem **500 Internal Server Error**.
