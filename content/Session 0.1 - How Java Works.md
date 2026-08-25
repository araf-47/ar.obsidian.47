# Session 0.1 — How Java Works

### Where this fits

This is the **foundation layer** of your Java rebuild.

```text
SESSION 0.1
How Java works
     ↓
Java source code
     ↓
Compilation
     ↓
.class / bytecode
     ↓
JVM
     ↓
Program execution
     ↓
Later: Classes → Objects → OOP → Interfaces → DI → Spring
```

The purpose of this session is to understand **what happens to your Java code between the moment you write it and the moment it runs**.

### This session covers

* Java source code
* `.java` files
* Compilation
* `javac`
* `.class` files
* JVM
* JDK vs JRE vs JVM
* `main()` method
* How a Java program starts and runs
* The basic Java execution process

### This session does NOT cover

We will **not** teach:

* classes and objects as an OOP topic
* inheritance
* interfaces
* collections
* exceptions
* Spring/Spring Boot
* dependency injection
* advanced JVM internals

We'll only mention a class briefly when necessary because a Java program needs one to demonstrate execution.

***

# 1. The Big Picture First

Suppose you write this:

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

You might currently think:

> "I wrote Java code, then Java runs it."

That's true at a very high level, but we're going to make the process precise.

The basic journey is:

```text
Hello.java
    │
    │ javac
    ▼
Hello.class
    │
    │ JVM
    ▼
Program runs
    │
    ▼
Hello
```

This is the most important mental model for today's session.

> **`.java` → `javac` → `.class` → JVM → execution**

Keep that in your head throughout the lesson.

***

# 2. What Is Java Source Code?

When you write Java code, you're writing **source code**.

For example:

```java
System.out.println("Hello");
```

This is something humans can reasonably read and write.

A complete tiny Java program might be:

```java
public class Hello {

    public static void main(String[] args) {
        System.out.println("Hello");
    }

}
```

This is **Java source code**.

The important point is:

> The JVM does not simply take your `.java` source code and execute it directly.

There is an intermediate step.

***

# 3. What Is a `.java` File?

A Java source file normally has the extension:

```text
.java
```

For example:

```text
Hello.java
```

Inside it we can have Java source code:

```java
public class Hello {

    public static void main(String[] args) {
        System.out.println("Hello");
    }

}
```

So:

```text
Hello.java
```

means:

> "This file contains Java source code."

Think of it like:

```text
Hello.java
    │
    └── Java source code
```

***

# 4. But Computers Don't Directly Understand Java Source Code

Here's where compilation comes in.

Your source code:

```java
System.out.println("Hello");
```

is written using Java's programming language syntax.

The computer ultimately needs instructions in a form that can be executed.

Java therefore uses a **compiler**.

The Java compiler is called:

```text
javac
```

Notice:

```text
java
```

and:

```text
javac
```

are different things.

***

# 5. What Is `javac`?

`javac` is the **Java compiler**.

Its job is to take Java source code:

```text
Hello.java
```

and compile it into:

```text
Hello.class
```

So:

```text
Hello.java
     │
     │ javac
     ▼
Hello.class
```

You can think of `javac` as a translator.

Very roughly:

```text
Human-written Java
        ↓
      javac
        ↓
Java bytecode
```

The resulting `.class` file contains **bytecode**.

***

# 6. What Is a `.class` File?

After compilation, you get:

```text
Hello.class
```

This is **not another source-code file that you normally edit**.

It contains Java **bytecode**.

For our purposes, think of bytecode as:

> An intermediate form of the program designed for the Java runtime to execute.

So now our pipeline becomes:

```text
Hello.java
   │
   │ javac
   ▼
Hello.class
   │
   │
   ▼
Java bytecode
```

And then something needs to execute that bytecode.

That's where the JVM comes in.

***

# 7. What Is the JVM?

JVM means:

> **Java Virtual Machine**

This is one of the most important terms in Java.

The JVM is the environment that **runs Java bytecode**.

So:

```text
Hello.class
    │
    │
    ▼
   JVM
    │
    ▼
Program executes
```

This gives us the fundamental Java model:

```text
.java
  ↓
javac
  ↓
.class / bytecode
  ↓
JVM
  ↓
execution
```

***

# 8. Why Does Java Use This Extra `.class` Step?

This is one of the reasons Java became famous for its portability.

Imagine you compile your Java program.

You get:

```text
Hello.class
```

That bytecode can be run by a JVM available for different operating systems.

Conceptually:

```text
              Hello.class
                   │
       ┌───────────┼───────────┐
       ↓           ↓           ↓
   JVM/Linux   JVM/Windows  JVM/macOS
       │           │           │
       ↓           ↓           ↓
    runs it      runs it     runs it
```

The JVM provides a common runtime environment.

This is related to the famous idea:

> **Write once, run anywhere.**

It's not literally guaranteed that every Java program runs everywhere without any compatibility considerations, but this is the fundamental idea.

***

# 9. JDK vs JRE vs JVM

This is a very common source of confusion.

Let's separate them carefully.

## JVM

**JVM = Java Virtual Machine**

Its main job for our current mental model is:

> Run Java bytecode.

```text
.class
  ↓
 JVM
  ↓
running program
```

***

## JRE

**JRE = Java Runtime Environment**

Historically, you can think of the JRE as the things needed to **run** Java programs, including the JVM and Java runtime libraries.

Conceptually:

```text
JRE
 ├── JVM
 └── Java runtime libraries
```

However, there's an important modern-Java detail:

> Modern JDK distributions generally don't come as a separate "JRE installation" in the way older Java versions did.

So don't get stuck thinking:

```text
I must separately install JDK + JRE + JVM
```

You normally install a **JDK**, which provides what you need for Java development and includes the JVM/runtime components.

***

## JDK

**JDK = Java Development Kit**

This is what a Java developer normally installs.

It contains development tools, including the Java compiler:

```text
JDK
 ├── javac
 ├── java
 ├── JVM/runtime components
 └── other development tools
```

Very simplified:

```text
JDK
 │
 ├── tools for DEVELOPING Java
 │      └── javac
 │
 └── tools/runtime for RUNNING Java
        └── JVM
```

### The practical distinction

Remember:

| Thing | Main idea                                      |
| -- | ---------------------------------------------- |
| JVM   | Runs Java bytecode                             |
| JRE   | Runtime environment for Java                   |
| JDK   | Development kit; includes compiler and runtime |

For your Java development:

> **You install/use a JDK.**

***

# 10. What Actually Happens When You Run a Java Program?

Let's use this tiny program:

```java
public class Hello {

    public static void main(String[] args) {
        System.out.println("Hello");
    }

}
```

Suppose the file is:

```text
Hello.java
```

## Step 1 — You write source code

```text
Hello.java
```

contains:

```java
public class Hello {

    public static void main(String[] args) {
        System.out.println("Hello");
    }

}
```

***

## Step 2 — Compile it

You run:

```bash
javac Hello.java
```

The compiler processes the Java source code.

If compilation succeeds, you get:

```text
Hello.class
```

So:

```text
Hello.java
    │
    │ javac Hello.java
    ▼
Hello.class
```

***

## Step 3 — Run it

You can then run:

```bash
java Hello
```

Notice something important:

You normally say:

```bash
java Hello
```

**not**

```bash
java Hello.java
```

for this traditional compile-and-run process.

The `java` launcher starts the Java runtime, which loads the compiled program and begins execution.

Conceptually:

```text
Hello.class
    ↓
Java runtime / JVM
    ↓
find starting point
    ↓
main(...)
    ↓
execute instructions
```

***

# 11. What Is `main()`?

Now we need to understand one specific piece of the program:

```java
public static void main(String[] args)
```

For today's session, you do **not** need to deeply understand every keyword.

We'll study those Java concepts properly later.

For now, understand its role:

> `main()` is the standard entry point for a traditional Java application.

"Entry point" means:

> The place where Java begins executing your application's code.

Think of it like the front door.

```text
Java program starts
        ↓
     main()
        ↓
other code executes
```

For example:

```java
public class Hello {

    public static void main(String[] args) {
        System.out.println("Hello");
        System.out.println("Java");
    }

}
```

Execution begins at:

```java
main()
```

and then Java executes the statements inside it in order.

***

# 12. Breaking Down `main()`

You don't need to master these keywords today, but let's make sure you aren't staring at mysterious syntax.

```java
public static void main(String[] args)
```

### `public`

An access modifier.

It means this method is accessible from outside its class.

For today's purpose, just remember:

> `main()` needs to be publicly accessible so the Java launcher can invoke it.

***

### `static`

This means the method belongs to the class rather than requiring an object instance.

**Important:** We're not going to dive into objects or static vs instance behavior today.

That belongs to your later Java foundation work.

For now:

> `main()` is declared `static` so Java can start the program without first needing to create an object of that class.

***

### `void`

This is the return type.

It means:

> This method doesn't return a value.

***

### `main`

This is the method's name.

The Java launcher recognizes this particular method as the traditional application entry point.

***

### `String[] args`

This is a parameter.

It allows command-line arguments to be passed into the program.

For today's purposes, you don't need to use it.

***

# 13. A Very Important Distinction

You may see:

```java
public static void main(String[] args)
```

and think:

> "Java starts by executing the whole class."

That's not the right mental model.

Instead:

```text
Java starts application
        ↓
finds main()
        ↓
starts executing main()
        ↓
statements inside main()
execute
```

For our basic mental model, **`main()` is the starting point.**

***

# 14. Let's Run One

Create a file named:

```text
Hello.java
```

Put this inside:

```java
public class Hello {

    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }

}
```

### Important

The file is called:

```text
Hello.java
```

and the class is called:

```text
Hello
```

For this simple example, those names correspond.

***

## Compile

Open your terminal in that directory and run:

```bash
javac Hello.java
```

If compilation succeeds, check the directory.

You should now have:

```text
Hello.java
Hello.class
```

The important transformation happened:

```text
Hello.java
      ↓
    javac
      ↓
Hello.class
```

***

## Run

Now:

```bash
java Hello
```

You should see:

```text
Hello, Java!
```

The process is:

```text
Hello.java
    │
    │ javac
    ▼
Hello.class
    │
    │ java
    ▼
   JVM
    │
    ▼
 main()
    │
    ▼
Hello, Java!
```

***

# 15. What If You Only Run `javac`?

Suppose you do:

```bash
javac Hello.java
```

and then stop.

You have:

```text
Hello.java
Hello.class
```

But nothing has been printed.

Why?

Because:

```text
javac
```

**compiles** the program.

It doesn't mean:

> "Run my program."

You still need to launch it:

```bash
java Hello
```

So:

```text
javac
→ compile

java
→ run
```

That's a very useful distinction.

***

# 16. What If There Is a Compilation Error?

Suppose you accidentally write:

```java
public class Hello {

    public static void main(String[] args) {
        System.out.println("Hello!"
    }

}
```

There's a missing:

```text
)
```

Now:

```bash
javac Hello.java
```

will produce a compilation error.

The compiler is essentially saying:

> "I cannot translate this source code into valid Java bytecode."

This is another important mental model:

```text
.java
  ↓
javac
  ↓
❌ compilation error
```

Therefore no usable `.class` file is produced from that successful compilation.

***

# 17. The Complete Mental Model

Let's put everything together.

```text
              YOU
               │
               │ write
               ▼
          Hello.java
        Java source code
               │
               │
          javac compiler
               │
               │ compile
               ▼
          Hello.class
        Java bytecode
               │
               │
               ▼
              JVM
      Java Virtual Machine
               │
               │ executes
               ▼
            main()
               │
               ▼
        program runs
```

This is the core of Session 0.1.

***

# 18. One More Important Idea: Java Is Not the JVM

People sometimes use "Java" to mean several different things.

Try to keep these separate:

```text
Java language
    ↓
the programming language you write

JDK
    ↓
development tools + runtime

javac
    ↓
Java compiler

.class
    ↓
compiled Java bytecode

JVM
    ↓
runs the bytecode
```

This distinction will make many future Java explanations easier.

***

# 19. Why This Matters for Spring

We're **not studying Spring today**.

But there is one useful connection.

Eventually you'll write something like:

```java
public class UserService {
    
    public void createUser() {
        // ...
    }
}
```

and Spring Boot will run your application.

Underneath all of that fancy Spring behavior, you are **still running a Java program**.

Spring doesn't replace:

```text
.java
 ↓
compile
 ↓
.class
 ↓
JVM
 ↓
execute
```

Spring operates **within the Java runtime environment**.

Later, when Spring creates Beans and calls methods, it's still ultimately Java code executing on the JVM.

So understanding today's foundation helps remove some of the "magic" feeling later.

***

# Practical Exercise

Do this yourself rather than just reading it.

## Exercise 1 — Hello Java

Create:

```text
Hello.java
```

with:

```java
public class Hello {

    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }

}
```

Then run:

```bash
javac Hello.java
```

Check that:

```text
Hello.class
```

appeared.

Then run:

```bash
java Hello
```

### Your task

After running it, answer these questions **without looking back at the explanation**:

1. What is `Hello.java`?
2. What does `javac Hello.java` do?
3. What is `Hello.class`?
4. What does the JVM do?
5. What is the role of `main()`?

***

# Code-Reading Checkpoint

Look at this:

```java
public class Test {

    public static void main(String[] args) {
        System.out.println("Starting...");
    }

}
```

Identify:

1. Which part is the Java source code?
2. What is the name of the `.java` file likely to be?
3. What command compiles it?
4. What `.class` file should be produced?
5. Which method is the entry point?
6. What ultimately executes the bytecode?

Don't worry about explaining `public`, `static`, `void`, or `String[]` deeply yet.

***

# Session Checkpoint

Answer these **without looking back if possible**:

### 1.

Complete the pipeline:

```text
.java
   ↓
_____
   ↓
.class
   ↓
_____
   ↓
program execution
```

### 2.

What is the difference between `javac` and `java`?

### 3.

What is the JVM's job?

### 4.

What is the difference between JDK and JVM?

### 5. Code reading

For this:

```java
public class Calculator {

    public static void main(String[] args) {
        System.out.println("2 + 3 = 5");
    }

}
```

Tell me:

* class name
* entry-point method
* what command compiles it
* what `.class` file is produced
* what command runs it

***

## Before considering Session 0.1 complete

You should be able to explain this **in your own words**:

> "I write Java source code in a `.java` file. `javac` compiles it into `.class` bytecode. The JVM runs that bytecode, and a traditional Java application begins execution through `main()`."

You **do not** need to memorize the historical details of JRE or JVM internals yet.

**Stop here.** Answer the checkpoint questions, and I'll evaluate your understanding before we move anywhere else.
