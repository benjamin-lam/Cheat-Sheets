---
title: Kubernetes Basics Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Kubernetes Basics: Pods, Deployments, Services & Debugging

Dieses Sheet bündelt die wichtigsten Kubernetes‑Konzepte und `kubectl`‑Befehle für produktionsnahe Cluster, lokale Entwicklung (kind, k3d, minikube) und CI/CD‑Automatisierung.

---

## ❓ Wie zeige ich Cluster‑Informationen an?
**Lösung:** Überblick über Nodes & Cluster.

```bash
kubectl cluster-info
kubectl get nodes
kubectl describe node <name>
```

---

## ❓ Wie deploye ich eine Anwendung?
**Lösung:** Deployment erstellen.

```bash
kubectl create deployment api --image=nginx
```

Oder per YAML:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api
spec:
  replicas: 3
  selector:
    matchLabels:
      app: api
  template:
    metadata:
      labels:
        app: api
    spec:
      containers:
        - name: api
          image: nginx
```

---

## ❓ Wie skaliere ich Deployments?
**Lösung:** replicas ändern.

```bash
kubectl scale deployment api --replicas=5
```

---

## ❓ Wie exponiere ich einen Service?
**Lösung:** ClusterIP, NodePort oder LoadBalancer.

```bash
kubectl expose deployment api --port=80 --type=ClusterIP
```

NodePort:

```bash
kubectl expose deployment api --port=80 --type=NodePort
```

---

## ❓ Wie sehe ich Pods & Logs?
**Lösung:** get, describe, logs.

```bash
kubectl get pods
kubectl describe pod <name>
kubectl logs <pod>
kubectl logs -f <pod>
```

---

## ❓ Wie öffne ich eine Shell im Pod?
**Lösung:** exec.

```bash
kubectl exec -it <pod> -- bash
```

---

## ❓ Wie debugge ich Pods?
**Lösung:** ephemeral containers.

```bash
kubectl debug <pod> -it --image=busybox
```

---

## ❓ Wie arbeite ich mit ConfigMaps?
**Lösung:** Key‑Value‑Konfiguration.

Erstellen:

```bash
kubectl create configmap app-config --from-literal=APP_ENV=prod
```

Mounten:

```yaml
env:
  - name: APP_ENV
    valueFrom:
      configMapKeyRef:
        name: app-config
        key: APP_ENV
```

---

## ❓ Wie arbeite ich mit Secrets?
**Lösung:** Base64‑kodiert.

Erstellen:

```bash
kubectl create secret generic app-secret --from-literal=DB_PASS=secret
```

Verwenden:

```yaml
env:
  - name: DB_PASS
    valueFrom:
      secretKeyRef:
        name: app-secret
        key: DB_PASS
```

---

## ❓ Wie mache ich Rolling Updates?
**Lösung:** image ändern.

```bash
kubectl set image deployment/api api=nginx:latest
```

Status prüfen:

```bash
kubectl rollout status deployment/api
```

Rollback:

```bash
kubectl rollout undo deployment/api
```

---

## ❓ Wie definiere ich Ingress?
**Lösung:** HTTP‑Routing.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: api
spec:
  rules:
    - host: example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: api
                port:
                  number: 80
```

---

## ❓ Wie arbeite ich mit Namespaces?
**Lösung:** isolierte Umgebungen.

```bash
kubectl get ns
kubectl create ns staging
kubectl -n staging get pods
```

---

## ❓ Wie prüfe ich Ressourcenverbrauch?
**Lösung:** metrics server.

```bash
kubectl top nodes
kubectl top pods
```

---

## ❓ Wie setze ich Resource Limits?
**Lösung:** requests & limits.

```yaml
resources:
  requests:
    cpu: "100m"
    memory: "256Mi"
  limits:
    cpu: "500m"
    memory: "512Mi"
```

---

## ❓ Wie mache ich Port‑Forwarding?
**Lösung:** lokal auf Pod zugreifen.

```bash
kubectl port-forward <pod> 8080:80
```

---

## ❓ Wie lösche ich Ressourcen?
**Lösung:** delete.

```bash
kubectl delete pod <name>
kubectl delete deployment api
kubectl delete -f file.yaml
```

---

## Pro-Tipp
Nutze `kubectl apply --server-side` für deklarative, konfliktarme Deployments — ideal für GitOps‑Workflows.
