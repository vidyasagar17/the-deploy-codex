# 📝 Vi Editor

> Revision notes — navigating and editing files using the Vi editor in Linux.

---

## 🚀 Opening Vi

```bash
vi filename.txt         # open an existing file
vi new_file.txt         # creates the file if it doesn't exist
```

---

## 🎮 Vi Modes

Vi has two main modes — you need to switch between them.

| Mode | What It Does | How to Enter |
|------|-------------|--------------|
| **Normal Mode** | Navigate, delete, copy, paste | Press `Esc` |
| **Insert Mode** | Type and edit content | Press `i` |

> Always press **Esc** first before using any command below.

---

## ⬆️⬇️ Moving Around

Navigate through the file in **Normal Mode**.

```
Arrow Keys          →   Move up, down, left, right

OR use keyboard:

  K                 →   Move Up
  J                 →   Move Down
  H                 →   Move Left
  L                 →   Move Right
```

> 💡 H J K L are faster than arrow keys once you get used to them.

---

## 🗑️ Delete

```
x                   →   Delete a single character under the cursor
dd                  →   Delete the entire current line
```

---

## 📋 Copy & Paste

```
yy                  →   Copy (yank) the current line
p                   →   Paste below the current line
```

---

## 📜 Scroll Up & Down

```
Ctrl + U            →   Scroll Up   (half page)
Ctrl + D            →   Scroll Down (half page)
```

---

## 🔍 Find / Search

Search for any word or pattern in the file in **Normal Mode**.

```
/word               →   Search FORWARD for "word"
?word               →   Search BACKWARD for "word"

n                   →   Jump to the NEXT occurrence
N                   →   Jump to the PREVIOUS occurrence
```

**Example:**
```
/error              →   finds the first occurrence of "error"
n                   →   moves cursor to the next occurrence
n                   →   keeps moving to the next one
N                   →   goes back to the previous occurrence
```

> 💡 Press `Esc` before typing `/` to make sure you are in Normal Mode.

---

## ⌨️ Commands — Save & Quit

Type `:` in Normal Mode to enter command mode.

```bash
:w                  # save the file (write)
:q                  # quit Vi
:wq                 # save and quit
:q!                 # quit WITHOUT saving (force quit)
```

---

## 🧠 Quick Reference

| Key / Command | What It Does |
|---------------|-------------|
| `i` | Enter Insert Mode (start typing) |
| `Esc` | Go back to Normal Mode |
| Arrow keys / `H J K L` | Move around the file |
| `x` | Delete a character |
| `dd` | Delete a line |
| `yy` | Copy a line |
| `p` | Paste a line |
| `Ctrl + U` | Scroll up |
| `Ctrl + D` | Scroll down |
| `/word` | Search forward for a word |
| `?word` | Search backward for a word |
| `n` | Jump to next occurrence |
| `N` | Jump to previous occurrence |
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and Quit |
| `:q!` | Quit without saving |

---

> 💡 **Tips**
> - Always press `Esc` before running any command — if something feels wrong, hit `Esc` first
> - `dd` + `p` together = cut and paste a line
> - `yy` + `p` together = duplicate a line
> - `:q!` is your emergency exit when you don't want to save changes
