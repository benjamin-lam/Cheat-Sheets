---
title: Load Balancing Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Load Balancing: HAProxy, Nginx & Health Checks

Dieses Sheet zeigt die wichtigsten Patterns für skalierbare Web‑Architekturen.

---

## ❓ Wie konfiguriere ich einfaches Round‑Robin‑Balancing?
**Lösung:** Nginx Upstream‑Block.

```nginx
upstream backend {
    server 10.0.0.1;
    server 10.0.0.2;
}

server {
    location / {
        proxy_pass http://backend;
    }
}
```

---

## ❓ Wie aktiviere ich Health Checks?
**Lösung:** HAProxy bietet eingebaute Checks.

```haproxy
backend app
    balance roundrobin
    option httpchk GET /health
    server app1 10.0.0.1:80 check
    server app2 10.0.0.2:80 check
```

---

## ❓ Wie verhindere ich Session‑Verlust?
**Lösung:** Sticky Sessions.

```haproxy
backend app
    balance roundrobin
    cookie SERVERID insert indirect nocache
    server app1 10.0.0.1:80 cookie s1
    server app2 10.0.0.2:80 cookie s2
```

---

## ❓ Wie verteile ich Last nach Server‑Kapazität?
**Lösung:** Weighted Balancing.

```nginx
upstream backend {
    server 10.0.0.1 weight=3;
    server 10.0.0.2 weight=1;
}
```

---

## ❓ Wie verhindere ich Überlastung?
**Lösung:** Rate Limiting.

```nginx
limit_req_zone $binary_remote_addr zone=api:10m rate=5r/s;

location /api/ {
    limit_req zone=api burst=10;
}
```

---

## ❓ Wie leite ich Traffic bei Ausfall um?
**Lösung:** Backup‑Server definieren.

```nginx
upstream backend {
    server 10.0.0.1;
    server 10.0.0.2 backup;
}
```

---

## ❓ Welche Balancing‑Methoden gibt es?
**Lösung:** Die wichtigsten Strategien.

- **round_robin** – gleichmäßige Verteilung  
- **least_conn** – ideal für APIs mit variabler Dauer  
- **ip_hash** – stabil für Sessions ohne Cookies  
- **random** – gut für große Pools  

---

## Pro-Tipp
Nutze `least_conn` für APIs mit stark schwankenden Response‑Zeiten.
