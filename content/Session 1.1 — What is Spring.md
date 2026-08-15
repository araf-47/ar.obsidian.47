# Session 1.1 — What is Spring?

We'll build this from **plain Java → traditional Java application → Spring → Spring Boot**. Since you already know Java, JDBC, JSP, SQL, and HTTP, I'll use those as reference points.

***

## 1. What is the Spring Framework?

At the simplest level:

> **Spring is a Java framework that helps you build large, maintainable Java applications by managing objects and their relationships for you.**

That's the definition I want you to remember for now.

But that raises an important question:

**What does "managing objects and their relationships" actually mean?**

Let's first look at Java without Spring.

### Traditional Java

Suppose you have:

```java
public class UserService {

    private UserRepository userRepository;

    public UserService() {
        this.userRepository = new UserRepository();
    }

    public void registerUser(String name) {
        userRepository.save(name);
    }
}
```

And:

```java
public class UserRepository {

    public void save(String name) {
        System.out.println("Saving " + name);
    }
}
```

`UserService` needs a `UserRepository`.

So `UserService` creates it:

```java
this.userRepository = new UserRepository();
```

This works perfectly.

But imagine your application has:

* 100 services
* 50 repositories
* 20 controllers
* multiple implementations of interfaces
* configuration requirements
* objects that depend on other objects

You can end up with a huge amount of code responsible for **creating and connecting objects**.

Spring's fundamental idea is:

> **Let the framework take responsibility for creating and connecting many of these objects.**

We'll study exactly how it does that in later sessions. For today, just understand the problem.

***

# 2. Why was Spring created?

Spring appeared in the early 2000s, during a time when Java enterprise development was often heavily dependent on complicated enterprise technologies and configuration.

A major problem was that developers could end up writing applications where business logic was tightly coupled to infrastructure.

For example, imagine:

```text
UserService
    ↓
Database code
    ↓
Transaction management
    ↓
Application server
```

The business code could become mixed with infrastructure concerns.

Spring's philosophy was essentially:

> **Make Java application development simpler and reduce unnecessary coupling.**

Two ideas became particularly important:

### 1. Dependency Injection

Instead of your class creating everything it needs:

```java
UserService → creates → UserRepository
```

Spring can provide the dependency:

```text
Spring
  ↓
creates UserRepository
  ↓
gives it to UserService
```

### 2. Inversion of Control

Normally, your code controls object creation:

```text
Your application
      ↓
creates objects
      ↓
connects objects
```

With Spring:

```text
Spring
  ↓
creates objects
  ↓
connects objects
  ↓
your application uses them
```

You don't need to master these terms yet. Just recognize them because they are central to Spring.

***

# 3. What problems does Spring solve?

Let's make this practical.

Imagine you're building your **LandLord** application.

You might eventually have:

```text
TenantController
TenantService
TenantRepository
PaymentService
PaymentRepository
PropertyService
PropertyRepository
...
```

And these classes depend on one another.

Without some framework managing the application:

```text
Controller
   ↓ creates
Service
   ↓ creates
Repository
   ↓ creates
Database connection
```

Your application code becomes responsible for a lot of object creation and configuration.

Spring helps separate these responsibilities.

Conceptually:

```text
                 Spring
                   │
       ┌───────────┼───────────┐
       ↓           ↓           ↓
 Controller     Service    Repository
       │           │           │
       └───────────┴───────────┘
```

Spring manages the objects and their relationships.

This gives you several benefits:

### Less coupling

A class doesn't necessarily need to know how its dependencies are created.

### Easier testing

You can replace real dependencies with test versions.

### Better organization

Different responsibilities can be separated into different components.

### Easier configuration

Spring provides mechanisms for configuring application behavior.

### Less boilerplate

Spring can handle many repetitive infrastructure tasks.

***

# 4. A small practical example

Let's see the basic problem Spring is trying to solve.

Suppose we have:

```java
class EmailService {

    public void sendEmail() {
        System.out.println("Email sent");
    }
}
```

And:

```java
class UserService {

    private EmailService emailService;

    public UserService() {
        emailService = new EmailService();
    }

    public void register() {
        System.out.println("User registered");
        emailService.sendEmail();
    }
}
```

The relationship is:

```text
UserService
     │
     └── creates
            ↓
      EmailService
```

The `UserService` is responsible for creating `EmailService`.

Now imagine we later want:

```java
class SmsService {
    public void sendSms() {
        System.out.println("SMS sent");
    }
}
```

Or we want different implementations of an interface.

The application can become increasingly coupled to concrete classes.

Spring's approach is closer to:

```text
             Spring
               │
       ┌───────┴────────┐
       ↓                ↓
UserService       EmailService
       │                ↑
       └────────────────┘
          dependency
```

The framework handles the construction and wiring.

**That's one of the most important ideas behind Spring.**

***

# 5. Spring Framework vs Spring Boot

This distinction is extremely important.

You will hear these names constantly:

* Spring Framework
* Spring Boot

They are **not the same thing**.

## Spring Framework

Spring Framework is the underlying framework/ecosystem that provides things such as:

* dependency injection
* object management
* configuration
* web application support
* database-related support
* transaction support
* and many other capabilities

Think:

> **Spring Framework = the foundation/toolkit.**

***

## Spring Boot

Spring Boot was created to make developing Spring applications **much easier and faster**.

Without Spring Boot, setting up a Spring application could involve a significant amount of configuration.

Spring Boot provides conventions, automatic configuration, embedded servers, and other conveniences that make starting a Spring application much simpler.

Think:

> **Spring Boot = an easier way to build and run applications using Spring.**

A useful analogy:

```text
Spring Framework
      ↓
Foundation / capabilities

Spring Boot
      ↓
Makes using Spring much easier
```

### Important misconception

Don't think:

> "Spring and Spring Boot are two completely unrelated frameworks."

Instead:

> **Spring Boot builds on top of the Spring ecosystem and simplifies application development.**

***

# 6. Your JSP/Tomcat experience makes this easier to understand

You've already worked with JSP and Tomcat.

A traditional Java web application might look roughly like:

```text
Browser
   ↓ HTTP
Tomcat
   ↓
Servlet/JSP
   ↓
Java code
   ↓
JDBC
   ↓
PostgreSQL
```

Spring can sit in the application architecture and provide a structured way to build the Java application.

With Spring Boot, a typical web application eventually looks more like:

```text
Browser / Angular
        ↓
       HTTP
        ↓
Spring Boot application
        ↓
   Controller
        ↓
     Service
        ↓
   Repository
        ↓
   PostgreSQL
```

Don't worry about Controller, Service, Repository yet. We're going to study those concepts later.

For this lesson, notice the important point:

**Spring Boot doesn't replace Java.**

It is a framework for building Java applications.

And it doesn't replace PostgreSQL either.

It helps your Java application interact with things such as databases, HTTP requests, configuration, and other infrastructure.

***

# 7. High-level Spring architecture

At a high level, think of Spring as a collection of modules/capabilities rather than one giant piece of code.

A simplified picture:

```text
                 Spring Framework
                       │
       ┌───────────────┼────────────────┐
       │               │                │
       ↓               ↓                ↓
 Dependency       Web/Application    Data/Transactions
 Injection           support             support
       │               │                │
       └───────────────┼────────────────┘
                       ↓
                 Your Java App
```

One of the most important foundations is the **Spring IoC Container**.

You don't need to study its internals today.

Just understand:

> The Spring container is responsible for managing objects that Spring knows about.

Those managed objects are commonly called **beans**.

So when you eventually hear:

> "Spring creates and manages a bean."

you should think:

```text
Spring Container
      ↓
creates object
      ↓
manages object
      ↓
provides it where needed
```

That's enough for today's lesson.

***

# 8. Why did Spring become important?

Spring became important because it provided a way to build Java applications that were:

* less tightly coupled
* easier to configure
* easier to test
* more modular
* easier to maintain
* less dependent on complicated infrastructure code

And importantly, Spring became an extremely large ecosystem.

You can think of the evolution roughly like:

```text
Traditional Java
       ↓
Spring Framework
       ↓
Spring Boot
       ↓
Modern Java backend development
```

Today, when people say:

> "I'm a Spring developer"

they often mean they're building Java backend applications using **Spring Boot and the Spring ecosystem**.

***

# 9. Practical exercise — identify the problem

Look at this code:

```java
class PaymentRepository {

    public void savePayment() {
        System.out.println("Payment saved");
    }
}
```

```java
class PaymentService {

    private PaymentRepository repository;

    public PaymentService() {
        repository = new PaymentRepository();
    }

    public void makePayment() {
        System.out.println("Making payment...");
        repository.savePayment();
    }
}
```

Answer these three questions:

### Question 1

Who creates the `PaymentRepository` object?

### Question 2

What is `PaymentService` tightly coupled to?

### Question 3

In very simple terms, how could Spring help here?

Don't worry about giving a technically perfect answer. I want to see whether you've understood the **problem Spring is designed to solve**.

***

# 10. The mental model to keep

For this session, remember this:

```text
Java
 ↓
You create and connect objects yourself

Spring
 ↓
Framework helps create and manage objects
and their relationships

Spring Boot
 ↓
Makes building Spring applications much easier
```

And the one-sentence answer to:

> **What is Spring, and why would a Java developer use it?**

is:

> **Spring is a Java framework that helps developers build maintainable applications by managing objects, their dependencies, configuration, and common application infrastructure, reducing the amount of code and coupling developers have to manage themselves.**

You **do not** need to memorize that sentence. Understand the idea.

***

## Checkpoint

Before moving to the next lesson, you should be able to answer these without looking back:

1. What problem was Spring created to address?
2. What does Spring do with application objects?
3. What is dependency injection at a very high level?
4. What is the difference between Spring Framework and Spring Boot?
5. Does Spring Boot replace Java?
6. Why is reducing coupling useful?
7. If `UserService` creates `UserRepository` with `new`, what responsibility does `UserService` have that Spring could take over?

**Your turn:** answer the 3 practical questions and the 7 checkpoint questions. I'll evaluate your answers before we continue.
