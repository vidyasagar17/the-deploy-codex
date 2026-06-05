# 🌿 Git — Branches

## 🔍 What is a Branch?

A branch is an **independent line of development** — a copy of the code where you can make changes without affecting the main codebase.

```
main  ──────────────────────────────────►
         └── feature/login ──────────►
         └── bugfix/crash  ──────────►
```

> Think of it like a parallel universe — changes in one branch don't affect others until you merge.

---

## 🌱 Why Use Branches?

- Work on a new feature without breaking `main`
- Fix a bug in isolation
- Multiple developers work on different things simultaneously
- Experiment freely — just delete the branch if it doesn't work

---

## 🚀 Creating & Switching Branches

```bash
git branch                          # list all branches (* = current branch)

git branch feature/login            # create a new branch

git checkout feature/login          # switch to a branch

git checkout -b feature/login       # create AND switch in one command ✅
#             ↑
#          -b = create + switch (shortcut)

git switch feature/login            # modern way to switch (Git 2.23+)
git switch -c feature/login         # modern way to create + switch
```

---

## 📋 Branch Naming Conventions

Use `/` to group branches by type — keeps things organised.

```
main                        # production-ready code
feature/search-bar          # new features
bugfix/login-error          # bug fixes
hotfix/payment-crash        # urgent production fixes
release/v2.0                # release preparation
story/frogs-and-ox          # story-based (course/demo convention)
```

---

## ✏️ Working on a Branch

```bash
git checkout -b feature/login       # create and switch to new branch

# make your changes...
touch login.py
git add login.py
git commit -m "Add login feature"

git commit -am "Update login logic"  # stage + commit tracked files in one step
```

---

## 🔀 Merging a Branch

Once your work is done, merge it back into `main`.

```bash
git checkout main                   # switch back to main first

git merge feature/login             # merge feature branch into main
#         ↑
#    branch to merge in

git branch -d feature/login         # delete branch after merging (clean up)
```

### Merge flow

```
main    ──────────────────────────────────────────►
              └── feature/login ──────────────────►
                                                   ↑
                                          git merge feature/login
```

---

## ⚡ Merge Conflicts

When two branches change the **same line** in a file, Git can't auto-merge — you must resolve it manually.

```bash
git merge feature/login
# CONFLICT (content): Merge conflict in login.py
# Automatic merge failed; fix conflicts and then commit the result.
```

Open the file — Git marks the conflict:
```
<<<<<<< HEAD
    print("Login v1")          ← your current branch (main)
=======
    print("Login v2")          ← incoming branch (feature/login)
>>>>>>> feature/login
```

Fix it, then:
```bash
git add login.py                    # mark conflict as resolved
git commit -m "Resolve merge conflict"
```

---

## 🗑️ Deleting Branches

```bash
git branch -d feature/login         # delete a merged branch (safe)
git branch -D feature/login         # force delete even if not merged
```

---

## 🌐 Remote Branches

```bash
git push origin feature/login       # push branch to remote

git branch -r                       # list remote branches

git pull origin feature/login       # pull a remote branch

git push origin --delete feature/login   # delete a remote branch
```

---

## 🔍 Useful Branch Commands

```bash
git log --oneline --graph           # visualize branch history

git diff main feature/login         # compare two branches

git branch --merged                 # branches already merged into current

git branch --no-merged              # branches NOT yet merged
```

---

## 🧠 Quick Reference

| Command | What It Does |
|---------|-------------|
| `git branch` | List all local branches |
| `git branch <name>` | Create a new branch |
| `git checkout <name>` | Switch to a branch |
| `git checkout -b <name>` | Create + switch in one command |
| `git switch -c <name>` | Modern create + switch |
| `git merge <branch>` | Merge a branch into current branch |
| `git branch -d <name>` | Delete a merged branch |
| `git branch -D <name>` | Force delete a branch |
| `git push origin <name>` | Push branch to remote |
| `git push origin --delete <name>` | Delete a remote branch |
| `git log --oneline --graph` | Visualize branch history |
| `git diff main <branch>` | Compare two branches |

---

> 💡 **Tips**
> - Never work directly on `main` — always create a branch
> - Delete branches after merging — keeps the repo clean
> - Use naming conventions (`feature/`, `bugfix/`, `hotfix/`) — makes branches easy to identify
> - `git checkout -b` is your most used command — create + switch in one shot
> - Pull latest `main` before creating a new branch — avoids conflicts later
> - Use `git log --oneline --graph` to visualize how branches relate to each other
