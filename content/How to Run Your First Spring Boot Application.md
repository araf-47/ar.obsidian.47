Absolutely. Let's do this as the **practical part of Session 2.3**. We'll assume you currently have **no Spring Boot project yet**.

# How to Run Your First Spring Boot Application

Our goal is very simple:

> Create a Spring Boot project → run it → see Spring Boot start successfully.

We are **not** building an API yet.

***

## 1. What do we need?

You need:

* Java/JDK
* A Spring Boot project
* An IDE/editor such as VS Code or IntelliJ
* Maven, which Spring Boot projects commonly use to manage dependencies and build/run the project

You already have Java and VS Code from your previous work.

The easiest way to create the project is **Spring Initializr**.

[Spring Initializr](https://start.spring.io/?utm_source=chatgpt.com)

Think of Spring Initializr as:

> **A website that generates the basic structure of a Spring Boot project for you.**

***

# 2. Create the project

Open Spring Initializr.

You'll see options for creating a project.

For our first application, use something approximately like:

```text
Project:          Maven
Language:         Java
Spring Boot:      current stable version
Group:            com.example
Artifact:         demo
Packaging:        Jar
Java:             21
```

The important ones for now are:

### Maven

```text
Maven
```

Maven will help manage your Java/Spring dependencies and build the project.

We won't study Maven in depth in this session.

### Java

Choose the JDK version you're actually using.

Since you've been working with Java 21, **Java 21** is a sensible choice.

### Artifact

For example:

```text
demo
```

This becomes the project name.

***

# 3. Add a Spring Web dependency

There will be a section called **Dependencies**.

Search for:

```text
Spring Web
```

Select it.

You might wonder:

> "Why are we adding Spring Web when we're not learning REST APIs yet?"

Because we want a **web-capable Spring Boot application**, which will allow Spring Boot to start an embedded web server such as Tomcat.

We're **not studying Spring Web itself yet**.

Click:

```text
Generate
```

Spring Initializr will download a `.zip` file.

***

# 4. Extract the project

Extract the ZIP file.

You'll get a project folder that looks roughly like:

```text
demo/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/demo/
│   │   │       └── DemoApplication.java
│   │   │
│   │   └── resources/
│   │
│   └── test/
│
├── pom.xml
└── ...
```

Don't worry about all of these files yet.

For this lesson, focus on:

```text
DemoApplication.java
pom.xml
```

***

# 5. Open the project in VS Code

Open VS Code.

Choose:

```text
File → Open Folder
```

and select the extracted:

```text
demo
```

folder.

Your project should appear in the VS Code Explorer.

***

# 6. Find the main application class

Navigate to something like:

```text
src
└── main
    └── java
        └── com.example.demo
            └── DemoApplication.java
```

Open it.

Spring Initializr has already created something like:

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

}
```

**This is the code we were studying earlier.**

Now it makes much more sense because you can see where it actually lives.

***

# 7. Let's understand the code

Start here:

```java
@SpringBootApplication
public class DemoApplication {
```

This tells Spring Boot:

> `DemoApplication` is the main application class.

Then:

```java
public static void main(String[] args) {
```

This is ordinary Java.

The JVM starts the program here.

Then:

```java
SpringApplication.run(DemoApplication.class, args);
```

This tells Spring Boot:

> **Start the Spring Boot application.**

So:

```text
JVM
 ↓
main()
 ↓
SpringApplication.run()
 ↓
Spring Boot starts
```

***

# 8. Now actually run it

There are several ways to run a Spring Boot project.

For now, let's use the terminal because it makes the process easier to understand.

Open the VS Code terminal:

```text
Terminal → New Terminal
```

Make sure you're in the project directory.

You should be somewhere like:

```text
~/demo
```

You should see:

```text
pom.xml
src/
```

if you run:

```bash
ls
```

***

# 9. Run the application

Because this is a Maven project, Spring Initializr provides a Maven wrapper.

On Linux, you can run:

```bash
./mvnw spring-boot:run
```

The first time, Maven may download various dependencies.

That can take a while.

Eventually you'll see a lot of startup output.

Look for something indicating that Tomcat has started, such as:

```text
Tomcat started on port 8080
```

You should also see something indicating that the application has started.

At this point:

> **Your Spring Boot application is running.**

***

# 10. What just happened?

This is the most important part.

You executed:

```bash
./mvnw spring-boot:run
```

That starts your Spring Boot application.

The application enters:

```java
public static void main(String[] args)
```

Then:

```java
SpringApplication.run(DemoApplication.class, args);
```

runs.

Spring Boot starts.

Conceptually:

```text
./mvnw spring-boot:run
             ↓
       Java application
             ↓
          main()
             ↓
SpringApplication.run(...)
             ↓
      Spring Boot starts
             ↓
     ApplicationContext
             ↓
    Embedded Tomcat starts
             ↓
      Application ready
```

***

# 11. What is Tomcat doing?

Because we included:

```text
Spring Web
```

Spring Boot has what it needs for a web application, including an embedded web server.

Tomcat starts on a port, commonly:

```text
8080
```

So your computer now has something listening at:

```text
localhost:8080
```

Think of it like:

```text
Your computer
│
└── Spring Boot application
       │
       └── Embedded Tomcat
              │
              └── Port 8080
```

***

# 12. Open the browser

Now open:

```text
http://localhost:8080
```

You may see an error page such as:

```text
Whitelabel Error Page
```

**That's okay!**

In fact, for this exercise, that's expected.

Why?

Because we haven't created anything that tells the application:

> "When someone visits `/`, send this particular response."

We're going to learn that later when we study controllers and ==REST APIs==.

For now, the important thing is:

> **The server is running.**

***

# 13. How do I stop the application?

Go back to the terminal where it's running.

Press:

```text
Ctrl + C
```

The Spring Boot application stops.

Now try:

```text
http://localhost:8080
```

It won't connect because your application isn't running anymore.

That's a useful experiment.

***

# 14. Your first complete mental model

You should now be able to understand this:

```text
                 Spring Initializr
                       │
                       ↓
              Creates Spring Boot
                  project
                       │
                       ↓
              DemoApplication.java
                       │
                       ↓
              public static void main()
                       │
                       ↓
          SpringApplication.run(...)
                       │
                       ↓
               Spring Boot starts
                       │
              ┌────────┴────────┐
              ↓                 ↓
      ApplicationContext   Embedded Tomcat
              │                 │
              └────────┬────────┘
                       ↓
                 Application
                    running
                       │
                       ↓
                localhost:8080
```

***

# 15. One important thing about `pom.xml`

You'll see:

```text
pom.xml
```

in the project.

It contains project configuration and dependencies.

For example, because we selected **Spring Web**, the generated project has a dependency related to Spring Web.

You don't need to learn Maven or the entire `pom.xml` in this session.

For now, just remember:

> **`pom.xml` tells Maven about your project and its dependencies.**

We'll leave the details for later.

***

# 16. Your practical task

Now I want **you** to actually do this.

### Step 1

Open:

[Spring Initializr](https://start.spring.io/?utm_source=chatgpt.com)

### Step 2

Create a project with:

```text
Maven
Java
Spring Boot
Java 21
Spring Web
```

You can call it:

```text
demo
```

### Step 3

Download and extract it.

### Step 4

Open the project folder in VS Code.

### Step 5

Find:

```text
DemoApplication.java
```

### Step 6

Run:

```bash
./mvnw spring-boot:run
```

### Step 7

Look at the terminal and find the message showing that Tomcat started.

### Step 8

Open:

```text
http://localhost:8080
```

If you get a **Whitelabel Error Page**, that's fine.

### Step 9

Stop it with:

```text
Ctrl + C
```

***

## Then tell me what happened

Especially tell me:

1. Did `./mvnw spring-boot:run` work?
2. What did the terminal say about Tomcat?
3. What happened when you opened `localhost:8080`?

Once you've done that, we'll continue **Session 2.3** from exactly there rather than jumping ahead.


# After my answer:
Perfect. **That means your first Spring Boot application is actually running.** 🎉

And the error page is **not a problem**.

Let's make sure you understand *why* you got that error page, because this is an important distinction.

### What you currently have

Your application contains:

```java
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

When you ran:

```bash
./mvnw spring-boot:run
```

this happened:

```text
Java starts
   ↓
main()
   ↓
SpringApplication.run()
   ↓
Spring Boot starts
   ↓
ApplicationContext starts
   ↓
Embedded Tomcat starts
   ↓
Tomcat listens on port 8080
   ↓
http://localhost:8080
```

So **Spring Boot itself is working correctly**.

***

## Then why the error page?

You visited:

```text
http://localhost:8080
```

Your browser essentially asked:

> "Hey application, what should you give me for `/`?"

But **we haven't created anything to handle `/` yet**.

So Spring Boot says, essentially:

> "I don't have anything configured to handle that request."

And you get the Whitelabel Error Page.

```text
Browser
   │
   │ GET /
   ↓
Tomcat
   ↓
Spring Boot
   ↓
"No handler for this request"
   ↓
Whitelabel Error Page
```

That's actually a **good sign for this exercise**.

If Tomcat weren't running, you'd get something more like:

```text
Unable to connect
Connection refused
```

Instead, you reached a Spring Boot-generated page.

***

## One thing I want you to notice

You didn't install Tomcat separately for this project.

Yet your terminal says Tomcat is running.

That's **embedded Tomcat**.

Your application is essentially:

```text
DemoApplication
      +
   Spring Boot
      +
 Embedded Tomcat
```

and running the application starts all of that together.

***

### So your current status is:

| Thing                         | Status                        |
| ----------------------------- | ----------------------------- |
| Spring Boot project created   | ✅                             |
| Main application class        | ✅                             |
| `@SpringBootApplication`      | ✅                             |
| `main()`                      | ✅                             |
| `SpringApplication.run()`     | ✅                             |
| Spring Boot startup           | ✅                             |
| ApplicationContext            | ✅                             |
| Embedded Tomcat               | ✅                             |
| Port 8080                     | ✅                             |
| Browser can reach application | ✅                             |
| `/` has actual content        | ❌ — **not learned/built yet** |

That last ❌ is **intentional**. We haven't learned the part that creates web endpoints yet.

**You have successfully completed the practical "run a Spring Boot application" portion of Session 2.3.**
