---
title: Prometheus & Grafana Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Prometheus & Grafana Basics: Metrics, Alerts & Dashboards

Dieses Sheet bündelt die wichtigsten Konzepte für Monitoring, Metriken, Alerting und Visualisierung — ideal für produktionsnahe Systeme, Microservices und Infrastruktur‑Beobachtung.

---

# Prometheus

## ❓ Wie funktioniert Prometheus?
**Lösung:** Pull‑basiertes Monitoring.

- Prometheus **scraped** Targets über HTTP  
- Targets liefern `/metrics` im Textformat  
- Zeitreihen werden lokal gespeichert  
- PromQL für Abfragen  
- Alertmanager für Benachrichtigungen  

---

## ❓ Wie sieht eine einfache prometheus.yml aus?
**Lösung:** Minimal‑Konfiguration.

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "api"
    static_configs:
      - targets: ["localhost:9100"]
```

---

## ❓ Wie exponiere ich Metriken?
**Lösung:** `/metrics` Endpoint.

Beispiele:

- Node Exporter → Systemmetriken  
- cAdvisor → Containermetriken  
- App‑Frameworks (Laravel, Spring, Go, Node)  

---

## ❓ Wie schreibe ich PromQL‑Queries?
**Lösung:** Grundformen.

Alle Metriken:

```promql
up
```

CPU‑Auslastung:

```promql
rate(process_cpu_seconds_total[5m])
```

Requests pro Sekunde:

```promql
rate(http_requests_total[1m])
```

Durchschnittliche Latenz:

```promql
histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))
```

---

## ❓ Wie mache ich Alerts?
**Lösung:** alerting rules.

```yaml
groups:
  - name: api-alerts
    rules:
      - alert: HighErrorRate
        expr: rate(http_requests_total{status=~"5.."}[5m]) > 0.1
        for: 2m
        labels:
          severity: critical
        annotations:
          description: "High error rate detected"
```

---

## ❓ Wie sende ich Alerts?
**Lösung:** Alertmanager.

Beispiel‑Konfiguration:

```yaml
route:
  receiver: "slack"

receivers:
  - name: "slack"
    slack_configs:
      - channel: "#alerts"
        send_resolved: true
```

---

# Grafana

## ❓ Wie verbinde ich Grafana mit Prometheus?
**Lösung:** Data Source hinzufügen.

```text
URL: http://prometheus:9090
Type: Prometheus
```

---

## ❓ Wie erstelle ich Dashboards?
**Lösung:** Panels + Queries.

Typische Panels:

- CPU / RAM / Disk  
- Request Rate  
- Error Rate  
- Latency (P50, P90, P95, P99)  
- Queue Length  
- DB Connections  

---

## ❓ Wie mache ich Variablen?
**Lösung:** Dashboard‑Variablen.

Beispiel:

- Typ: Query  
- Query: `label_values(job)`  
- Name: `job`  

Dann in Panels:

```promql
rate(http_requests_total{job="$job"}[5m])
```

---

## ❓ Wie mache ich Alerts in Grafana?
**Lösung:** Grafana Alerting.

- Query definieren  
- Threshold setzen  
- Notification Channel wählen  

---

## ❓ Wie importiere ich fertige Dashboards?
**Lösung:** Grafana.com ID.

Beispiele:

- Node Exporter Full → ID 1860  
- Kubernetes Cluster Monitoring → ID 6417  
- Prometheus 2.0 Stats → ID 3662  

---

# Exporter Übersicht

## ❓ Welche Exporter sind wichtig?
**Lösung:** Die wichtigsten Standard‑Exporter.

| Exporter          | Zweck |
|-------------------|-------|
| Node Exporter     | Systemmetriken |
| cAdvisor          | Containermetriken |
| Blackbox Exporter | HTTP/TCP/ICMP Checks |
| MySQL Exporter    | DB‑Metriken |
| Postgres Exporter | DB‑Metriken |
| Redis Exporter    | Redis‑Stats |
| NGINX Exporter    | Webserver‑Metriken |

---

# Pro-Tipp
Nutze **Recording Rules**, um teure PromQL‑Queries vorzuberechnen — das macht Dashboards schneller und Alerts zuverlässiger.
