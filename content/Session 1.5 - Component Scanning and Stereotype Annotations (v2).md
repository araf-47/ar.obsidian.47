Absolutely. The key correction is: **I will not assume you understand Controller, Service, Repository, or application architecture.** We will first build the concept from ordinary Java, then introduce the three annotations.

# Session 1.5 — Component Scanning and Stereotype Annotations

## What you should understand by the end

You should be able to explain:

```text
@Component
@Service
@Repository
```

and answer:

* What does each annotation mean?
* Why can Spring manage these classes as Beans?
* What is component scanning?
* Why does Spring have different stereotype annotations?
* What is the practical difference between a general component, a service, and a repository?

We will **not** study application architecture in this session.

***

# Part 1 — Start with what you already know: Java classes and objects

Let's forget Spring for a moment.

Suppose we have:

```java
public class EmailSender {

    public void send() {
        System.out.println("Sending email");
    }
}
```

This is simply a Java class.

If we want an object of this class:

```java
EmailSender emailSender = new EmailSender();
```

We manually created the object.

So:

```text
EmailSender
    ↓
new EmailSender()
    ↓
EmailSender object
```

This is ordinary Java.

***

# Part 2 — What changes when Spring is involved?

Spring can create and manage objects for us.

Suppose we write:

```java
@Component
public class EmailSender {

    public void send() {
        System.out.println("Sending email");
    }
}
```

Now `@Component` is giving Spring information about this class.

It is essentially saying:

> **"Spring, this class is a component that you should discover and manage."**

So Spring can discover `EmailSender`, create an object from it, and manage that object.

That object is called a **Bean**.

So:

```text
@Component
      ↓
Spring discovers the class
      ↓
Spring creates an object
      ↓
That object is a Spring Bean
```

This is the most important idea in this lesson.

***

# Part 3 — What is Component Scanning?

Now an obvious question:

> How does Spring find my `@Component` classes?

This is where **component scanning** comes in.

Imagine your project contains:

```text
MyApplication
EmailSender
FileProcessor
ReportGenerator
```

and three of those classes have:

```java
@Component
```

When the Spring application starts, Spring scans the appropriate packages looking for classes marked as components.

Conceptually:

```text
Spring starts
     ↓
Component scanning
     ↓
Finds @Component classes
     ↓
Creates objects
     ↓
Registers them as Beans
```

For example:

```java
@Component
public class EmailSender {
}
```

Spring finds it.

Then:

```text
EmailSender class
       ↓
Spring creates
       ↓
EmailSender object
       ↓
Spring manages it as a Bean
```

***

# Part 4 — What does "Spring manages the Bean" mean?

This phrase appears everywhere in Spring, so let's make it concrete.

Suppose:

```java
@Component
public class EmailSender {
}
```

Spring creates an object:

```text
EmailSender object
```

and keeps track of it inside the Spring Container.

So conceptually:

```text
Spring Container
       │
       └── EmailSender Bean
```

Instead of your application being completely responsible for creating and managing that object, Spring is responsible for it.

You have already seen the idea of the **Spring Container** in the previous sessions.

For this lesson, just remember:

> **The Spring Container stores and manages Spring Beans.**

***

# Part 5 — Then why do we have `@Service` and `@Repository`?

Now we can finally answer the question that caused the confusion.

Spring has:

```java
@Component
@Service
@Repository
```

At a basic level, all three are **stereotype annotations**.

A stereotype annotation communicates:

> **"This class has a particular role in the application."**

Think of them as labels.

For example:

```java
@Component
public class EmailSender {
}
```

The label says:

> General Spring component.

While:

```java
@Service
public class UserService {
}
```

the label says:

> This class is intended to represent service/business logic.

And:

```java
@Repository
public class UserRepository {
}
```

the label says:

> This class is intended to deal with data access.

***

# Part 6 — `@Component`

Let's start with the most general one.

```java
@Component
public class EmailSender {
}
```

`@Component` means:

> **"Spring should discover and manage this class as a component."**

Example:

```java
@Component
public class EmailSender {

    public void send() {
        System.out.println("Sending email");
    }
}
```

Spring can discover this class during component scanning.

Then Spring creates and manages an object from it.

That object becomes a Bean.

### Mental model

```text
@Component
     ↓
Component scanning finds class
     ↓
Spring creates object
     ↓
Spring manages object
     ↓
Bean
```

***

# Part 7 — `@Service`

Now imagine a class whose job is to perform some kind of **application/business operation**.

For example:

```java
@Service
public class UserService {

    public void registerUser() {
        System.out.println("Registering user");
    }
}
```

`@Service` tells Spring:

> **"This class is a service component."**

And because it is a Spring stereotype annotation, Spring can discover it during component scanning and manage it as a Bean.

So:

```text
@Service
     ↓
Spring discovers it
     ↓
Spring creates object
     ↓
Spring manages object as Bean
```

The important difference from `@Component` is the **meaning/role**.

```java
@Component
```

means:

> General component.

```java
@Service
```

means:

> Service/business-logic component.

***

# Part 8 — What does "business logic" mean?

You don't need a deep understanding of application architecture to understand this phrase.

Imagine a library program.

You might have an operation:

```text
Borrow a book
```

There could be rules such as:

```text
Is the book available?
Does the member have permission?
Can this member borrow another book?
```

Those rules are **business logic**.

A service class is commonly used to contain this kind of application logic.

For example:

```java
@Service
public class LibraryService {

    public void borrowBook() {
        // application rules
    }
}
```

You don't need to learn how a complete library application is architected yet.

Just remember:

> **Service = a class used for application/business logic.**

***

# Part 9 — `@Repository`

Now consider a class whose job is working with stored data.

For example:

```java
@Repository
public class UserRepository {

    public void saveUser() {
        System.out.println("Saving user");
    }
}
```

`@Repository` communicates:

> **"This class is responsible for data-access work."**

For example, a repository might eventually contain operations such as:

```text
save user
find user
delete user
update user
```

and those operations might ultimately interact with a database.

Since you already know JDBC and PostgreSQL, you can think of this as the part of an application that would eventually perform database-related operations.

But **we are not studying Spring database access here.**

Just understand the role:

```text
@Repository
     ↓
Data-access component
```

***

# Part 10 — Compare the three

Now we can compare them without assuming you know application architecture.

| Annotation    | What it communicates             |
| ------------- | -------------------------------- |
| `@Component`  | General Spring-managed component |
| `@Service`    | Service/business-logic component |
| `@Repository` | Data-access component            |

And all three can be discovered by Spring's component scanning and become Spring-managed Beans.

So:

```text
@Component
@Service
@Repository
      ↓
Spring can discover them
      ↓
Spring can create objects from them
      ↓
Spring manages those objects as Beans
```

The major difference we're concerned with here is **the role the annotation communicates**.

***

# Part 11 — Why not just use `@Component` everywhere?

This is a very good question.

Technically, you might wonder:

> If `@Component` can tell Spring to manage the class, why not just write `@Component` on everything?

For example:

```java
@Component
public class UserService {
}
```

instead of:

```java
@Service
public class UserService {
}
```

The more specific annotation communicates useful information to humans reading the code.

Compare:

```java
@Component
public class UserService {
}
```

with:

```java
@Service
public class UserService {
}
```

The second one immediately communicates:

> "This class is a service."

Likewise:

```java
@Repository
public class UserRepository {
}
```

communicates:

> "This class handles data access."

So these annotations aren't just about telling Spring what to do.

They also make the **intention of the class clearer**.

***

# Part 12 — One important relationship

For this lesson, you can think of:

```text
@Component
```

as the general stereotype.

And:

```text
@Service
@Repository
```

as more specific stereotypes used for particular roles.

You may encounter explanations saying that `@Service` and `@Repository` are specialized forms of `@Component`.

That's a useful mental model at your current level:

```text
                 @Component
                /          \
               /            \
          @Service       @Repository
```

Don't worry about the exact internal implementation of these annotations yet.

***

# Part 13 — Practical Exercise

Now let's actually create three classes.

**Do not worry about connecting them together.**

That would introduce concepts we're not studying yet.

Create:

### Class 1

```java
@Component
public class EmailSender {

    public void send() {
        System.out.println("Email sent");
    }
}
```

### Class 2

```java
@Service
public class UserService {

    public void register() {
        System.out.println("User registered");
    }
}
```

### Class 3

```java
@Repository
public class UserRepository {

    public void save() {
        System.out.println("User saved");
    }
}
```

Now your application has three different Spring components:

```text
EmailSender
UserService
UserRepository
```

with three different roles:

```text
EmailSender
    → general component

UserService
    → service/business logic

UserRepository
    → data access
```

***

# Part 14 — Observe the Beans

Now we want to verify that Spring actually discovered them.

Inside your application, you can obtain the Spring `ApplicationContext`.

For example:

```java
ApplicationContext context =
        SpringApplication.run(MyApplication.class, args);
```

Then:

```java
EmailSender emailSender =
        context.getBean(EmailSender.class);
```

And:

```java
UserService userService =
        context.getBean(UserService.class);
```

And:

```java
UserRepository userRepository =
        context.getBean(UserRepository.class);
```

Then:

```java
emailSender.send();
userService.register();
userRepository.save();
```

You should get output such as:

```text
Email sent
User registered
User saved
```

The important thing is **where those objects came from**.

You did **not** write:

```java
new EmailSender();
```

or:

```java
new UserService();
```

or:

```java
new UserRepository();
```

Instead:

```java
context.getBean(...)
```

asks Spring for the objects it is managing.

***

# Part 15 — What actually happened?

Let's slow this down.

You wrote:

```java
@Component
public class EmailSender {
}
```

When Spring starts:

```text
Spring starts
      ↓
Component scanning
      ↓
Finds EmailSender
      ↓
Spring creates EmailSender object
      ↓
Spring manages that object
      ↓
EmailSender becomes a Bean
```

Same idea:

```java
@Service
public class UserService {
}
```

becomes:

```text
Spring scans
     ↓
Finds UserService
     ↓
Creates UserService object
     ↓
Manages it as a Bean
```

And:

```java
@Repository
public class UserRepository {
}
```

becomes:

```text
Spring scans
     ↓
Finds UserRepository
     ↓
Creates UserRepository object
     ↓
Manages it as a Bean
```

***

# Part 16 — Don't confuse these two concepts

There's one distinction I particularly want you to understand.

### Component scanning

Means:

> **How does Spring find classes that it should manage?**

```text
@Component
@Service
@Repository
        ↓
Component scanning
        ↓
Spring discovers them
```

### Dependency Injection

Means:

> **How does Spring provide one object's dependency to another object?**

That's a separate concept.

For example, eventually you might have:

```text
Class A
   ↓
needs
   ↓
Class B
```

Spring can provide Class B to Class A.

**That is Dependency Injection.**

We already studied DI in Session 1.3, but we're not combining it with today's exercise because the goal here is specifically to understand **component scanning and stereotype annotations**.

***

# The complete mental model

At this point, I want you to be able to look at:

```java
@Component
public class EmailSender {
}
```

and think:

```text
This is a Java class
        ↓
@Component tells Spring:
"treat this as a component"
        ↓
Spring's component scanning finds it
        ↓
Spring creates an object
        ↓
Spring manages that object
        ↓
The object is a Bean
```

And:

```java
@Service
public class UserService {
}
```

means:

```text
This is a service/business-logic component
        ↓
Spring discovers it
        ↓
Spring manages its object as a Bean
```

And:

```java
@Repository
public class UserRepository {
}
```

means:

```text
This is a data-access component
        ↓
Spring discovers it
        ↓
Spring manages its object as a Bean
```

***

# Checkpoint

Don't look back while answering these.

### 1. In ordinary Java, what does this do?

```java
EmailSender sender = new EmailSender();
```

### 2. What is the purpose of:

```java
@Component
```

### 3. What is **component scanning**?

Explain it in your own words.

### 4. If Spring finds this:

```java
@Service
public class UserService {
}
```

what does Spring do with it?

### 5. What is the difference between these?

```java
@Component
@Service
@Repository
```

### 6. Why would we use `@Service` instead of simply using `@Component` on a service class?

### 7. What does `@Repository` communicate about a class?

### 8. What is the difference between:

```text
Component scanning
```

and

```text
Dependency Injection
```

If you can answer these comfortably, **Session 1.5 is complete**.
