# Session 2.2 — Spring Initializr + Project Setup

This session is important because **this is where you actually create the Spring Boot project you'll work with**.

So far, you've been learning Spring concepts without needing a Spring Boot project. Now we're moving from:

> "What does Spring do?"

to:

> "Let's create a real Spring Boot application."

We'll keep this practical.

***

# 1. What is Spring Initializr?

**Spring Initializr** is a tool that generates the starting structure of a Spring Boot project for you.

Think of it as a **project generator**.

Instead of manually creating:

* Maven configuration
* folders
* `pom.xml`
* Spring Boot setup
* dependency configuration
* main application class

you tell Initializr what you want, and it generates the project.

![Image](https://images.openai.com/static-rsc-4/vYq-niEHaeyzhYQcAc8yCx_duRZfFSsccjdJmwmZTWo7zwOg3m6KhGvLuWxtrfzb-dYl0n0tBS3v3eQwYtMzk--srcCsYiZwZ6rf05fjr17d0DwZ9S63h68hGdFya_jUQBZsO5XK-6Kodb-S_z8U-8a2lhS7JEOZA9CuJPjEaTKRKvmwqfmuZ6WdXFXo2nI-?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/MKSreYNZkm_gJwtp1IQmg4fLklMmVsaQeJWREirBmlZ_otfjBu5SdbyVX1r0fd3Snai9uBBdo8e550iN8d6QCboDFlFdg-JFqzWuMffB1AScuq88Pt5C6jQv-fXh1guX1R990FterjbHptafy-X8Rm9oYVMuUTCP-MAoeqF77tcVmB3VN4TYjfaLhB4zFxfp?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/YmCXyZ_UUATtOGUYcP_RjzwxNrSmPM2Rce_g2ntxkHj51EkOGILOWNSg1-xD4e2n0BFDdk9G_0_ddHPRaPGOeduTupHyj4SNJwherxJkf_Wp9srX4FQUmWDT0_2gYmSfHAKN4iqMlCUsBx8c3jvhjXDZ5gdpSPRQXYZjEikrRyc318TPFVMGQn7ULRcgdi7h?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/cwc7vlko6UBKaRnL3GrUNLzh-HB9v5q-hdUfQVotiAYNewJt2pMBEVAlSLGdBdRVQZuit1kA70E_iGlnhZGVV4tkw4SSzBujdgqqUUi_ah3cssq1ZVsWYXsF_IiEj989KA3rR3OPNA17Dy8TwnLc4GFPbC8cDoHzUCpdS9ynivP_MuK1lIDSqf9tXqlmLRNk?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/DmZj8DPi01hdbW-USGmzetChaJI2cJ1HklzvjjfckNU6srpgAYGlHv4kdOs-j6m87DaFKGuQbyjh1iyqYhiczg5vwA0imQH636zzmOEhUZRicSQ1ZEl6vAbSAx8q-0OTvO3yHz_qyq_LODAc9P7dLkYv3u6twGICf2dFOOl6bvI4JZ_JfCT2Pv4USupZmRST?purpose=fullsize)

The official tool is:

[start.spring.io — Spring Initializr](https://start.spring.io/?utm_source=chatgpt.com)

You can think of it like this:

```text
You
 │
 │ "I want a Java + Spring Boot + Web project"
 ↓
Spring Initializr
 │
 │ generates
 ↓
Complete starter project
```

### Why does this exist?

Because a Spring Boot project has quite a bit of setup that you **don't want to create manually every time**.

Initializr gives you a sensible starting point.

***

# 2. Let's create a project

Open:

[Spring Initializr](https://start.spring.io/?utm_source=chatgpt.com)

You'll see several fields.

We'll go through each one because these terms will appear throughout your Spring Boot work.

Use something approximately like this:

```text
Project:       Maven
Language:      Java
Spring Boot:   current stable version
Group:         com.example
Artifact:      demo
Packaging:     Jar
Java:          21
```

Then add:

```text
Spring Web
Spring Boot DevTools
```

Don't worry about the other options yet.

***

# 3. Maven

This is one of the most important things on this screen.

You already know Java, so you may have previously created something like:

```text
MyProject/
    src/
        Main.java
```

But a real Spring Boot application has many dependencies.

For example, your application may need:

```text
Spring Boot
Spring Web
Jackson
Tomcat
PostgreSQL driver
JPA
etc.
```

You don't want to manually download and manage all those `.jar` files.

That's where **Maven** comes in.

### Maven is a build and dependency management tool.

It can:

* download dependencies
* manage dependency versions
* compile your project
* package your application
* run various build tasks

You can think of it as a more sophisticated version of the dependency management you experienced with JDBC.

Previously you might have manually added:

```text
postgresql-42.7.11.jar
```

With Maven, you describe the dependency in your project configuration, and Maven obtains it for you.

***

# 4. `pom.xml`

When you generate a Maven Spring Boot project, you'll get:

```text
pom.xml
```

`pom` means **Project Object Model**.

This file tells Maven important information about your project.

For example:

```xml
<groupId>com.example</groupId>
<artifactId>demo</artifactId>
```

and dependencies:

```xml
<dependencies>

    <dependency>
        ...
    </dependency>

</dependencies>
```

You don't need to memorize the XML syntax right now.

The important idea is:

```text
pom.xml
   │
   ├── Project information
   ├── Dependencies
   ├── Java version
   └── Build configuration
```

Later, when you add something like PostgreSQL or JPA, you'll often do it through dependencies in this file.

***

# 5. Group

Initializr asks for:

```text
Group
```

For example:

```text
com.example
```

The **Group** identifies the organization or namespace associated with your project.

A common convention is to use a reversed domain name.

For example, if a company owns:

```text
example.com
```

it might use:

```text
com.example
```

For learning, this is perfectly fine:

```text
com.example
```

Don't overthink this field.

***

# 6. Artifact

The next field is:

```text
Artifact
```

Suppose you enter:

```text
landlord
```

Then your project is essentially named:

```text
landlord
```

It also influences things such as the generated project directory and the built artifact.

For your practice project, you could use:

```text
landlord
```

or simply:

```text
demo
```

***

# 7. Group + Artifact together

These two are easier to understand together.

Suppose:

```text
Group:     com.example
Artifact:  landlord
```

You can think of it roughly as:

```text
com.example
     +
landlord
```

identifying your project.

Later you'll see these values in `pom.xml`.

For example:

```xml
<groupId>com.example</groupId>
<artifactId>landlord</artifactId>
```

***

# 8. Java Version

Initializr also asks:

```text
Java
```

This specifies which Java version the project is intended to use.

For example:

```text
Java 21
```

Since you've been working with modern Java, use Java 21 if it's available and compatible with the Spring Boot version you're selecting.

The important concept is:

```text
Spring Boot project
        ↓
uses
        ↓
specified Java version
```

This doesn't mean Maven somehow installs Java for you.

You still need a JDK installed on your computer.

***

# 9. Packaging

You'll see:

```text
Packaging
```

Usually:

```text
Jar
```

or:

```text
War
```

For this course, choose:

```text
Jar
```

### What is a JAR?

JAR stands for:

**Java ARchive**

It's essentially a packaged Java application.

For example, after building your Spring Boot application, you might end up with something like:

```text
landlord-0.0.1-SNAPSHOT.jar
```

Spring Boot applications are commonly packaged this way.

You don't need to study WAR packaging right now.

Just remember:

```text
Packaging → Jar
```

for our project.

***

# 10. Dependencies

This is probably the most important part of Initializr.

You'll see an option to add dependencies.

A **dependency** is something your application needs from an external library/framework.

For example:

```text
Your application
      │
      ├── Spring Web
      ├── PostgreSQL Driver
      └── Spring Data JPA
```

Instead of writing all of those libraries yourself, Maven manages them.

For today's project, add:

```text
Spring Web
```

and:

```text
Spring Boot DevTools
```

### Spring Web

This provides functionality we'll need for building web applications and REST APIs.

We'll use it extensively later.

### DevTools

We'll discuss this shortly.

***

# 11. What happens when you click Generate?

After configuring Initializr, click:

**Generate**

It downloads a ZIP file.

For example:

```text
landlord.zip
```

Extract it.

You'll get a project something like:

```text
landlord/
│
├── .mvn/
├── src/
├── pom.xml
├── mvnw
├── mvnw.cmd
└── ...
```

This is your actual Spring Boot project.

***

# 12. Project Structure

Now let's understand the important pieces.

A typical project looks approximately like:

```text
landlord/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/landlord/
│   │   │       └── LandlordApplication.java
│   │   │
│   │   └── resources/
│   │       └── application.properties
│   │
│   └── test/
│       └── java/
│
├── pom.xml
├── mvnw
└── mvnw.cmd
```

Don't try to memorize everything.

Focus on these:

```text
src/main/java
```

This is where your Java code goes.

For example:
- [^1]
```text
Controller
Service
Repository
```

will eventually live here.

***

## `src/main/resources`

This is where application resources/configuration live.

You'll see:

```text
application.properties
```

This will become important when we configure things such as:

```text
server port
database connection
Spring settings
```

We'll learn those when they are actually needed.

***

## `src/test`

This is where tests go.

For now, just recognize it.

***

## `pom.xml`

This is Maven's project configuration.

Remember:

```text
pom.xml
   ↓
Maven configuration
   ↓
dependencies + build information
```

***

# 13. The Main Application Class

Initializr also creates something like:

```java
package com.example.landlord;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class LandlordApplication {

    public static void main(String[] args) {
        SpringApplication.run(LandlordApplication.class, args);
    }

}
```

Don't worry about understanding every line yet.

For this session, recognize:

```java
public static void main(String[] args)
```

This is still Java's normal entry point.

And:

```java
SpringApplication.run(...)
```

==starts the Spring Boot application==.

So conceptually:

```text
main()
  ↓
SpringApplication.run()
  ↓
Spring Boot application starts
```

We'll study what Spring Boot is doing here in more detail when appropriate.

***

# 14. Practical Exercise #1 — Create the Project

Now do this yourself.

Create a project using Initializr with:

```text
Project:       Maven
Language:      Java
Java:          21
Group:         com.example
Artifact:      landlord
Packaging:     Jar
Dependencies:  Spring Web
               Spring Boot DevTools
```

Download and extract it.

Then open the project in your IDE/editor.

### Your task

Find these three things:

```text
pom.xml

src/main/java/

src/main/resources/application.properties
```

Don't modify anything yet.

Just locate them.

***

# 15. `spring-boot-devtools`

Now let's talk about the second dependency.

You added:

```text
Spring Boot DevTools
```

What is it?

**DevTools provides development-time conveniences that make working on a Spring Boot application easier.**

One of its useful features is automatic restart.

***

# 16. Why automatic restart is useful

Imagine your application is running:

```text
Spring Boot application
        ↓
      RUNNING
```

You edit some Java code.

Without development tooling, you may need to:

```text
Stop application
     ↓
Start application again
```

DevTools can detect certain changes and automatically restart the application context.

Conceptually:

```text
Application running
       ↓
You change Java code
       ↓
DevTools detects change
       ↓
Application restarts
       ↓
Your change is available
```

This saves you from manually restarting the application every time you make a development change.

***

# 17. Is this really "hot reload"?

You'll often hear people say:

> "DevTools gives hot reload."

That's a useful simplification, but don't think of it as magic where **every change is instantly injected into the running program**.

Spring Boot DevTools primarily provides an **automatic restart mechanism** for development.

So the simple mental model we want is:

```text
DevTools
   ↓
detect development changes
   ↓
restart application automatically
```

That's enough for this course.

We don't need to study its internal classloader architecture or advanced configuration.

***

# 18. Practical Exercise #2 — See DevTools Working

Start your Spring Boot application.

~~You should see output indicating that the application has started.~~

~~Then make a small change to a Java source file—for example, add a comment:~~

```java
// Testing DevTools
```

~~Save the file.~~

~~Watch the console.~~

~~You may see the application restart automatically.~~

~~The exact console output can vary depending on your IDE and setup, so don't worry if it doesn't look exactly like an example online.~~

~~### The important observation:~~

~~You changed code → Spring Boot detected it → application restarted.~~
🫳🏻

You're absolutely right. **I skipped a step.** I told you:

> "Start your Spring Boot application"

without teaching you **how to start it**.

That violates your instruction to teach only what has been covered.

### For now, don't do the DevTools exercise yet.

We haven't properly learned the ways to run a Spring Boot project. That should be taught before asking you to test DevTools.

For **this session**, you only need to understand what DevTools is:

```text
spring-boot-devtools
        ↓
development convenience
        ↓
can automatically restart the application
when relevant code changes are detected
```

But the actual procedure for:

```text
"How do I start my Spring Boot application?"
```

needs to be explained first.

So let's correct the lesson:

1. Create the project with Spring Initializr.
2. Understand Maven, `pom.xml`, dependencies, project structure.
3. Add DevTools and understand **what it does**.
4. **Do not perform the DevTools exercise yet.**
5. When we reach the point where running the application is actually being taught, I'll show you exactly how to run it and then we can test DevTools.

Good catch. I should not have assumed that step.


***

# 19. One important distinction

Don't confuse these three things:

### Spring Initializr

Creates the **starting project**.

```text
Spring Initializr
       ↓
generates project
```

### Maven

Manages the **project build and dependencies**.

```text
Maven
  ↓
dependencies
build
package
```

### DevTools

Makes **development** more convenient.

```text
DevTools
   ↓
automatic restart
```

They have different jobs.

***

# 20. Your mental model for this session

At this point, you should be able to visualize:

```text
              Spring Initializr
                     │
                     │ generates
                     ↓
             Spring Boot Project
                     │
          ┌──────────┴──────────┐
          ↓                     ↓
       Maven                  Java
          │
          ↓
      pom.xml
          │
          ↓
    Dependencies
          │
          ├── Spring Web
          └── DevTools
```

And the project itself:

```text
landlord/
│
├── src/
│   ├── main/
│   │   ├── java/          ← Java code
│   │   └── resources/     ← configuration/resources
│   │
│   └── test/              ← tests
│
├── pom.xml                ← Maven configuration
└── ...
```

***

# 🧠 Session 2.2 Checkpoint

Don't look back at the lesson if possible. Answer these in your own words:

### 1.

What is Spring Initializr?

### 2.

What is Maven used for?

### 3.

What is the purpose of `pom.xml`?

### 4.

Suppose you have:

```text
Group:    com.example
Artifact: landlord
```

What do these two fields represent?

### 5.

For our project, why are we choosing:

```text
Packaging: Jar
```

### 6.

What is a dependency?

### 7.

What does `spring-boot-devtools` help us with during development?

### 8.

What is the difference between:

```text
src/main/java
```

and

```text
src/main/resources
```

### 9.

Complete this:

```text
Spring Initializr → __________
Maven             → __________
DevTools          → __________
```

**If you can answer those without memorizing definitions, Session 2.2 is understood.**

***

# Footnotes
[^1]: [[what is controller, service, repository in spring-boot]].
