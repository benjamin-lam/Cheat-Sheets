---
title: GitHub Basics Cheat Sheet
category: DevOps
last_updated: 2025-09-02
status: stable
---

# GitHub Basics: Repos, Pull Requests, Actions & Collaboration

Dieses Sheet bündelt die wichtigsten GitHub‑Konzepte für moderne Software‑Teams — ideal für Open Source, interne Repos und CI/CD‑Automatisierung.

---

## ❓ Wie erstelle ich ein Repository?
**Lösung:** GitHub UI oder CLI.

CLI:

```bash
gh repo create myproject --public
```

Clone:

```bash
git clone git@github.com:org/myproject.git
```

---

## ❓ Wie funktionieren Pull Requests?
**Lösung:** Code‑Änderungen vorschlagen & reviewen.

Typischer Ablauf:

1. Branch erstellen  
2. Änderungen committen  
3. Branch pushen  
4. Pull Request öffnen  
5. Review & Diskussion  
6. Merge  

PR erstellen:

```bash
gh pr create --title "Add login" --body "Implements login flow"
```

---

## ❓ Wie funktionieren Reviews?
**Lösung:** Kommentare, Approvals, Change Requests.

Reviewer können:

- kommentieren  
- einzelne Zeilen markieren  
- „Approve“ geben  
- „Request Changes“ setzen  

---

## ❓ Wie funktionieren Issues?
**Lösung:** Aufgaben, Bugs, Ideen.

Typische Felder:

- Titel  
- Beschreibung  
- Labels  
- Assignees  
- Milestones  

Issue erstellen:

```bash
gh issue create --title "Bug: Login fails" --body "Steps to reproduce..."
```

---

## ❓ Wie funktionieren Labels?
**Lösung:** Kategorisierung.

Beispiele:

- bug  
- enhancement  
- documentation  
- good first issue  
- help wanted  

---

## ❓ Wie funktionieren Milestones?
**Lösung:** Releases planen.

Beispiel:

- v1.0  
- Q3‑Release  
- Sprint 12  

---

## ❓ Wie funktionieren GitHub Projects?
**Lösung:** Kanban‑Boards & Roadmaps.

Typische Spalten:

- Todo  
- In Progress  
- Review  
- Done  

---

## ❓ Wie funktionieren GitHub Actions?
**Lösung:** CI/CD‑Workflows.

Beispiel:

```yaml
name: CI
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm test
```

---

## ❓ Wie funktionieren Environments?
**Lösung:** Deployment‑Gates.

Beispiele:

- staging  
- production  

Mit Schutz:

- required reviewers  
- wait timers  
- secrets pro Environment  

---

## ❓ Wie funktionieren GitHub Packages?
**Lösung:** Container Registry & Package Hosting.

Docker Push:

```bash
docker tag myapp ghcr.io/org/myapp:latest
docker push ghcr.io/org/myapp:latest
```

---

## ❓ Wie sichere ich Secrets?
**Lösung:** GitHub Encrypted Secrets.

Beispiele:

- API Keys  
- DB Credentials  
- Tokens  

Zugriff in Actions:

```yaml
env:
  API_KEY: ${{ secrets.API_KEY }}
```

---

## ❓ Wie mache ich Releases?
**Lösung:** Tags + Release Notes.

```bash
gh release create v1.0.0 --notes "Initial release"
```

---

## ❓ Wie arbeite ich mit Dependabot?
**Lösung:** automatische Updates.

Beispiel:

```yaml
version: 2
updates:
  - package-ecosystem: npm
    directory: "/"
    schedule:
      interval: weekly
```

---

## Pro-Tipp
Nutze **Branch Protection + Required Reviews + Actions**, um ein sicheres, reproduzierbares und teamfähiges GitHub‑Ökosystem aufzubauen.
