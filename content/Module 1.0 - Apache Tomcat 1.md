Perfect, and thanks for the correction. From now on, I'll use your actual Tomcat installation path:

```text
/home/araf/server/apache-tomcat-9.0.119
```

---

# Day 1 - Module 1

# Apache Tomcat

## Learning Objectives

By the end of this module, you will understand:

* What Tomcat actually is
* Why JSP needs Tomcat
* What happens when Tomcat starts
* Every important folder inside Tomcat
* How Tomcat processes requests
* How to start and stop Tomcat from Linux
* What deployment means

---

# First, Let's Correct a Very Common Misconception

Many beginners think:

> Tomcat runs JSP.

That statement is **partially true**, but it's incomplete.

Tomcat does **much more** than simply "running JSP."

Think of Tomcat as the **manager of an entire web application**.

---

# Imagine You Own a Restaurant

Customers arrive.

Someone has to:

* Open the door
* Seat customers
* Take orders
* Send orders to the kitchen
* Deliver food
* Handle payments

The chef only cooks.

The restaurant manager coordinates everything.

Tomcat is the manager.

JSP is one of the chefs.

---

# So What Exactly is Tomcat?

Let's build the definition from scratch.

Tomcat is a Java program.

When you start it,

```bash
/home/araf/server/apache-tomcat-9.0.119/bin/startup.sh
```

you're simply starting another Java application.

But this Java application has a very special job.

Its job is to:

* Listen for HTTP requests
* Run Servlets
* Run JSP pages
* Manage Sessions
* Manage Cookies
* Serve static files
* Send HTTP Responses

---

## Definition

> **Apache Tomcat is a Java Web Server and Servlet Container that executes Java web applications.**

Don't worry if "Servlet Container" sounds unfamiliar.

We'll build that understanding gradually.

---

# What Does Tomcat Actually Do?

Imagine you type:

```text
http://localhost:8080
```

The flow is:

```text
Browser

↓

HTTP Request

↓

Tomcat

↓

Find Application

↓

Find Resource

↓

Execute JSP / Servlet

↓

Generate HTML

↓

HTTP Response

↓

Browser
```

Tomcat is responsible for almost everything in the middle.

---

# Why Can't JSP Run by Itself?

Let's compare it to a normal Java program.

You wrote this before:

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

You can run it like this:

```bash
java Hello
```

Easy.

---

Now imagine this JSP:

```jsp
<h1>Hello</h1>

<%= 2 + 3 %>
```

Can you run:

```bash
java index.jsp
```

No.

Why?

Because a JSP is **not a Java program**.

It contains:

* HTML
* JSP syntax
* Java expressions

It must first be converted into a Servlet.

Tomcat performs that conversion automatically.

Without Tomcat (or another Servlet container), a JSP file is just text.

---

# Tomcat's Main Responsibilities

Let's list its jobs.

### 1. Listen for HTTP Requests

Tomcat waits on port:

```text
8080
```

When Firefox sends:

```http
GET / HTTP/1.1
```

Tomcat receives it.

---

### 2. Manage Web Applications

Tomcat may host multiple applications.

Imagine:

```text
Tomcat

├── StudentManagement
├── Blog
├── Hospital
└── Library
```

Tomcat knows which application should handle each request.

---

### 3. Execute Servlets

Later you'll write:

```java
public class StudentServlet extends HttpServlet
```

Tomcat creates the object.

Tomcat calls:

```java
doGet()

doPost()
```

You never call them yourself.

---

### 4. Convert JSP to Servlet

Suppose you create:

```text
index.jsp
```

Tomcat internally does something like:

```text
index.jsp

↓

Generated Java Servlet

↓

Compile

↓

Run
```

This is one of Tomcat's coolest features.

---

### 5. Session Management

Earlier we learned:

HTTP is stateless.

Tomcat provides:

```java
session.setAttribute()

session.getAttribute()

session.invalidate()
```

Tomcat manages those sessions.

---

### 6. Cookie Management

Tomcat automatically reads cookies sent by the browser.

It can also send cookies back.

---

### 7. Serve Static Files

Tomcat also serves:

```text
style.css

logo.png

app.js

favicon.ico
```

Not every request needs JSP.

Sometimes it's just:

> "Please send this image."

---

# Tomcat Architecture

Here's a simplified view.

```text
                 Browser
                     │
             HTTP Request
                     │
                     ▼
            +----------------+
            |     Tomcat     |
            +----------------+
             │      │      │
             │      │      │
             ▼      ▼      ▼
         Servlet   JSP   Static Files
             │      │
             ▼      ▼
             JDBC
               │
               ▼
            SQLite
               │
               ▼
        HTTP Response
               │
               ▼
            Browser
```

Everything passes through Tomcat.

---

# Your Tomcat Directory

Let's use your installation.

```text
/home/araf/server/apache-tomcat-9.0.119
```

Inside you'll find something like:

```text
apache-tomcat-9.0.119/

├── bin
├── conf
├── lib
├── logs
├── temp
├── webapps
├── work
└── webapps.dist
```

Some additional files may also be present.

Over the next lessons, we'll understand each important directory.

---

# The Most Important Directories

We'll focus on these.

```text
bin/
```

Scripts for starting and stopping Tomcat.

---

```text
conf/
```

Configuration files.

Port number.

Server settings.

Users.

Hosts.

---

```text
lib/
```

Libraries (JAR files) that Tomcat needs.

---

```text
logs/
```

Log files.

Very useful for debugging.

---

```text
temp/
```

Temporary files.

Usually safe for Tomcat to manage.

---

```text
webapps/
```

The most important folder for beginners.

Your web applications live here.

Later, your Student Management project will be deployed here.

---

```text
work/
```

Tomcat's working directory.

This is where compiled JSP artifacts are typically stored.

We'll explore this later when discussing the JSP lifecycle.

---

# How Tomcat Starts

When you run:

```bash
cd /home/araf/server/apache-tomcat-9.0.119/bin

./startup.sh
```

Tomcat roughly performs these steps:

1. Starts the Java Virtual Machine (JVM).
2. Reads configuration from `conf/`.
3. Loads required libraries from `lib/`.
4. Starts listening on port 8080.
5. Deploys applications from `webapps/`.
6. Waits for incoming HTTP requests.

Then it sits idle until a request arrives.

---

# A Mental Model

Think of Tomcat as an office building.

```text
Browser

↓

Reception

↓

Tomcat

↓

Correct Department

↓

Servlet

↓

Database

↓

Response

↓

Browser
```

Tomcat is never "doing your business logic."

It coordinates everything and forwards work to the appropriate component.

---

# Knowledge Check

Let's make sure you've built the right mental model.

### Question 1

What is Apache Tomcat?

Try to explain it in your own words.

---

### Question 2

Why can't we simply run a JSP file using:

```bash
java index.jsp
```

---

### Question 3

Name at least **five responsibilities** of Tomcat.

---

### Question 4

Suppose Firefox requests:

```text
http://localhost:8080/index.jsp
```

Who receives the HTTP request first?

* Firefox
* JSP
* Tomcat
* SQLite

---

### Question 5

What is the purpose of the `webapps/` directory?

---

### Question 6

If Tomcat is stopped, can your JSP page run?

Why or why not?

---

### Question 7 (Thinking Question)

Imagine you accidentally delete the entire `logs/` directory.

What do you think will happen?

* Tomcat won't start.
* Tomcat starts but loses old log history.
* Your JSP files stop working.

Don't worry if you're unsure. I want to see how you're reasoning. We'll use your answer to discuss how important logs really are in day-to-day development.
