---
title: Kafka Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Kafka Basics: Topics, Partitions, Consumers & Delivery Guarantees

Dieses Sheet bündelt die wichtigsten Kafka‑Konzepte für Event‑Streaming, Microservices, Log‑Pipelines und verteilte Systeme — ideal für produktionsnahe Architekturen.

---

## ❓ Was ist Kafka?
**Lösung:** Ein verteilter Event‑Streaming‑Dienst mit:

- Topics (logische Streams)
- Partitionen (Skalierung + Parallelität)
- Producer (schreiben Events)
- Consumer (lesen Events)
- Broker (Server)
- Consumer Groups (Lastverteilung)

---

## ❓ Wie erstelle ich ein Topic?
**Lösung:** kafka-topics CLI.

```bash
kafka-topics.sh --create \
  --topic events \
  --bootstrap-server localhost:9092 \
  --partitions 3 \
  --replication-factor 1
```

---

## ❓ Wie liste ich Topics auf?
**Lösung:** list.

```bash
kafka-topics.sh --list --bootstrap-server localhost:9092
```

---

## ❓ Wie produziere ich Nachrichten?
**Lösung:** kafka-console-producer.

```bash
kafka-console-producer.sh \
  --topic events \
  --bootstrap-server localhost:9092
```

Dann Text eingeben.

---

## ❓ Wie konsumiere ich Nachrichten?
**Lösung:** kafka-console-consumer.

```bash
kafka-console-consumer.sh \
  --topic events \
  --bootstrap-server localhost:9092 \
  --from-beginning
```

---

## ❓ Wie funktionieren Consumer Groups?
**Lösung:** Mehrere Consumer teilen sich Partitionen.

- Jeder Consumer einer Gruppe liest **exakt eine Partition**  
- Mehr Consumer als Partitionen → einige sind idle  
- Mehr Partitionen als Consumer → Skalierung möglich  

Status anzeigen:

```bash
kafka-consumer-groups.sh \
  --bootstrap-server localhost:9092 \
  --describe \
  --group mygroup
```

---

## ❓ Wie funktionieren Offsets?
**Lösung:** Jeder Consumer speichert seinen Fortschritt.

- automatisch (`enable.auto.commit=true`)
- manuell (`commitSync()` / `commitAsync()`)

Offsets bestimmen:

- wo ein Consumer weitermacht  
- Replays (z. B. für Debugging)  

---

## ❓ Welche Delivery Guarantees gibt es?
**Lösung:** Kafka bietet drei Stufen.

- **at most once** – schnell, aber Datenverlust möglich  
- **at least once** – Standard, Duplikate möglich  
- **exactly once** – teuer, nur mit Transaktionen  

Producer‑Einstellungen:

```properties
acks=all
retries=∞
enable.idempotence=true
```

---

## ❓ Wie mache ich Replays?
**Lösung:** Offsets zurücksetzen.

```bash
kafka-consumer-groups.sh \
  --bootstrap-server localhost:9092 \
  --group mygroup \
  --reset-offsets --to-earliest --execute \
  --topic events
```

---

## ❓ Wie skaliere ich Kafka?
**Lösung:** Partitionen erhöhen.

```bash
kafka-topics.sh --alter \
  --topic events \
  --partitions 6 \
  --bootstrap-server localhost:9092
```

Achtung: Reihenfolge der Events pro Partition bleibt, aber global nicht.

---

## ❓ Wie überwache ich Kafka?
**Lösung:** Wichtige Metriken.

- Lag pro Consumer Group  
- Anzahl Partitionen  
- Broker‑Health  
- ISR (in‑sync replicas)  
- Under‑replicated partitions  

Tools:

- Kafka UI  
- Prometheus + Grafana  
- Burrow  

---

## ❓ Wie sichere ich Kafka ab?
**Lösung:** TLS + SASL.

TLS aktivieren:

```properties
security.protocol=SSL
ssl.truststore.location=/etc/kafka/truststore.jks
```

SASL (SCRAM):

```properties
security.protocol=SASL_SSL
sasl.mechanism=SCRAM-SHA-512
```

---

## Pro-Tipp
Kafka ist am stärksten, wenn Events **immutable** bleiben — nie ändern, immer neue Events schreiben. Das macht Replays, Debugging und Auditing trivial.
