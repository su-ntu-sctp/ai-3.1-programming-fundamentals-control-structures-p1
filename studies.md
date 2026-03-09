# **Self-Study Preparation Guide**

**⏳ Estimated Prep Time:** 60–80 minutes

Welcome to our flipped-classroom session, where you'll review foundational concepts beforehand to maximize our time for hands-on coding and debugging. This pre-study focuses on the essential building blocks of Java programming: **Setting Up Your Environment**, **Variables & Data Types**, and **Operators**.

By mastering these concepts now, you will be better equipped to write, compile, and run your first Java programs confidently during our live session.

---

## ⚡ Your Self-Study Tasks

Please complete the following activities before our session.

---

### 📝 Task 1: Setting Up Java & Your First Program (20 Minutes)

**Activity:**

Review the following official documentation:
- [Install WSL2 on Windows](https://learn.microsoft.com/en-us/windows/wsl/install)
- [Install SDKMan](https://sdkman.io/)
- [Java SE Support Roadmap - Why JDK 21 LTS](https://www.oracle.com/java/technologies/java-se-support-roadmap.html)

Also watch the video titled [**"How to Install WSL2 on Windows"**](https://www.youtube.com/watch?v=eId6K8d0v6o).

[![video](https://img.youtube.com/vi/eId6K8d0v6o/default.jpg)](https://www.youtube.com/watch?v=eId6K8d0v6o)

Review the following sections from the [`lesson.md`](./lesson.md) file:
- **Installing WSL2** (Windows users)
- **Installing SDKMan**
- **Installing Eclipse Temurin JDK 21**
- **Installing Maven**
- **The `class` and `main` method**
- **Compiling and running a Java program**

Pay close attention to the relationship between the JDK, JRE, and JVM, and how a Java program goes from source code to execution.

**Guiding Questions:**
* **JDK vs JRE vs JVM:** What is the difference between the three? Which one do you need to write and run Java code?
* **SDKMan:** Why is it useful to manage multiple JDK versions on the same machine?
* **Temurin JDK 21:** Why are we using JDK 21 specifically? What does LTS mean?
* **Compilation:** What does the `javac` command do, and what file does it produce?
* **main method:** Why must every Java program have a `main` method? What happens if it's missing?

---

### 📝 Task 2: Variables, Data Types & Casting (25 Minutes)

**Activity:**

Watch the following videos:

[**"Java Data Types Explained"**](https://www.youtube.com/watch?v=D3DqJrlckbs)

[![video](https://img.youtube.com/vi/D3DqJrlckbs/default.jpg)](https://www.youtube.com/watch?v=D3DqJrlckbs)

[**"Java Variables and Data Types"**](https://www.youtube.com/watch?v=sVIvhzEizEQ)

[![video](https://img.youtube.com/vi/sVIvhzEizEQ/default.jpg)](https://www.youtube.com/watch?v=sVIvhzEizEQ)

Review the following sections from the [`lesson.md`](./lesson.md) file:
- **Primitive Data Types** (byte, short, int, long, float, double, char, boolean)
- **Casting** (widening vs narrowing)
- **Converting String to Numeric Types** (`Integer.parseInt()`, etc.)
- **Wrapper Classes, Boxing and Unboxing**

Pay attention to when Java automatically handles type conversion and when you need to do it manually.

**Guiding Questions:**
* **Primitive Types:** Why does Java have both `int` and `long`? When would you use one over the other?
* **Casting:** What is the difference between widening and narrowing casting? Why does narrowing require an explicit cast?
* **String Parsing:** Why can't you directly add a `String` and an `int`? What must you do first?
* **Wrapper Classes:** When would you use `Integer` instead of `int`? What extra functionality does it provide?

---

### 📝 Task 3: Operators (20 Minutes)

**Activity:**

Watch the video titled [**"Java Operators"**](https://www.youtube.com/watch?v=RbjB3SIaabM).

[![video](https://img.youtube.com/vi/RbjB3SIaabM/default.jpg)](https://www.youtube.com/watch?v=RbjB3SIaabM)

Review the following sections from the [`lesson.md`](./lesson.md) file:
- **Arithmetic Operators**
- **Unary Operators** (pre vs post increment/decrement)
- **Assignment and Compound Assignment Operators**
- **Relational Operators**
- **Logical / Conditional Operators**
- **Operator Precedence**

Pay close attention to the difference between pre and post increment/decrement, and how operator precedence affects the result of expressions.

**Guiding Questions:**
* **Arithmetic:** What is the `%` operator and when would you use it in a real program?
* **Pre vs Post Increment:** What is the difference between `x++` and `++x`? How does the result differ when used inside an expression?
* **Compound Assignment:** How is `x += 5` different from `x = x + 5`? Are they always equivalent?
* **Operator Precedence:** Given the expression `10 + 5 * 2`, what is the result and why? How would you change it to get `30`?

---

## 🙌🏻 Active Engagement Strategies

To deepen your retention, try one of the following while you review:

* **"Code Tracing":** Pick a casting or operator example from the lesson and trace through it line by line. Predict the output before running it.
* **"Type Mapping":** Draw a table mapping each primitive type to its wrapper class and write one use case for each wrapper class method.
* **"Real-World Application":** Think of a real-world scenario where data types matter — for example, storing a person's age vs a bank account balance. Which data type would you choose and why?
* **"Operator Challenge":** Write 3 arithmetic expressions on paper, predict the output based on operator precedence, then verify by running them in JShell.

---

## 📖 Additional Reading Material

**Java Basics:**
- [Oracle Java Tutorial - Getting Started](https://docs.oracle.com/javase/tutorial/getStarted/index.html)
- [W3Schools - Java Data Types](https://www.w3schools.com/java/java_data_types.asp)
- [W3Schools - Java Type Casting](https://www.w3schools.com/java/java_type_casting.asp)

**Java Operators:**
- [Oracle Java Tutorial - Operators](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/operators.html)
- [W3Schools - Java Operators](https://www.w3schools.com/java/java_operators.asp)
- [GeeksforGeeks - Java Wrapper Classes](https://www.geeksforgeeks.org/wrapper-classes-java/)

**Environment Setup:**
- [SDKMan Documentation](https://sdkman.io/)
- [Java SE Support Roadmap](https://www.oracle.com/java/technologies/java-se-support-roadmap.html)

---

### 🙋🏻‍♂️ See you in the session!