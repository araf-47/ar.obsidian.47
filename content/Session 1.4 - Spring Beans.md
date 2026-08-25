# Session 1.4 — Spring Beans

This session connects what you learned in **IoC (1.2)** and **Dependency Injection (1.3)**.

The main idea is:

> **A Spring Bean is an object that Spring creates and manages for you.**

***

## 1. What is a Bean?

Let's start with normal Java.

```java
Service service = new Service();
```

You created an object of `Service`.

Now suppose Spring creates that object instead:

```text
Spring
   ↓
creates
   ↓
Service object
```

==That Spring-managed object is called== a **Bean**.

So:

```text
Java object
    +
created/managed by Spring
    ↓
Spring Bean
```

### Very important distinction

Not every Java object is a Spring Bean.

For example:

```java
Service service = new Service();
```

This is a normal Java object.

But if Spring creates and manages the `Service` object:

```text
Spring Container
       ↓
   Service object
       ↓
      Bean
```

then it is a **Spring Bean**.

### Small example

```java
public class EmailService {

    public void sendEmail() {
        System.out.println("Email sent");
    }
}
```

If you do:

```java
EmailService service = new EmailService();
```

you have an ordinary Java object.

If Spring creates the `EmailService` and manages it, it becomes a **Bean**.

***

# 2. Who creates Beans?

**The Spring Container creates Beans.**

Remember our previous IoC lesson.

Without Spring:

```text
Your code
   ↓
new Service()
   ↓
Service object
```

With Spring:

```text
Spring Container
       ↓
creates Service
       ↓
Service Bean
```

This is one of the important consequences of **IoC**.

You are no longer responsible for creating certain application objects yourself.

***

# 3. Who manages Beans?

The **Spring Container** manages them.

Think of the Spring Container as an object manager.

It can:

* create Beans
* keep track of Beans
* provide Beans when needed
* manage their lifecycle

For this lesson, you don't need to memorize every internal detail.

Just remember:

> **Spring Container = the place where Spring creates and manages your Beans.**

***

# 4. Spring Container and Beans

Let's connect everything.

Suppose your application has:

```text
Controller
Service
Repository
```

Spring can manage these as Beans.

Conceptually:

```text
Spring Container
      │
      ├── Controller Bean
      ├── Service Bean
      └── Repository Bean
```

These aren't three completely separate Spring systems.

They are objects being managed by the **same Spring Container**.

This is why the container is so important.

***

# 5. What is `ApplicationContext`?

Now we need to introduce one important Spring term.

`ApplicationContext` is a major interface used to represent the **Spring Container**.

You can think of it like this:

```text
ApplicationContext
       ↓
Spring Container
       ↓
contains/manages Beans
```

For our level of understanding, you can treat:

> **ApplicationContext = an interface through which we interact with the Spring Container.**

For example, we can ask it:

> "Give me the Bean of this type."

Like this:

```java
ApplicationContext context = ...;

EmailService service =
        context.getBean(EmailService.class);
```

Then:

```text
ApplicationContext
       ↓
Spring Container
       ↓
find EmailService Bean
       ↓
return it
```

Notice something important.

We didn't write:

```java
new EmailService();
```

Spring already created the object.

We're asking the container for the object.

***

# 6. Let's build a tiny example

Let's create a very small Spring Boot application.

Suppose we have:

```text
EmailService
```

and we want Spring to create it as a Bean.

### Step 1 — Create the service

```java
import org.springframework.stereotype.Service;

@Service
public class EmailService {

    public void sendEmail() {
        System.out.println("Email sent!");
    }
}
```

The important part for this lesson is:

```java
@Service
```

This tells Spring that this class should be discovered and managed as a Bean.

Conceptually:

```text
@Service
     ↓
Spring discovers EmailService
     ↓
Spring creates EmailService object
     ↓
EmailService becomes a Bean
```

We're not going deeply into annotations yet. For now, just understand the result.

***

# 7. Getting the Bean through `ApplicationContext`

Now let's use the Spring container directly.

For example:

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {

        ApplicationContext context =
                SpringApplication.run(MyApplication.class, args);

        EmailService service =
                context.getBean(EmailService.class);

        service.sendEmail();
    }
}
```

Let's slow down and understand this.

### This line:

```java
ApplicationContext context =
        SpringApplication.run(MyApplication.class, args);
```

starts the Spring application.

As part of starting the application, Spring creates its container.

We get access to that container through `ApplicationContext`.

***

### Then:

```java
EmailService service =
        context.getBean(EmailService.class);
```

We're saying:

> "Spring, give me the `EmailService` Bean."

Spring returns the Bean.

Then:

```java
service.sendEmail();
```

uses that Bean.

***

# 8. Compare this with normal Java

### Traditional Java

```java
EmailService service = new EmailService();

service.sendEmail();
```

You create the object.

### Spring

```java
EmailService service =
        context.getBean(EmailService.class);

service.sendEmail();
```

Spring created the object.

You retrieve it from the container.

That's the key difference.

***

# 9. A useful mental picture

Think of the Spring Container as a **warehouse of managed objects**.

```text
              Spring Container
        ┌─────────────────────────┐
        │                         │
        │  EmailService Bean      │
        │  UserService Bean       │
        │  ProductService Bean    │
        │  Controller Bean        │
        │                         │
        └─────────────────────────┘
                    ↑
                    │
             ApplicationContext
                    ↑
                    │
               Your code
```

Your code can interact with the container through `ApplicationContext`.

***

# 10. Basic Bean Lifecycle

Your syllabus says **basic understanding**, so we will keep this simple.

A Bean generally goes through a lifecycle like this:[^1]

```text
Spring starts
     ↓
Bean is created
     ↓
Bean is initialized
     ↓
Bean is used
     ↓
Spring shuts down
     ↓
Bean is destroyed
```

So conceptually:

```text
Create
  ↓
Initialize
  ↓
Use
  ↓
Destroy
```

You do **not** need to study advanced lifecycle hooks right now.

The important idea is:

> Spring controls the lifecycle of the Beans it manages.

***

# 11. Putting Sessions 1.2, 1.3 and 1.4 together

This is the important connection.

### Session 1.2 — IoC

Instead of your code controlling object creation:

```text
Your code
   ↓
new Service()
```

Spring takes control:

```text
Spring
   ↓
creates Service
```

That's **Inversion of Control**.

***

### Session 1.3 — Dependency Injection

Suppose:

```text
Controller
    ↓
needs
    ↓
Service
```

Instead of:

```java
public Controller() {
    service = new Service();
}
```

Spring can provide the Service to the Controller.

That's **Dependency Injection**.

***

### Session 1.4 — Beans

What is that Service object Spring created and manages?

**A Bean.**

So:

```text
Spring Container
       │
       │ creates/manages
       ↓
   Service Bean
       │
       │ injected into
       ↓
 Controller Bean
```

This is the big picture you should have in your head.

***

# 12. Practical Exercise

Now do this yourself.

Create a simple Spring Boot application with a class:

```java
GreetingService
```

It should have:

```java
public void greet() {
    System.out.println("Hello from Spring!");
}
```

Make Spring manage it as a Bean.

Then, in your application's `main()` method:

1. Start the Spring application.
2. Obtain the `ApplicationContext`.
3. Use `context.getBean(...)` to retrieve the `GreetingService`.
4. Call `greet()`.

Your target flow is:

```text
SpringApplication.run()
        ↓
ApplicationContext
        ↓
getBean(GreetingService.class)
        ↓
GreetingService Bean
        ↓
greet()
        ↓
Hello from Spring!
```

### Don't do this:

```java
GreetingService service = new GreetingService();
```

The point of this exercise is to practice getting the object **from Spring**.

***

# 13. One terminology trap to avoid

Don't think:

> "Bean is a special kind of Java class."

It isn't.

A Bean is essentially a **Java object that is managed by Spring**.

For example, the class:

```java
public class GreetingService {
}
```

is just a Java class.

An instance:

```java
GreetingService service = new GreetingService();
```

is a normal Java object.

When Spring creates and manages an instance of that class:

```text
GreetingService object
        +
Spring management
        ↓
Spring Bean
```

That's the important distinction.

***

# Checkpoint 🧠

Before moving on, answer these **without looking back**:

### 1.

What is a Spring Bean?

### 2.

Who creates and manages Spring Beans?

### 3.

What is the relationship between `ApplicationContext` and the Spring Container?

### 4.

What's the difference between these two?

```java
GreetingService service = new GreetingService();
```

and

```java
GreetingService service =
        context.getBean(GreetingService.class);
```

### 5.

Complete this diagram:

```text
Spring Container
       ↓
       ?
       ↓
       ?
```

Hint: Think about what happens to a Bean from creation until the application shuts down.

Once you can answer those five and complete the practical exercise, **Session 1.4 is understood at the level needed for this crash course.**
***
# Footnotes
[^1]: [[what is initialization (in programming)]].
