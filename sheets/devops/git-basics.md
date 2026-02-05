---
title: Git Basics Cheat Sheet
category: DevOps
last_updated: 2025-09-02
status: stable
---

# Git Basics: Branching, Commits, Merges & Workflows

Dieses Sheet bündelt die wichtigsten Git‑Konzepte für tägliche Entwicklungsarbeit, Team‑Workflows und saubere Repositories.

---

## ❓ Wie initialisiere ich ein Repository?
**Lösung:** git init.

```bash
git init
```

Remote hinzufügen:

```bash
git remote add origin git@github.com:org/repo.git
```

---

## ❓ Wie mache ich Commits?
**Lösung:** add → commit.

```bash
git add .
git commit -m "Add feature"
```

---

## ❓ Wie arbeite ich mit Branches?
**Lösung:** branch + switch.

Neuen Branch erstellen:

```bash
git checkout -b feature/login
```

Branch wechseln:

```bash
git switch main
```

Branches anzeigen:

```bash
git branch
```

---

## ❓ Wie merge ich Branches?
**Lösung:** merge.

```bash
git checkout main
git merge feature/login
```

Fast‑Forward verhindern:

```bash
git merge --no-ff feature/login
```

---

## ❓ Wie löse ich Merge‑Konflikte?
**Lösung:** Dateien bearbeiten → add → commit.

Konflikte anzeigen:

```bash
git status
```

Nach dem Fix:

```bash
git add <file>
git commit
```

---

## ❓ Wie mache ich Rebase?
**Lösung:** rebase statt merge für lineare Historie.

```bash
git checkout feature/login
git rebase main
```

Interaktiv:

```bash
git rebase -i HEAD~5
```

---

## ❓ Wie pushe ich Änderungen?
**Lösung:** push.

```bash
git push origin main
git push origin feature/login
```

Upstream setzen:

```bash
git push -u origin feature/login
```

---

## ❓ Wie hole ich Änderungen?
**Lösung:** pull oder fetch + merge.

```bash
git pull
```

Oder:

```bash
git fetch
git merge origin/main
```

---

## ❓ Wie mache ich Stashing?
**Lösung:** stash.

```bash
git stash
git stash pop
```

---

## ❓ Wie sehe ich Logs?
**Lösung:** log.

```bash
git log --oneline --graph --decorate
```

---

## ❓ Wie mache ich Tags?
**Lösung:** lightweight oder annotated.

```bash
git tag v1.0.0
git tag -a v1.0.0 -m "Release 1.0.0"
git push origin --tags
```

---

## ❓ Wie mache ich ein sauberes Release?
**Lösung:** Release‑Branch + Tag.

Typisch:

- main → stabil  
- develop → Integration  
- feature/* → Features  
- release/* → Vorbereitung  
- hotfix/* → schnelle Fixes  

---

## ❓ Wie entferne ich versehentlich commitete Dateien?
**Lösung:** reset oder revert.

Letzten Commit rückgängig:

```bash
git reset --soft HEAD~1
```

Commit rückgängig mit neuem Commit:

```bash
git revert <commit>
```

---

## ❓ Wie lösche ich Branches?
**Lösung:** branch -d.

Lokal:

```bash
git branch -d feature/login
```

Remote:

```bash
git push origin --delete feature/login
```

---

## Pro-Tipp
Nutze **rebase für Feature‑Branches** und **merge für Releases** — so bleibt die Historie sauber und nachvollziehbar.
