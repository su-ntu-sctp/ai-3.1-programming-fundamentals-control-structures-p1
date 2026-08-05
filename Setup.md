# Setup Guide: Development Environment Installation

## Overview

Before attending the first lesson, please complete the installation and setup steps below. This ensures you have a working Java development environment ready to go.

---

## Prerequisites

- Basic programming concepts
- VS Code installed
- Internet connection for installations

---

## Part 1: Installation of Development Environment (45 minutes)

### For Windows Users: Install WSL2

Windows users need to install WSL2 (Windows Subsystem for Linux) to follow this course.

**Step 1: Open PowerShell as Administrator**

Right-click Start menu → Windows PowerShell (Admin)

**Step 2: Install WSL**

```powershell
wsl --install
```

**Step 3: Restart your computer**

**Step 4: Set up Ubuntu**

After restart, Ubuntu will open automatically. Create a username and password.

**Step 5: Update packages**

```bash
sudo apt update && sudo apt upgrade -y
```

**Reference:** https://learn.microsoft.com/en-us/windows/wsl/install

**Video walkthrough:** [How to Install WSL2 on Windows](https://www.youtube.com/watch?v=eId6K8d0v6o)

[![video](https://img.youtube.com/vi/eId6K8d0v6o/default.jpg)](https://www.youtube.com/watch?v=eId6K8d0v6o)

---

> **📌 Which terminal do I use from here on?**
> - **Windows users:** Now that WSL2 is installed, do **all** remaining commands in this guide — SDKMan, JDK, Maven, everything — inside your **Ubuntu (WSL) terminal**, not PowerShell or Command Prompt. PowerShell was only needed for the WSL install itself.
> - **Mac users:** Use the built-in **Terminal** app for every command in this guide.
> - This is different from Module 2, where you worked with VS Code directly on Windows/Mac with no WSL involved — WSL is a new piece for this module.

---

### For Windows Users: Connect VS Code to WSL

Since Module 2 you've used VS Code directly on Windows (for React). WSL is new — by default, VS Code opens folders and terminals in Windows, **not** in your Ubuntu (WSL) environment. You need to connect the two, or none of the tools you're about to install (Java, Maven, SDKMan) will be visible to VS Code.

**Step 1: Install the WSL extension**

Open VS Code → Extensions icon (Ctrl+Shift+X) → search "WSL" → install the one published by **Microsoft**.

**Step 2: Create your project folder inside WSL (not Windows)**

Open your Ubuntu terminal (search "Ubuntu" in the Start menu) and run:

```bash
mkdir -p ~/projects
cd ~/projects
```

This keeps your Java projects on the Linux filesystem, where they'll run faster and avoid path issues — rather than under `C:\Users\...`.

**Step 3: Launch VS Code connected to WSL**

From that same Ubuntu terminal:

```bash
code .
```

The first time you run this, VS Code will install a small "VS Code Server" inside WSL — this is expected and only happens once.

**Step 4: Confirm you're connected**

Look at the **bottom-left corner** of the VS Code window. It should show a green box reading **"WSL: Ubuntu"**. If you see that, VS Code, its terminal, and everything you install going forward are all running inside WSL — not Windows.

From now on, any terminal you open inside VS Code (`` Ctrl+` ``) will automatically be your WSL Ubuntu terminal.

---

### For Windows Users: Git Setup in WSL

Configure Git in your WSL environment:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

**Reference:** https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git

---

### For Mac Users: Git Setup

Mac usually comes with Git pre-installed via Xcode Command Line Tools, but let's confirm and configure it.

**Step 1: Check if Git is installed**

```bash
git --version
```

If Git isn't installed, macOS will prompt you to install the **Xcode Command Line Tools** — click **Install** and wait for it to finish, then run `git --version` again to confirm.

**Step 2: Configure Git**

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

**Optional — create a folder for your course work:** any location and name works fine on Mac (e.g. `~/projects`, `~/java-course`, `~/module3`) — just pick one you'll remember, so it's easy to find your work during class.

```bash
mkdir -p ~/projects
cd ~/projects
```

---

### Terminology

**Java Development Kit (JDK)** - Toolkit which includes the Java compiler and runtime environment for developers to write code

**Java Runtime Environment (JRE)** - Consists of JVM, core classes and supporting libraries. Required to run Java applications

**Java Virtual Machine (JVM)** - A platform-independent virtual machine that runs Java bytecode. All Java programs are compiled into bytecode, which is then executed by the JVM

When you install JDK, JRE is included.

**More info:** https://www.digitalocean.com/community/tutorials/difference-jdk-vs-jre-vs-jvm

---

### Install SDKMan

SDKMan is a popular command line tool for managing multiple JDK versions on Unix-based systems (Linux and Mac).

**Benefits:**
- Install, manage and switch between multiple JDK versions easily
- JDKs are installed locally, avoiding conflicts with system-wide installations
- Update itself and all SDKs with a single command

**Step 1: Install prerequisites (WSL/Ubuntu users only)**

```bash
sudo apt install zip unzip curl -y
```

**Mac users:** Skip this step (curl is pre-installed)

**Step 2: Install SDKMan (For WSL/Ubuntu and Mac users)**

```bash
curl -s "https://get.sdkman.io" | bash
```

**Step 3: Initialize SDKMan (For WSL/Ubuntu and Mac users)**

```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

**Step 4: Verify installation (For WSL/Ubuntu and Mac users)**

```bash
sdk version
```

You should see `SDKMAN!` followed by script and native version numbers.

**Reference:** https://sdkman.io/

---

### Install JDK 21

We will install **Eclipse Temurin JDK 21** — the current **LTS** release with long-term support until 2031.

**Step 1: List available Java SDKs (For WSL/Ubuntu and Mac users)**

```bash
sdk list java
```

**Step 2: Install Java 21 (For WSL/Ubuntu and Mac users)**

```bash
sdk install java 21-tem
```

This always installs the latest patch of Java 21. To install a specific patch version, use the exact identifier from the list, e.g. `sdk install java 21.0.7-tem`.

**Step 3: Verify installation (For WSL/Ubuntu and Mac users)**

```bash
java -version
```

You should see `OpenJDK 21.x.x` — the exact patch number may differ.

**Java SE Support Roadmap:** https://www.oracle.com/java/technologies/java-se-support-roadmap.html

---

### Install Homebrew (Mac Users Only)

Homebrew is macOS's package manager — you'll use it to install Maven. Skip this section if you already have it (check first with `brew --version`).

**Step 1: Install Homebrew**

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

You may be prompted to install Xcode Command Line Tools first if you don't already have them — approve this if asked.

**Step 2: Add Homebrew to your PATH (Apple Silicon Macs only — M1/M2/M3/M4)**

After installation finishes, the terminal shows a "Next steps" block with two lines — run them:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

**Intel Macs:** Homebrew installs to `/usr/local` and is usually already on your PATH — no extra step needed.

**Step 3: Verify installation**

```bash
brew --version
```

You should see a Homebrew version number.

---

### Install Maven

Maven is a build automation tool used for Java projects.

**For WSL/Ubuntu users:**

```bash
sudo apt update
sudo apt install maven -y
```

**For Mac users:**

```bash
brew install maven
```

**Verify installation:**

```bash
mvn --version
```

You should see `Apache Maven 3.x.x` with Java 21 listed.

---

### JShell

JShell is a REPL (Read-Eval-Print-Loop) tool for executing Java code interactively — useful for quickly testing snippets without creating a project.

```bash
jshell
```

```bash
jshell> System.out.println("Hello World");
Hello World
jshell> /exit
```

---

### Install Extension Pack for Java

**Step 1:** Open VS Code

**Step 2:** Click Extensions icon (Ctrl+Shift+X / Cmd+Shift+X)

**Step 3:** Search for "Extension Pack for Java" and click Install

**Link:** https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack

---

### Final Verification Checklist

Run each command below in your terminal (WSL Ubuntu terminal for Windows, Terminal app for Mac). If every command produces the expected type of output, your setup is complete.

| Command | Expected output |
| :--- | :--- |
| `java -version` | `OpenJDK 21.x.x` |
| `javac -version` | `javac 21.x.x` |
| `mvn --version` | `Apache Maven 3.x.x` with Java 21 listed |
| `sdk version` | `SDKMAN!` with version numbers |
| `git --version` | A Git version number |
| `code .` (from your project folder) | VS Code opens — **Windows users:** bottom-left corner shows "WSL: Ubuntu" |

If any command fails, check the Troubleshooting Guide below for that specific symptom before class.

---

✅ **If all the steps above completed without errors, your setup is done. You do not need to read anything below this point.**

---

## ⚠️ Troubleshooting Guide — Only If Something Went Wrong

**Do not follow these steps as part of the normal setup process.** This section is a reference to consult *only if* you hit a specific error above. If your installation completed successfully, skip this entirely.

<br>

### Issue 1: `sdk` command not found

*Symptom: after installing SDKMan, running `sdk version` gives "command not found."*

```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

Or restart your terminal.

---

### Issue 2: Permission denied when installing packages (WSL)

*Symptom: installing Maven fails with a permission error.*

```bash
sudo apt install maven -y
```

---

### Issue 3: Java version mismatch

*Symptom: `java -version` shows a different version than expected (e.g. an older system JDK instead of 21).*

```bash
sdk current java
sdk use java 21-tem
```

---

## Additional Resources

- [SDKMan Documentation](https://sdkman.io/)

---

**End of Setup Guide**