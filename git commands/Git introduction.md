# 🔀 Git — Introduction


## 🔍 What is Git?

Git is a **Distributed Version Control System (DVCS)**.

It is not just a central server storing code — every developer has a **full copy** of the repository on their local machine.

---

## 🌐 Distributed Version Control System

```
                    Remote Repository
                    (Server / GitHub)
                          ▲  ▼
               ┌──────────┴──┴──────────┐
               ▼                        ▼
         Local Repo                Local Repo
        (Developer A)             (Developer B)
        direct access             direct access
```

- The **server** has a remote repository (GitHub, GitLab, Bitbucket)
- Each **user** has a full copy of the local repository
- He/she can make changes locally and then **push** to the remote
- Anyone can **pull** from the remote to get the latest changes

---

## 🔄 How the Workflow Works

```
1. Clone / Pull     →  Get the latest code from remote to local
        ↓
2. Make Changes     →  Edit files in your local repo
        ↓
3. Push             →  Send your changes back to the remote repo
        ↓
4. Pull again       →  Verify local and remote are in sync
```

> Each person has a local repo and can **pull** from the remote repository.
> After making changes to the local repo, **push** it back to the remote.
> Pull again to confirm both are in sync.

---

## 🗂️ Three Areas of a Local Repository

Every local Git repository has **3 areas**:

```
Working Area  ──(git add)──►  Staging Area  ──(git commit)──►  Committed Area
    ↑                                                                  ↓
  Edit files                  Files ready                      Saved in Git
  here                        to commit                        history
```

| Area | What it is |
|------|-----------|
| **Working Area** | Where you edit and create files |
| **Staging Area** | Files you've marked ready to commit (`git add`) |
| **Committed Area** | Files permanently saved in Git history (`git commit`) |

---

## 🚀 Basic Git Demo

```bash
# Step 1 — Initialize a new local repo
git init

# Step 2 — Create a file
touch story.txt

# Step 3 — Add content to the file
echo "This is a beautiful world" >> story.txt

# Step 4 — Move file from Working Area → Staging Area
git add story.txt

# Step 5 — Move from Staging → Committed Area
git commit -m "Add story.txt"

# Step 6 — Push to remote
git push origin main
```

---

## 🔁 Staging, Committing & Restoring

```bash
git add .                               # stage ALL changed files
git add story.txt                       # stage a specific file

git status                              # check what's staged / unstaged

git commit -m "Updated first story"     # commit with a message

git restore story.txt                   # discard changes in working area
git restore --staged story.txt          # unstage a file (move back from staging to working)
```

---

## 🗑️ Removing Files

```bash
git rm notes.txt                        # remove file from repo AND disk

git rm --cached notes.txt              # remove from staging only (keep file on disk)
#        ↑
#     --cached = unstage/untrack without deleting the actual file

git rm -f notes.txt                    # force remove even if file has changes
```

---

## 🙈 .gitignore — Ignore Files

Tell Git to **never track** certain files (logs, secrets, temp files).

```bash
echo "notes.txt" >> .gitignore         # add notes.txt to gitignore
```

**Example `.gitignore`:**
```
notes.txt
*.log
*.env
node_modules/
__pycache__/
```

> Any file listed in `.gitignore` will never be tracked or committed by Git.

---

## ✅ Best Practices

> **Commit each change/problem individually** — don't bundle unrelated changes into one commit.

```bash
# ❌ Bad — one big commit for everything
git commit -m "Fixed bugs and added features and updated docs"

# ✅ Good — one commit per change
git commit -m "Fix login bug"
git commit -m "Add search feature"
git commit -m "Update README"
```

> We can also **revert** a git commit if something goes wrong.

```bash
git revert HEAD                        # revert the last commit
git revert <commit-hash>               # revert a specific commit
```

---

## 🧠 Quick Reference

| Command | What It Does |
|---------|-------------|
| `git init` | Initialize a new local repository |
| `git clone <url>` | Clone a remote repo to local |
| `git add <file>` | Move file to staging area |
| `git add .` | Stage all changed files |
| `git status` | See which area your files are in |
| `git commit -m "msg"` | Save staged changes to committed area |
| `git restore <file>` | Discard changes in working area |
| `git restore --staged <file>` | Unstage a file |
| `git rm <file>` | Remove file from repo and disk |
| `git rm --cached <file>` | Untrack file without deleting it |
| `git push origin main` | Push local commits to remote |
| `git pull` | Pull latest changes from remote |
| `git revert HEAD` | Revert the last commit |

---

> 💡 **Tips**
> - Git is **distributed** — every developer has the full history, not just the latest snapshot
> - `git add` = "I want to include this in my next commit"
> - `git commit` = "Save this snapshot permanently in history"
> - `git push` = "Share my commits with the team on the remote"
> - Always `git pull` before starting work to stay in sync with the remote
> - Commit each change/bug fix individually — makes reverting much easier
> - Use `.gitignore` to keep secrets, logs, and temp files out of your repo
