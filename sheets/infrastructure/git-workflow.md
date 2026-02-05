---
title: Git Workflow Cheat Sheet
category: Infrastructure
last_updated: 2025-09-02
status: stable
---

# Git Workflow: Rettungs‑Befehle, Rebase‑Tricks & Branch‑Cleanup

Dieses Sheet bündelt die wichtigsten Git‑Kommandos für tägliche Arbeit, saubere Historien und schnelle Rettung aus schwierigen Situationen.

---

## ❓ Wie mache ich einen Commit rückgängig?
**Lösung:** Soft, Mixed oder Hard Reset.

Soft (nur Commit rückgängig, Änderungen bleiben gestaged):

```bash
git reset --soft HEAD~1
```

Mixed (Änderungen bleiben, aber ungestaged):

```bash
git reset HEAD~1
```

Hard (alles verwerfen):

```bash
git reset --hard HEAD~1
```

---

## ❓ Wie hole ich gelöschte Dateien zurück?
**Lösung:** Checkout aus der Historie.

```bash
git checkout HEAD -- path/to/file
```

---

## ❓ Wie finde ich verlorene Commits?
**Lösung:** reflog zeigt alles.

```bash
git reflog
```

Wiederherstellen:

```bash
git checkout <commit>
```

---

## ❓ Wie squash ich mehrere Commits?
**Lösung:** Interaktives Rebase.

```bash
git rebase -i HEAD~5
```

Dann `pick` → `squash`.

---

## ❓ Wie löse ich Merge‑Konflikte sauber?
**Lösung:** Konflikte markieren, bearbeiten, committen.

```bash
git status
git add <file>
git rebase --continue
```

---

## ❓ Wie aktualisiere ich meinen Feature‑Branch?
**Lösung:** Rebase statt Merge.

```bash
git checkout feature
git fetch origin
git rebase origin/main
```

---

## ❓ Wie pushe ich ein Rebase sauber?
**Lösung:** Force‑Push mit Sicherheit.

```bash
git push --force-with-lease
```

---

## ❓ Wie lösche ich lokale und Remote‑Branches?
**Lösung:** Cleanup.

Lokal:

```bash
git branch -d feature
```

Remote:

```bash
git push origin --delete feature
```

---

## ❓ Wie sehe ich eine schöne Commit‑Historie?
**Lösung:** One‑line Log.

```bash
git log --oneline --graph --decorate --all
```

---

## ❓ Wie stashe ich Änderungen?
**Lösung:** Temporär speichern.

```bash
git stash
git stash pop
```

Mit Nachricht:

```bash
git stash push -m "WIP: refactor"
```

---

## ❓ Wie patche ich einzelne Dateien aus einem Commit?
**Lösung:** Checkout mit Commit‑Hash.

```bash
git checkout <commit> -- file.php
```

---

## ❓ Wie mache ich einen Commit amend?
**Lösung:** Letzten Commit überschreiben.

```bash
git commit --amend
```

---

## Pro-Tipp
Nutze `git worktree`, um mehrere Branches gleichzeitig ausgecheckt zu haben — ideal für Hotfixes während laufender Features.
