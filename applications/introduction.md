# 🖥️ Applications — Introduction

## 📌 Types of Programming Languages

| Compiled | Interpreted |
|----------|-------------|
| Java, C, C++ | Python, Node.js, Ruby, Perl |

### Compiled
- Source code is **converted to machine code** before running
- Works **only on the platform** it was compiled for
- Must recompile for each OS/architecture

### Interpreted
- Code is read and executed **line by line** at runtime
- More **portable** — runs anywhere the interpreter is installed
- No separate compile step needed

---

## ⚙️ How Compiled Languages Work (Java Example)

```
Step 1 — Write Source Code
──────────────────────────
MyClass.java

public class MyClass {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}

Step 2 — Compile
──────────────────────────
javac MyClass.java
→ produces MyClass.class   (compiled bytecode)

Step 3 — Run
──────────────────────────
java MyClass
→ Hello World
```

> The compiler creates `MyClass.class` — the compiled version of the source code.

---

## 🔄 How Code Becomes Machine Code

```
Human Readable          Compiler          Machine Readable
Source Code    ──────────────────►        Machine Code
  main.py                                 01101000 10111100
                                          01100100 01011100
                                          00001010 00001110
                                          ...
```

> The compiler translates what you write into binary instructions the CPU understands.

---

## 🐍 Python — Virtual Machine (Interpreted + Compiled)

Python does **both** — it compiles to bytecode first, then interprets it.

```
Source Code       Compiler        Byte Code           Interpreter       Machine Code
  main.py    ──────────────►    main.pyc (bytecode)  ──────────────►   01101000...
                                                       Python VM
                               Intermediary
                               Byte Code
```

**What's inside `main.pyc` (bytecode):**
```
Hello World
  1   LOAD_NAME     0 (dig)
  3   LOAD_NAME     1 (print)
  6   LOAD_CONST    0 ('Hello World')
 12   CALL_FUNCTION 1 (1 positional, 0 keyword)
 15   PRINT_EXPR
 16   LOAD_CONST    1 (None)
 19   RETURN_VALUE
```

> All of this happens **automatically in the background** when you run `python main.py`.

---

## 📦 Packages / Modules / Libraries

Pre-written code you can import and use in your application.

| Category | Purpose |
|----------|---------|
| Filesystems | Read/write files |
| Math | Mathematical operations |
| Operating System | Interact with the OS |
| HTTP | Make web requests |
| Security | Encryption, auth |
| Networking | Sockets, protocols |

```python
# Example — importing built-in Python modules
import os           # operating system
import math         # math operations
import http         # HTTP requests
```

---

## 🏗️ Build

Building an application involves these steps in order:

```
1. Compile        →   Convert source code to executable/bytecode
2. Run Tests      →   Verify the code works correctly
3. Package        →   Bundle everything into a deployable artifact
4. Delivery       →   Ship it to the target environment
```

### Build procedures by language

| Language | Compile | Test | Package |
|----------|---------|------|---------|
| **Python** | `python -m py_compile app.py` | `pytest` | `pip install` / wheel |
| **Java** | `javac MyClass.java` | `junit` | `.jar` file |
| **Node.js** | none (interpreted) | `npm test` | `npm pack` |

---

## 🧠 Quick Reference

| Concept | What It Means |
|---------|--------------|
| Compiled | Code converted to machine code before running (Java, C, C++) |
| Interpreted | Code executed line by line at runtime (Python, Node.js, Ruby) |
| Bytecode | Intermediary code — between source and machine code (Python `.pyc`) |
| Virtual Machine | Runs bytecode and converts to machine code (Python VM, JVM) |
| Package/Library | Pre-written reusable code you import |
| Build | Compile → Test → Package → Deliver |

---

> 💡 **Tips**
> - Python feels interpreted but actually compiles to `.pyc` bytecode first — you just never see it
> - Java also uses a VM (JVM) — write once, run anywhere
> - The build step is what CI/CD automates — compile, test, package, deploy automatically
