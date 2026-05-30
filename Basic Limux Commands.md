# 🐧 Linux Basic Commands

> Revision notes — fundamental Linux commands for navigating and managing the filesystem.

---

## 📢 echo — Print to Screen

Used to display text or output on the terminal.

```bash
echo "Hello, World!"
echo hi
```

---

## 📁 ls — List Files & Folders

Lists all files and directories in the current directory.

```bash
ls              # basic list
ls -l           # detailed list (permissions, size, date)
ls -a           # show hidden files too
ls -la          # detailed + hidden
```

---

## 📂 cd — Change Directory

Navigate between directories.

```bash
cd my_dir           # go into a folder
cd ..               # go one level up
cd ~                # go to home directory
cd /                # go to root directory
```

---

## 🔍 pwd — Present Working Directory

Shows the full path of the directory you're currently in.

```bash
pwd
# Output: /home/vidya/projects
```

---

## 🗂️ mkdir — Make New Directory

Creates a new folder.

```bash
mkdir new_directory             # create a single folder

mkdir -p /tmp/asia/india/bangalore   # create nested folders in one shot
#        (-p flag creates all parent directories if they don't exist)
```

---

## ⚡ Multiple Commands at Once

Use `;` to run multiple commands on a single line.

```bash
cd new_directory; mkdir www; pwd
# goes into new_directory, creates www inside it, then prints current path
```

---

## 📦 mkdir — Create Multiple Nested Directories

```bash
mkdir new_dir1/new_dir2         # create dir2 inside dir1 (dir1 must exist)

mkdir -p new_dir1/new_dir2      # safer — creates both even if dir1 doesn't exist
```

---

## 📋 cp — Copy Files & Directories

```bash
cp -r mydir1 /tmp/mydir1
#    ↑          ↑
#  source     target

# -r flag = recursive (required when copying directories)
```

---

## 🗑️ rm — Remove Files & Directories

```bash
rm -r directory_1       # remove a directory and everything inside it

# ⚠️  Be careful — there is no trash/recycle bin in Linux.
#     Deleted files are gone permanently.
```

---

## 🧠 Quick Reference

| Command | What It Does |
|---------|-------------|
| `echo` | Print text to the screen |
| `ls` | List files and folders |
| `cd` | Change directory |
| `pwd` | Show current directory path |
| `mkdir` | Create a new directory |
| `mkdir -p` | Create nested directories in one shot |
| `cp -r` | Copy a directory recursively |
| `rm -r` | Remove a directory and its contents |

---

> 💡 **Tip:** Chain commands with `;` to run them one after another on a single line.
