---
title: RabbitMQ Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# RabbitMQ Basics: Queues, Exchanges, Routing & Acknowledgements

Dieses Sheet bündelt die wichtigsten RabbitMQ‑Konzepte für Messaging, Event‑Verarbeitung, Microservices und verlässliche Hintergrundjobs — ideal für produktionsnahe Systeme.

---

## ❓ Was ist RabbitMQ?
**Lösung:** Ein Message Broker mit:

- **Exchanges** (verteilen Nachrichten)
- **Queues** (halten Nachrichten)
- **Bindings** (Routing‑Regeln)
- **Producers** (senden Nachrichten)
- **Consumers** (verarbeiten Nachrichten)
- **Acks** (Zustellbestätigung)

RabbitMQ basiert auf AMQP 0.9.1.

---

## ❓ Welche Exchange‑Typen gibt es?
**Lösung:** Vier Standardtypen.

| Typ        | Verhalten |
|------------|-----------|
| direct     | exakte Routing Keys |
| topic      | Wildcards (`*`, `#`) |
| fanout     | broadcast an alle Queues |
| headers    | Routing nach Header‑Werten |

---

## ❓ Wie sende ich Nachrichten?
**Lösung:** Producer CLI.

```bash
rabbitmqadmin publish exchange=amq.direct routing_key=test payload="Hello"
```

---

## ❓ Wie empfange ich Nachrichten?
**Lösung:** Consumer CLI.

```bash
rabbitmqadmin get queue=myqueue
```

---

## ❓ Wie erstelle ich eine Queue?
**Lösung:** Queue deklarieren.

```bash
rabbitmqadmin declare queue name=myqueue durable=true
```

---

## ❓ Wie binde ich eine Queue an eine Exchange?
**Lösung:** Binding.

```bash
rabbitmqadmin declare binding source=amq.direct destination=myqueue routing_key=test
```

---

## ❓ Wie funktionieren Acknowledgements?
**Lösung:** Drei Modi.

- **auto‑ack** → Nachricht gilt sofort als verarbeitet  
- **manual ack** → Consumer bestätigt explizit  
- **nack / reject** → Nachricht zurück in Queue oder verwerfen  

Beispiel:

```bash
basic.ack
basic.nack requeue=true
```

---

## ❓ Wie verhindere ich Message‑Loss?
**Lösung:** Drei Ebenen absichern.

1. **durable queue**  
2. **persistent messages**  
3. **publisher confirms**

Queue:

```bash
durable=true
```

Message:

```bash
delivery_mode=2
```

Publisher Confirms:

```bash
confirm_select
```

---

## ❓ Wie mache ich Dead Letter Queues (DLQ)?
**Lösung:** DLX + Routing Key.

```bash
rabbitmqadmin declare exchange name=dlx type=direct
rabbitmqadmin declare queue name=dlq durable=true
rabbitmqadmin declare binding source=dlx destination=dlq routing_key=dead
```

Queue mit DLX:

```bash
arguments='{"x-dead-letter-exchange":"dlx","x-dead-letter-routing-key":"dead"}'
```

---

## ❓ Wie setze ich TTLs?
**Lösung:** Per Queue oder Message.

Queue‑TTL:

```bash
arguments='{"x-message-ttl":60000}'
```

Message‑TTL:

```bash
expiration: "60000"
```

---

## ❓ Wie mache ich Prioritäts‑Queues?
**Lösung:** x-max-priority.

```bash
arguments='{"x-max-priority":10}'
```

---

## ❓ Wie skaliere ich Consumer?
**Lösung:** Prefetch.

```bash
basic.qos prefetch_count=10
```

Verhindert, dass ein Consumer zu viele Nachrichten auf einmal bekommt.

---

## ❓ Wie überwache ich RabbitMQ?
**Lösung:** Management Plugin.

Aktivieren:

```bash
rabbitmq-plugins enable rabbitmq_management
```

UI:

```
http://localhost:15672
```

Wichtige Metriken:

- Queue‑Länge  
- Unacked Messages  
- Consumer‑Lag  
- Connection‑Health  

---

## ❓ Wie sichere ich RabbitMQ ab?
**Lösung:** Benutzer + VHosts + TLS.

Benutzer:

```bash
rabbitmqctl add_user ben secret
rabbitmqctl set_permissions -p / ben ".*" ".*" ".*"
```

TLS aktivieren in `rabbitmq.conf`:

```ini
listeners.ssl.default = 5671
ssl_options.cacertfile = /etc/ssl/ca.pem
ssl_options.certfile   = /etc/ssl/cert.pem
ssl_options.keyfile    = /etc/ssl/key.pem
```

---

## Pro-Tipp
Nutze **Lazy Queues** (`x-queue-mode=lazy`) für große Backlogs — Nachrichten werden auf Disk statt im RAM gehalten und verhindern Memory‑Pressure.
