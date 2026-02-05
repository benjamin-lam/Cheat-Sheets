---
title: Tracing Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Tracing Basics: Distributed Traces, Spans, Context & Sampling

Dieses Sheet bündelt die wichtigsten Konzepte für Distributed Tracing in Microservices‑Architekturen — ideal für Debugging, Performance‑Analyse und Observability.

---

## ❓ Was ist Distributed Tracing?
**Lösung:** End‑to‑End‑Verfolgung einer Anfrage durch mehrere Services.

Ein Trace besteht aus:

- **Trace ID** → eindeutige Anfrage  
- **Spans** → einzelne Schritte  
- **Parent/Child‑Beziehungen** → Kausalität  
- **Context Propagation** → Weitergabe über HTTP/Queues  

Tracing beantwortet:

- Wo entsteht Latenz  
- Welche Services sind beteiligt  
- Welche Fehler passieren wo  
- Wie hängen Systeme zusammen  

---

## ❓ Welche Standards gibt es?
**Lösung:** OpenTelemetry (OTel).

OpenTelemetry liefert:

- API (Tracing, Metrics, Logs)  
- SDKs für alle Sprachen  
- Exporter (OTLP, Jaeger, Zipkin)  
- Auto‑Instrumentation  

---

## ❓ Wie sieht ein Span aus?
**Lösung:** typische Felder.

```json
{
  "trace_id": "abc123",
  "span_id": "def456",
  "parent_id": "000000",
  "name": "GET /api/users",
  "start": 1693650000,
  "end": 1693650001,
  "attributes": {
    "http.method": "GET",
    "http.status_code": 200,
    "db.statement": "SELECT * FROM users"
  }
}
```

---

## ❓ Wie funktioniert Context Propagation?
**Lösung:** Trace‑Header werden weitergereicht.

Standard: **W3C Trace Context**

HTTP‑Header:

```
traceparent: 00-<trace-id>-<span-id>-01
tracestate: vendor-specific
```

Jeder Service:

- liest Header  
- erzeugt neuen Span  
- setzt Parent‑ID  
- gibt Header weiter  

---

## ❓ Wie instrumentiere ich eine Anwendung?
**Lösung:** Auto‑Instrumentation.

Beispiele:

Node.js:

```bash
npm install @opentelemetry/sdk-node
```

Go:

```go
import "go.opentelemetry.io/otel"
```

Java:

```bash
java -javaagent:opentelemetry-javaagent.jar -jar app.jar
```

---

## ❓ Wie exportiere ich Traces?
**Lösung:** OTLP Exporter.

Beispiel:

```yaml
exporters:
  otlp:
    endpoint: "http://collector:4317"
```

---

## ❓ Wie sieht eine Collector‑Pipeline aus?
**Lösung:** OpenTelemetry Collector.

```yaml
receivers:
  otlp:
    protocols:
      grpc:

processors:
  batch:

exporters:
  jaeger:
    endpoint: "jaeger:14250"

service:
  pipelines:
    traces:
      receivers: [otlp]
      processors: [batch]
      exporters: [jaeger]
```

---

## ❓ Welche Backends gibt es?
**Lösung:** typische Tracing‑UIs.

- **Jaeger**  
- **Zipkin**  
- **Grafana Tempo**  
- **Honeycomb**  
- **Datadog APM**  
- **New Relic**  

---

## ❓ Wie analysiere ich Traces?
**Lösung:** typische Fragen.

- Wo ist der langsamste Span?  
- Welche Services sind beteiligt?  
- Welche DB‑Queries dauern zu lange?  
- Gibt es Retries oder Timeouts?  
- Welche Fehler propagieren sich?  

---

## ❓ Wie funktioniert Sampling?
**Lösung:** reduziert Datenmenge.

Typen:

- **Always On** → alles speichern  
- **Always Off** → nichts speichern  
- **Probabilistic** → z. B. 10%  
- **Tail‑Based** → erst nach Analyse entscheiden  

Beispiel:

```yaml
samplers:
  parentbased_traceidratio:
    ratio: 0.1
```

---

## ❓ Wie korreliere ich Logs, Metrics & Traces?
**Lösung:** IDs verknüpfen.

Jeder Log‑Eintrag:

- enthält `trace_id`  
- enthält `span_id`  

Metrics:

- enthalten Labels wie `service`, `endpoint`  

Dadurch entsteht **echte Observability**.

---

## Pro-Tipp
Nutze **Tail‑Based Sampling**, um nur wirklich relevante Traces zu speichern — z. B. Fehler, hohe Latenzen oder ungewöhnliche Muster.
