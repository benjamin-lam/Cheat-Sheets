---
title: NGINX Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# NGINX Basics: Reverse Proxy, Caching & Security

Dieses Sheet zeigt die wichtigsten NGINX‑Konfigurationen für Webserver, Reverse Proxies, SSL‑Termination und Performance‑Optimierung.

---

## ❓ Wie starte ich einen einfachen Static File Server?
**Lösung:** Minimal‑Konfiguration.

```nginx
server {
    listen 80;
    server_name example.com;

    root /var/www/html;
    index index.html;
}
```

---

## ❓ Wie richte ich einen Reverse Proxy ein?
**Lösung:** Proxy‑Pass auf Backend.

```nginx
location / {
    proxy_pass http://127.0.0.1:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
}
```

---

## ❓ Wie aktiviere ich HTTPS?
**Lösung:** SSL‑Block + Zertifikate.

```nginx
server {
    listen 443 ssl;
    server_name example.com;

    ssl_certificate     /etc/ssl/cert.pem;
    ssl_certificate_key /etc/ssl/key.pem;
}
```

---

## ❓ Wie leite ich HTTP auf HTTPS um?
**Lösung:** 301 Redirect.

```nginx
server {
    listen 80;
    server_name example.com;
    return 301 https://$host$request_uri;
}
```

---

## ❓ Wie aktiviere ich Gzip‑Kompression?
**Lösung:** gzip on.

```nginx
gzip on;
gzip_types text/plain text/css application/json application/javascript;
gzip_min_length 1024;
```

---

## ❓ Wie setze ich Caching‑Header?
**Lösung:** Cache‑Control für statische Assets.

```nginx
location ~* \.(css|js|png|jpg|svg|woff2)$ {
    expires 30d;
    add_header Cache-Control "public, immutable";
}
```

---

## ❓ Wie limitiere ich Requests?
**Lösung:** Rate Limiting.

```nginx
limit_req_zone $binary_remote_addr zone=api:10m rate=5r/s;

location /api/ {
    limit_req zone=api burst=10 nodelay;
}
```

---

## ❓ Wie verhindere ich große Uploads?
**Lösung:** client_max_body_size.

```nginx
client_max_body_size 10M;
```

---

## ❓ Wie logge ich Requests übersichtlich?
**Lösung:** Custom Log Format.

```nginx
log_format main '$remote_addr - $request_time "$request" $status $body_bytes_sent';
access_log /var/log/nginx/access.log main;
```

---

## ❓ Wie leite ich Pfade um?
**Lösung:** rewrite.

```nginx
rewrite ^/old/(.*)$ /new/$1 permanent;
```

---

## ❓ Wie blockiere ich IP‑Adressen?
**Lösung:** deny.

```nginx
deny 192.168.1.10;
allow all;
```

---

## Pro-Tipp
Nutze `nginx -t` vor jedem Reload — Syntaxfehler sind der häufigste Grund für Downtime nach Deployments.
