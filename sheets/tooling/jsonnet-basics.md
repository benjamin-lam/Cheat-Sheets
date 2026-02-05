---
title: Jsonnet Basics Cheat Sheet
category: Tooling
last_updated: 2025-09-02
status: stable
---

# Jsonnet: Strukturierte Konfiguration für K8s, CI/CD & Templates

Dieses Sheet zeigt die wichtigsten Jsonnet‑Konzepte, um komplexe Konfigurationen modular, wiederverwendbar und DRY zu halten — ideal für Kubernetes‑Manifeste, CI/CD‑Pipelines und Infrastruktur‑Templates.

---

## ❓ Was ist Jsonnet?
**Lösung:** Eine erweiterte JSON‑Superset‑Sprache mit:

- Variablen  
- Funktionen  
- Imports  
- Mixins  
- Vererbung  
- Templates  

Perfekt für große Konfigurationslandschaften.

---

## ❓ Wie definiere ich Variablen?
**Lösung:** Lokale Bindings.

```jsonnet
local port = 8080;

{
  servicePort: port,
}
```

---

## ❓ Wie nutze ich Funktionen?
**Lösung:** Parameterisierte Konfigurationen.

```jsonnet
local mkService(name, port) = {
  apiVersion: "v1",
  kind: "Service",
  metadata: { name: name },
  spec: {
    ports: [{ port: port }],
  },
};

mkService("api", 8080)
```

---

## ❓ Wie importiere ich andere Dateien?
**Lösung:** `import` oder `importstr`.

```jsonnet
local config = import "config.libsonnet";
local raw = importstr "template.yaml";
```

---

## ❓ Wie mache ich Konfigurationen wiederverwendbar?
**Lösung:** Mixins kombinieren.

```jsonnet
local base = {
  replicas: 2,
};

local prod = base + {
  replicas: 5,
};

prod
```

---

## ❓ Wie generiere ich mehrere Dateien?
**Lösung:** Multi‑Document‑Output.

```jsonnet
{
  "deployment.json": deployment,
  "service.json": service,
}
```

Mit `jsonnet -m out/ config.jsonnet` werden Dateien erzeugt.

---

## ❓ Wie rendere ich Kubernetes‑Manifeste?
**Lösung:** Jsonnet + kubernetes‑libsonnet.

```jsonnet
local k = import "k8s.libsonnet";

k.Deployment("api") {
  spec+: {
    replicas: 3,
  },
}
```

---

## ❓ Wie überschreibe ich Felder elegant?
**Lösung:** `+:` für Deep Merge.

```jsonnet
spec+: {
  template+: {
    spec+: {
      containers+: [{
        image: "app:v2",
      }],
    },
  },
}
```

---

## ❓ Wie debugge ich Jsonnet?
**Lösung:** `std.log` und `--trace`.

```jsonnet
std.log("Debug info: " + std.toString(x))
```

CLI:

```bash
jsonnet --trace config.jsonnet
```

---

## Pro-Tipp
Nutze `.libsonnet` für wiederverwendbare Module und `.jsonnet` für konkrete Instanzen — so bleibt deine Struktur sauber und skalierbar.
