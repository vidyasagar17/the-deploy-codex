# ☕ Java — Build and Packaging

## 🔄 Java Build Process

```
Develop       Compile              Package             Document
────────────────────────────────────────────────────────────────
Write Code  →  javac MyClass.java  →  jar cf MyApp.jar  →  javadoc MyClass.java
   ↓                ↓                       ↓                      ↓
 Code          MyClass.class           MyApp.jar              /doc folder
```

---

## ⚙️ Step 1 — Compile

Converts `.java` source code into `.class` bytecode.

```bash
javac MyClass.java              # compile single file → produces MyClass.class

javac *.java                    # compile multiple files at once
```

---

## 📦 Step 2 — Package (JAR / WAR)

### JAR — Java Archive
Used to **archive all `.class` files into one** deployable file.

```bash
jar cf MyApp.jar MyClass.class  # create JAR from compiled class files
#   ↑
#   c = create, f = filename

java -jar MyApp.jar             # run the JAR file
java cf MyApp.jar MyClass.class # another way to create it
```

### WAR — Web Archive
Used to archive **files AND images** (web apps — HTML, JSP, images, servlets).

```
JAR  →  Java Archive   →  packages .class files (regular Java apps)
WAR  →  Web Archive    →  packages .class files + images + HTML (web apps)
```

---

## 📄 Step 3 — Document

Generates HTML documentation from your source code comments.

```bash
javadoc -d doc MyClass.java     # generates docs in /doc folder
#       ↑
#       -d = destination directory
```

---

## 🛠️ Build Tools — Automate the Entire Process

Manually running `javac`, `jar`, `javadoc` every time is tedious.
Build tools **automate** all these steps with a single command.

| Tool | Config File | Notes |
|------|------------|-------|
| **ANT** | `build.xml` | Oldest, XML-based, manual config |
| **Maven** | `pom.xml` | Convention-based, downloads dependencies |
| **Gradle** | `build.gradle` | Modern, fast, uses Groovy/Kotlin DSL |

---

## 🐜 ANT — Build Tool Example

ANT reads a `build.xml` file and runs the build steps automatically.

```bash
ant                             # runs the build
# Output:
# BUILD SUCCESSFUL
# Total time: 2 seconds
```

**What ANT replaces manually:**
```bash
# Without ANT — you run these manually every time:
javac MyClass.java
javadoc MyClass.java
jar cf MyClass.jar ..

# With ANT — just run:
ant
```

### ANT `build.xml` Example

```xml
<?xml version="1.0"?>
<project name="Ant" default="main" basedir=".">

    <!-- Step 1: Compile the Java code -->
    <target name="compile">
        <javac srcdir="/app/src" destdir="/app/build">
        </javac>
    </target>

    <!-- Step 2: Generate Javadoc documentation -->
    <target name="docs" depends="compile">
        <javadoc packagenames="src"
                 sourcepath="/app/src"
                 destdir="/app/docs">
            <fileset dir="/app/src">
                <include name="**" />
            </fileset>
        </javadoc>
    </target>

    <!-- Step 3: Create the deployable JAR file -->
    <target name="jar" depends="compile">
        <jar basedir="/app/build" destfile="/app/dist/MyClass.jar">
            <manifest>
                <attribute name="Main-Class" value="MyClass" />
            </manifest>
        </jar>
    </target>

    <!-- Main target — runs compile, jar, and docs together -->
    <target name="main" depends="compile, jar, docs">
        <description>Main target</description>
    </target>

</project>
```

---

## 🧠 Quick Reference

| Command | What It Does |
|---------|-------------|
| `javac MyClass.java` | Compile Java source → `.class` bytecode |
| `javac *.java` | Compile all `.java` files |
| `jar cf MyApp.jar MyClass.class` | Package into a JAR file |
| `java -jar MyApp.jar` | Run a JAR file |
| `javadoc -d doc MyClass.java` | Generate HTML documentation |
| `ant` | Run ANT build (reads `build.xml`) |

---

## 🔑 Key Terms

| Term | Meaning |
|------|---------|
| JDK | Java Development Kit — needed to compile (has `javac`) |
| JRE | Java Runtime Environment — needed to run (has `java`) |
| `.class` | Compiled bytecode file |
| JAR | Java Archive — bundles all class files into one |
| WAR | Web Archive — JAR + web files (HTML, images) for web apps |
| ANT | Build tool — automates compile, package, document |
| Maven | Build tool — also manages dependencies automatically |
| Gradle | Build tool — modern, faster than Maven/ANT |

---

> 💡 **Tips**
> - You need **JDK** to compile, **JRE** to run — servers only need JRE
> - JAR = just code, WAR = code + web files (use WAR for web apps)
> - ANT just automates what you'd manually run — same commands, just defined in XML
> - Maven and Gradle also auto-download dependencies — ANT doesn't
> - In CI/CD pipelines, Maven/Gradle is most common for Java builds
