# Session 1.5 — Component Scanning and Stereotype Annotations

This session connects several things you've already learned:

```text
@Component
@Service
@Repository
       ↓
Spring discovers them
       ↓
Spring creates Objects (Beans)
       ↓
Spring manages those Beans
```

The important thing is to understand **why Spring can find your classes without you writing `new` yourself**.

***

## 1. First: What is a component?

Suppose you have a normal Java class:

```java
public class EmailService {

    public void sendEmail() {
        System.out.println("Sending email...");
    }
}
```

In ordinary Java, if you want an object:

```java
EmailService service = new EmailService();
```

You created the object.

But in Spring, you can tell Spring:

> "This class is something that Spring should manage."

You do that using an annotation:

```java
@Component
public class EmailService {

    public void sendEmail() {
        System.out.println("Sending email...");
    }
}
```

Now Spring can discover this class and create an object from it.

That object becomes a **Spring-managed Bean**.

So:

```java
@Component
public class EmailService {
}
```

roughly results in:

```text
Spring Container
      │
      └── EmailService Bean
```

You don't have to manually do:

```java
new EmailService()
```

for the Spring-managed object.

***

# 2. What does `@Component` actually mean?

`@Component` basically tells Spring:

> **"This class is a component that Spring should discover and manage."**

Example:

```java
@Component
public class EmailService {

    public void sendEmail() {
        System.out.println("Email sent");
    }
}
```

Spring sees `@Component` and says:

```text
Oh, EmailService is a component.

I'll create an EmailService object
and manage it as a Bean.
```

So:

```java
@Component
public class EmailService
```

does **not** mean:

> "Create an object immediately when Java reads this line."

It means:

> "When Spring's application context starts and scans this class, treat it as something that Spring should manage."

That's an important distinction.

***

# 3. What is Component Scanning?

This is the other major concept in this session.

You might be wondering:

> How does Spring even find my `@Component` classes?

Spring performs **component scanning**.

Imagine your project contains:

```text
com.example.app
│
├── controller
│     └── UserController.java
│
├── service
│     └── UserService.java
│
└── repository
      └── UserRepository.java
```

And your classes have:

```java
@Component
public class UserService {
}
```

Spring scans the appropriate packages looking for classes marked with Spring's component annotations.

It finds:

```text
UserService
```

and effectively says:

```text
I found a component.
I'll create and manage a Bean for it.
```

So the basic process is:

```text
Application starts
       ↓
Spring performs component scanning
       ↓
Spring finds @Component / @Service / @Repository
       ↓
Spring creates objects
       ↓
Those objects become Spring Beans
```

***

# 4. Why three annotations?

Now we get to:

```java
@Component
@Service
@Repository
```

You might ask:

> If all of them create Spring-managed Beans, why do we need three?

Because they communicate **different roles**.

Think about your application architecture:

```text
Controller
     ↓
Service
     ↓
Repository
     ↓
Database
```

Each layer has a different responsibility.

***

# 5. `@Component`

`@Component` is the **general-purpose** stereotype.

Example:

```java
@Component
public class EmailService {
}
```

It tells Spring:

> "This is a Spring-managed component."

You use it when the class doesn't have a more specific stereotype.

For example:

```java
@Component
public class FileProcessor {
}
```

***

# 6. `@Service`

Now suppose the class represents business logic:

```java
@Service
public class UserService {

    public void registerUser() {
        System.out.println("Registering user...");
    }
}
```

`@Service` tells both Spring and other developers:

> "This class represents a service/business-logic component."

And importantly:

**`@Service` is also discovered by component scanning and becomes a Spring Bean.**

Conceptually:

```text
@Service
    ↓
Spring discovers it
    ↓
Spring creates Bean
```

So you can think:

```java
@Service
public class UserService
```

as a more specific form of:

```java
@Component
public class UserService
```

For now, don't worry about the internal implementation details. The important thing is the role.

***

# 7. `@Repository`

Now imagine the database-access layer:

```java
@Repository
public class UserRepository {

    public void saveUser() {
        System.out.println("Saving user...");
    }
}
```

`@Repository` tells us:

> "This class is responsible for data-access/repository work."

And again, Spring discovers it and manages it as a Bean.

So:

```text
@Repository
UserRepository
      ↓
Spring discovers it
      ↓
Spring-managed Bean
```

***

# 8. Compare the three

This is the part I want you to remember.

| Annotation    | Role                     |
| ------------- | ------------------------ |
| `@Component`  | General Spring component |
| `@Service`    | Business/service logic   |
| `@Repository` | Data/database access     |

All three can result in **Spring-managed Beans**.

Think:

```text
@Component
   │
   ├── general component
   │
   ├── @Service
   │      └── business logic
   │
   └── @Repository
          └── data access
```

For your Spring Boot applications, you'll commonly see:

```text
Controller
   ↓
@Service
   ↓
@Repository
```

***

# 9. Where does Controller fit?

You may notice something interesting.

We're studying:

```java
@Component
@Service
@Repository
```

but our practical application contains:

```text
Controller
Service
Repository
```

A Controller is also normally a Spring-managed component, but it uses another stereotype annotation:

```java
@Controller
```

or, for REST APIs, commonly:

```java
@RestController
```

We're **not going to study those annotations in this session**, because they belong to later Spring/Spring Boot topics.

For now, just understand:

```text
Controller
Service
Repository
```

are different application roles, and Spring can discover and manage these components.

***

# 10. A complete small example

Let's build the architecture.

### Repository

```java
@Repository
public class UserRepository {

    public void save() {
        System.out.println("User saved");
    }
}
```

### Service

```java
@Service
public class UserService {

    public void register() {
        System.out.println("Registering user...");
    }
}
```

### Controller

For the moment, imagine:

```java
@Controller
public class UserController {
}
```

The structure is:

```text
UserController
      ↓
UserService
      ↓
UserRepository
```

Spring scans the application and discovers these classes.

Conceptually:

```text
Spring Container

├── UserController Bean
├── UserService Bean
└── UserRepository Bean
```

Notice something important:

**The classes are not Beans themselves.**

The **objects created from those classes** are the Beans.

For example:

```java
@Service
public class UserService {
}
```

is a class.

Spring can create:

```text
UserService object
```

and that object is managed by Spring as a Bean.

***

# 11. Component scanning is NOT the same as dependency injection

This distinction is very important because you're going to study DI separately.

### Component scanning

Answers:

> **"Which classes should Spring manage?"**

For example:

```java
@Service
public class UserService {
}
```

Spring discovers it.

### Dependency Injection

Answers:

> **"How does one Spring-managed object receive another Spring-managed object?"**

For example, conceptually:

```text
Controller
    ↓
needs
    ↓
Service
```

Spring can provide the Service object to the Controller.

That's DI.

So:

```text
Component scanning
        ↓
Find and register components

Dependency Injection
        ↓
Connect/manage their dependencies
```

Don't mix these two concepts.

***

# 12. Practical Exercise

Let's make a tiny Spring Boot application.

You should have:

```text
Controller
   ↓
Service
   ↓
Repository
```

### Step 1 — Repository

Create:

```java
@Repository
public class UserRepository {

    public void save() {
        System.out.println("User saved to database");
    }
}
```

### Step 2 — Service

Create:

```java
@Service
public class UserService {

    public void registerUser() {
        System.out.println("Registering user");
    }
}
```

### Step 3 — Controller

Create:

```java
@Controller
public class UserController {
}
```

At this point, don't worry about connecting them together yet.

That's dependency injection territory.

The purpose of **this exercise** is simply to observe that Spring discovers the classes.

***

# 13. Actually observe the Beans

You can use the `ApplicationContext` to ask Spring for a Bean.

For example:

```java
ApplicationContext context =
        SpringApplication.run(MyApplication.class, args);

UserService service =
        context.getBean(UserService.class);
```

Then:

```java
service.registerUser();
```

You should see:

```text
Registering user
```

The important part is:

```java
context.getBean(UserService.class);
```

You didn't do:

```java
new UserService();
```

Instead, you're asking Spring:

> "Give me the UserService Bean that you're managing."

Spring already discovered the class through component scanning and created the managed object.

***

# 14. The whole picture

This is the mental model I want you to have after this lesson:

```text
             Spring Application
                    │
                    ↓
          Component Scanning
                    │
          ┌─────────┼─────────┐
          ↓         ↓         ↓
     Controller   Service   Repository
          │         │         │
          └─────────┼─────────┘
                    ↓
             Spring creates
              and manages
                  Beans
```

And the annotations communicate the roles:

```java
@Component   → general component

@Service     → business/service layer

@Repository  → data-access layer
```

***

## One very important correction to keep in your head

Don't think:

> "`@Service` magically creates an object."

A better mental model is:

> "`@Service` marks a class as a component that Spring's component scanning can discover; Spring then creates and manages an object from that class as a Bean."

That distinction will make Spring much easier to understand.

***

# Checkpoint

Try answering these **without looking back**:

### 1.

What does this tell Spring?

```java
@Service
public class PaymentService {
}
```

### 2.

What is component scanning?

### 3.

What's the difference between:

```java
@Component
@Service
@Repository
```

### 4.

True or false:

> `@Service` and `@Repository` can result in Spring-managed Beans.

### 5.

Suppose you have:

```text
UserController
UserService
UserRepository
```

Which role would you normally associate with each?

### 6.

What's the difference between **component scanning** and **dependency injection**?

If you can answer those six in your own words, **Session 1.5 is understood well enough to move on.**
