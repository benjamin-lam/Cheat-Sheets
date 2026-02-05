---
title: Makefile Patterns Cheat Sheet
category: Tooling
last_updated: 2025-09-02
status: stable
---

# Makefile Patterns: Targets, Rules & Build-Pipelines

Dieses Sheet zeigt die wichtigsten Makefile‑Techniken für wiederholbare Builds, Self‑Documentation und modulare Automatisierung.

---

## ❓ Wie definiere ich einfache Targets?
**Lösung:** Targets ohne Datei‑Abhängigkeit als `.PHONY`.

```make
.PHONY: build clean

build:
	@echo "Building project..."

clean:
	rm -rf dist/
```

---

## ❓ Wie mache ich ein Makefile selbst-dokumentierend?
**Lösung:** Help‑Target mit automatischer Beschreibung.

```make
help:
	@grep -E '^[a-zA-Z_-]+:.*?##' Makefile | awk 'BEGIN {FS = ":.*?##"}; {printf "%-20s %s\n", $$1, $$2}'
```

Targets:

```make
build: ## Build the project
clean: ## Remove build artifacts
```

---

## ❓ Wie nutze ich Variablen?
**Lösung:** Variablen definieren und wiederverwenden.

```make
APP=server.php
PHP=php

run:
	$(PHP) $(APP)
```

---

## ❓ Wie definiere ich Pattern Rules?
**Lösung:** Automatische Regeln für Dateitypen.

```make
%.o: %.c
	gcc -c $< -o $@
```

`$<` = erste Abhängigkeit  
`$@` = Zielname  

---

## ❓ Wie baue ich mehrere Targets in einem Schritt?
**Lösung:** Multi‑Target‑Definition.

```make
.PHONY: all
all: clean build test
```

---

## ❓ Wie nutze ich Umgebungsvariablen?
**Lösung:** Variablen überschreibbar machen.

```make
ENV ?= dev

deploy:
	@echo "Deploying to $(ENV)"
```

Aufruf:

```bash
make deploy ENV=prod
```

---

## ❓ Wie verhindere ich unnötige Rebuilds?
**Lösung:** Abhängigkeiten definieren.

```make
app: main.o utils.o
	gcc main.o utils.o -o app
```

Nur geänderte `.o`‑Dateien werden neu gebaut.

---

## ❓ Wie definiere ich Default‑Targets?
**Lösung:** Erstes Target wird automatisch ausgeführt.

```make
default: build
```

---

## ❓ Wie nutze ich Includes für modulare Makefiles?
**Lösung:** Mehrere Makefiles kombinieren.

```make
include config.mk
include tasks/*.mk
```

---

## Pro-Tipp
Nutze `set -e` in Shell‑Commands, um Builds bei Fehlern sofort zu stoppen — oder schreibe komplexe Schritte in eigene Skripte.
