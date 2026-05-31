# ⚙️ Services & systemd

## 🔍 What are Services?

Services are background processes that run on Linux (web servers, databases, apps).
We need to keep track of them — make sure they are **running** and start in the **correct order**.

Linux uses **systemd** to manage services.

---

## 🚀 Starting & Stopping Services

### Old way (still works):
```bash
service httpd start         # start HTTPD service
```

### New way (preferred — systemctl):
```bash
systemctl start httpd       # start HTTPD service
systemctl stop httpd        # stop HTTPD service
systemctl status httpd      # check if service is running
```

---

## 🔁 Enable / Disable at Startup

```bash
systemctl enable httpd      # start automatically when system boots
systemctl disable httpd     # do NOT start at boot
```

---

## 📁 Where Service Files Live

```
/etc/systemd/system/        # custom service files go here
/lib/systemd/system/        # system/package service files (e.g. docker.service)
```

---

## 📝 Writing a Custom Service File

To run your own application as a service, create a `.service` file.

**File:** `/etc/systemd/system/my_app.service`

```ini
[Unit]
Description=My Python Web Application

[Service]
ExecStartPre=/opt/code/configure_db.sh      # runs BEFORE the app starts
ExecStart=/usr/bin/python3 /opt/code/my_app.py   # main command to start the app
ExecStartPost=/opt/code/email_status.sh     # runs AFTER the app starts
Restart=always                               # restart automatically if it crashes

[Install]
WantedBy=multi-user.target                  # run at normal bootup (multi-user mode)
```

### Service File Sections Explained

| Section | Purpose |
|---------|---------|
| `[Unit]` | Description and dependencies |
| `[Service]` | How to start, stop, restart the service |
| `[Install]` | When to start during boot |

---

## 🔄 Reload After Creating a New Service

Whenever you create or modify a `.service` file, run:

```bash
systemctl daemon-reload         # tell systemd a new service is configured
systemctl start my_app          # then start it
systemctl enable my_app         # enable it to run at bootup
```

---

## 🐳 Real Example — Docker Service File

Docker itself runs as a systemd service.

**File:** `/lib/systemd/system/docker.service`

```ini
[Unit]
Description=Docker Application Container Engine
Documentation=https://docs.docker.com
BindsTo=containerd.service
After=network-online.target firewalld.service containerd.service
Wants=network-online.target
Requires=docker.socket

[Service]
Type=notify
ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
ExecReload=/bin/kill -s HUP $MAINPID
Restart=always
StartLimitBurst=3
StartLimitInterval=60s
LimitNOFILE=infinity
LimitNPROC=infinity
LimitCORE=infinity

[Install]
WantedBy=multi-user.target
```

> 💡 The `[Service]` section has the command that runs the Docker daemon — specified under `ExecStart`.

---

## 🧠 Quick Reference

| Command | What It Does |
|---------|-------------|
| `service httpd start` | Start a service (old method) |
| `systemctl start httpd` | Start a service |
| `systemctl stop httpd` | Stop a service |
| `systemctl status httpd` | Check service status |
| `systemctl enable httpd` | Enable service at boot |
| `systemctl disable httpd` | Disable service at boot |
| `systemctl daemon-reload` | Reload after adding/editing a service file |
| `systemctl restart httpd` | Restart a running service |

---

> 💡 **Tips**
> - Always run `systemctl daemon-reload` after creating or editing a `.service` file
> - `Restart=always` in `[Service]` makes your app auto-recover from crashes
> - `WantedBy=multi-user.target` means the service starts in normal (non-GUI) boot mode
> - Use `systemctl status <service>` to debug — it shows recent logs too
> - Docker's service file is a great real-world reference for writing your own
