# 🐍 Python — Package Manager (pip)


## 📦 What is pip?

pip is Python's package manager — used to install libraries and dependencies for your Python apps.

```bash
pip install flask           # install a package
```

---

## 🔢 pip versions — Python 2 vs Python 3

Two Python versions can exist on the same system.
Each has its own pip.

```bash
python2 -V                  # Python 2.7.16
python3 -V                  # Python 3.6.8

pip2 -V                     # pip 9.0.3 from /usr/lib/python2.7/site-packages (python 2.7)
pip3 -V                     # pip 9.0.3 from /usr/lib/python3.6/site-packages (python 3.6)

pip -V                      # pip 9.0.3 from /usr/lib/python2.7/site-packages (python 2.7)
#                             ↑ plain 'pip' points to Python 2.7 by default
```

> ⚠️ `pip` alone may point to Python 2. Always use `pip3` for Python 3 packages.

---

## ⬇️ Installing Packages

```bash
pip install flask                       # install latest version
pip2 install flask                      # install for Python 2
pip3 install flask                      # install for Python 3
```

---

## 🔍 Inspecting a Package

```bash
pip show flask
# Output:
# Name:         Flask
# Version:      1.1.1
# Summary:      A simple framework for building complex web applications
# Home-page:    https://palletsprojects.com/p/flask/
# Author:       Armin Ronacher
# License:      BSD-3-Clause
# Location:     /usr/lib64/python2.7/site-packages
# Requires:     Werkzeug, click, Jinja2, itsdangerous
```

---

## 📁 Where Packages Get Installed

When you run `pip install flask`, it goes into the `site-packages` folder of that Python version.

```
/usr/
├── lib/
│   ├── python2.7/
│   │   └── site-packages/
│   └── Python3.6/
│       └── site-packages/
└── lib64/
    ├── python2.7/
    │   └── site-packages/
    │       └── Flask-1.1.1.dist-info   ← installed here for Python 2
    └── python3.6/
        └── site-packages/
```

### Check where Python looks for packages

```bash
python2 -c "import sys; print(sys.path)"
# Output:
# '/usr/lib/python27.zip'
# '/usr/lib64/python2.7'
# '/usr/lib64/python2.7/plat-linux2'
# '/usr/lib64/python2.7/site-packages'   ← pip installs here
# '/usr/lib/python2.7/site-packages'
```

> When you import a package, Python searches through these directories in order.

---

## 📋 requirements.txt — Install All Dependencies at Once

Instead of installing one by one:

```bash
# ❌ tedious — one by one
pip install flask
pip install jinja2
pip install markupsafe
pip install Werkzeug
pip install requests
pip install gunicorn
```

Put them all in a `requirements.txt` file:

```
# requirements.txt
Flask
Jinja2
MarkupSafe
Werkzeug
requests
gunicorn
```

Then install everything in one shot:

```bash
pip install -r requirements.txt
#           ↑
#           -r = read from file
```

> All dependencies are stored in one file — anyone can recreate your environment with one command.

---

## 📦 Other Package Managers (Python)

### easy_install (older)
```bash
easy_install install app        # older method
# app.py → setuptools → app.egg
```

### Wheels (modern — preferred)
```bash
pip install app.whl             # install from a wheel file
# app.py → setuptools → app.whl
```

| Format | Tool | Notes |
|--------|------|-------|
| `.egg` | easy_install | Old format — rarely used now |
| `.whl` | pip / wheels | Modern format — faster installs |

---

## 🧠 Quick Reference

| Command | What It Does |
|---------|-------------|
| `pip install flask` | Install a package |
| `pip2 install flask` | Install for Python 2 |
| `pip3 install flask` | Install for Python 3 |
| `pip -V` | Check pip version and Python it points to |
| `pip show flask` | Show package details, version, location |
| `pip install flask jinja2` | Install multiple packages at once |
| `pip install -r requirements.txt` | Install all packages from requirements file |
| `pip install app.whl` | Install from a wheel file |

---

> 💡 **Tips**
> - Always use `pip3` when working with Python 3 — `pip` alone may point to Python 2
> - `pip show <package>` is the fastest way to find where a package is installed
> - Always keep a `requirements.txt` — it makes your project reproducible anywhere
> - `pip install -r requirements.txt` is what CI/CD pipelines use to set up Python environments
