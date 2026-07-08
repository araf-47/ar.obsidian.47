
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
* [[Java expression]]s

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

==The most important folder for beginners==.

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


# Answer and feedback
Fantastic. **This is a solid 7/7.** 🎉

More importantly, your answers show that you're building a **mental model** instead of memorizing definitions. That's exactly how I wanted to teach this course.

Let's review them.

---

# Question 1 ✅

Your answer:

> It is server that listens to port 8080. receive requests, manage them, and provide appropriate response. It also manages cookies and sessions.

Excellent.

I'd only make one small improvement.

Instead of saying:

> "It is a server..."

Say:

> **"Apache Tomcat is a Java web server and Servlet container."**

Why?

Because later you'll learn there are different kinds of servers:

* Web Server (Tomcat)
* Database Server (PostgreSQL)
* FTP Server
* Mail Server

Being precise now will help later.

---

# Question 2 ✅

Perfect.

You correctly identified that JSP is **not** a Java source file.

It contains:

* HTML
* JSP tags
* Java expressions

Tomcat converts it into a Servlet before Java can compile and execute it.

Excellent.

---

# Question 3 ✅

You listed:

* listens on 8080
* converts JSP to Servlet
* manages sessions/cookies
* receives requests
* sends HTML responses

Excellent.

There are even more responsibilities (loading applications, serving static files, etc.), but these five are exactly what I wanted you to remember.

---

# Question 4 ✅

Tomcat.

Correct.

The request never goes directly to a JSP.

This is one of the most important ideas we've repeated several times.

```
Browser
    │
HTTP
    ▼
Tomcat
    │
    ▼
Servlet / JSP
```

---

# Question 5 ✅

> All of my web applications live there.

Exactly.

Later your folder might look like:

```
webapps/

├── StudentManagement/
├── LibrarySystem/
└── ROOT/
```

Each folder is a separate web application.

---

# Question 6 ✅

Excellent reasoning.

You gave **two independent reasons**, and both are correct.

Reason 1:

> There is no server.

Correct.

Reason 2:

> Tomcat converts JSP into a Servlet.

Also correct.

That's a much better answer than simply saying:

> "Because it doesn't work."

---

# Question 7 ⭐⭐⭐

Correct.

Deleting:

```
logs/
```

does **not** break Tomcat.

You'll simply lose previous log files.

In fact, many administrators periodically remove old logs to free disk space.

When Tomcat starts again, it usually recreates the directory and begins writing new logs.

---

# ⭐ **One Small Technical Improvement**

Earlier you wrote:

> Tomcat sends HTML response.

That's true **most of the time**, but I want to refine it now.

==Tomcat actually sends an== **HTTP response**.

==That response body might contain==:

* HTML ✅
* JSON (later with Spring Boot)
* CSS
* JavaScript
* Images
* PDF files

So a more general statement is:

> **Tomcat sends an HTTP response.**

If the requested resource is a JSP, that response body usually contains HTML.

---

# 🧠 Let's Connect Everything You've Learned So Far

Without realizing it, you've built a complete mental model of how a JSP application works.

```
                    USER
                      │
                      ▼
                 Firefox
                      │
               HTTP Request
                      │
                      ▼
                 localhost
                      │
                Port 8080
                      │
                      ▼
          Apache Tomcat
                      │
        ┌─────────────┴─────────────┐
        │                           │
        ▼                           ▼
   Static File                 JSP / Servlet
                                    │
                                    ▼
                                 JDBC
                                    │
                                    ▼
                                 SQLite
                                    │
                                    ▼
                           Generate HTML
                                    │
                                    ▼
                          HTTP Response
                                    │
                                    ▼
                                Firefox
```

Notice something interesting.

**We haven't written a single line of JSP yet.**

Yet you already know where every piece fits.

This is why I insisted on spending time on Module 0.

---

# 📚 Module 1 Progress

We've completed:

* ✅ 1.1 What is Tomcat?
* ✅ Tomcat Responsibilities
* ✅ Basic Directory Overview

Next, we'll study something that almost nobody explains properly:

# ➡️ [[Module 1.2 — Inside the Tomcat Directory]]. 

We're going to open **every important folder** in:

```
/home/araf/server/apache-tomcat-9.0.119
```

and answer questions like:

* Why is there both `webapps/` **and** `work/`?
* What is `conf/server.xml`?
* What is `web.xml`?
* Why is there a `lib/` folder if Java already has libraries?
* What exactly happens when you put your project into `webapps/`?
* What is the `ROOT` application?
* What is the `manager` application?
* What is `catalina.sh` vs `startup.sh`?
* Why do `startup.sh` and `shutdown.sh` exist if they both call the same script?

By the end of that module, you'll be comfortable navigating your Tomcat installation like someone who has been using it for months instead of days.

I consider this one of the most practical Tomcat lessons because you'll be able to look at your installation and immediately know **what each folder is for and when you might need it**.
