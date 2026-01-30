# Lesson 3.1: Programming Fundamentals and Control Structures

<<<<<<< HEAD
**Module:** 3.1  
**Duration:** 180 minutes (3 hours)  
**Level:** Beginner
=======
## Lesson Overview
- **Briefing:** This lesson introduces the Java development environment and essential programming basics. Students will set up JDK, learn about classes, compilation, variables, data types, wrapper classes, user input, and operators. By the end, they will be able to write, compile, and execute simple Java programs in VS Code.  
- **Module.Lesson:** 3.1  
- **Duration:** 180 min  
- **Prerequisites:** Basic programming concepts, VS Code installed  

## Lesson Objectives
By the end of the lesson, the students will be able to:  
- Install and configure JDK, SDKMan, and Java extensions in VS Code.  
- Write and execute a Java program using the `class` and `main` method.  
- Apply variables, data types, casting, and wrapper classes in code.  
- Read and process user input from the console.  
- Demonstrate usage of arithmetic, relational, logical, and assignment operators.  
>>>>>>> 5498a9faa3cc00adabbf14225ab7d80ac237eb00

---

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

**Java Development Kit (JDK)** - Toolkit which includes the Java compiler and runtime environment for developers to write code (also called SDK in earlier versions)

**Java Runtime Environment (JRE)** - Consists of JVM, core classes and supporting libraries. It is required to run Java applications

**Java Virtual Machine (JVM)** - A platform-independent virtual machine that runs Java bytecode. All Java programs are compiled into bytecode, which is then executed by the JVM

**More info:** https://www.digitalocean.com/community/tutorials/difference-jdk-vs-jre-vs-jvm

When you install JDK, JRE is part of it.

---

### Install SDKMan

SDKMan is a popular command line tool for managing multiple versions of SDKs on Unix-based systems (Linux and Mac). Commonly used to manage JDK versions.

**Benefits:**

- **Multiple JDK versions:** easily install, manage and switch between multiple versions of JDK
  - Useful when working on different projects that require different JDK versions, or testing application compatibility across different versions
- **Isolation:** JDKs are installed in local directory, avoiding conflicts with system-wide JDK installation
- **Easy updates:** Update itself and all SDKs with a single command

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

After installation, run this line to initialize SDKMan:

```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

**Step 4: Verify installation**

```bash
sdk version
```

**Expected output:**
```
SDKMAN!
script: 5.18.2
native: 0.4.6
```

---

### Install JDK 21

We will install **Eclipse Temurin JDK 21** because it is the current **LTS** release with long‑term support.

**Step 1: List available Java SDKs**

```bash
sdk list java
```

**Step 2: Find Java 21 in the list**

Look for an identifier like:
```
21.0.5-tem
```

The identifier format is: `VERSION-VENDOR`
- VERSION: e.g., 21.0.5
- VENDOR: tem (Eclipse Temurin)

**Step 3: Install Java 21**

Replace `21.0.5-tem` with the actual identifier you see in the list:

```bash
sdk install java 21.0.5-tem
```

Or install the latest Java 21 version automatically:

```bash
sdk install java 21-tem
```

**Step 4: Verify installation**

```bash
java -version
```

**Expected output:**
```
openjdk version "21.0.5" 2024-10-15 LTS
OpenJDK Runtime Environment Temurin-21.0.5+11 (build 21.0.5+11-LTS)
OpenJDK 64-Bit Server VM Temurin-21.0.5+11 (build 21.0.5+11-LTS, mixed mode, sharing)
```

**Java SE Support Roadmap:** https://www.oracle.com/java/technologies/java-se-support-roadmap.html

---

### Install Maven

Maven is a build automation tool used for Java projects. We'll need it for later lessons.

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

**Expected output:**
```
Apache Maven 3.x.x
Maven home: /usr/share/maven
Java version: 21.0.5, vendor: Eclipse Adoptium
```

---

### JShell

JShell is a REPL (Read-Eval-Print-Loop) tool that allows you to execute Java code in an interactive manner. This is useful for testing out simple Java code without having to create a Java project.

**Start JShell:**

```bash
jshell
```

**Try your first Java code:**

```bash
jshell> System.out.println("Hello World");
Hello World
jshell> /exit
```

---

### Install Extension Pack for Java

This is a collection of extensions that can help you write Java code in VS Code.

**Step 1:** Open VS Code

**Step 2:** Click Extensions icon (or press Ctrl+Shift+X / Cmd+Shift+X)

**Step 3:** Search for "Extension Pack for Java"

**Step 4:** Click Install

**Link:** https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack

---

## Part 2: `class` and `main` Method (10 minutes)

### Step 1: Create a `Main.java` file

In a new folder, create a file named `Main.java`.

The naming convention for a `class` is to use **PascalCase**. This means that the first letter of each word is capitalized.

**Reference:** https://www.oracle.com/java/technologies/javase/codeconventions-namingconventions.html

### Step 2: Define a class `Main`

The class name must be identical to the filename.

```java
public class Main {
  public static void main(String args[]) {
    System.out.println(args[0]);
  }
}
```

**Explanation:**
- `class` is used to define a class
- `main` is the entry point of all Java programs
- `System.out.println(args[0])` will output its value to the console
- `public` is an access modifier - it means the class is accessible to all other classes
- `args` is an array of String arguments passed from the command line

---

## Part 3: Compile and Run (10 minutes)

To compile the file, we use the `javac` command on the Java file. This generates a `.class` file of the same name.

Then, we use the `java` command to run the `.class` file. String values can be passed into the `main` method as arguments.

**In Terminal/WSL:**

```bash
javac Main.java
java Main "Hello World"
```

**Expected output:**
```
Hello World
```

You may also run the code directly from VS Code using the "Run Java" button (appears above the main method).

---

## Part 4: Variables & Data Types (30 minutes)

### Step 1: Create `LearnDataTypes.java`

### Step 2: Insert the following code

```java
public class LearnDataTypes {
    public static void main(String args[]) {
        int num1 = 10;
        // The String needs to be converted into an Integer
        int num2 = Integer.parseInt(args[0]);
        System.out.println(num1 + num2);
    }
}
```

**Compile and run:**

```bash
javac LearnDataTypes.java
java LearnDataTypes 5
```

**Expected output:**
```
15
```

🤔 **Try this:** Replace `Integer.parseInt(args[0])` with just `args[0]`. What happens and why?

In Java, variables must belong to a data type.

---

### Primitive Data Types

There are 8 primitive data types in Java:

| Whole Number | Decimal | Single Char | Boolean |
| :----------: | :-----: | :---------: | :-----: |
|     byte     |  float  |    char     | boolean |
|    short     | double  |
|     int      |         |
|     long     |         |

You cannot perform `11 + "1"`. This expression adds a `String` value of `"1"` to `int` value of `11`, which would not work. Therefore, we had to perform `Integer.parseInt()` to parse a `String` to an `Integer`.

---

### Casting

Casting is the process of converting a value from one data type to another.

Casting can be done **explicitly** or **implicitly**.

**Explicit casting** is done by the developer using the `()` operator:

```java
int a = 10;
double b = 1.5;
int result = a + (int) b;  // result = 11 (b is cast to 1)
```

**Implicit casting** is done automatically by the compiler:

```java
int a = 10;
double b = 1.5;
double result = a + b;  // result = 11.5 (a is automatically cast to 10.0)
```

This is possible because the converted value (`int`) fits within the range of the new data type (`double`).

In Java, there are two types of casting:

- **Widening Casting** (automatically) - converting a smaller type to a larger type size
- **Narrowing Casting** (manually) - converting a larger type to a smaller size type

**Example:**

```java
// Widening Casting
int myInt = 9;
double myDouble = myInt; // Automatic casting: int to double

System.out.println(myInt);      // Outputs 9
System.out.println(myDouble);   // Outputs 9.0

// Narrowing Casting
double myDouble2 = 9.78;
int myInt2 = (int) myDouble2; // Manual casting: double to int

System.out.println(myDouble2);   // Outputs 9.78
System.out.println(myInt2);      // Outputs 9
```

---

### Converting from `String` to Numeric Types

The earlier way of using `Integer.parseInt()` is for converting a `String` to an `Integer`. It uses the `parseInt()` method from the `Integer` class. This is not the same as casting, which uses the `()` operator.

The following methods can convert String to numeric primitive types:

| Method | Example |
| :----: | :-----: |
| `Byte.parseByte()` | `byte num = Byte.parseByte("10");` |
|`Short.parseShort()` | `short num = Short.parseShort("10");` |
| `Integer.parseInt()` | `int num = Integer.parseInt("10");` |
| `Long.parseLong()` | `long num = Long.parseLong("10000000000");` |
| `Float.parseFloat()` | `float num = Float.parseFloat("1.5");` |
| `Double.parseDouble()` | `double num = Double.parseDouble("1.5");` |
|`Boolean.parseBoolean()` | `boolean bool = Boolean.parseBoolean("true");` |

---

### Numeric Literal Character Suffixes

Numeric literal character suffixes are used to indicate the type of the numeric literal.

```java
// L suffix for long
long longNum = 10000000000L;

// F suffix for float
float floatNum = 1.5F;

// D suffix for double (optional)
double doubleNum = 1.5D;
```

**Why do we need to specify the type?**

Without the suffix, the compiler will generally treat a whole number as an `int`, and a decimal number as a `double`.

```java
// Compiler treats 1.5 as a double
float f = 1.5;  // Error: incompatible types: possible lossy conversion from double to float

// Correct way:
float f = 1.5F;  // No error

// For double, the suffix is optional
double d = 1.5;  // No error
```

---

### 👨‍💻 Activity: Try out Different Data Types

Create a new file `DataTypesPractice.java` and initialize the following five data types and print them:

- `String`
- `char`
- `int`
- `float`
- `boolean`

**Example code structure:**

```java
public class DataTypesPractice {
  public static void main(String args[]) {
    // Initialize variables of different data types here
    String myName = "Neo";
    char myChar = 'X';
    int myNumber = 42;
    float myFloat = 3.14F;
    boolean myBoolean = true;
    
    // Print them onto the console
    System.out.println("Name: " + myName);
    System.out.println("Char: " + myChar);
    System.out.println("Number: " + myNumber);
    System.out.println("Float: " + myFloat);
    System.out.println("Boolean: " + myBoolean);
  }
}
```

---

## Part 5: Wrapper Classes, Boxing and Unboxing (20 minutes)

### Wrapper Classes

Recall Java has 8 primitive data types. For each of those types, there is a corresponding wrapper class (classes will be covered in more detail in a later lesson).

| Primitive Data Type | Wrapper Class |
| :-----------------: | :-----------: |
|        byte         |     Byte      |
|        short        |     Short     |
|        char         |   Character   |
|         int         |    Integer    |
|        long         |     Long      |
|        float        |     Float     |
|       double        |    Double     |
|       boolean       |    Boolean    |

Wrapper classes provide a way to use primitive data types as objects, as well as provide some simple operations, which cannot be performed on primitives.

For example, as you saw earlier, the `Integer` class provides a useful method to convert a `String` to an `Integer`:

```java
int num = Integer.parseInt("10");
```

You can also check the maximum and minimum values of an `Integer`:

```java
System.out.println(Integer.MAX_VALUE);  // 2147483647
System.out.println(Integer.MIN_VALUE);  // -2147483648
```

We can declare an `Integer` object like this instead of using the primitive data type:

```java
Integer num = 10;
```

But as a rule of thumb, it is better to use the primitive data type unless you need to use the wrapper class methods.

---

### Boxing and Unboxing

**Boxing** is the process of converting a primitive data type to its corresponding wrapper class.

Java does **autoboxing**, which is the automatic conversion of a primitive data type to its corresponding wrapper class:

```java
Integer boxedNum = 10;  // int 10 is automatically boxed to Integer
```

**Unboxing** is the process of converting a wrapper class to its corresponding primitive data type.

Java does **auto-unboxing**, which is the automatic conversion of a wrapper class to its corresponding primitive data type:

```java
int unboxedNum = boxedNum;  // Integer is automatically unboxed to int
```

---

## Part 6: Reading User Input (15 minutes)

There are a few ways to read a user's input. We will be using the `Scanner` class.

### Step 1: Create `UserInputDemo.java`

### Step 2: Insert the following code

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

**Compile and run:**

```bash
javac UserInputDemo.java
java UserInputDemo
```

**How it works:**
- `Scanner` is a class that reads input from various sources
- `System.in` represents the standard input (keyboard)
- `nextLine()` reads a line of text from the user
- `close()` closes the Scanner when done

---

### 👨‍💻 Activity: Get 2 Numbers from User and Add Them

Create a new file `AddTwoNumbers.java` and write a program that:
1. Reads 2 numbers from the console
2. Adds them together
3. Prints the result

**Hint:** Use `scanner.nextInt()` to read integers.

**Example structure:**

```java
import java.util.Scanner;

public class AddTwoNumbers {
  public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    
    System.out.print("Enter first number: ");
    int num1 = scanner.nextInt();
    
    System.out.print("Enter second number: ");
    int num2 = scanner.nextInt();
    
    // Calculate and print result
    
    scanner.close();
  }
}
```

---

## Part 7: Operators (30 minutes)

Operators are symbols that perform operations on variables and values.

The basic types of operators:

- Arithmetic
- Unary
- Assignment
- Relational
- Logical / Conditional

Create a `LearnOperators.java` file and code along:

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

| Operator |  Description   | Example |
| :------: | :------------: | :-----: |
|    +     |    Addition    |  x + y  |
|    -     |  Subtraction   |  x - y  |
|    *     | Multiplication |  x * y  |
|    /     |    Division    |  x / y  |
|    %     |   Remainder    |  x % y  |

**Notes:**
- `+` is also used to concatenate strings e.g. `"Hello" + "World"` becomes `"HelloWorld"`

```java
System.out.println("a + b = " + (a + b));
System.out.println("a - b = " + (a - b));
System.out.println("a * b = " + (a * b));
System.out.println("a / b = " + (a / b));
System.out.println("b % a = " + (b % a));
```

---

### Unary Operators

| Operator | Description | Example |
| :------: | :---------: | :-----: |
|    +     |    Plus     |   +x    |
|    -     |    Minus    |   -x    |
|    ++    |  Increment  |   ++x   |
|    --    |  Decrement  |   --x   |
|    !     |     NOT     |   !x    |

```java
int unaryPlus = +10;
int unaryMinus = -10;
System.out.println("unaryPlus: " + unaryPlus);
System.out.println("unaryMinus: " + unaryMinus);

int preIncrement = ++unaryPlus;
System.out.println("preIncrement: " + preIncrement);

int preDecrement = --unaryMinus;
System.out.println("preDecrement: " + preDecrement);

int postIncrement = unaryPlus++;
System.out.println("postIncrement: " + postIncrement);

int postDecrement = unaryMinus--;
System.out.println("postDecrement: " + postDecrement);

boolean isTrue = true;
System.out.println("isTrue: " + isTrue);
System.out.println("!isTrue: " + !isTrue);
```

Observe the output of the above code. What is the difference between pre and post increment/decrement?

---

### Pre vs Post Increment/Decrement

**Pre-increment/decrement** operators increment/decrement the value of the variable **before** returning the value.

**Post-increment/decrement** operators increment/decrement the value of the variable **after** returning the value.

```java
int x = 10;
int y = 10;

System.out.println("x: " + x);  // 10
System.out.println("y: " + y);  // 10

System.out.println("x++: " + x++);  // 10 (then x becomes 11)
System.out.println("++y: " + ++y);  // 11 (y becomes 11 first)

System.out.println("x: " + x);  // 11
System.out.println("y: " + y);  // 11
```

---

### Assignment and Compound Assignment Operators

- Assignment: `=`
- Compound Assignment:

| Operator |  Description   | Example |
| :------: | :------------: | :-----: |
|    +=    |    Addition    | x += y  |
|    -=    |  Subtraction   | x -= y  |
|    *=    | Multiplication | x *= y  |
|    /=    |    Division    | x /= y  |
|    %=    |   Remainder    | x %= y  |

**Notes:**
- Compound assignment operators are shorthand for performing an operation and assigning the result to the same variable. For example, `x += y` is the same as `x = x + y`
- Compound operators cannot be used to declare variables. For example, `int x += 5` is invalid

```java
int compoundAdd = 8;
compoundAdd += 10;
System.out.println("compoundAdd: " + compoundAdd);  // 18

int compoundSub = 10;
compoundSub -= 5;
System.out.println("compoundSub: " + compoundSub);  // 5
```

---

### Relational Operators

| Operator |    Description     | Example |
| :------: | :----------------: | :-----: |
|    ==    |       Equals       | x == y  |
|    !=    |     Not Equal      | x != y  |
|    >     |      Greater       |  x > y  |
|    >=    |  Greater or Equal  | x >= y  |
|    <     |     Less Than      |  x < y  |
|    <=    | Less Than or Equal | x <= y  |

```java
System.out.println("a == b: " + (a == b));  // false
System.out.println("a != b: " + (a != b));  // true
System.out.println("a > b: " + (a > b));    // false
System.out.println("a >= b: " + (a >= b));  // false
System.out.println("a < b: " + (a < b));    // true
System.out.println("a <= b: " + (a <= b));  // true
```

---

### Logical / Conditional Operators

| Operator | Description |  Example  |
| :------: | :---------: | :-------: |
|    &&    |     AND     |  x && y   |
|   \|\|   |     OR      | x \|\| y  |
|    !     |     NOT     |    !x     |
|   ? :    |   Ternary   | x ? y : z |

```java
boolean value1 = true;
boolean value2 = false;
System.out.println("value1 && value2: " + (value1 && value2));  // false
System.out.println("value1 || value2: " + (value1 || value2));  // true
System.out.println("!value1: " + (!value1));  // false
System.out.println(a > b ? "a is larger" : "b is larger");  // b is larger
```

---

### Type Comparison Operator

|  Operator  |    Example     |
| :--------: | :------------: |
| instanceof | x instanceof y |

You can use the `instanceof` operator to check whether an object is an instance of a specific class or an instance of a subclass of that class.

```java
String name = "John";
System.out.println("name is String? " + (name instanceof String));  // true
```

---

### Operator Precedence

Operator precedence determines the order in which operators are evaluated. Operators with higher precedence are evaluated first.

| Operator | Precedence |
| :------: | :--------: |
|    ()    |     15     |
|    !     |     13     |
|    *     |     12     |
|    /     |     12     |
|    %     |     12     |
|    +     |     11     |
|    -     |     11     |

```java
int order1 = 10 + 5 * 2;        // 20 (multiplication first)
int order2 = (10 + 5) * 2;      // 30 (parentheses first)
System.out.println("10 + 5 * 2: " + order1);
System.out.println("(10 + 5) * 2: " + order2);
```

**Complete Precedence Table:**
https://www.cs.bilkent.edu.tr/~guvenir/courses/CS101/op_precedence.html

---

## Part 8: Useful Tips (5 minutes)

### Code Formatting

To configure Java code formatting in VS Code:
1. Open a Java file
2. Right-click in the editor
3. Select "Format Document With"
4. Choose "Language Support for Java by Red Hat"

---

### Shortcuts

- Type `sout` and press Tab to generate `System.out.println()`
- Type `psvm` and press Tab to generate `public static void main(String[] args)`

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
- **Casting** converts between data types (widening is automatic, narrowing is manual)
- **Wrapper classes** provide object versions of primitive types with useful methods
- **Scanner** is the reliable way to read user input
- **Operators** follow precedence rules - use parentheses when in doubt

---

## Troubleshooting Guide

### Issue 1: sdk command not found

**Solution:**
Run the initialization command:
```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

Or restart your terminal.

---

### Issue 2: Permission denied when installing packages (WSL)

**Solution:**
Use `sudo` before the command:
```bash
sudo apt install maven -y
```

---

### Issue 3: Java version mismatch

**Solution:**
Check which Java version is active:
```bash
sdk current java
```

Switch to Java 21:
```bash
sdk use java 21.0.5-tem
```

---

### Issue 4: Scanner not found error

**Solution:**
Add the import statement at the top of your file:
```java
import java.util.Scanner;
```

---

## Additional Resources

### Java Documentation
- [Java Tutorials - Oracle](https://docs.oracle.com/javase/tutorial/)
- [Java SE 21 Documentation](https://docs.oracle.com/en/java/javase/21/)
- [SDKMan Documentation](https://sdkman.io/)

### Video Tutorials
- [Java Tutorial for Beginners](https://www.youtube.com/results?search_query=java+tutorial+beginners)
- [Java Operators Explained](https://www.youtube.com/results?search_query=java+operators+tutorial)

---

**End of Lesson 3.1**

**Congratulations!** You've successfully set up your Java development environment and learned the fundamentals of Java programming. You're now ready to build more complex programs! 🎉

**Next Lesson:** Control Structures (if statements, loops)