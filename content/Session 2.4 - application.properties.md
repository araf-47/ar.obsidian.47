# Session 2.4 — `application.properties`

This session is small, but **very important in real Spring Boot applications**.

We are going to learn only:

* What `application.properties` is
* What application configuration means
* How to change the server port
* Basic configuration properties
* Why configuration is separated from Java code

We will **not** go into profiles, environment variables, YAML, external configuration servers, or advanced configuration yet.

***

# 1. First: What is configuration?

Let's start without Spring.

Suppose you have a Java program:

```java
public class App {

    public static void main(String[] args) {

        int port = 8080;

        System.out.println("Server running on port " + port);
    }
}
```

Here:

```java
int port = 8080;
```

is a **configuration value**.

It tells the application:

> "Use port 8080."

The problem is that the value is inside Java code.

If tomorrow you want port `9090`, you'd have to change:

```java
int port = 8080;
```

to:

```java
int port = 9090;
```

Then recompile/rebuild the application.

That's not ideal.

***

# 2. Configuration should be separate from application code

A better idea is:

**Java code:**

```java
// application logic
```

**Configuration:**

```text
server port = 8080
```

Keep them separately.

This is the basic idea behind **application configuration**.

Think of it like this:

```text
Java code
   │
   │  "What should I do?"
   │
   ▼
Application logic


Configuration
   │
   │  "How should the application be configured?"
   │
   ▼
Settings
```

For example:

```text
Application code
    ↓
Handle HTTP request
Calculate result
Return response

Configuration
    ↓
Which port?
Database URL?
Other settings?
```

We're only dealing with the basic idea today.

***

# 3. What is `application.properties`?

Spring Boot provides a special configuration file called:

```text
application.properties
```

It normally lives here:

```text
src
└── main
    ├── java
    │
    └── resources
        └── application.properties
```

So your project might look like:

```text
my-spring-app/
│
├── src/
│   └── main/
│       ├── java/
│       │   └── ...
│       │
│       └── resources/
│           └── application.properties
│
└── pom.xml
```

The important part is:

```text
src/main/resources/application.properties
```

Spring Boot automatically looks for this file and reads configuration from it.

***

# 4. Your first property

Open:

```text
application.properties
```

and write:

```properties
server.port=8080
```

That's it.

The structure is:

```text
property=value
```

So:

```properties
server.port=8080
```

means roughly:

> Configure the application's server to use port 8080.

***

# 5. Changing the server port

You already ran your Spring Boot application on:

```text
http://localhost:8080
```

Now let's change it.

In `application.properties`:

```properties
server.port=9090
```

Restart your Spring Boot application.

Now go to:

```text
http://localhost:9090
```

Your application should be there.

Notice what happened.

You **didn't modify your Java code**.

You simply changed:

```properties
server.port=9090
```

That's the main lesson of this session.

***

# 6. Why is this useful?

Imagine your application has this:

```text
server.port=8080
```

During development, you might want:

```text
8080
```

But another environment might use:

```text
9090
```

You don't necessarily want to modify your Java source code just because the environment's configuration is different.

So instead:

```text
Java code
    ↓
does the application's work

application.properties
    ↓
controls configuration
```

This gives us a separation between:

**Application logic**

and

**Application settings**

***

# 7. Think about it using something you already know

Since you've worked with JDBC, this should feel familiar.

You might have Java code like:

```java
Connection connection = DriverManager.getConnection(
    "jdbc:postgresql://localhost:5432/Practice_DB",
    "postgres",
    "password"
);
```

The database URL, username, and password are **configuration information**.

They're not really the business logic of your application.

Conceptually, we'd prefer something like:

```text
Java code
    ↓
"Connect to the database"

Configuration
    ↓
"Which database?"
"Which username?"
"Which password?"
```

We're **not learning database configuration in this session**. That's just an analogy to understand why configuration exists.

***

# 8. Basic configuration properties

A `.properties` file is basically a collection of:

```text
key=value
```

For example:

```properties
server.port=9090
```

Another hypothetical property could look like:

```properties
some.setting=value
```

Or:

```properties
app.name=My Application
```

The important syntax is:

```properties
key=value
```

You don't write Java syntax here.

❌ Don't write:

```properties
server.port = 9090;
```

There is no semicolon.

Use:

```properties
server.port=9090
```

***

# 9. Comments

You can also put comments in `application.properties`.

Use:

```properties
# This is a comment
server.port=9090
```

Spring Boot ignores the comment.

Comments are useful for explaining configuration.

***

# 10. One important distinction

Don't think:

> "`application.properties` contains Java configuration code."

It doesn't.

It's a **configuration file**.

For example:

```properties
server.port=9090
```

is not Java.

It's a configuration instruction that Spring Boot understands.

So we have:

```text
Java
↓
Application behavior


application.properties
↓
Application configuration
```

***

# 11. Practical exercise

Let's actually do this with the Spring Boot project you already have running.

### Step 1

Find:

```text
src/main/resources/application.properties
```

### Step 2

Put:

```properties
server.port=9090
```

inside it.

### Step 3

Stop your Spring Boot application.

### Step 4

Start it again.

### Step 5

Look at the console.

You should see that Tomcat is now running on port:

```text
9090
```

### Step 6

Open:

```text
http://localhost:9090
```

You should get your Spring Boot application.

***

## Your first mini-challenge

Now change:

```properties
server.port=9090
```

to:

```properties
server.port=8081
```

Restart the application.

Then open:

```text
http://localhost:8081
```

### Question

Why did you **not** need to change any Java code when changing the port from `9090` to `8081`?

Think about that before looking at the answer.

<details>
<summary>Answer</summary>

Because the port is **configuration**, not application logic.

Spring Boot reads:

```properties
server.port=8081
```

from `application.properties` and configures the embedded server accordingly.

The Java source code doesn't need to know the port directly.

</details>

***

# 12. The mental model you should remember

For this session, remember just this:

```text
application.properties
        │
        │ configuration
        ▼
   Spring Boot
        │
        ▼
Configure application
```

For example:

```properties
server.port=8081
```

means:

> "Spring Boot, configure the application's server to use port 8081."

And the big idea is:

> **Keep configuration/settings separate from Java application logic.**

***

# Checkpoint

Don't worry about memorizing lots of properties. I want to check whether you understand the concept.

Answer these **without looking back**:

### 1.

What is `application.properties`?

### 2.

Where is it normally located in a Spring Boot project?

### 3.

What does this mean?

```properties
server.port=9090
```

### 4.

If I change:

```properties
server.port=8080
```

to:

```properties
server.port=9090
```

why don't I need to modify my Java code?

### 5.

What is the difference between **application logic** and **configuration**?

Send me your answers, and I'll check them before we move on.
