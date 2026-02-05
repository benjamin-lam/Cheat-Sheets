---
title: Hardened .htaccess Cheat Sheet
category: Security
last_updated: 2025-09-02
status: stable
---

# Hardened .htaccess: Server-Sicherheit & Routing

Dieses Sheet bietet erprobte Lösungen für Apache-Server, um die Sicherheit zu erhöhen und sauberes Routing zu garantieren.

### ❓ Wie schütze ich sensible System-Ordner vor direktem Zugriff?
**Lösung:** Nutze eine RewriteRule, die den Zugriff auf Kern-Verzeichnisse blockiert und einen "403 Forbidden" sendet.
```apache
# Blockiert Zugriff auf core, content, jobs und templates
RewriteRule ^(core|content|jobs|templates)(/.*)?$ - [F,L,NC]
```

### ❓ Wie verhindere ich, dass Nutzer die Dateiliste eines Ordners sehen?
**Lösung:** Deaktiviere das automatische Directory Indexing.
```apache
Options -Indexes
```

### ❓ Wie erzwinge ich HTTPS und entferne gleichzeitig das "www"?
**Lösung:** Kombiniere beide Regeln, um unnötige Redirect-Ketten zu vermeiden (gut für SEO und Performance).
```apache
RewriteCond %{HTTP_HOST} ^www\.(.*)$ [NC]
RewriteRule ^(.*)$ https://%1/$1 [R=301,L]

RewriteCond %{HTTPS} !=on
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

### ❓ Wie blockiere ich den Zugriff auf versteckte Dateien (z.B. .env oder .git)?
**Lösung:** Nutze eine FilesMatch-Direktive für alle Dateien, die mit einem Punkt beginnen.
```apache
<FilesMatch "^\.">
    Order Allow,Deny
    Deny from all
</FilesMatch>
```

### ❓Wie gebe ich die llms.txt für KI-Crawler frei (CORS)?
**Lösung:** Setze den Header spezifisch für diese Datei, damit KI-Agenten sie domänenübergreifend lesen können.
```apache
<Files "llms.txt">
    <IfModule mod_headers.c>
        Header set Access-Control-Allow-Origin "*"
    </IfModule>
</Files>
```
Pro-Tipp: Teste Änderungen an der .htaccess immer erst in einer Staging-Umgebung, da Syntaxfehler sofort zu einem "500 Internal Server Error" führen.

