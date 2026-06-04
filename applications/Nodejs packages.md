# 🟢 Node.js — NPM (Node Package Manager)

> Revision notes — installing Node.js, managing packages with NPM, and understanding package.json.

---

## 📦 What is NPM?

NPM = **Node Package Manager** — used to install packages/libraries for Node.js apps.

NPM supports packages for:
- Files
- Web Servers
- Databases
- Security
- And much more → [npmjs.com](https://www.npmjs.com/)

> NPM is **automatically installed** when you install Node.js — no separate install needed.

---

## ⬇️ Installing Node.js

```bash
# Using curl (install script)
curl -sL https://rpm.nodesource.com/setup_14.x | bash -

# Then install via yum (CentOS)
yum install nodejs

# Verify installation
node -v             # check Node.js version
npm -v              # check NPM version → 6.13.7
```

---

## 🔍 NPM Commands

### Check version
```bash
npm -v
# Output: 6.13.7
```

### Search for a package
```bash
npm search file
# Output:
# NAME         DESCRIPTION              AUTHOR          DATE
# file         Higher level path...     =aconbere       2014-02-21
# File         HTML5 FileAPI...         =coolaj86        2014-10-24
# dotenv       Loads environment...     =~jcblw          2019-10-16
# fs-extra     fs-extra contains...     =jprichardson    2019-06-28
# file-loader  A file loader...         =d3viantOne      2020-02-19
```

### Install a package
```bash
npm install file
# Output:
# + file@0.2.2
# added 1 package from 1 contributor and audited 1 package in 1.072s
# found 0 vulnerabilities
```

### Check where Node looks for modules
```bash
node -e "console.log(module.paths)"
# Output:
# [ '/app/node_modules', '/node_modules' ]
```

### List installed global modules
```bash
ls /usr/lib/node_modules/
ls /usr/lib/node_modules/npm/node_modules/
```

---

## 📁 Where Packages Get Installed

When you run `npm install`, packages go into `node_modules/` in your project.

```
my_application/
├── app.js
└── node_modules/
    └── file/
        ├── LICENSE
        ├── README.md
        ├── package.json      ← package metadata
        └── lib/
```

---

## 🧑‍💻 Using a Package in Code

```javascript
// app.js
var file = require("file");           // import the package

file.mkdirs("/tmp/dir1")              // use it
```

---

## 📋 package.json — Application Dependencies

Every Node.js app has a `package.json` — stores the app name, version, and all dependencies.

```json
{
  "name": "example-contentful-theExampleApp-js",
  "version": "0.0.0",
  "private": true,
  "dependencies": {
    "body-parser":  "^1.18.2",
    "contentful":   "^6.0.0",
    "cookie-parser":"~1.4.3",
    "dotenv":       "^5.0.0",
    "execa":        "^0.9.0",
    "express":      "^4.16.2",
    "helmet":       "^3.11.0",
    "lodash":       "^4.17.5",
    "marked":       "^0.3.16",
    "morgan":       "^1.9.1",
    "pug":          "~2.0.0-beta6"
  }
}
```

> `package.json` is Node's equivalent of Python's `requirements.txt` — lists all dependencies in one place.

### Install all dependencies from package.json
```bash
npm install
# reads package.json and installs everything listed under dependencies
```

---

## 📦 Inside a Package's package.json

Each installed package also has its own `package.json` inside `node_modules/`:

```json
{
  "name": "file",
  "version": "0.2.2",
  "author": {
    "name": "Anders Conbere",
    "email": "aconbere@gmail.com"
  },
  "license": "MIT",
  "main": "./lib/file",
  "devDependencies": {
    "mocha": "1.9.x"
  },
  "repository": {
    "type": "git",
    "url": "git+ssh://git@github.com/aconbere/node-file-utils.git"
  },
  "tags": ["file", "path", "fs", "walk"]
}
```

> Useful for troubleshooting dependency errors — check the package's own `package.json`.

---

## 🧩 Common Modules

### Built-In Modules (no install needed)

| Module | Purpose |
|--------|---------|
| `fs` | Handle filesystem (read/write files) |
| `http` | Host an HTTP server |
| `os` | Work with the Operating System |
| `events` | Handle events |
| `tls` | Implement TLS and SSL |
| `url` | Parse URL strings |

### External Modules (install via npm)

| Module | Purpose |
|--------|---------|
| `express` | Fast, minimalist web framework |
| `react` | Create user interfaces |
| `debug` | Debug applications |
| `async` | Work with asynchronous JS |
| `lodash` | Work with arrays, objects, strings |

---

## 🧠 Quick Reference

| Command | What It Does |
|---------|-------------|
| `node -v` | Check Node.js version |
| `npm -v` | Check NPM version |
| `npm search file` | Search for a package by name |
| `npm install file` | Install a package |
| `npm install` | Install all deps from package.json |
| `node -e "console.log(module.paths)"` | Show where Node looks for modules |
| `ls /usr/lib/node_modules/` | List globally installed modules |

---

> 💡 **Tips**
> - NPM installs packages into `node_modules/` inside your project — never commit this folder to git
> - Always add `node_modules/` to your `.gitignore`
> - `package.json` = Node's `requirements.txt` — commit this, not `node_modules/`
> - Built-in modules need no install — just `require('fs')`, `require('http')` etc.
> - Check a package's `package.json` in `node_modules/` when debugging dependency issues
