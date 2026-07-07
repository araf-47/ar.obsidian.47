Excellent. Based on what I know about your learning style from our previous Java and JDBC sessions, I'll teach this from **first principles**. I won't assume you know anything, but I'll also explain *why* things work instead of asking you to memorize them.

---

# Day 1 — Module 0.1

# Client vs Server

This is arguably the **most important concept** in web development.

If you truly understand this module, everything else (Tomcat, JSP, Servlets, Spring Boot) becomes much easier.

---

# Imagine This Situation

You open Firefox and type

```text
https://www.google.com
```

Then press **Enter**.

Have you ever wondered what actually happens?

Most people think:

> "The browser opens Google."

That's true...

But **how?**

Let's follow the journey.

```
You
 │
 ▼
Firefox
 │
 ▼
Internet
 │
 ▼
Google's Computer
 │
 ▼
Internet
 │
 ▼
Firefox
 │
 ▼
You see Google
```

There are actually **two computers** involved.

---

# The Client

The computer that **requests** something is called the **Client**.

In our example:

```
Your Laptop
```

is the client.

Your browser (Firefox, Chrome, Edge, etc.) is a **client application**.

Its job is to ask for information.

Example:

> "Please give me Google's homepage."

The browser itself does **not** know what Google's homepage looks like.

It has to ask someone else.

---

# The Server

Somewhere else in the world is another computer.

```
Google's Computer
```

This computer stores:

* webpages
* images
* videos
* search engine logic
* user accounts

This computer waits for requests.

When someone asks,

> "Can I have the homepage?"

it replies with the webpage.

That computer is called a **Server**.

---

# Simple Definition

## Client

A computer or application that **requests** resources.

Examples:

* Firefox
* Chrome
* Mobile App
* Desktop App

---

## Server

A computer or application that **provides** resources.

Examples:

* Google
* Facebook
* YouTube
* Your future Tomcat server

---

# Real Life Analogy

Think of a restaurant.

```
Customer
```

↓

asks

↓

```
Waiter
```

↓

takes order

↓

```
Kitchen
```

↓

prepares food

↓

```
Customer eats
```

Who requested food?

The customer.

The customer is the **Client**.

Who provided food?

The kitchen.

The kitchen is the **Server**.

---

# Another Analogy

Imagine a library.

```
You
```

↓

ask librarian

↓

```
"I need a Java book."
```

↓

Librarian searches

↓

Returns book

You are the **Client**.

The library is the **Server**.

---

# What Does a Client Actually Do?

A client mainly does four things:

* Sends requests
* Receives responses
* Displays information
* Accepts user input

For example:

```
Open Browser

↓

Enter URL

↓

Click Button

↓

Fill Form

↓

Submit Form
```

Everything starts from the client.

---

# What Does a Server Actually Do?

The server:

* Waits for requests
* Processes them
* Reads databases if needed
* Generates a response
* Sends it back

Example:

```
Receive Request

↓

Check Database

↓

Create HTML

↓

Send HTML
```

---

# Can One Computer Be Both?

Yes.

Your own computer can be both a client and a server.

Example:

You install Tomcat.

```
Your Laptop

Tomcat running

Browser running
```

Firefox asks Tomcat for a page.

Even though it's the same physical machine,

Firefox is the **Client**.

Tomcat is the **Server**.

This is called **localhost development**.

---

# Where Does JSP Fit?

Suppose later you build this:

```
Student Management System
```

The browser asks:

```
Show all students.
```

Tomcat receives the request.

Tomcat executes:

```
students.jsp
```

That JSP talks to SQLite.

SQLite returns student data.

JSP creates HTML.

Tomcat sends HTML back.

The browser displays it.

The flow looks like this:

```
Browser
(Client)
      │
      ▼
Tomcat
(Server)
      │
      ▼
JSP
      │
      ▼
JDBC
      │
      ▼
SQLite
      │
      ▲
Student Data
      │
      ▲
HTML Response
      │
      ▲
Browser
```

Notice that **the browser never talks directly to SQLite**. The server sits in the middle.

---

# Why Doesn't the Browser Talk Directly to the Database?

Imagine if it could.

The browser would need to know:

* Database username
* Database password
* Database location

Anyone could inspect the page and steal those credentials.

Instead, the server keeps all of that secret.

Only the server communicates with the database.

This separation improves both security and control.

---

# Common Misconception

Many beginners think:

```
Browser
↓

Database
```

This is **not** how a typical web application works.

The correct flow is:

```
Browser
(Client)

↓

Server (Tomcat)

↓

Application Code
(JSP / Servlet / Java)

↓

JDBC

↓

SQLite Database
```

---

# Key Terms to Remember

| Term    | Meaning                                                      |
| ------- | ------------------------------------------------------------ |
| Client  | Requests resources                                           |
| Server  | Provides resources                                           |
| Browser | A client application                                         |
| Tomcat  | A web server/Servlet container that runs your Java web app   |
| JSP     | Server-side page that generates HTML                         |
| SQLite  | Database storing application data                            |
| JDBC    | Java API used by the server to communicate with the database |

---

# Quick Knowledge Check

Try answering these without looking back:

1. What is the difference between a **client** and a **server**?
2. Is Firefox a client or a server?
3. Is Tomcat a client or a server?
4. Can one physical computer act as both a client and a server? Why?
5. Why shouldn't a browser connect directly to a database?
6. In our future project, who communicates with SQLite: the browser or Tomcat?

If you can answer all six correctly, you've mastered the foundation of client-server architecture. Then we'll move on to **Module 0.2: HTTP Basics**, where we'll examine what is actually inside the messages exchanged between the client and server.

## 1st response
**Excellent.** You got **6/6 correct.** More importantly, your answers show understanding rather than memorization.

Let me expand on a few points so you build a stronger mental model.

---

## 1. Client vs Server ✅

Your answer:

> Client is the one makes the request. Server responds to the request.

Correct.

A slightly more complete definition is:

* **Client** → Initiates communication by requesting a service or resource.
* **Server** → Waits for requests, processes them, and returns a response.

Notice I said **service or resource**.

A server doesn't only send files. It can also:

* Perform calculations
* Authenticate users
* Generate reports
* Send emails
* Process payments
* Query databases

For example:

```
Browser:
"Please log me in."
```

The server doesn't just send a file—it checks your username and password first.

---

## 2. Firefox = Client ✅

Correct.

One thing to remember:

**Firefox is not the client.**

**You are technically the client.**

Firefox is **client software**.

Just like:

* Outlook is an email client.
* Spotify is a music client.
* Discord is a chat client.

---

## 3. Tomcat = Server ✅

Correct.

More precisely:

Tomcat is a **Web Server + Servlet Container**.

We'll learn later why people say "Servlet Container."

---

## 4. One Computer Can Be Both ✅

Exactly.

This is what you'll be doing every day while learning JSP.

Your laptop will look like this:

```
                Your Laptop

+----------------------------------------+

Firefox  -----------------------> Tomcat
(Client)                       (Server)

                     |
                     |
                     V

                SQLite Database

+----------------------------------------+
```

Everything runs on one computer.

Professionally, these may all be separate machines, but conceptually the flow is identical.

---

## 5. Browser → Database ❌

Your answer is correct.

Let's think a little deeper.

Suppose browsers could connect directly to SQLite.

Then your login page would have to contain something like:

```text
Database: students.db

Username: admin

Password: secret123
```

Anyone could press **F12** (Developer Tools) and inspect the page.

Game over.

Now imagine a banking website.

The browser knowing the bank's database password would be catastrophic.

So instead:

```
Browser

↓

Tomcat

↓

SQLite
```

Only Tomcat knows:

* where the database is
* how to connect
* database credentials (if required)
* SQL queries

The browser never sees any of that.

---

## 6. Tomcat Talks to SQLite ✅

Perfect.

This is the architecture we'll build.

```
User
 │
 ▼
Browser
 │
 ▼
HTTP Request
 │
 ▼
Tomcat
 │
 ▼
Servlet
 │
 ▼
DAO
 │
 ▼
JDBC
 │
 ▼
SQLite
```

Everything after Tomcat happens **inside the server**.

The browser has no idea what happens there.

---

## The Biggest Beginner Misconception

I want to fix something that confuses almost everyone.

Many beginners think:

```
Browser
      │
      ▼
JSP
```

Actually...

```
Browser
      │
      ▼
Tomcat
      │
      ▼
JSP
```

Tomcat executes the JSP.

The browser **never sees JSP code**.

---

Suppose you write:

```jsp
<h1>Hello</h1>

<%= 2 + 3 %>
```

Tomcat executes it.

The browser receives only:

```html
<h1>Hello</h1>

5
```

The browser never receives:

```jsp
<%=2+3%>
```

This is extremely important.

---

# Another Important Concept

People often say:

> "The browser opens index.jsp."

That statement isn't technically correct.

What actually happens is:

```
Browser requests index.jsp

↓

Tomcat receives request

↓

Tomcat executes index.jsp

↓

Tomcat creates HTML

↓

Tomcat sends HTML

↓

Browser displays HTML
```

The browser never executes JSP.

It only knows HTML, CSS, and JavaScript.

---

# Mental Model (Memorize This)

Think of JSP as a chef in a restaurant.

```
Customer (Browser)

↓

Waiter (Tomcat)

↓

Chef (JSP)

↓

Kitchen (SQLite)

↓

Food (HTML)

↓

Customer
```

The customer never enters the kitchen.

Similarly:

The browser never enters SQLite.

---

# Mini Challenge

Let's see if your understanding is deep enough.

Suppose you create this file:

```jsp
<h1>Welcome</h1>

Current Year:

<%= 2026 %>
```

### Question 1

What will the browser finally receive?

A)

```jsp
<h1>Welcome</h1>

Current Year:

<%=2026%>
```

or

B)

```html
<h1>Welcome</h1>

Current Year:

2026
```

---

### Question 2

Who executes the `<%= 2026 %>` expression?

* Browser
* SQLite
* Tomcat
* Firefox

---

### Question 3

Imagine your SQLite database suddenly crashes.

Will the browser still be able to show student records?

Why or why not?

Answer these three questions, and if they're correct, we'll move on to **Module 0.2: HTTP Basics**, where we'll learn what an HTTP request and response actually look like "on the wire."

## 🔻
**Perfect.** That's **3/3**. More importantly, your explanation for Question 3 shows you're reasoning about the architecture instead of guessing.

Let's refine it slightly.

---

## Question 1 ✅

You answered:

> **B**

Correct.

The browser receives:

```html
<h1>Welcome</h1>

Current Year:

2026
```

Notice something interesting.

The browser has **no evidence that JSP even existed**.

From the browser's perspective, it simply received HTML.

---

## Question 2 ✅

You answered:

> Tomcat

Exactly.

The sequence is:

```text
Browser
    │
    ▼
Tomcat
    │
    ▼
JSP Engine
    │
    ▼
Generated HTML
    │
    ▼
Browser
```

The browser never executes JSP.

---

## Question 3 ✅

Your answer:

> Browser won't be able to show the record because the records are in the database and JSP/JDBC won't be able to communicate with it.

Exactly.

Let's visualize it.

### Normal case

```text
Browser
↓
Tomcat
↓
JSP / Servlet
↓
JDBC
↓
SQLite ✅
↓
Student Data
↓
HTML
↓
Browser
```

Everything works.

---

### Database crashes

```text
Browser
↓
Tomcat
↓
JSP / Servlet
↓
JDBC
↓
SQLite ❌
```

Now JDBC tries something like:

```java
SELECT * FROM students;
```

SQLite doesn't respond.

JDBC throws an exception (for example, a `SQLException`).

Tomcat cannot generate the student list.

Instead of student records, the user may see:

* an error page,
* a friendly "Database unavailable" message (if you've handled the error well), or
* an HTTP 500 Internal Server Error.

The browser isn't "broken"—it simply displays whatever response the server sends.

---

# A Small but Important Mindset Shift

This will help throughout your web development journey.

Many beginners think:

> "The browser opens the database."

It doesn't.

The browser only knows one thing:

> "I'm talking to a server."

It doesn't know:

* whether the server uses SQLite,
* PostgreSQL,
* MySQL,
* Oracle,
* or even no database at all.

The browser simply sends a request and waits for a response.

This is one of the biggest strengths of client-server architecture: **the client doesn't need to know how the server does its job.**

---

# Think Like an Engineer

Imagine that, a year from now, you decide to replace SQLite with PostgreSQL.

Will the browser need to change?

**No.**

The flow becomes:

```text
Browser

↓

Tomcat

↓

JSP / Servlet

↓

JDBC

↓

PostgreSQL
```

The browser still receives HTML.

It doesn't know—and doesn't need to know—that the database changed.

This separation of responsibilities is a core design principle in software engineering.

---

# What You've Learned So Far

You should now clearly understand:

* ✅ What a client is
* ✅ What a server is
* ✅ Why Tomcat is needed
* ✅ Why browsers don't connect directly to databases
* ✅ Why JSP runs on the server
* ✅ Why browsers only receive HTML
* ✅ How the browser, Tomcat, JSP, JDBC, and SQLite fit together

That foundation will make the rest of JSP much easier to understand.

---

## Ready for Module 0.2: HTTP Basics

In the next module, we'll answer questions like:

* What exactly is **HTTP**?
* What is inside an **HTTP request**?
* What is inside an **HTTP response**?
* What are **headers**?
* Why do we use **GET** and **POST**?
* What are **404**, **403**, **500**, and **200** status codes?
* What actually travels between the browser and Tomcat?



# 👉 [[Module 0.2 - HTTP Basics]].
