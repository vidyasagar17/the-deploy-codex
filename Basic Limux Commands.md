# 🐧 Linux Basic Commands

> Revision notes — navigating directories and managing files in Linux.

---

## 📢 echo — Print to Screen

Used to display text or output on the terminal.

```bash
echo hi
echo "Hello, World!"
```

---

## 📁 ls — List Files & Folders

Lists all files and directories in the current directory.

```bash
ls          # basic list
ls -l       # detailed list (permissions, size, date)
ls -a       # show hidden files too
ls -la      # detailed + hidden
```

---

## 📂 cd — Change Directory

Navigate between directories.

```bash
cd my_dir       # go into a folder
cd ..           # go one level up
cd ~            # go to home directory
cd /            # go to root directory
```

---

## 🔍 pwd — Present Working Directory

Shows the full path of the directory you are currently in.

```bash
pwd
# Output: /home/vidya/projects
```

---

## 🗂️ mkdir — Make New Directory

Creates a new folder.

```bash
mkdir new_directory                     # create a single folder
mkdir new_dir1/new_dir2                 # create dir2 inside dir1 (dir1 must already exist)
mkdir -p /tmp/asia/india/bangalore      # create deeply nested folders in one shot
                                        # -p creates all parent folders automatically
```

---

## ⚡ Multiple Commands at Once

Use `;` to run multiple commands on a single line.

```bash
cd new_directory; mkdir www; pwd
# goes into new_directory → creates www inside it → prints current path
```

---

## 📄 touch — Create a New File

Creates a new empty file.

```bash
touch new_file.txt

# create multiple files at once
touch file1.txt file2.txt file3.txt
```

---

## ✏️ cat > — Write Content to a File

Writes content directly into a file from the terminal.

```bash
cat > new_file.txt
This is some basic content.
Hello from the terminal!
```
> Press **Ctrl + D** to save and exit.

```bash
# To APPEND instead of overwrite, use >>
cat >> new_file.txt
Adding more content without deleting the old stuff.
```
> Press **Ctrl + D** to save and exit.

⚠️ `cat >` **overwrites** existing content. `cat >>` **appends** to it.

---

## 👁️ cat — View File Contents

Displays the contents of a file on the screen.

```bash
cat new_file.txt
# Output:
# This is some basic content.
# Hello from the terminal!
```

---

## 📋 cp — Copy Files & Directories

```bash
cp new_file.txt copy_file.txt           # copy a file
#  ↑                ↑
# source          target

cp -r mydir1 /tmp/mydir1                # copy a directory
#   ↑            ↑
# source       target
# -r flag = recursive (required for directories)
```

---

## 🔀 mv — Move or Rename

Used to rename a file or move it to another location.

```bash
mv new_file.txt sample_file.txt         # rename a file

mv new_file.txt /tmp/new_file.txt       # move a file to another directory

mv mydir1 /tmp/mydir1                   # move a directory
```

---

## 🗑️ rm — Remove Files & Directories

```bash
rm new_file.txt                         # delete a file

rm -r directory_1                       # delete a directory and everything inside it
```

⚠️ There is no trash/recycle bin in Linux. Deleted files are **gone permanently**.

---

## 🧠 Quick Reference

| Command | What It Does |
|---------|--------------|
| `echo` | Print text to the screen |
| `ls` | List files and folders |
| `cd` | Change directory |
| `pwd` | Show current directory path |
| `mkdir` | Create a new directory |
| `mkdir -p` | Create nested directories in one shot |
| `touch` | Create a new empty file |
| `cat > file` | Write/overwrite content into a file |
| `cat >> file` | Append content to a file |
| `cat file` | View contents of a file |
| `cp source target` | Copy a file or directory |
| `mv source target` | Rename or move a file or directory |
| `rm -r` | Remove a directory and all its contents |

---

> 💡 **Tips**
> - Chain commands with `;` to run them one after another
> - Always use `-p` with `mkdir` when creating nested folders
> - `cat >` overwrites. `cat >>` appends. One wrong `>` can wipe your file.
> - `rm` is permanent — double check before you delete
