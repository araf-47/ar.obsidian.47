# Session 2.1 — What is Spring Boot?

This is the beginning of **Day 2**, where we move from the Spring Framework concepts you learned yesterday into **Spring Boot**.

The most important idea for this lesson is:

> **Spring Boot is a way to build Spring applications much more easily and quickly.**

You already know Java, JDBC, JSP, HTTP, and you're learning Angular. I'll use those to make the differences concrete.

***

# 1. First: What problem does Spring Boot solve?

Before Spring Boot, you could build a Spring application using the **Spring Framework**, but you often had to make many decisions and configurations yourself.

Imagine you want to build a simple web application.

You need things like:

```text
Java application
      ↓
Spring
      ↓
Web server
      ↓
HTTP requests
      ↓
Your controllers
```

Spring itself provides the framework for this.

But historically, getting all the pieces configured correctly could involve a lot of setup.

Spring Boot's philosophy is essentially:

> **"Let me configure the common things for you so you can concentrate on your application."**

So instead of spending a lot of time configuring infrastructure, you can start writing application code quickly.

***

# 2. Spring Framework vs Spring Boot

This distinction is extremely important.

## Spring Framework

The **Spring Framework** is the underlying framework that provides things such as:

* IoC
* Dependency Injection
* Beans
* `ApplicationContext`
* configuration
* many other features

You've already been learning these.

For example:

```java
@Service
public class EmailService {

    public void sendEmail() {
        System.out.println("Email sent");
    }
}
```

Spring can manage `EmailService` as a Bean.

***

## Spring Boot

Spring Boot builds **on top of Spring Framework**.

It makes setting up and running Spring applications much easier.

Think of it like this:

```text
Spring Framework
       ↑
       │
   Spring Boot
```

Spring Boot doesn't replace Spring.

It helps you **use Spring with much less setup**.

### A useful analogy

Think about Java itself.

You could theoretically manage many low-level details yourself, but libraries and frameworks make common tasks easier.

Similarly:

```text
Spring Framework
= powerful foundation

Spring Boot
= convenient way to build applications using that foundation
```

***

# 3. Why does Spring Boot exist?

Let's imagine building a Spring web application.

Without Boot, you might need to think about:

```text
Which dependencies?
Which configuration?
Which server?
How should Spring be configured?
How should the application start?
How should common components be configured?
```

Spring Boot tries to reduce this work.

So instead of:

```text
Developer
   ↓
lots of configuration
   ↓
Spring setup
   ↓
server setup
   ↓
application
```

you get something closer to:

```text
Developer
   ↓
Spring Boot
   ↓
sensible defaults + automatic configuration
   ↓
application
```

This is one of the main reasons Spring Boot became so popular.

***

# 4. Starter Dependencies

This is one of the first Spring Boot concepts you'll encounter.

Suppose you're building a REST API[^1].

You need several libraries to make that work.

Instead of manually finding and adding every individual library, Spring Boot provides **starter dependencies**.

For example:

```text
spring-boot-starter-web
```

A starter is basically a convenient bundle of dependencies commonly needed for a particular purpose.

Think:

```text
spring-boot-starter-web
        │
        ├── dependencies needed for web development
        ├── dependencies needed for Spring MVC
        └── other related pieces
```

You don't need to memorize exactly what's inside it right now.

The important idea is:

> **A starter dependency gives your application a convenient set of libraries for a particular type of application.**

You'll encounter this when we create a Spring Boot project.

***

# 5. Small analogy with your Angular experience

You can think of a starter somewhat like choosing an Angular package/setup that brings together the pieces needed for a particular capability.

It's not exactly the same mechanism, but the mindset is similar:

> "I need functionality X, so give me the commonly required pieces for X."

For example:

```text
Spring Boot application
        +
spring-boot-starter-web
        ↓
Web/API development
```

***

# 6. Auto-configuration

This is probably the most important Spring Boot feature in today's lesson.

Spring Boot looks at what you've included in your application and tries to configure common things automatically.

For example, suppose your project includes the web starter.

Spring Boot can recognize:

> "This is a web application."

It can then provide appropriate default configuration.

Conceptually:

```text
You add web-related dependencies
             ↓
      Spring Boot notices
             ↓
    sensible web configuration
             ↓
       application works
```

That's **auto-configuration**.

***

## Don't think of it as magic

A common beginner mistake is:

> "Spring Boot magically knows everything."

Not really.

It has a large amount of predefined configuration and rules for common situations.

You don't need to understand how those rules are implemented internally for this course.

Your current mental model should simply be:

> **Spring Boot automatically configures many common things based on what my application needs.**

***

# 7. Convention over Configuration

This phrase sounds complicated, but the idea is simple.

It means:

> **If you follow the common/recommended way of doing things, Spring Boot can make many configuration decisions for you.**

Instead of telling Spring Boot every little detail:

```text
Configure this...
Configure that...
Use this default...
Set this...
Set that...
```

you follow Spring Boot's conventions.

Then Boot says, roughly:

> "Okay, you're following the normal structure. I'll use the sensible defaults."

***

## Example

Suppose your project follows Spring Boot's normal structure.

You don't necessarily have to manually configure every piece of the application.

The framework already has expectations about how a typical Spring application is organized.

So:

```text
Convention
    ↓
Spring Boot understands the situation
    ↓
Less configuration required
```

That's the basic idea.

***

# 8. Embedded Server

This is particularly important because you already know JSP and Tomcat.

Previously, you learned that Tomcat can act as a web server/servlet container.

With traditional Java web development, you might have:

```text
Your application
      ↓
WAR file
      ↓
Tomcat installed separately
      ↓
Deploy application
      ↓
Run
```

Spring Boot commonly works differently.

It can include an **embedded web server** inside your application.

Conceptually:

```text
Spring Boot application
       │
       ├── Your Java code
       │
       └── Embedded web server
```

So you can run your application as a normal Java application.

For example, conceptually:

```bash
java -jar my-application.jar
```

and the application starts its embedded server.

***

## Why is this useful?

You don't necessarily need to:

1. install Tomcat separately
2. create a WAR
3. manually deploy the WAR
4. start/configure Tomcat separately

Instead:

```text
Run Spring Boot application
          ↓
Application starts
          ↓
Embedded server starts
          ↓
Application can receive HTTP requests
```

This makes development and deployment much simpler.

### Important connection to your JSP knowledge

You already installed Tomcat and used it with JSP.

So remember:

**Tomcat hasn't become useless.**

Spring Boot can simply package/use a web server such as Tomcat **inside the application** rather than requiring you to manage a separate Tomcat installation.

***

# 9. Putting the major ideas together

Let's combine what we've learned.

Imagine we're building a Spring Boot web application.

We add:

```text
spring-boot-starter-web
```

Then:

```text
Starter dependency
        ↓
Spring Boot knows we're building a web application
        ↓
Auto-configuration
        ↓
Common web configuration is provided
        ↓
Embedded server
        ↓
Application can run as a web application
```

And because we're following Spring Boot conventions:

```text
Convention over configuration
        ↓
Less manual configuration
```

That's the overall picture.

***

# 10. What does a Spring Boot application look like?

Soon you'll create one.

A very simplified Spring Boot application looks something like this:

```java
@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {

        SpringApplication.run(MyApplication.class, args);

    }
}
```

Don't worry about `@SpringBootApplication` in detail yet.

For today's lesson, just understand what happens conceptually:

```java
SpringApplication.run(...)
```

means roughly:

> "Start my Spring Boot application."

Then Spring Boot starts the application and, for a web application, can start the embedded server as part of that process.

***

# 11. What is `@SpringBootApplication`?

You'll see this constantly, so you should recognize it.

```java
@SpringBootApplication
public class MyApplication {
```

For this lesson, think:

> **This marks the main class of a Spring Boot application and enables the normal Spring Boot setup.**

Don't go deeper yet.

The internal details of what this annotation combines are **not part of today's lesson**.

***

# 12. High-level production-ready features

Spring Boot also provides features that help applications beyond just getting them running.

For example, Spring Boot has support for things such as:

* externalized configuration
* logging
* application monitoring/health information
* metrics
* production-oriented configuration

You don't need to study these deeply right now.

The important point is:

> **Spring Boot isn't just a shortcut for starting a development project. It also provides infrastructure useful for real-world applications.**

We'll leave the details for later if your course requires them.

***

# 13. Your mental model of Spring Boot

At this point, I want you to have this picture:

```text
                    SPRING BOOT
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ↓                ↓                ↓
   Starter          Auto-             Embedded
 dependencies     configuration         server
        │                │                │
        └────────────────┼────────────────┘
                         ↓
                Less manual setup
                         ↓
              Build Spring applications
                    more easily
```

And underneath it:

```text
Spring Boot
     ↓
Spring Framework
     ↓
IoC / DI / Beans / ApplicationContext
```

This connects directly to everything you learned in Day 1.

***

# 14. Very important: Spring ≠ Spring Boot

Don't accidentally think:

```text
Spring = old version
Spring Boot = new version
```

That's not the right relationship.

Instead:

```text
Spring Framework
      │
      │ provides the core framework
      ↓
Spring Boot
      │
      │ makes building Spring applications easier
      ↓
Your application
```

Spring Boot **uses Spring Framework**.

***

# 15. Practical Exercise

Since you don't yet have to manually set up all of this, today's exercise is mainly about recognizing the pieces.

Imagine you create a Spring Boot project with:

```text
spring-boot-starter-web
```

Answer these questions:

### Question 1

Why would you choose:

```text
spring-boot-starter-web
```

instead of manually searching for every library needed for web development?

***

### Question 2

Suppose you run your Spring Boot application and Tomcat starts without you installing a separate Tomcat server for this application.

Which Spring Boot feature is responsible for this?

A. Starter dependency
B. Embedded server
C. Component scanning
D. Dependency injection

***

### Question 3

You add web-related dependencies and Spring Boot automatically applies common web configuration.

What feature is this?

***

### Question 4

Complete this:

> Spring Boot does not replace the Spring Framework. Instead, Spring Boot __________.

***

### Question 5 — most important

Imagine you're explaining Spring Boot to a friend who knows Java but doesn't know Spring.

Give me your own explanation of:

> **"What is Spring Boot, and why do we use it?"**

Don't try to use textbook language. Explain it in your own words.

***

## Session 2.1 checkpoint

If you can clearly explain these **six ideas**, you're ready to move on:

| Concept                       | Your understanding should be                                  |
| ----------------------------- | ------------------------------------------------------------- |
| Spring Framework              | The underlying framework providing things like IoC, DI, Beans |
| Spring Boot                   | Makes building/running Spring applications easier             |
| Starter dependency            | Convenient bundle of related dependencies                     |
| Auto-configuration            | Boot automatically provides common configuration              |
| Embedded server               | Web server can run inside the application                     |
| Convention over configuration | Follow common conventions → less manual configuration         |

**Don't worry about how Spring Boot performs auto-configuration internally.** That's explicitly outside today's scope.

Answer the 5 checkpoint questions above, especially **#5**, and I'll check your understanding before we continue.

***
# Footnote
[^1]: [[What is REST API  (for now)]]?
