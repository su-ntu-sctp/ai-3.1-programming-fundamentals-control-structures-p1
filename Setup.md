# Setup Guide: Development Environment Installation

## Overview

Complete this guide before class. It ensures you have a working Java development environment ready to go.

## Prerequisites

- Basic programming concepts
- VS Code installed
- Internet connection for installations

## Choose Your Path

- **Windows users:** follow **PART A** below, start to finish.
- **Mac users:** skip to **PART B**, start to finish.

Each part is fully self-contained — you won't need to jump back and forth.

---
---

# PART A: WINDOWS SETUP

### Install WSL2

Windows users need to install WSL2 (Windows Subsystem for Linux) to follow this course.

**Step 1: Open PowerShell as Administrator**

Right-click Start menu → Windows PowerShell (Admin)

*(On newer Windows 11 systems, you may see "Terminal (Admin)" instead — click that; it opens PowerShell by default.)*

**Step 2: Install WSL**
```powershell
wsl --install
```

**Step 3: Restart your computer**

**Step 4: Set up Ubuntu**

After restart, Ubuntu will open automatically. Create a username and password.

*(Your terminal may first show a path like `/mnt/c/Users/...` — that's normal and harmless; you'll move to your Linux home folder in the next section.)*

**Step 5: Update packages**
```bash
sudo apt update && sudo apt upgrade -y
```

**Reference:** https://learn.microsoft.com/en-us/windows/wsl/install

**Video walkthrough:** [How to Install WSL2 on Windows](https://www.youtube.com/watch?v=eId6K8d0v6o)

---

> **📌 Which terminal do I use from here on?**
> Now that WSL2 is installed, do **all** remaining commands inside your **Ubuntu (WSL) terminal**, not PowerShell.

---

### Connect VS Code to WSL

**Step 1:** Open VS Code → Extensions (Ctrl+Shift+X) → search "WSL" → install the one by **Microsoft**

**Step 2:** Open your Ubuntu terminal, run:
```bash
mkdir -p ~/projects
cd ~/projects
```

**Step 3:** Launch VS Code connected to WSL:
```bash
code .
```

**Step 4:** Confirm the bottom-left corner shows a green **"WSL: Ubuntu"** box.

---

### Git Setup in WSL
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
**Reference:** https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git

---

### Terminology

**JDK (Java Development Kit)** – the full toolkit: compiler + runtime. Installed by the developer.

**JRE (Java Runtime Environment)** – runs Java apps. Included in the JDK.

**JVM (Java Virtual Machine)** – executes bytecode. Platform-independent.

When you install JDK, JRE is included.

---

### Install SDKMan

**Step 1:**
```bash
sudo apt install zip unzip curl -y
```

**Step 2:**
```bash
curl -s "https://get.sdkman.io" | bash
```

**Step 3:**
```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

**Step 4:**
```bash
sdk version
```
You should see `SDKMAN!` with version numbers.

---

### Install JDK 21

**Step 1:**
```bash
sdk install java 21-tem
```

**Step 2:**
```bash
java -version
```
You should see `OpenJDK 21.x.x`.

---

### Install Maven

```bash
sudo apt update && sudo apt install maven -y
```

**Verify:**
```bash
mvn --version
```
You should see `Apache Maven 3.x.x` with Java 21 listed.

---

### JShell (optional)
```bash
jshell
```
```
jshell> System.out.println("Hello World");
jshell> /exit
```

---

### Install Extension Pack for Java (in VS Code)

**Step 1:** Open VS Code

**Step 2:** Extensions icon (Ctrl+Shift+X) → search "Extension Pack for Java" → Install

*(If VS Code is already connected to WSL, it will show "Install in WSL: Ubuntu" instead of a plain "Install" button — click that version, it's correct.)*

---

### Final Verification Checklist (Windows)

| Command | Expected output |
|---|---|
| `java -version` | `OpenJDK 21.x.x` |
| `javac -version` | `javac 21.x.x` |
| `mvn --version` | `Apache Maven 3.x.x` with Java 21 listed |
| `sdk version` | `SDKMAN!` with version numbers |
| `git --version` | A Git version number |
| `code .` | VS Code opens — bottom-left shows "WSL: Ubuntu" |

---

### Troubleshooting Guide (Windows)

**Only consult this if something went wrong above.**

**Issue 1: `sdk` command not found**
```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```
Or restart your terminal.

**Issue 2: Permission denied when installing packages**
```bash
sudo apt install maven -y
```

**Issue 3: Java version mismatch**
```bash
sdk current java
sdk use java 21-tem
```

**Issue 4: Odd warnings during `apt update && upgrade`**

*Symptom: "Failed to get properties: Transport endpoint is not connected" or "Failed to connect to system scope bus."* These are harmless systemd/dbus warnings on WSL. The update still completes successfully.

**Issue 5: Maven install shows a very long or inconsistent time estimate**

*Symptom: apt shows "5 hours remaining," or two different percentages at once.* Normal — apt's time estimates are often inaccurate, especially on a fresh install. Just let it run. If the download speed itself is genuinely stuck (very low KB/s for several minutes): `Ctrl+C`, then in PowerShell (Admin) run `wsl --shutdown`, wait 10 seconds, reopen Ubuntu, and retry.

**Issue 6: Want to see all available Java versions**
```bash
sdk list java
```
This opens a scrollable list — press `q` to exit. Optional, not required for the install.

---
---

# PART B: MAC SETUP

> **⚠️ Important — read before starting:** If your Mac is on an older macOS version (Ventura/13 or earlier), Homebrew may not have a ready-made version of Bash for your system, and will build it from source instead. This can make the "Install a Modern Bash" step below take **15-30+ minutes** instead of a couple of minutes. This is normal, not a sign of failure — just budget extra time and let it run. If possible, updating macOS beforehand will avoid this entirely.

### Git Setup

**Step 1: Check if Git is installed**
```bash
git --version
```
If not installed, macOS will prompt you to install the **Xcode Command Line Tools** — click Install, then run `git --version` again.

**Step 2: Configure Git**
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

**Optional — create a folder for your course work:**
```bash
mkdir -p ~/projects
cd ~/projects
```
Any name/location works — just pick one you'll remember.

---

### Terminology

**JDK (Java Development Kit)** – the full toolkit: compiler + runtime. Installed by the developer.

**JRE (Java Runtime Environment)** – runs Java apps. Included in the JDK.

**JVM (Java Virtual Machine)** – executes bytecode. Platform-independent.

When you install JDK, JRE is included.

---

### Install Homebrew

Homebrew is macOS's package manager. In this guide, its only job is installing a modern version of Bash (needed for SDKMan below) — Java and Maven come through SDKMan directly, not Homebrew.

**Step 1: Install Homebrew**
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

You may see a warning that your macOS version isn't officially supported — this is safe to proceed past.

**Step 2: Follow the "Next steps" it prints**

After installing, Homebrew prints a **"Next steps"** block with 2-3 commands to add it to your PATH (usually involving `.zprofile`). **Copy and run exactly what it shows you** — this applies on every Mac, Intel or Apple Silicon, so don't skip it.

**Step 3: Verify**
```bash
brew --version
```

---

### Install a Modern Bash

macOS ships with an old default Bash (3.2) that SDKMan cannot use. This step is **required**, not optional.

**Step 1:**
```bash
brew install bash
```
*(On older macOS versions, this may compile from source and take 15-30+ minutes — this is expected, just let it run.)*

**Step 2: Open a brand new Terminal window/tab** (important — so your updated PATH loads)

**Step 3: Verify**
```bash
bash --version
```
You should see version 5.x, not 3.2.

---

### Install SDKMan

```bash
curl -s "https://get.sdkman.io" | bash
```

Then:
```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

Verify:
```bash
sdk version
```
You should see `SDKMAN!` with version numbers.

---

### Install JDK 21

**Step 1:**
```bash
sdk install java 21-tem
```

**Step 2:**
```bash
java -version
```
You should see `OpenJDK 21.x.x`.

---

### Install Maven

```bash
sdk install maven
```

**Verify:**
```bash
mvn --version
```
You should see `Apache Maven 3.x.x` with Java 21 listed.

---

### JShell (optional)
```bash
jshell
```
```
jshell> System.out.println("Hello World");
jshell> /exit
```

---

### Install Extension Pack for Java (in VS Code)

**Step 1:** Open VS Code

**Step 2:** Extensions icon (Cmd+Shift+X) → search "Extension Pack for Java" → Install

---

### Final Verification Checklist (Mac)

| Command | Expected output |
|---|---|
| `java -version` | `OpenJDK 21.x.x` |
| `javac -version` | `javac 21.x.x` |
| `mvn --version` | `Apache Maven 3.x.x` with Java 21 listed |
| `sdk version` | `SDKMAN!` with version numbers |
| `bash --version` | Version 5.x |
| `brew --version` | A Homebrew version number |
| `git --version` | A Git version number |

---

### Troubleshooting Guide (Mac)

**Only consult this if something went wrong above.**

**Issue 1: "This macOS version is not supported" warning during any `brew install`**

Safe to proceed (type `y`/Enter). It just means Homebrew doesn't have a ready-made binary for your OS and will build from source, which is slower but works fine.

**Issue 2: `bash --version` still shows 3.2 after installing a newer one**

Close and reopen your terminal completely (not just a new tab in an old session) — this reloads your PATH so it picks up the new Bash.

**Issue 3: SDKMan install still says "Bash 4 or higher required"**

You're likely in a terminal session opened before the Bash upgrade. Open a completely fresh terminal window and retry:
```bash
curl -s "https://get.sdkman.io" | bash
```

**Issue 4: Java version mismatch**
```bash
sdk current java
sdk use java 21-tem
```

**Issue 5: A `brew install` step seems frozen with no output for a long time**

Open a new terminal tab and run `top -o cpu` — look for process names like `cc1`, `clang`, `make`, or `cmake` using CPU. If you see activity, it's genuinely still compiling, not stuck — just let it continue. Press `q` to exit `top`.

**Issue 6: Want to see all available Java versions**
```bash
sdk list java
```
This opens a scrollable list — press `q` to exit. Optional, not required for the install.

**Issue 7: `brew install maven` fails with "A full installation of Xcode.app is required"**

*Symptom: trying to install Maven via Homebrew instead of SDKMan triggers this error, asking for the full Xcode app (several GB) from the App Store.* This happens because Homebrew has no ready-made Maven for your macOS version and tries to build a dependency (`openjdk`) from source, which needs the full Xcode app, not just Command Line Tools. **Fix: don't use Homebrew for Maven at all** — use `sdk install maven` instead (see the Install Maven step above), which avoids this entirely.