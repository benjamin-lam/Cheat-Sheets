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
