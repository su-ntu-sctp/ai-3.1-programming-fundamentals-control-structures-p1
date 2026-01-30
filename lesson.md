# Lesson Title: Programming Fundamentals and Control Structures |

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

---

# Part 1: Installation of JDK and Extension

Note:

1. Windows users need to install WSL2 to follow this lesson.

- https://learn.microsoft.com/en-us/windows/wsl/install

2. Git setup for WSL

- https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git

## Terminology

- Java Development Kit (JDK) - Toolkit wich includes the Java compiler and runtime environment for developers to write code (also called SDK in earlier versions).
- Java Runtime Environment (JRE) - Consists of JVM, core classes and supporting libraries. It is required to run Java applications.
- Java Virtual Machine (JVM) - A platform-independent virtual machine that runs Java bytecode. All Java programs are compiled into bytecode, which is then executed by the JVM.

More info: https://www.digitalocean.com/community/tutorials/difference-jdk-vs-jre-vs-jvm

When you install JDK, JRE is part of it.

## SDKMan

SDKMan is a popular command line tool for managing multiple versions of SDKs on Unix-based systems (Linux and Mac). Commonly used to manage JDK versions.

Benefits  :

- Multiple JDK versions: easily install, manage and switch between multiple versions of JDK.
  - Useful when working on different projects that require different JDK versions, or testing application compatibility across different versions.
- Isolation: JDKs are installed in local directory, avoiding conflicts with system-wide JDK installation.
- Easy updates: Update itself and all SDKs with a single command.

Install SDKMan:

```bash
# Note: For WSL users, you will need to install zip and unzip first.
$ sudo apt install zip unzip

$ curl -s "https://get.sdkman.io" | bash
```

After installation, you will need to run this line to initialize SDKMan:

```bash
$ source "$HOME/.sdkman/bin/sdkman-init.sh"
```

Check if sdkman is installed:

```bash
$ sdk version
```

## Install JDK

List the available Java SDKs:

```bash
$ sdk list java
```

We will install **Eclipse Temurin JDK 21** because it is the current **LTS** release with long‑term support. LTS stands for **Long‑Term Support**, which means this version will receive updates for an extended period. Refer to the Java SE Support Roadmap for exact timelines.

> Java SE Support Roadmap: https://www.oracle.com/java/technologies/java-se-support-roadmap.html

```bash
# Choose the latest version of Java 21 e.g. 21.0.x-tem
$ sdk install java 21.x.x-tem
```

Check if Java is installed:

```bash
$ java -version
```

## JShell

Jshell is a REPL (Read-Eval-Print-Loop) tool that allows you to execute Java code in an interactive manner. This is useful for testing out simple Java code without having to create a Java project.

Start jshell in your terminal:

```bash
$ jshell
```

Try your first Java code:

```bash
jshell> System.out.println("Hello World");
Hello World
jshell> /exit
```

## Install Extension Pack for Java

This is a collection of extensions that can help you write Java code in VSCode.

https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack

---

## Part 2 - `class` and `main` method

### Step 1: Create a `Main.java` file

In the root folder, create a file named `Main.java`.

The naming convention for a `class` is to use **PascalCase**. This means that the first letter of each word is capitalized.

https://www.oracle.com/java/technologies/javase/codeconventions-namingconventions.html

### Step 2: Define a class `Main`. The class name must be identical to the filename.

```java
public class Main {
  public static void main(String args[]){
    System.out.println(args[0]);
  }
}
```

- `class` is used to define a class.
- `main` is the entry point of all Java projects.
- `System.out.println(args[0])` will output its value to the console.
- `public` is an access modifier. It means that the class is accessible to all other classes.

---

## Part 3 - Compile and Run

To compile the file, we use the `javac` command on the java file. This generates a `.class` file of the same name.

Then, we use the `java` command to run the `.class` file. String values can be passed into the `main` method as arguments.

```sh
$ javac Main.java
$ java Main "Hello World"
```

You may also run the code directly from VSCode using the "Run Java" button.

---

## Part 4 - Variables & Data Types

### Step 1: Create `LearnDataTypes.java`

### Step 2: Insert the following code

```java
public class LearnDataTypes {
    public static void main(String args[]){
        int num1 = 10;
        // The String needs to be converted into an Integer
        int num2 = Integer.parseInt(args[0]);
        System.out.println(num1 + num2);
    }
}
```

🤔 Try replacing `Integer.parseInt(args[0])` with just `args[0]`. What happens and why?

In Java, variables must belong to a data type.

There are 8 primitive data types in Java:

| Whole Number | Decimal | Single Char | Boolean |
| :----------: | :-----: | :---------: | :-----: |
|     byte     |  float  |    char     | boolean |
|    short     | double  |
|     int      |         |
|     long     |         |

You cannot perform `11 + "1"`. This expression adds a `String` value of `1` to `int` value of `11`, which would not work. Therefore, we had to perform `Integer.parseInt()` to parse a `String` to an `Integer`.

### Casting

Casting is the process of converting a value from one data type to another.

Casting can be done **explicitly** or **implicitly**.

**Explicit casting** is done by the developer using the `()` operator.

```java
int a = 10;
double b = 1.5;
int result = a + (int) b;
```

**Implicit casting** is done automatically by the compiler.

```java
int a = 10;
double b = 1.5;
double result = a + b;
```

This is possible because the converted value (`int`) fits within the range of the new data type (`double`).

In Java, there are two types of casting:

- **Widening Casting** (automatically) - converting a smaller type to a larger type size.
- **Narrowing Casting** (manually) - converting a larger type to a smaller size type.

```java
// Widening Casting
int myInt = 9;
double myDouble = myInt; // Automatic casting: int to double

System.out.println(myInt);      // Outputs 9
System.out.println(myDouble);   // Outputs 9.0

// Narrowing Casting
double myDouble = 9.78;
int myInt = (int) myDouble; // Manual casting: double to int

System.out.println(myDouble);   // Outputs 9.78
System.out.println(myInt);      // Outputs 9
```

#### Converting from `String` to `Integer`

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

### Numeric Literal Character Suffixes

Numeric literal character suffixes are used to indicate the type of the numeric literal.

```java
// L suffix for long
long longNum = 10000000000L;

// F suffix for float
float floatNum = 1.5F;

// D suffix for double
double doubleNum = 1.5D;
```

Why do we need to specify the type of the numeric literal?

- Without the suffix, the compiler will generally treat a whole number as an `int`, and a decimal number as a `double`.

```java
// Compiler treats 1.5 as a double
float f = 1.5; // Error: incompatible types: possible lossy conversion from double to float

// For double, the suffix is optional
double d = 1.5; // No error
```

➡ Demo with int, long and casting

### 👨‍💻 Activity: Try out the different data types

Try initializing the following five data types and print them

- `String`
- `char`
- `int`
- `float`
- `boolean`

Your code should look something like this:

```java
public class LearnDataTypes {
  public static void main(String args[]){
    // Initializing variables of different data types here

    // Print them onto the console.

  }
}
```

Compile and run the program. This is the expected output:

```
11
myName prints Neo
a prints x
n prints 5
f prints 1.45
x prints true
```

---

## Part 5 - Wrapper Classes, Boxing and Unboxing

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

Wrapper classes provide a way to use primitive data types as objects, as well as provide some simple operations, which cannot be stored on a primitive.

For example, as you saw earlier, the `Integer` class provide a useful method to convert a `String` to an `Integer`.

```java
int num = Integer.parseInt("10");
```

You can also check the maximum and minimum values of an `Integer`.

```java
System.out.println(Integer.MAX_VALUE);
System.out.println(Integer.MIN_VALUE);
```

We can declare an `Integer` object like this instead using the primitive data type:

```java
Integer num = 10;
```

But as a rule of thumb, it is better to use the primitive data type unless you need to use the wrapper class methods.

### Boxing and Unboxing

Boxing is the process of converting a primitive data type to its corresponding wrapper class.

Java does autoboxing, which is the automatic conversion of a primitive data type to its corresponding wrapper class.

```java
Integer boxedNum = 10;
```

Unboxing is the process of converting a wrapper class to its corresponding primitive data type.

Java does auto-unboxing, which is the automatic conversion of a wrapper class to its corresponding primitive data type.

```java
int unboxedNum = boxedNum;
```

---

## Part 6 - Reading User Input

There are a few ways to read a user's input. We will be using `System.console().readLine()`.

### Step 1: Create `UserInputDemo.java`

### Step 2: Insert the following code

```java
public class UserInputDemo {
  public static void main(String[] args) {
    String userInput = System.console().readLine("Enter your name:");
    System.out.println("Hello " + userInput);
  }
}
```

### 👨‍💻 Activity: Get 2 numbers from user and add them

Create a new file `AddTwoNumbers.java` and write a program that reads 2 numbers from the console and add them together.

---

## Part 7: Operators

Operators are symbols that perform operations on variables and values.

The basic types of operators:

- Arithmetic
- Unary
- Assignment
- Relational
- Logical / Conditional

You can create a `LearnOperators.java` file and code along as we go through these operators.

```java
public class LearnOperators {
  public static void main(String[] args) {

    int a = 10;
    int b = 20;
  }
}
```

### Arithmetic Operators

| Operator |  Description   | Example |
| :------: | :------------: | :-----: |
|    +     |    Addition    |  x + y  |
|    -     |  Subtraction   |  x - y  |
|    \*    | Multiplication | x \* y  |
|    /     |    Division    |  x / y  |
|    %     |   Remainder    |  x % y  |

Notes:

- `+` is also used to concatenate strings e.g. `"Hello" + "World"` becomes `"HelloWorld"`.

```java
System.out.println("a + b = " + (a + b));
System.out.println("a - b = " + (a - b));
System.out.println("a * b = " + (a * b));
System.out.println("a / b = " + (a / b));
System.out.println("b % a = " + (b % a));
```

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

#### Pre vs Post Increment/Decrement:

Pre-increment/decrement operators increment/decrement the value of the variable **before** returning the value.

Post-increment/decrement operators increment/decrement the value of the variable **after** returning the value.

```java
int x = 10;
int y = 10;

System.out.println("x: " + x);
System.out.println("y: " + y);

System.out.println("x++: " + x++);
System.out.println("++y: " + ++y);

System.out.println("x: " + x);
System.out.println("y: " + y);
```

### Assignment and Compound Assignment Operators

- Assignment `=`
- Compound Assignment:

| Operator |  Description   | Example |
| :------: | :------------: | :-----: |
|    +=    |    Addition    | x += y  |
|    -=    |  Subtraction   | x -= y  |
|   \*=    | Multiplication | x \*= y |
|    /=    |    Division    | x /= y  |
|    %=    |   Remainder    | x %= y  |

Notes:

- Compound assignment operators are shorthand for performing an operation and assigning the result to the same variable. For example, `x += y` is the same as `x = x + y`.
- Compound operators cannot be used to declare variables. For example, `int x += 5` is invalid.

```java
int compoundAdd = 8;
compoundAdd += 10;
System.out.println("compoundAdd: " + compoundAdd);

int compoundSub = 10;
compoundSub -= 5;
System.out.println("compoundSub: " + compoundSub);
System.out.println();
```

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
System.out.println("a == b: " + (a == b));
System.out.println("a != b: " + (a != b));
System.out.println("a > b: " + (a > b));
System.out.println("a >= b: " + (a >= b));
System.out.println("a < b: " + (a < b));
System.out.println("a <= b: " + (a <= b));
```

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
System.out.println("value1 && value2: " + (value1 && value2));
System.out.println("value1 || value2: " + (value1 || value2));
System.out.println("!value1: " + (!value1));
System.out.println(a > b ? "a is larger" : "b is larger");
```

### Type Comparison Operator

|  Operator  |    Example     |
| :--------: | :------------: |
| instanceof | x instanceof y |

You can use the `instanceof` operator to check whether an object is an instance of a specific class or an instance of a subclass of that class.

```java
String name = "John";
System.out.println("name is String?" + name instanceof String);
```

### Operator Precedence

Operator precedence determines the order in which operators are evaluated. Operators with higher precedence are evaluated first.

| Operator | Precedence |
| :------: | :--------: |
|    ()    |     15     |
|    !     |     13     |
|    \*    |     12     |
|    /     |     12     |
|    %     |     12     |
|    +     |     11     |
|    -     |     11     |

```java
int order1 = 10 + 5 * 2;
int order2 = (10 + 5) * 2;
System.out.println("10 + 5 * 2: " + order1);
System.out.println("(10 + 5) * 2: " + order2);
```

Complete Precedence Table:
https://www.cs.bilkent.edu.tr/~guvenir/courses/CS101/op_precedence.html

### 👨‍💻 Activity: `OperatorsPractice.java` and `TernaryOperator.java`

---

## Part 8 - Useful Tips

### Code Formatting

To configure Java code formatting in VS Code, when in a Java file, right click and select "Format Document With" and choose "Language Support for Java by Red Hat".

### Shortcuts

- Type "so" and press tab to generate `System.out.println()`
- Type "psvm" and press tab to generate `public static void main(String[] args)`

---

End
