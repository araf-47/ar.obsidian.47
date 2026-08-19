# Session 1.3 — Dependency Injection

This session is very important because **Dependency Injection (DI) is one of the core ideas behind how Spring works**.

We'll build the idea from plain Java first, then let Spring do the work.

***

# 1. What is a Dependency?

Let's start with something you already know from Java.

Suppose we have:

```java
class Service {
    public void doSomething() {
        System.out.println("Doing something...");
    }
}
```

And another class:

```java
class Controller {

    private Service service;

    public Controller() {
        service = new Service();
    }
}
```

Here, `Controller` **needs** a `Service` object to do its job.

We say:

> `Service` is a **dependency** of `Controller`.

Why?

Because `Controller` depends on `Service`.

Think of it like this:

```text
Controller
    |
    | needs
    ↓
 Service
```

The important part is not the word "dependency."

The important idea is:

> **One object needs another object to perform its work.**

### A more realistic example

Imagine your application has:

```text
UserController
       ↓
UserService
       ↓
UserRepository
```

`UserController` needs `UserService`.

Therefore:

```text
UserService = dependency of UserController
```

And `UserRepository` is a dependency of `UserService`.

***

## Small exercise

Look at this:

```java
class EmailService {
    public void sendEmail() {
        System.out.println("Email sent");
    }
}

class UserController {

    private EmailService emailService;

    public UserController() {
        emailService = new EmailService();
    }
}
```

**Question:** What is the dependency of `UserController`?

Answer it before continuing. [^1]

***

# 2. What is Dependency Injection?

Now we have a problem.

Look carefully at this:

```java
class UserController {

    private EmailService emailService;

    public UserController() {
        emailService = new EmailService();
    }
}
```

`UserController` is responsible for creating its own dependency.

```text
UserController
      |
      | creates
      ↓
new EmailService()
```

Spring says, essentially:

> "You don't need to create the dependency yourself. I'll give it to you."

That's **Dependency Injection**.

Instead of:

```java
emailService = new EmailService();
```

the dependency is **provided to the object from outside**.

So:

```text
Before DI:

Controller
    |
    | creates
    ↓
Service
```

With DI:

```text
Spring
  |
  | creates/provides
  ↓
Service
  |
  | injected into
  ↓
Controller
```

The word **injection** simply means:

> **Giving an object the dependency it needs.**

That's the core idea.

***

# 3. Why do we need Dependency Injection?

Let's compare the two approaches.

### Without DI

```java
class UserController {

    private UserService userService;

    public UserController() {
        userService = new UserService();
    }
}
```

The controller is saying:

> "I will decide exactly which `UserService` to create."

This creates **tight coupling** between the classes.

### With DI

Conceptually:

```java
class UserController {

    private UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }
}
```

Now the controller says:

> "I need a `UserService`. Whoever creates me can give me one."

That's much more flexible.

And in Spring, the **Spring Container** is the thing that creates and provides these objects.

You learned about the Spring Container in Session 1.2.

So now we're connecting the ideas:

```text
IoC
 ↓
Spring controls object creation

Dependency Injection
 ↓
Spring provides objects with their dependencies
```

***

# 4. Constructor Injection

This is the most important form of DI for this session.

Consider:

```java
class UserController {

    private UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }
}
```

Look carefully at the constructor:

```java
public UserController(UserService userService) {
    this.userService = userService;
}
```

The `UserController` doesn't do:

```java
new UserService()
```

Instead, someone gives it a `UserService`.

That's **constructor injection**.

### Why is it called constructor injection?

Because the dependency is provided through the **constructor**.

```text
UserService
     ↓
constructor
     ↓
UserController
```

***

# 5. Let's connect this to Spring

Now let's make this a Spring example.

```java
@Service
public class UserService {

    public void doSomething() {
        System.out.println("User service working");
    }
}
```

And:

```java
@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }
}
```

Don't worry too much about `@Service` and `@RestController` yet. You already encountered the general idea of Spring-managed objects.

The important part for **this lesson** is:

```java
public UserController(UserService userService) {
    this.userService = userService;
}
```

Spring sees that `UserController` needs a `UserService`.

It provides one.

Conceptually:

```text
Spring Container

    UserService
         |
         | inject
         ↓
   UserController
```

You don't write:

```java
new UserService()
```

inside `UserController`.

Spring handles that.

***

# 6. Why `final`?

You'll frequently see this:

```java
private final UserService userService;
```

instead of:

```java
private UserService userService;
```

`final` means that once the constructor assigns the dependency:

```java
this.userService = userService;
```

the reference cannot later be replaced.

For example, this is not allowed:

```java
this.userService = anotherService;
```

after the field has already been initialized.

For constructor-injected dependencies, `final` is generally a good practice.

For now, remember:

> Constructor injection + `final` field is a very common Spring pattern.

***

# 7. Why is Constructor Injection Preferred?

Your syllabus specifically asks why constructor injection is preferred.

There are several reasons.

### 1. The dependency is required

Suppose `UserController` cannot work without `UserService`.

The constructor makes that obvious:

```java
public UserController(UserService userService)
```

You cannot properly create the controller without providing the service.

***

### 2. The object is fully initialized

After this constructor finishes:

```java
public UserController(UserService userService) {
    this.userService = userService;
}
```

the controller has its required dependency.

***

### 3. Dependencies can be `final`

```java
private final UserService userService;
```

This makes the dependency harder to accidentally replace.

***

### 4. It is easier to test

Later, if you want to test `UserController`, you can provide a particular `UserService` yourself.

For example:

```java
UserService service = new UserService();
UserController controller = new UserController(service);
```

You don't need Spring just to construct the object.

***

### The main idea

Don't memorize four reasons yet.

Remember this:

> **Constructor injection clearly communicates what an object requires, ensures required dependencies are provided when the object is created, and works well with immutable `final` fields and testing.**

***

# 8. Setter Injection — Basic Understanding

Now let's look at another form.

Instead of giving the dependency through the constructor, we can provide it through a setter method.

```java
class UserController {

    private UserService userService;

    public void setUserService(UserService userService) {
        this.userService = userService;
    }
}
```

Then someone can do:

```java
UserService service = new UserService();

UserController controller = new UserController();

controller.setUserService(service);
```

The dependency is provided through:

```java
setUserService(...)
```

Therefore:

> **Setter injection = dependency is provided through a setter method.**

Conceptually:

```text
UserController
      ↑
      |
setUserService()
      ↑
      |
 UserService
```

### When might setter injection make sense?

It's useful when a dependency is **optional** or can legitimately be changed after object creation.

==But for a required dependency, constructor injection is usually preferred==.

That's all you need to know about setter injection for this session.

***

# 9. Field Injection — Understand It, Don't Default to It

You may see this in Spring code:

```java
@Autowired
private UserService userService;
```

This is **field injection**.

The dependency is placed directly into the field.

Conceptually:

```text
UserController

private UserService userService;
              ↑
              |
          Spring injects
```

You don't write a constructor or setter.

However, **don't use field injection as your default**.

Prefer:

```java
private final UserService userService;

public UserController(UserService userService) {
    this.userService = userService;
}
```

rather than:

```java
@Autowired
private UserService userService;
```

You don't need to study the deeper problems with field injection right now.

Just remember:

```text
Constructor injection → preferred
Setter injection      → useful in some cases
Field injection       → understand it, but don't make it your default
```

***

# 10. The Three Forms Side by Side

### Constructor injection

```java
class Controller {

    private final Service service;

    public Controller(Service service) {
        this.service = service;
    }
}
```

Dependency comes through the constructor.

### Setter injection

```java
class Controller {

    private Service service;

    public void setService(Service service) {
        this.service = service;
    }
}
```

Dependency comes through a setter.

### Field injection

```java
class Controller {

    @Autowired
    private Service service;
}
```

Spring injects directly into the field.

For this course:

> **Constructor injection is your default.**

***

# 11. Practical Exercise — Controller → Service

Now let's actually build the thing from your syllabus.

We want:

```text
Controller
    ↓
Service
```

And Spring should inject the `Service` into the `Controller`.

## Step 1 — Create the Service

```java
@Service
public class UserService {

    public void sayHello() {
        System.out.println("Hello from UserService");
    }
}
```

The important part for DI is:

```java
@Service
```

This tells Spring that this class should be managed by Spring.

***

## Step 2 — Create the Controller

```java
@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }
}
```

Notice what we **didn't** write:

```java
new UserService()
```

That's the key.

Spring provides the `UserService`.

***

## Step 3 — Use the Service

Let's give the controller an endpoint:

```java
@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/hello")
    public String hello() {
        userService.sayHello();
        return "Hello";
    }
}
```

The dependency relationship is now:

```text
Spring Container
       |
       | creates
       ↓
 UserService
       |
       | injects
       ↓
UserController
       |
       | calls
       ↓
 UserService
```

The important thing is that **you never manually create `UserService` inside `UserController`**.

***

# 12. What exactly happens when the application starts?

At a high level:

```text
Spring starts
     ↓
Spring scans your application
     ↓
Finds UserService
     ↓
Creates UserService object
     ↓
Finds UserController
     ↓
Sees that UserController needs UserService
     ↓
Provides UserService to Controller's constructor
     ↓
UserController is created
```

So when you write:

```java
public UserController(UserService userService)
```

you're essentially telling Spring:

> "When you create `UserController`, give it a `UserService`."

That's Dependency Injection.

***

# 13. One Very Important Distinction

Don't confuse these two:

### Creating a dependency yourself

```java
class Controller {

    private Service service;

    public Controller() {
        service = new Service();
    }
}
```

Here:

```text
Controller → creates Service
```

### Receiving a dependency

```java
class Controller {

    private Service service;

    public Controller(Service service) {
        this.service = service;
    }
}
```

Here:

```text
Someone else → provides Service → Controller
```

In Spring:

```text
Spring Container
       ↓
   provides
       ↓
    Service
       ↓
   Controller
```

**That difference is the heart of Dependency Injection.**

***

# 14. Mental Model for Session 1.3

Keep this simple mental model:

```text
DEPENDENCY

A class needs another class.

Controller
    ↓
 Service


DEPENDENCY INJECTION

Instead of Controller creating Service,
something else provides Service.

Spring
   ↓
Service
   ↓
Controller


CONSTRUCTOR INJECTION

Spring provides Service
through Controller's constructor.

Service
   ↓
Controller(Service service)


PREFERENCE

Constructor injection  ← default/preferred
Setter injection      ← basic alternative
Field injection       ← understand, don't default to it
```

***

# Checkpoint 🧠

Don't look back at the lesson while answering these.

### 1. What is a dependency?

Suppose:

```java
class OrderController {

    private OrderService orderService;
}
```

What is the dependency?

***

### 2. What's wrong with this?

```java
class OrderController {

    private OrderService service;

    public OrderController() {
        service = new OrderService();
    }
}
```

***

### 3. Is this constructor injection?

```java
class OrderController {

    private final OrderService service;

    public OrderController(OrderService service) {
        this.service = service;
    }
}
```

Why?

***

### 4. What is setter injection?

Explain this:

```java
public void setOrderService(OrderService service) {
    this.service = service;
}
```

***

### 5. Which should normally be your default in Spring?

A. Field injection
B. Setter injection
C. Constructor injection

***

### 6. Most important question

In your own words, explain the difference between:

```text
Controller
    ↓
new Service()
```

and:

```text
Spring
   ↓
Service
   ↓
Controller
```

If you can answer **#6 clearly**, you've understood the central idea of Dependency Injection.

***

# Footnotes:
[^1]: [[Is it still a dependency (java + spring)(.bVVmS)]].

