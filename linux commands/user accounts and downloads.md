# 👤 User Accounts & 📥 Download Files

> Revision notes — managing users, switching accounts, downloading files and checking OS version in Linux.

---

## 🙋 whoami — Who Am I?

Prints the name of the currently logged-in user.

```bash
whoami
# Output: sagar
```

---

## 🪪 id — User Details

Shows the user ID, group ID, and all groups the user belongs to.

```bash
id
# Output: uid=1001(sagar) gid=1001(sagar) groups=1001(sagar),27(sudo)
```

---

## 🔄 su — Switch User

Switch to another user account within the same system.

```bash
su sagar            # switch to user "sagar"
                    # you will be prompted for sagar's password

su -                # switch to root user
```

> 💡 Type `exit` to go back to the previous user.

---

## 🌐 ssh — Switch to Another System

Connect to a remote machine over the network securely.

```bash
ssh sagar@192.168.1.10      # connect as user "sagar" to a remote machine
ssh sagar@hostname          # connect using hostname instead of IP
```

> 💡 You will be prompted for the remote user's password unless SSH keys are set up.

---

## 🔐 sudo — Run as Root (Without Being Root)

Normal users are **not** given direct root access.
Instead they are given **sudo** access to run specific commands as root.

```bash
# Without sudo — permission denied for normal users
ls /root
# Output: Permission denied

# With sudo — runs the command as root
sudo ls /root
# Output: lists root's home directory
```

```bash
sudo apt install nginx      # install a package as root
sudo systemctl restart app  # restart a service as root
```

> ⚠️ Always be careful with `sudo` — commands run with root privileges can affect the entire system.

---

## 📥 curl — Download from URL

Used to transfer data from a URL. Great for APIs and quick downloads.

```bash
curl https://example.com/file.tar.gz                    # download and print to screen

curl https://example.com/file.tar.gz -o myfile.tar.gz   # save with a custom name
#                                    ↑
#                               -o = output file name

curl -O https://example.com/file.tar.gz                 # save with the original filename
```

**Common curl flags:**

```bash
curl -L https://...         # follow redirects
curl -s https://...         # silent mode (no progress bar)
curl -I https://...         # fetch headers only
```

---

## 📦 wget — Download Files

Simpler than curl — built specifically for downloading files.

```bash
wget https://example.com/file.tar.gz                    # download with original filename

wget https://example.com/file.tar.gz -O some-file.txt   # save with a custom name
#                                    ↑
#                               -O = output file name
```

**Common wget flags:**

```bash
wget -q https://...         # quiet mode (no output)
wget -c https://...         # resume an interrupted download
wget -P /tmp https://...    # save file to a specific directory
```

---

## 🆚 curl vs wget

| Feature | curl | wget |
|---------|------|------|
| Download files | ✅ | ✅ |
| Save with custom name | `-o filename` | `-O filename` |
| Follow redirects | `-L` | automatic |
| Resume downloads | ❌ | `-c` |
| API / REST calls | ✅ great | ❌ not ideal |

---

## 🖥️ OS Version — Check What Linux You're On

```bash
cat /etc/*release*
# Output example:
# NAME="Ubuntu"
# VERSION="22.04.3 LTS (Jammy Jellyfish)"
# VERSION_ID="22.04"
```

**Other ways to check:**

```bash
uname -a                # kernel version + system info
uname -r                # just the kernel version
lsb_release -a          # detailed distro info (Ubuntu/Debian)
hostnamectl             # hostname + OS + kernel in one shot
```

---

## 🧠 Quick Reference

| Command | What It Does |
|---------|-------------|
| `whoami` | Shows the current logged-in username |
| `id` | Shows user ID, group ID and groups |
| `su sagar` | Switch to user "sagar" on same system |
| `su -` | Switch to root user |
| `ssh user@host` | Connect to a remote system securely |
| `sudo <command>` | Run a command with root privileges |
| `exit` | Log out / go back to previous user |
| `curl <url> -o file` | Download and save with custom name |
| `wget <url> -O file` | Download and save with custom name |
| `wget -c <url>` | Resume an interrupted download |
| `cat /etc/*release*` | Show OS name and version |
| `uname -a` | Show kernel and system info |

---

> 💡 **Tips**
> - `whoami` is your quickest sanity check when switching users
> - Prefer `sudo` over logging in as root — safer and auditable
> - Use `wget` for simple file downloads — fewer flags to remember
> - Use `curl` when working with APIs or need more control
> - Always check `/etc/*release*` first when SSH-ing into an unfamiliar server
