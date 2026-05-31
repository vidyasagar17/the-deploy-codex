# 📦 Package Managers

## 🔍 What is a Package Manager?

Package managers are used to **install, update, and remove** various software on Linux systems.

---

## ⚙️ RPM — Red Hat Package Manager

Used on **CentOS / RHEL** based systems.

```bash
rpm -i telnet.rpm       # Install a package
rpm -e telnet           # Uninstall a package
rpm -qa telnet          # Query — check if a package is installed
```

> ⚠️ **RPM installs only the package itself — NOT its dependencies.**
> If `telnet` needs other packages to work, RPM won't install them automatically.

---

## 🚀 YUM — Yellowdog Updater Modified

YUM is built on top of RPM and **solves the dependency problem**.

```bash
yum install ansible         # installs ansible AND all its dependent packages
```

> ✅ YUM automatically finds and installs all required dependencies.

---

## 📋 Common YUM Commands

```bash
yum install ansible                     # install a package with all dependencies

yum list ansible                        # view / check a package

yum remove ansible                      # remove / uninstall a package

yum --showduplicates list ansible       # show all available versions of a package

yum install ansible-2.4.2.0            # install a specific version of a package
```

---

## 🔄 Installing the Latest Version

Sometimes running `yum install` may install an **older version** of a package.

To get the latest version:
1. Go to the official software website
2. Look for the install commands for the latest version and repo
3. Add the repo manually, then run `yum install`

```bash
# Example — adding a custom repo before installing
yum --showduplicates list ansible       # check all available versions first
yum install ansible-2.4.2.0            # then install the specific latest version
```

---

## 🆚 RPM vs YUM

| Feature | RPM | YUM |
|---------|-----|-----|
| Installs package | ✅ | ✅ |
| Installs dependencies | ❌ | ✅ |
| Remove package | ✅ | ✅ |
| Query installed packages | ✅ | ✅ |
| Install specific version | ✅ | ✅ |
| Works with repos | ❌ | ✅ |

---

## 🧠 Quick Reference

| Command | What It Does |
|---------|-------------|
| `rpm -i package.rpm` | Install a package (no dependencies) |
| `rpm -e package` | Uninstall a package |
| `rpm -qa package` | Query if a package is installed |
| `yum install package` | Install package + all dependencies |
| `yum remove package` | Remove a package |
| `yum list package` | View / check a package |
| `yum --showduplicates list package` | Show all available versions |
| `yum install package-2.4.2.0` | Install a specific version |

---

> 💡 **Tips**
> - Always prefer `yum` over `rpm` — it handles dependencies automatically
> - Use `yum --showduplicates list <package>` before installing to see all versions
> - If `yum` installs an older version, look up the official repo and add it manually
> - `rpm -qa` is useful to verify if a package got installed correctly
