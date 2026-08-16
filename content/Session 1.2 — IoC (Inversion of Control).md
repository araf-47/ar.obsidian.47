# Session 1.2 — IoC (Inversion of Control)

This is one of the **most important ideas in Spring**. Don't worry about memorizing the terminology yet. The goal is to understand **who creates objects and who decides what depends on what**.

***

## 1. What does "control" mean in traditional Java?

Let's start with ordinary Java, without Spring.

Suppose you have three classes:

```java
class Repository {
    public void save() {
        System.out.println("Saving data...");
    }
}
```

```java
class Service {
    private Repository repository;

    public Service() {
        repository = new Repository();
    }

    public void doSomething() {
        repository.save();
    }
}
```

And:

```java
class Controller {
    private Service service;

    public Controller() {
        service = new Service();
    }

    public void handleRequest() {
        service.doSomething();
    }
}
```

Now imagine:

```java
Controller controller = new Controller();
```

What happens?

`Controller` creates a `Service`:

```text
Controller
    ↓
new Service()
```

Then `Service` creates a `Repository`:

```text
Service
    ↓
new Repository()
```

So the complete chain is:

```text
Controller
    ↓
new Service()
    ↓
new Repository()
```

### Where is the "control"?

The **application code itself controls object creation**.

`Controller` says:

> "I need a Service, so I'll create one."

And `Service` says:

> "I need a Repository, so I'll create one."

That's what we're calling **control** here.

***

# 2. The problem with this approach

At first, this seems perfectly reasonable.

But imagine your `Service` changes.

Today:

```java
repository = new Repository();
```

Tomorrow you want:

```java
repository = new PostgreSQLRepository();
```

Now `Service` has to know which specific repository implementation to create.

Your classes become tightly connected:

```text
Service
   │
   └── knows how to create Repository
```

And as your application grows, you can end up with a large network of classes creating other classes.

For example:

```text
Controller
   ↓
Service
   ↓
Repository
   ↓
DatabaseConnection
   ↓
Configuration
```

Every class is responsible not only for **doing its job**, but also for figuring out **how to construct the objects it needs**.

This is where IoC becomes useful.

***

# 3. What is Inversion of Control?

The name sounds complicated, but the basic idea is simple:

> **Instead of your application controlling the creation of its objects, another system controls it.**

That is **Inversion of Control (IoC)**.

Normally:

```text
Your code
   ↓
creates objects
   ↓
uses objects
```

With IoC:

```text
Spring
   ↓
creates objects
   ↓
gives them to your code
   ↓
your code uses them
```

So the responsibility has been **inverted**.

### Traditional Java

You say:

> "I need a Service. I'll create it."

```java
Service service = new Service();
```

### Spring

You say, essentially:

> "Spring, my Controller needs a Service."

And Spring takes responsibility for creating/managing that object.

Conceptually:

```text
Spring Container
       ↓
creates Service
       ↓
provides Service to Controller
```

That's the core idea of IoC.

***

# 4. Traditional object creation vs IoC

Let's make the difference very explicit.

### Traditional Java

```java
class Controller {

    private Service service;

    public Controller() {
        service = new Service();
    }
}
```

The `Controller` is responsible for creating its dependency.

```text
Controller
    │
    │ creates
    ↓
Service
```

### With IoC

The Controller doesn't create the Service.

Conceptually:

```java
class Controller {

    private Service service;

    // Spring provides Service
}
```

And Spring handles the creation:

```text
              Spring Container
                    │
             creates Service
                    │
                    ↓
               Controller
```

The important change is:

**Who creates `Service`?**

Traditional:

```text
Controller
```

Spring:

```text
Spring Container
```

That is IoC.

***

# 5. What is the Spring Container?

Now we need one important Spring term.

The **Spring Container** is the part of Spring that manages objects for your application.

Think of it as an **object manager**.

You tell Spring, in effect:

> "These are the objects my application uses."

Spring then:

* creates those objects
* keeps track of them
* manages them
* provides them to other objects that need them

For example:

```text
Spring Container
│
├── Controller
├── Service
└── Repository
```

Instead of:

```text
Controller → new Service()
Service    → new Repository()
```

Spring can manage the whole set:

```text
              Spring Container
             /       |       \
            ↓        ↓        ↓
      Controller   Service  Repository
```

So when you hear:

> **Spring Container**

think:

> **The Spring system responsible for creating and managing application objects.**

For this lesson, that's enough. We don't need to go into the different container types or advanced configuration yet.

***

# 6. Let's connect this to something you already know

You've worked with JDBC.

Normally, you might write something like:

```java
Connection connection =
    DriverManager.getConnection(url, username, password);
```

Your code explicitly asks for and creates/obtains the connection.

Now imagine a system where you simply say:

> "I need a database connection."

and another system handles obtaining and managing that connection for you.

The same **general idea** is happening with IoC:

```text
You:
"I need this object."

Spring:
"Okay, I'll manage it and provide it."
```

Don't take this analogy too literally—the mechanics are different. It's just a way to understand the **responsibility shift**.

***

# 7. Why does IoC matter?

The biggest reason is **reduced responsibility and coupling**.

Consider:

```java
class Service {

    private Repository repository;

    public Service() {
        repository = new Repository();
    }
}
```

`Service` has two responsibilities:

1. Use the repository.
2. Decide how to create the repository.

With IoC, the idea becomes:

```text
Service
   ↓
uses Repository
```

while:

```text
Spring
   ↓
creates/manages Repository
```

So responsibilities become more separated:

```text
Service
   → focuses on business logic

Repository
   → focuses on data access

Spring
   → manages the objects
```

That's a major reason Spring became useful in large Java applications.

***

# 8. Tiny practical example — without Spring

Let's build the exercise in two stages.

Create these three classes.

### `Repository.java`

```java
public class Repository {

    public void save() {
        System.out.println("Saving data...");
    }
}
```

### `Service.java`

```java
public class Service {

    private Repository repository;

    public Service() {
        repository = new Repository();
    }

    public void doSomething() {
        repository.save();
    }
}
```

### `Main.java`

```java
public class Main {

    public static void main(String[] args) {

        Service service = new Service();

        service.doSomething();
    }
}
```

Run it.

The important part isn't the output.

Look at this:

```java
Service service = new Service();
```

and inside `Service`:

```java
repository = new Repository();
```

The application is controlling object creation.

```text
Main
 ↓
new Service()
 ↓
new Repository()
```

***

# 9. Now imagine Spring managing them

We aren't going to learn Spring configuration details yet.

For now, just understand the **conceptual version**.

Instead of:

```java
Service service = new Service();
```

and:

```java
repository = new Repository();
```

we want Spring to manage them:

```text
             Spring Container
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
     Repository            Service
                              │
                              ↓
                         Repository
```

The important difference is:

### Before

```text
Your code
   ↓
new Service()
   ↓
new Repository()
```

### With IoC

```text
Spring Container
   ↓
creates Service
   ↓
Service receives/uses Repository
```

The application is no longer responsible for constructing the entire dependency chain itself.

***

# 10. One very important distinction

Don't confuse **IoC** with:

> "Spring eliminates `new`."

That's not quite right.

You can still use `new` in a Spring application.

The important idea is:

> **Objects that Spring is responsible for managing are created and managed by Spring rather than being manually constructed by your application code.**

So IoC is about **control and responsibility**, not about banning the `new` keyword.

***

# 11. The big picture

You should now be able to look at these two diagrams and explain the difference.

### Traditional Java

```text
Controller
    ↓
new Service()
    ↓
new Repository()
```

Your application controls object creation.

### Spring / IoC

```text
Spring Container
      ↓
creates and manages
      ↓
Controller
Service
Repository
```

Spring takes control of object creation and management.

***

# Practical Exercise

Before moving on, try this yourself.

Create:

```text
Repository
Service
Controller
Main
```

### Part A — Traditional Java

Make:

```text
Main
 ↓
Controller
 ↓
Service
 ↓
Repository
```

using `new`.

For example, the flow should ultimately resemble:

```java
Controller controller = new Controller();
```

and the `Controller` creates the `Service`, while the `Service` creates the `Repository`.

### Part B — Think about IoC

Don't implement Spring yet.

Instead, answer these questions:

1. Who creates `Controller` in Part A?
2. Who creates `Service`?
3. Who creates `Repository`?
4. In a Spring IoC approach, who should be responsible for creating these objects?
5. What is the **Spring Container**?

***

# Session 1.2 Checkpoint

Try answering these **without looking back**:

**1. What does "control" mean in the context of IoC?**

**2. What is the difference between these two?**

```java
Service service = new Service();
```

and the idea of:

```text
Spring Container → Service
```

**3. What does "Inversion" mean in Inversion of Control?**

**4. What is the Spring Container?**

**5. Why is IoC useful?**

And finally, explain this in your own words:

> **Traditional Java gives object-creation control to your code, while Spring IoC gives that responsibility to the Spring Container.**

If you can explain that last statement clearly, **Session 1.2 is understood at the basic level we need before moving forward.**
