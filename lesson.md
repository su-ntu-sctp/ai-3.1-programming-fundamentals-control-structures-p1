# Lesson 3.1: Programming Fundamentals and Control Structures

## Lesson Overview

This lesson introduces the Java development environment and essential programming basics. Students will set up JDK, learn about classes, compilation, variables, data types, wrapper classes, user input, and operators. By the end, they will be able to write, compile, and execute simple Java programs in VS Code.

---

## Prerequisites

- Basic programming concepts
- VS Code installed
- Internet connection for installations

---

## Lesson Objectives

By the end of this lesson, you will be able to:
- Install and configure WSL (Windows users), JDK, SDKMan, Maven, and Java extensions in VS Code
- Write and execute a Java program using the `class` and `main` method
- Apply variables, data types, casting, and wrapper classes in code
- Read and process user input from the console
- Demonstrate usage of arithmetic, relational, logical, and assignment operators

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

---

### For Windows Users: Git Setup in WSL

Configure Git in your WSL environment:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

**Reference:** https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git

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

**Step 2: Install SDKMan**

```bash
curl -s "https://get.sdkman.io" | bash
```

**Step 3: Initialize SDKMan**

```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

**Step 4: Verify installation**

```bash
sdk version
```

You should see `SDKMAN!` followed by script and native version numbers.

---

### Install JDK 21

We will install **Eclipse Temurin JDK 21** — the current **LTS** release with long-term support until 2031.

**Step 1: List available Java SDKs**

```bash
sdk list java
```

**Step 2: Install Java 21**

```bash
sdk install java 21-tem
```

This always installs the latest patch of Java 21. To install a specific patch version, use the exact identifier from the list, e.g. `sdk install java 21.0.7-tem`.

**Step 3: Verify installation**

```bash
java -version
```

You should see `OpenJDK 21.x.x` — the exact patch number may differ.

**Java SE Support Roadmap:** https://www.oracle.com/java/technologies/java-se-support-roadmap.html

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

## Part 2: `class` and `main` Method (10 minutes)

### Step 1: Create `Main.java`

The naming convention for a `class` is **PascalCase** — first letter of each word capitalised.

**Reference:** https://www.oracle.com/java/technologies/javase/codeconventions-namingconventions.html

### Step 2: Define the class

The class name must match the filename exactly.

```java
public class Main {
  public static void main(String[] args) {
    System.out.println(args[0]);
  }
}
```

**Explanation:**
- `class` defines a class; the name must match the filename
- `main` is the entry point of every Java program
- `public` means the class is accessible to all other classes
- `args` is an array of String arguments passed from the command line

---

## Part 3: Compile and Run (10 minutes)

`javac` compiles the `.java` file into a `.class` bytecode file. `java` runs it.

```bash
javac Main.java
java Main "Hello World"
```

**Expected output:**
```
Hello World
```

You can also run directly from VS Code using the **Run Java** button above the main method.

---

## Part 4: Variables & Data Types (20 minutes)

### Step 1: Create `LearnDataTypes.java`

```java
public class LearnDataTypes {
    public static void main(String[] args) {
        int num1 = 10;
        int num2 = Integer.parseInt(args[0]);
        System.out.println(num1 + num2);
    }
}
```

```bash
javac LearnDataTypes.java
java LearnDataTypes 5
```

**Expected output:**
```
15
```

`Integer.parseInt()` converts a `String` to an `int`. In Java, all variables must have an explicit data type — you cannot add a `String` directly to an `int`.

---

### Primitive Data Types

There are 8 primitive data types in Java:

| Whole Number | Decimal | Single Char | Boolean |
| :----------: | :-----: | :---------: | :-----: |
|     byte     |  float  |    char     | boolean |
|    short     | double  |             |         |
|     int      |         |             |         |
|     long     |         |             |         |

---

### Casting

Casting converts a value from one data type to another.

```java
// Narrowing (explicit) — developer must cast manually, data may be lost
int a = 10;
double b = 1.5;
int result = a + (int) b;  // result = 11 (b cast to 1, decimal lost)

// Widening (implicit) — compiler handles it automatically, no data loss
double result2 = a + b;  // result2 = 11.5 (a automatically cast to 10.0)
```

---

### Converting `String` to Numeric Types

| Method | Example |
| :----: | :-----: |
| `Byte.parseByte()` | `byte num = Byte.parseByte("10");` |
| `Short.parseShort()` | `short num = Short.parseShort("10");` |
| `Integer.parseInt()` | `int num = Integer.parseInt("10");` |
| `Long.parseLong()` | `long num = Long.parseLong("10000000000");` |
| `Float.parseFloat()` | `float num = Float.parseFloat("1.5");` |
| `Double.parseDouble()` | `double num = Double.parseDouble("1.5");` |
| `Boolean.parseBoolean()` | `boolean bool = Boolean.parseBoolean("true");` |

---

### Numeric Literal Character Suffixes

Without a suffix, the compiler treats whole numbers as `int` and decimals as `double`.

```java
long longNum = 10000000000L;   // L suffix required — exceeds int range
float floatNum = 1.5F;         // F suffix required — default decimal is double
double doubleNum = 1.5;        // D suffix optional
```

---

### 👨‍💻 Activity: Data Types Explorer

Create `DataTypesExplorer.java`. Declare variables of at least 5 different data types, print them, and include at least one explicit cast and one `parse` conversion from a String.

**Example structure:**

```java
public class DataTypesExplorer {
  public static void main(String[] args) {
    String name = "Ada Lovelace";
    char grade = 'A';
    int age = 30;
    double salary = 95000.50;
    boolean isActive = true;
    long companyId = 9876543210L;

    // Explicit cast: double to int (decimal truncated)
    int salaryInt = (int) salary;

    // Parse: String to int
    int parsedAge = Integer.parseInt("42");

    System.out.println("Name: " + name);
    System.out.println("Grade: " + grade);
    System.out.println("Age: " + age);
    System.out.println("Salary: " + salary);
    System.out.println("Salary as int: " + salaryInt);
    System.out.println("Active: " + isActive);
    System.out.println("Company ID: " + companyId);
    System.out.println("Parsed age: " + parsedAge);
  }
}
```

---

## Part 5: Wrapper Classes, Boxing and Unboxing (15 minutes)

### Wrapper Classes

Each primitive type has a corresponding wrapper class that allows it to be used as an object and provides useful utility methods.

| Primitive | Wrapper |
| :-------: | :-----: |
| byte | Byte |
| short | Short |
| char | Character |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |
| boolean | Boolean |

Wrapper classes are important in Spring Boot — for example, JPA entity fields use `Integer` instead of `int` to allow `null` values.

```java
System.out.println(Integer.MAX_VALUE);  // 2147483647
System.out.println(Integer.MIN_VALUE);  // -2147483648
int num = Integer.parseInt("10");       // String to int
```

---

### Boxing and Unboxing

**Boxing** converts a primitive to its wrapper class. **Unboxing** does the reverse. Java handles both automatically (autoboxing / auto-unboxing).

```java
Integer boxed = 10;      // autoboxing: int → Integer
int unboxed = boxed;     // auto-unboxing: Integer → int
```

Use primitives by default — reach for wrapper classes only when you need `null` support or utility methods.

---

### 👨‍💻 Activity: Explore Wrapper Classes

Create `WrapperClassesPractice.java` and try the following:

1. Print the `MAX_VALUE` and `MIN_VALUE` of `Integer`, `Double`, and `Long`
2. Parse the string `"false"` into a boolean and print it
3. Assign an `Integer` object the value `42`, unbox it into a plain `int`, and print both

```java
public class WrapperClassesPractice {
  public static void main(String[] args) {
    System.out.println("Int max: " + Integer.MAX_VALUE);
    System.out.println("Int min: " + Integer.MIN_VALUE);
    // Add the rest here
  }
}
```

---

## Part 6: Reading User Input (15 minutes)

### Step 1: Create `UserInputDemo.java`

```java
import java.util.Scanner;

public class UserInputDemo {
  public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);

    System.out.print("Enter your name: ");
    String userInput = scanner.nextLine();

    System.out.println("Hello " + userInput);

    scanner.close();
  }
}
```

```bash
javac UserInputDemo.java
java UserInputDemo
```

**How it works:**
- `Scanner` reads input from various sources — here we use `System.in` (keyboard)
- `nextLine()` reads a full line of text
- `close()` releases the resource when done

---

### 👨‍💻 Activity: Console Calculator

Create `ConsoleCalculator.java`. The program should:
1. Ask the user to enter two numbers
2. Ask the user to choose an operation: `+`, `-`, `*`, `/`
3. Perform the operation and print the result
4. Handle division by zero with a friendly message

**Example structure:**

```java
import java.util.Scanner;

public class ConsoleCalculator {
  public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);

    System.out.print("Enter first number: ");
    double num1 = scanner.nextDouble();

    System.out.print("Enter second number: ");
    double num2 = scanner.nextDouble();

    System.out.print("Enter operator (+, -, *, /): ");
    String operator = scanner.next();

    double result;

    if (operator.equals("+")) {
      result = num1 + num2;
      System.out.println("Result: " + result);
    } else if (operator.equals("-")) {
      result = num1 - num2;
      System.out.println("Result: " + result);
    } else if (operator.equals("*")) {
      result = num1 * num2;
      System.out.println("Result: " + result);
    } else if (operator.equals("/")) {
      if (num2 == 0) {
        System.out.println("Error: Cannot divide by zero.");
      } else {
        result = num1 / num2;
        System.out.println("Result: " + result);
      }
    } else {
      System.out.println("Invalid operator.");
    }

    scanner.close();
  }
}
```

---

## Part 7: Operators (20 minutes)

Operators are symbols that perform operations on variables and values.

Create `LearnOperators.java` and code along:

```java
public class LearnOperators {
  public static void main(String[] args) {
    int a = 10;
    int b = 20;
  }
}
```

---

### Arithmetic Operators

| Operator | Description | Example |
| :------: | :---------: | :-----: |
| + | Addition | x + y |
| - | Subtraction | x - y |
| * | Multiplication | x * y |
| / | Division | x / y |
| % | Remainder | x % y |

`+` is also used for String concatenation: `"Hello" + "World"` → `"HelloWorld"`

```java
System.out.println("a + b = " + (a + b));   // 30
System.out.println("a - b = " + (a - b));   // -10
System.out.println("a * b = " + (a * b));   // 200
System.out.println("a / b = " + (a / b));   // 0
System.out.println("b % a = " + (b % a));   // 0
```

---

### Unary Operators

| Operator | Description | Example |
| :------: | :---------: | :-----: |
| + | Plus | +x |
| - | Minus | -x |
| ++ | Increment | ++x / x++ |
| -- | Decrement | --x / x-- |
| ! | NOT | !x |

**Pre vs Post increment:** pre-increment (`++x`) increments the value *before* returning it; post-increment (`x++`) returns the current value *then* increments.

```java
int x = 10;
System.out.println(x++);   // 10 (returns 10, then x becomes 11)
System.out.println(++x);   // 12 (x becomes 12, then returns 12)
```

---

### Assignment and Compound Assignment Operators

Compound assignment operators are shorthand — `x += y` is the same as `x = x + y`.

| Operator | Example |
| :------: | :-----: |
| = | x = y |
| += | x += y |
| -= | x -= y |
| *= | x *= y |
| /= | x /= y |
| %= | x %= y |

```java
int compoundAdd = 8;
compoundAdd += 10;
System.out.println("compoundAdd: " + compoundAdd);  // 18
```

---

### Relational Operators

| Operator | Description | Example |
| :------: | :---------: | :-----: |
| == | Equals | x == y |
| != | Not Equal | x != y |
| > | Greater | x > y |
| >= | Greater or Equal | x >= y |
| < | Less Than | x < y |
| <= | Less Than or Equal | x <= y |

```java
System.out.println("a == b: " + (a == b));  // false
System.out.println("a != b: " + (a != b));  // true
System.out.println("a < b: " + (a < b));    // true
```

---

### Logical / Conditional Operators

| Operator | Description | Example |
| :------: | :---------: | :-------: |
| && | AND | x && y |
| \|\| | OR | x \|\| y |
| ! | NOT | !x |
| ? : | Ternary | x ? y : z |

```java
boolean value1 = true;
boolean value2 = false;
System.out.println("value1 && value2: " + (value1 && value2));  // false
System.out.println("value1 || value2: " + (value1 || value2));  // true
System.out.println(a > b ? "a is larger" : "b is larger");      // b is larger
```

---

### Type Comparison Operator

```java
String name = "John";
System.out.println(name instanceof String);  // true
```

---

### Operator Precedence

Operators follow standard precedence rules — multiplication before addition, parentheses override everything. When in doubt, use parentheses.

```java
int order1 = 10 + 5 * 2;    // 20 (multiplication first)
int order2 = (10 + 5) * 2;  // 30 (parentheses first)
```

**Full precedence table:** https://www.cs.bilkent.edu.tr/~guvenir/courses/CS101/op_precedence.html

---

## 👨‍💻 Activity: Operators in Action

Create `LearnOperators.java` and complete the following:

1. Declare `int score = 10`
2. Use **post-increment** to print score, then print it again to confirm it incremented
3. Use **pre-increment** and print — observe the difference from post-increment
4. Use a **compound assignment** to add 5 to score in one line and print the result
5. Use a **ternary operator** to check if the final score is above 20 — print `"High Score"` or `"Keep Going"`

**Expected Output:**

10
11
12
After += 5: 17
Keep Going

**Bonus (if you finish early):** Change the initial value of `score` to `18` and predict 
the output before running — then verify.

## Part 8: Code Formatting (5 minutes)

To format Java code in VS Code:
1. Open a Java file
2. Right-click in the editor → **Format Document With**
3. Choose **Language Support for Java by Red Hat**

**Shortcut:** Shift+Alt+F (Windows) / Shift+Option+F (Mac)

---

## Summary

### What You Accomplished Today

1. ✅ Installed WSL (Windows users), JDK 21, Maven, and VS Code Java extensions
2. ✅ Learned about classes and the main method
3. ✅ Compiled and ran Java programs
4. ✅ Worked with variables, data types, and casting
5. ✅ Used wrapper classes, boxing, and unboxing
6. ✅ Read user input using Scanner
7. ✅ Applied various operators in Java programs

### Key Takeaways

- **Java requires explicit data types** for all variables
- **The main method** is the entry point of every Java application
- **Narrowing cast** is manual (data may be lost); **widening cast** is automatic
- **Wrapper classes** provide object versions of primitives — important in Spring Boot for `null` support
- **Scanner** is the standard way to read user input from the console
- **Operators** follow standard precedence — use parentheses when in doubt

---

## Troubleshooting Guide

### Issue 1: `sdk` command not found

```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

Or restart your terminal.

---

### Issue 2: Permission denied when installing packages (WSL)

```bash
sudo apt install maven -y
```

---

### Issue 3: Java version mismatch

```bash
sdk current java
sdk use java 21-tem
```

---

### Issue 4: Scanner not found error

Add the import at the top of your file:
```java
import java.util.Scanner;
```

---

## Additional Resources

- [Java Tutorials - Oracle](https://docs.oracle.com/javase/tutorial/)
- [Java SE 21 Documentation](https://docs.oracle.com/en/java/javase/21/)
- [SDKMan Documentation](https://sdkman.io/)

---

**End of Lesson 3.1**