# Git Quick Reference Guide

**Created:** 2026-02-06
**Repo:** github.com/blubat-hub/git-basics

---

## Mental Model

| Concept | What It Is |
|---------|-----------|
| **Repository** | A project folder with memory — remembers every version |
| **Commit** | A save point (snapshot of all files at that moment) |
| **Staging area** | Shopping cart — pick which changes go into the next save |
| **Branch** | A parallel timeline for experimenting safely |
| **Remote** | Cloud copy of your repo (GitHub) |

## The Core Loop

```
Edit files → git add → git commit → git push
```

## File States

```
Untracked → Staged → Committed → Pushed
   (new)     (cart)    (saved)    (on GitHub)
```

In VS Code Source Control:
| Letter | Meaning |
|--------|---------|
| **U** | Untracked (new file) |
| **M** | Modified (changed since last commit) |
| **A** | Added (staged) |
| **D** | Deleted |

---

## Commands

### Setup (one-time)
```bash
git config --global user.name "blubat"
git config --global user.email "blubat.genai.mail@gmail.com"
gh auth login              # authenticate GitHub CLI
gh auth setup-git          # let git use GitHub credentials
```

### Starting a Project
```bash
git init                           # create a repo in current folder
gh repo create name --public       # create on GitHub
git push -u origin main            # first push (-u remembers the link)
```

### Daily Workflow
```bash
git status                 # what's changed?
git diff                   # see exact changes (before staging)
git add file.md            # stage specific file
git commit -m "message"    # save snapshot
git push                   # upload to GitHub
git log --oneline          # view commit history (compact)
```

### Fixing Mistakes (before pushing)
```bash
git commit --amend -m "new message"   # rename last commit message
git reset --soft HEAD~1               # undo last commit, keep changes staged
git reset HEAD~1                      # undo last commit, unstage changes
```

### Branches
```bash
git checkout -b branch-name    # create + switch to new branch
git checkout main              # switch back to main
git merge branch-name          # merge branch into current branch
git branch -d branch-name      # delete branch (after merging)
git branch                     # list all branches
```

### Ignoring Files
Create `.gitignore` in project root:
```
.DS_Store
node_modules/
.env
```

---

## VS Code Equivalents

| Action | VS Code |
|--------|---------|
| Stage + Commit | Source Control panel → type message → Commit |
| Push | Sync button (or ↑ in status bar) |
| Switch branch | Click branch name (bottom-left status bar) |
| Create branch | Click branch name → "Create new branch..." |
| Merge | Cmd+Shift+P → "Git: Merge Branch..." |
| View history | Git Graph panel (bottom of Source Control) |

---

## Git Graph (VS Code) Visual Cues

| Visual | Meaning |
|--------|---------|
| Open circle | Local commit, not pushed |
| Filled purple circle | Synced with GitHub |
| `main` label | Where your local branch points |
| `origin/main` + cloud | Where GitHub is |
| ↑1 in status bar | 1 commit ahead of GitHub |

---

## Commit Message Best Practices

- **Imperative tone:** "Add", "Fix", "Update", "Remove" (not "Added")
- **Short:** under 50 characters
- **What, not how:** "Add bulgogi recipe" (not "Edit recipes.md")

---

## Full Branch Workflow

```
1. git checkout -b feature-name    # branch off main
2. (edit files)
3. git add + git commit             # save on branch
4. git checkout main                # switch back
5. git merge feature-name           # bring changes into main
6. git push                         # sync to GitHub
7. git branch -d feature-name       # clean up
```

Repeat for every feature.
