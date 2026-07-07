Awesome! This is one of my favorite topics because **HTTP is the foundation of every web framework**. JSP, Servlets, Spring Boot, Django, ASP.NET, Node.js—they all exist on top of HTTP.

---

# Day 1 - Module 0.2

# HTTP Basics

## Learning Objectives

By the end of this module, you should be able to answer:

* What is HTTP?
* Why do we need HTTP?
* What is a Request?
* What is a Response?
* Who sends what?
* What are Headers?
* What is a Status Code?
* How does Tomcat understand a browser?

---

# 1. Why Do We Need HTTP?

Let's start with a problem.

Imagine you're in Bangladesh and your friend is in Japan.

You call them.

If you both start talking in completely different languages, what happens?

```
You:  আমি ভাত খাই।
Friend: 私は分かりません。
```

Neither understands the other.

So what do you need?

A **common language**.

---

Computers have the same problem.

Your browser and Tomcat are two different programs.

How should they communicate?

They need a common language.

That language is called **HTTP**.

---

## Definition

**HTTP** stands for:

> **HyperText Transfer Protocol**

Let's break that down.

### HyperText

Originally meant HTML pages containing links (hyperlinks).

Nowadays HTTP is used to transfer much more than HTML:

* HTML
* CSS
* JavaScript
* Images
* PDFs
* JSON
* Videos
* Audio

---

### Transfer

Move data.

From one computer...

...to another.

---

### Protocol

This is the important word.

A **protocol** is simply:

> **A set of rules that both sides agree to follow.**

Examples from everyday life:

* Traffic rules
* Chess rules
* Football rules

HTTP is just a communication rulebook.

---

# Definition (Simple)

> HTTP is the set of rules that browsers and web servers use to communicate.

---

# 2. Client and Server Speak HTTP

Remember last lesson?

```
Browser
      │
      ▼
Tomcat
```

Now let's add HTTP.

```
Browser

      │

 HTTP Request

      │

      ▼

Tomcat

      │

HTTP Response

      │

      ▼

Browser
```

Notice:

Both directions use HTTP.

---

# 3. Every Communication Has Two Parts

Think of ordering pizza.

You say:

> "I'd like one large pizza."

That's a request.

The restaurant gives you:

> "Here's your pizza."

That's a response.

Web applications work exactly the same way.

---

# HTTP Request

A request asks for something.

Example:

```
Please give me:

index.jsp
```

---

# HTTP Response

The server replies:

```
Okay.

Here is the HTML.
```

---

# Visual Flow

```
Browser
(Client)

    │

Request

    ▼

Tomcat

    │

Processes JSP

    │

Response

    ▼

Browser
```

---

# 4. A Real Example

Suppose you visit

```
http://localhost:8080/
```

What happens?

Step 1

Browser sends

```
HTTP Request
```

Step 2

Tomcat receives it.

Step 3

Tomcat processes it.

Step 4

Tomcat sends

```
HTTP Response
```

Step 5

Browser displays the page.

---

# 5. What Does an HTTP Request Look Like?

Here's a simplified request:

```http
GET /index.jsp HTTP/1.1
Host: localhost:8080
User-Agent: Firefox
Accept: text/html
```

Don't panic.

We'll understand every line.

---

### First Line

```http
GET /index.jsp HTTP/1.1
```

This means:

* I want to **GET** something.
* I want `/index.jsp`.
* I'm using HTTP version 1.1.

---

### Host

```http
Host: localhost:8080
```

Which server?

```
localhost

Port 8080
```

---

### User-Agent

```http
User-Agent: Firefox
```

The browser identifies itself.

Servers sometimes change behavior depending on the client.

---

### Accept

```http
Accept: text/html
```

Meaning:

"I can understand HTML."

---

# 6. What Does the Server Respond With?

Example:

```http
HTTP/1.1 200 OK
Content-Type: text/html

<html>
<body>

Hello

</body>
</html>
```

Again...

We'll understand every line.

---

### Status Line

```http
HTTP/1.1 200 OK
```

Meaning:

Everything worked.

---

### Content-Type

```http
Content-Type: text/html
```

Tomcat tells Firefox:

"I'm sending HTML."

If it were a PNG image, it might be:

```http
Content-Type: image/png
```

If it were a PDF:

```http
Content-Type: application/pdf
```

This tells the browser how to interpret the data.

---

### Response Body

Everything after the blank line is the actual content:

```html
<html>
<body>

Hello

</body>
</html>
```

Firefox renders this into the web page you see.

---

# 7. What Is a Header?

A header is **metadata**.

Think of it as information *about* the message, not the message itself.

Example:

Suppose someone mails you a package.

Outside the box:

* Sender
* Receiver
* Weight
* Fragile

That's metadata.

Inside the box:

* The actual item you ordered.

HTTP works the same way.

```
Headers
↓
Information about the message
↓
Body
↓
Actual data
```

---

## Example Request

```http
GET /students HTTP/1.1
Host: localhost:8080
User-Agent: Firefox
Accept: text/html
```

Everything except the first line and the blank line consists of headers.

---

# 8. Status Codes

One of the most useful parts of HTTP.

The server doesn't just send data.

It also tells the browser what happened.

---

## 200 OK

Everything succeeded.

```
Browser
↓
Show page
```

---

## 404 Not Found

Requested page doesn't exist.

Example:

```
localhost:8080/abc.jsp
```

but

```
abc.jsp
```

doesn't exist.

Tomcat replies:

```
404
```

---

## 500 Internal Server Error

The page exists...

but something went wrong while processing it.

Example:

```java
int x = 10 / 0;
```

or

```java
Connection connection = null;
connection.createStatement();
```

The server encountered an unexpected error.

---

## 403 Forbidden

The server understood the request...

but refuses to allow access.

Example:

Trying to access an admin-only page without permission.

---

## 301 / 302 Redirect

Instead of returning the requested page, the server says:

> "The resource has moved. Go over there instead."

Your browser automatically follows the new location.

---

# Quick Summary

```
Browser
↓
HTTP Request
↓
Tomcat
↓
Process JSP
↓
HTTP Response
↓
Browser
```

Every single interaction between a browser and a web server follows this basic pattern.

---

# Real-Life Example: Student Management System

Imagine we build:

```
http://localhost:8080/student/list
```

When you visit it:

```
Browser

↓

HTTP Request

GET /student/list

↓

Tomcat

↓

Servlet

↓

DAO

↓

SQLite

↓

Student Records

↓

JSP

↓

Generated HTML

↓

HTTP Response

↓

Browser
```

Notice something important:

The browser never sees:

* SQL queries
* Java code
* JDBC code
* SQLite database

It only sees the final HTML returned in the response.

---

# Knowledge Check

Let's test your understanding before we move on.

### Question 1

Why do browsers and servers need HTTP? Why can't they just "talk" without it?

---

### Question 2

What is the difference between an **HTTP Request** and an **HTTP Response**?

---

### Question 3

Who sends the HTTP Request?

* Browser
* Tomcat
* SQLite

---

### Question 4

Who sends the HTTP Response?

* Browser
* Tomcat
* SQLite

---

### Question 5

What is the purpose of an HTTP header?

(Answer in your own words.)

---

### Question 6

Suppose you type:

```
http://localhost:8080/unknown.jsp
```

The file doesn't exist.

What status code do you expect?

Why?

---

### Question 7 (Thinking Question)

Suppose your browser sends this request:

```http
GET /students HTTP/1.1
Host: localhost:8080
```

Can SQLite read this request directly?

If not, who reads it first, and why?

Take your time. These questions are designed to make sure you're building a solid mental model before we dive into GET vs. POST and the anatomy of URLs in the next modules.

# Answer and feedback
Excellent! I'd give this **6.5/7**. You're understanding the concepts instead of memorizing definitions, which is exactly what we want.

Let's review each answer.

---

## Question 1 ✅

Your answer:

> They are different programs; they need a common protocol like HTTP (a set of agreed-upon rules) to talk to each other.

Perfect.

That's exactly what a protocol is.

Think of HTTP as the **grammar** of a conversation between a browser and a web server.

---

## Question 2 ✅

Your answer:

> Request is sent from browser asking for a response like index.jsp. Response comes from server.

Correct.

A slightly more formal way to think about it is:

* **Request** → "I want something."
* **Response** → "Here's the result."

---

## Question 3 ✅

Browser.

Correct.

---

## Question 4 ✅

Tomcat.

Correct.

Technically, **your web application running inside Tomcat** creates the response, and Tomcat sends it back to the browser.

---

## Question 5 ✅

Your answer:

> It has the information about the response like a label on a sealed box.

I love this analogy.

Exactly.

Headers describe the message.

Examples include:

```http
Content-Type: text/html

Content-Length: 528

User-Agent: Firefox

Host: localhost:8080
```

Notice these aren't the webpage itself—they're information *about* the webpage or request.

---

## Question 6 ✅

404.

Correct.

The page doesn't exist.

Simple.

---

## Question 7 ⭐

Your answer:

> No.
> I think it's jsp engine or something.

You're very close.

This is where I want to sharpen your mental model.

---

### What Actually Happens?

Suppose the browser sends:

```http
GET /students HTTP/1.1
Host: localhost:8080
```

Who receives it first?

Not the JSP engine.

The answer is:

### **Tomcat**

Think of Tomcat as the receptionist of a company.

```
Visitor

↓

Receptionist (Tomcat)

↓

Correct Department
```

Tomcat receives **every** HTTP request.

Then Tomcat asks:

> "What resource did they request?"

If it's:

```
index.html
```

Tomcat sends the HTML file.

If it's:

```
students.jsp
```

Tomcat forwards it to the JSP engine.

If it's:

```
/student/list
```

Tomcat forwards it to the appropriate Servlet.

So the real flow is:

```
Browser

↓

HTTP Request

↓

Tomcat

↓

JSP Engine / Servlet

↓

JDBC

↓

SQLite
```

SQLite never understands HTTP.

SQLite only understands SQL.

For example:

```sql
SELECT * FROM students;
```

That SQL command is created by your Java code using JDBC—not by the browser.

---

# This Is One of the Biggest Ideas in Web Development

Notice that each component speaks a different "language":

```
Browser
      │
      │ HTTP
      ▼
Tomcat
      │
      │ Java Method Calls
      ▼
Servlet / JSP
      │
      │ JDBC API
      ▼
JDBC Driver
      │
      │ SQL
      ▼
SQLite
```

Let's translate that into plain English:

* **Browser ↔ Tomcat:** HTTP
* **Tomcat ↔ JSP/Servlet:** Java method calls inside the same JVM
* **JSP/Servlet ↔ JDBC:** Java API
* **JDBC ↔ SQLite:** SQL commands

This layered communication is what makes the whole system work.

---

# A Small Preview of What's Coming

Later, when we write something like:

```java
PreparedStatement ps =
    connection.prepareStatement(
        "SELECT * FROM students"
    );
```

Here's what's happening behind the scenes:

```
Browser
      │
HTTP
      ▼
Tomcat
      │
Java
      ▼
Servlet
      │
JDBC
      ▼
SQLite
```

Every layer has its own responsibility and its own protocol or API.

---

# Congratulations 🎉

You've now mastered the first two foundational topics:

* ✅ Client vs. Server
* ✅ HTTP Basics

Most beginners rush past these ideas, but they're the foundation for everything else in Java web development.

When we get to Servlets, JSP, and Spring Boot, you'll already understand *why* each piece exists instead of just learning the syntax.

---

## Next Module: 0.3 — HTTP Methods (GET vs. POST)

This is one of the most practical topics you'll learn.

We'll answer questions like:

* Why does clicking a link usually send a **GET** request?
* Why do login forms usually use **POST**?
* Why shouldn't you use **GET** for passwords?
* What exactly gets sent over the network in each case?
* How does `request.getParameter()` retrieve form data?

This module will directly prepare you for handling HTML forms in JSP and Servlets.

# 👉 [[Module 0.3 - HTTP Methods (GET vs. POST)]].
