---
title: Logging Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Logging Basics: Struktur, Levels, Pipelines & Best Practices

Dieses Sheet bündelt die wichtigsten Logging‑Konzepte für produktionsnahe Systeme, verteilte Architekturen, Observability‑Stacks und Debugging.

---

## ❓ Warum ist Logging wichtig?
**Lösung:** Logs sind die primäre Quelle für:

- Debugging  
- Incident Response  
- Monitoring & Alerting  
- Auditing & Compliance  
- Performance‑Analyse  

Gute Logs sind **strukturiert, vollständig, maschinenlesbar**.

---

## ❓ Welche Log‑Levels gibt es?
**Lösung:** Standard‑Levels.

| Level     | Bedeutung |
|-----------|-----------|
| TRACE     | extrem detailliert |
| DEBUG     | Entwickler‑Infos |
| INFO      | normaler Betrieb |
| WARN      | ungewöhnlich, aber nicht kritisch |
| ERROR     | Fehler, aber System läuft weiter |
| FATAL     | System nicht mehr funktionsfähig |

---

## ❓ Wie sollten Logs strukturiert sein?
**Lösung:** JSON‑Format.

Beispiel:

```json
{
  "timestamp": "2025-09-02T12:00:00Z",
  "level": "info",
  "message": "User logged in",
  "user_id": 42,
  "ip": "192.168.1.10",
  "request_id": "abc-123"
}
```

Wichtig:

- keine freien Textwüsten  
- keine stack traces ohne Kontext  
- immer `request_id` / `correlation_id`  

---

## ❓ Wie logge ich in Microservices?
**Lösung:** Korrelation über Request‑IDs.

Jeder Service:

- liest `X-Request-ID`  
- erzeugt eine, wenn keine existiert  
- schreibt sie in jeden Log‑Eintrag  

---

## ❓ Wie leite ich Logs weiter?
**Lösung:** Log‑Pipelines.

Typische Stacks:

- **ELK** (Elasticsearch, Logstash, Kibana)  
- **EFK** (Elasticsearch, Fluentd, Kibana)  
- **Loki + Promtail + Grafana**  
- **OpenSearch + FluentBit**  

---

## ❓ Wie sieht eine Fluent Bit Config aus?
**Lösung:** Minimal‑Pipeline.

```ini
[INPUT]
    Name tail
    Path /var/log/app.log

[OUTPUT]
    Name  es
    Host  elasticsearch
    Port  9200
    Index logs
```

---

## ❓ Wie sieht eine Loki‑Pipeline aus?
**Lösung:** Promtail.

```yaml
scrape_configs:
  - job_name: app
    static_configs:
      - targets: [localhost]
        labels:
          job: app
          __path__: /var/log/app.log
```

---

## ❓ Wie logge ich Exceptions richtig?
**Lösung:** Stacktrace + Kontext.

```json
{
  "level": "error",
  "message": "Payment failed",
  "order_id": 123,
  "exception": {
    "type": "TimeoutException",
    "message": "Gateway timeout",
    "stack": "..."
  }
}
```

---

## ❓ Wie verhindere ich Log‑Spam?
**Lösung:** Rate‑Limiting & Sampling.

Beispiel:

- nur 1 ERROR pro Sekunde  
- nur 10% DEBUG‑Logs in High‑Traffic‑Systemen  

---

## ❓ Wie mache ich Audit‑Logging?
**Lösung:** unveränderbare Logs.

Wichtig:

- keine Löschung  
- separate Storage‑Klasse  
- fälschungssichere Formate (WORM)  

---

## ❓ Wie mache ich Log‑Rotation?
**Lösung:** logrotate.

```ini
/var/log/app/*.log {
  daily
  rotate 14
  compress
  missingok
}
```

---

## ❓ Wie analysiere ich Logs?
**Lösung:** typische Queries.

Elasticsearch:

```json
status:500 AND service:api
```

Loki:

```logql
{job="api"} |= "error"
```

---

## Pro-Tipp
Nutze **strukturierte Logs + zentrale Pipelines + Request‑IDs**, um echte Observability zu erreichen — Logs werden erst dadurch durchsuchbar, korrelierbar und wertvoll.
