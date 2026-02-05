---
title: CI/CD Basics Cheat Sheet
category: DevOps
last_updated: 2025-09-02
status: stable
---

# CI/CD Basics: Pipelines, Builds, Tests & Deployments

Dieses Sheet bündelt die wichtigsten Konzepte für Continuous Integration und Continuous Delivery — ideal für moderne Software‑Teams, Automatisierung und reproduzierbare Deployments.

---

## ❓ Was ist CI/CD?
**Lösung:** Automatisierte Software‑Lieferkette.

- **CI**: Code zusammenführen, testen, bauen  
- **CD**: Deployments automatisieren  
- Ziel: schneller, sicherer, reproduzierbarer  

---

## ❓ Was gehört in eine CI‑Pipeline?
**Lösung:** typische Stufen.

- Checkout  
- Dependency Install  
- Static Analysis (Linting)  
- Unit Tests  
- Build  
- Artifact Upload  
- Security Scans  
- Integration Tests  

---

## ❓ Was gehört in eine CD‑Pipeline?
**Lösung:** Deployment‑Stufen.

- Build Artifact holen  
- Environment vorbereiten  
- Secrets laden  
- Migrations ausführen  
- Deployment (z. B. Kubernetes, Docker, Server)  
- Health Checks  
- Rollback‑Strategien  

---

## ❓ Wie sieht eine einfache GitHub Actions Pipeline aus?
**Lösung:** Minimal‑Workflow.

```yaml
name: CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npm test
```

---

## ❓ Wie mache ich Caching?
**Lösung:** cache‑Action.

```yaml
- uses: actions/cache@v4
  with:
    path: ~/.npm
    key: npm-${{ hashFiles('package-lock.json') }}
```

---

## ❓ Wie baue ich Docker Images in CI?
**Lösung:** docker build + push.

```yaml
- run: docker build -t myapp:${{ github.sha }} .
- run: docker push myapp:${{ github.sha }}
```

---

## ❓ Wie deploye ich nach Kubernetes?
**Lösung:** kubectl.

```yaml
- uses: azure/k8s-deploy@v4
  with:
    manifests: |
      k8s/deployment.yaml
      k8s/service.yaml
```

---

## ❓ Wie mache ich Canary Deployments?
**Lösung:** Traffic‑Splitting.

Beispiele:

- Kubernetes Ingress  
- Service Mesh (Istio, Linkerd)  
- Feature Flags  

---

## ❓ Wie mache ich Rollbacks?
**Lösung:** automatisiert.

Kubernetes:

```bash
kubectl rollout undo deployment/api
```

GitOps (ArgoCD):

- Revisions vergleichen  
- Sync zurücksetzen  

---

## ❓ Wie sichere ich Secrets?
**Lösung:** Secret Manager.

Optionen:

- GitHub Encrypted Secrets  
- HashiCorp Vault  
- AWS Secrets Manager  
- Kubernetes Secrets (mit KMS)  

---

## ❓ Wie verhindere ich „broken main“?
**Lösung:** Branch Protection.

- Required Status Checks  
- Required Reviews  
- No direct pushes  
- Enforced CI  

---

## ❓ Wie mache ich Multi‑Environment Deployments?
**Lösung:** Environments + Promotion.

Typisch:

- dev → staging → prod  
- manuelle Gates  
- automatische Tests  

---

## ❓ Wie messe ich Pipeline‑Qualität?
**Lösung:** DORA‑Metriken.

- Deployment Frequency  
- Lead Time for Changes  
- Change Failure Rate  
- Mean Time to Recovery  

---

## Pro-Tipp
Nutze **kleine, schnelle Pipelines** für Feedback und **lange, tiefe Pipelines** für Releases — CI/CD wird erst durch diese Trennung wirklich effizient.
