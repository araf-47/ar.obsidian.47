# Session 2.3 — Spring Boot Application

This session is about one simple question:

> **When I create a Spring Boot project and run it, what actually happens?**

By the end, you should understand why this code is the starting point of almost every Spring Boot application:

```java
@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

We will **not** study the internal implementation of `@SpringBootApplication`.

***

# 1. The Main Application Class

Let's start with a normal Java concept you already know.

A Java program needs a `main()` method:

```java
public static void main(String[] args) {
    // program starts here
}
```

For example:

```java
public class MyProgram {

    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

When you run this program:

```text
JVM
 ↓
main()
 ↓
your code
```

Spring Boot still has a `main()` method.

The difference is that instead of writing all the startup code ourselves, we give Spring Boot the responsibility of starting the application.

***

# 2. `@SpringBootApplication`

You'll usually see:

```java
@SpringBootApplication
public class MyApplication {
```

The annotation tells Spring Boot:

> **"This is the main application class of my Spring Boot application."**

So:

```java
@SpringBootApplication
public class MyApplication
```

means roughly:

```text
MyApplication
     ↓
Main Spring Boot application
```

Don't worry about what is *inside* the annotation.

Your syllabus specifically says:

> Do not study the internal implementation of `@SpringBootApplication`.

So for now, remember its **purpose**, not its internal mechanics.

***

## Small Example

Imagine your project is called `LandlordApplication`.

You might have:

```java
@SpringBootApplication
public class LandlordApplication {

    public static void main(String[] args) {
        SpringApplication.run(LandlordApplication.class, args);
    }
}
```

This class is the **entry point** of your Spring Boot application.

### Practical exercise

Look at this:

```java
@SpringBootApplication
public class ShopApplication {

    public static void main(String[] args) {
        SpringApplication.run(ShopApplication.class, args);
    }
}
```

Answer:

**Which class is the main application class?**

<details>
<summary>Answer</summary>

`ShopApplication`

Because it is the class containing:

```java
@SpringBootApplication
```

and the `main()` method.

</details>

***

# 3. `SpringApplication.run(...)`

Now we reach the most important line:

```java
SpringApplication.run(MyApplication.class, args);
```

This is what actually tells Spring Boot:

> **"Start my Spring Boot application."**

Think about it this way:

```java
public static void main(String[] args) {
    SpringApplication.run(MyApplication.class, args);
}
```

The Java program starts at:

```text
main()
```

Then `main()` tells Spring Boot:

```text
Start the Spring Boot application.
```

So the basic flow is:

```text
Operating System
       ↓
      JVM
       ↓
    main()
       ↓
SpringApplication.run(...)
       ↓
Spring Boot starts
```

***

# 4. Why `MyApplication.class`?

You may wonder about this:

```java
SpringApplication.run(MyApplication.class, args);
                         ↑
```

What is this?

You already know Java classes.

```java
MyApplication.class
```

is a reference to the `Class` object representing `MyApplication`.

For now, you don't need to go deeper into Java reflection or `Class<T>`.

Just understand:

```java
SpringApplication.run(MyApplication.class, args);
```

is basically saying:

> "Spring Boot, start the application using `MyApplication` as the main application class."

***

# 5. What about `args`?

You see:

```java
String[] args
```

in:

```java
public static void main(String[] args)
```

These are command-line arguments passed to the Java program.

Spring Boot receives them here:

```java
SpringApplication.run(MyApplication.class, args);
```

For this session, you don't need to study command-line arguments further.

Just recognize that `args` is being passed from Java's `main()` method to Spring Boot.

***

# 6. What Happens When Spring Boot Starts?

Now let's put the pieces together.

Suppose you have:

```java
@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

You run the application.

Conceptually:

```text
1. JVM starts
       ↓
2. main() runs
       ↓
3. SpringApplication.run(...)
       ↓
4. Spring Boot starts the application
       ↓
5. Spring starts its application context
       ↓
6. Spring Boot starts the web server
       ↓
7. Application is ready
```

You have already learned about the **Spring ApplicationContext**[^1] in the previous sessions.

So this is where your previous knowledge connects.

Spring Boot starts the Spring environment for your application.

***

# 7. Embedded Tomcat

This is an important difference between the old JSP/Tomcat style you know and Spring Boot.

You have worked with JSP and Tomcat.

Traditionally, you might think:

```text
Your application
      ↓
WAR
      ↓
Tomcat installed separately
      ↓
Deploy application
```

For example:

```text
Tomcat
 ├── your JSP application
 └── your application files
```

With Spring Boot, things are much more convenient.

Spring Boot can include an **embedded Tomcat** server in your application.

Conceptually:

```text
Spring Boot Application
│
├── Your Java code
│
├── Spring
│
└── Embedded Tomcat
```

So you don't normally need to separately install and manually configure Tomcat just to run your Spring Boot web application.

***

# 8. What Does "Embedded" Mean?

Embedded simply means:

> **The server is included as part of the application.**

Instead of:

```text
Tomcat
   ↑
   │
your application deployed into it
```

you can think of Spring Boot as:

```text
Your Spring Boot application
          │
          └── contains/uses an embedded web server
```

When you run:

```java
SpringApplication.run(...)
```

Spring Boot can start that embedded server.

***

# 9. What Do You See When It Starts?

When you run a typical Spring Boot web application, you'll see startup messages in the terminal.

Eventually you'll see something indicating that Tomcat has started, often including a port such as:

```text
Tomcat started on port 8080
```

Then your application is running.

You can access it through something like:

```text
http://localhost:8080
```

You already know what `localhost`, ports, HTTP, and Tomcat mean from your previous experience.

So think:

```text
Browser
   │
   │ HTTP request
   ↓
localhost:8080
   │
   ↓
Embedded Tomcat
   │
   ↓
Spring Boot application
```

**Important:** At this stage, we're only understanding startup. We aren't yet building REST controllers or APIs.

***

# 10. Application Startup — Putting Everything Together

Let's look at the entire process.

You write:

```java
@SpringBootApplication
public class LandlordApplication {

    public static void main(String[] args) {
        SpringApplication.run(LandlordApplication.class, args);
    }
}
```

Then you run the application.

Conceptually:

```text
                Run application
                       │
                       ↓
                     JVM
                       │
                       ↓
                    main()
                       │
                       ↓
       SpringApplication.run(...)
                       │
                       ↓
             Spring Boot starts
                       │
              ┌────────┴────────┐
              ↓                 ↓
       Spring environment   Embedded Tomcat
              │                 │
              └────────┬────────┘
                       ↓
                Application ready
                       │
                       ↓
                localhost:8080
```

That's the main idea of this session.

***

# 11. A Very Important Distinction

Don't confuse these three things:

### `@SpringBootApplication`

Identifies the main Spring Boot application class.

```java
@SpringBootApplication
public class MyApplication
```

### `main()`

The normal Java entry point.

```java
public static void main(String[] args)
```

### `SpringApplication.run()`

Tells Spring Boot to start the application.

```java
SpringApplication.run(MyApplication.class, args);
```

Think:

```text
@SpringBootApplication
        ↓
"This is my Spring Boot application class"

main()
        ↓
"Java starts here"

SpringApplication.run()
        ↓
"Spring Boot, start the application"
```

***

# 12. Your First Practical Exercise

Suppose you're creating a Spring Boot project called `Library`.

Write the main application class yourself.

You should produce something like:

```java
@SpringBootApplication
public class LibraryApplication {

    public static void main(String[] args) {
        SpringApplication.run(LibraryApplication.class, args);
    }
}
```

### Check yourself

Before looking at the answer, explain what each part does:

1. `@SpringBootApplication`
2. `main()`
3. `SpringApplication.run(...)`
4. `LibraryApplication.class`
5. `args`

***

# 13. One More Practical Exercise

Look at this:

```java
@SpringBootApplication
public class StudentApplication {

    public static void main(String[] args) {

        SpringApplication.run(StudentApplication.class, args);

    }
}
```

Imagine you run it.

Put these in the correct order:

**A.** Embedded Tomcat starts
**B.** JVM starts the `main()` method
**C.** Application becomes ready
**D.** `SpringApplication.run()` is called
**E.** Spring Boot starts the application

Correct order:

```text
B → D → E → A → C
```

The important mental model is:

```text
Java starts it
     ↓
Spring Boot takes over startup
     ↓
Spring starts
     ↓
Embedded Tomcat starts
     ↓
Application is ready
```

***

# Checkpoint

Try answering these **without looking back**.

### 1.

What is the purpose of:

```java
@SpringBootApplication
```

### 2.

Where does a Java application normally begin execution?

### 3.

What does this line do?

```java
SpringApplication.run(MyApplication.class, args);
```

### 4.

What does **embedded Tomcat** mean?

### 5.

In a traditional JSP application, you might install/configure Tomcat separately. What is different with Spring Boot?

### 6.

Explain this entire code in plain English:

```java
@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

If you can explain **#6 in your own words**, you understand the core of Session 2.3.

***

# Footnotes
[^1]: [[What is Spring ApplicationContext]]?
