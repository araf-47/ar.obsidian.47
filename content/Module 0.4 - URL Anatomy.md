Excellent. This module is much shorter than the previous ones, but it is **extremely practical**. Every time you write a link, configure Tomcat, or use JSP/Servlets, you'll be dealing with URLs.

By the end of this lesson, you'll be able to look at a URL and explain **every single part of it**.

---

# Day 1 – Module 0.4

# URL Anatomy

---

# Learning Objectives

By the end of this module, you should be able to:

* Explain what a URL is.
* Identify every part of a URL.
* Understand what `localhost` means.
* Understand what a port is.
* Know what a context path is.
* Know what query parameters are.
* Understand how Tomcat uses URLs to find your application.

---

# 1. What is a URL?

**URL** stands for:

> **Uniform Resource Locator**

That's a formal name.

A simpler definition is:

> **A URL is the address of a resource on a network.**

Think of it like your home address.

If someone wants to visit your house, they need your address.

Similarly, if a browser wants a webpage, it needs the webpage's address.

That address is the URL.

---

# Example URL

Let's use one we'll actually see later.

```text
http://localhost:8080/StudentManagement/students?id=5
```

At first glance, it looks complicated.

Let's break it into pieces.

---

## The Complete Structure

```text
http://localhost:8080/StudentManagement/students?id=5
│      │         │      │                 │
│      │         │      │                 └── Query Parameter
│      │         │      └──────────────────── Resource Path
│      │         └────────────────────────── Port
│      └──────────────────────────────────── Host
└─────────────────────────────────────────── Protocol
```

We'll examine each part.

---

# 2. Protocol (Scheme)

```text
http://localhost:8080/StudentManagement/students?id=5
^^^^
```

This tells the browser **which communication protocol to use**.

Common ones are:

* `http`
* `https`
* `ftp` (older file transfer protocol)

For now, you'll mostly use:

```text
http
```

because Tomcat's default configuration doesn't use HTTPS.

---

## HTTP vs HTTPS

| HTTP                    | HTTPS                            |
| ----------------------- | -------------------------------- |
| No encryption           | Encrypted                        |
| Used for local learning | Used on most production websites |
| Port 80 (default)       | Port 443 (default)               |

Later, we'll learn how HTTPS protects data such as passwords.

---

# 3. Host

```text
http://localhost:8080/StudentManagement/students?id=5
       ^^^^^^^^^
```

The host tells the browser:

> **Which computer should receive this request?**

---

## During Learning

You'll mostly see:

```text
localhost
```

What does that mean?

It literally means:

> **"My own computer."**

So when you visit:

```text
http://localhost:8080
```

you're telling Firefox:

> "Send this request back to my own machine."

---

## Another Way to Write It

These are equivalent:

```text
http://localhost:8080
```

and

```text
http://127.0.0.1:8080
```

`127.0.0.1` is known as the **loopback IP address**.
==It always points back to the same computer==.

---

# 4. Port

```text
http://localhost:8080/StudentManagement/students?id=5
                 ^^^^
```

This confuses almost every beginner.

Let's use an analogy.

---

## Apartment Building Analogy

Imagine this address:

```text
City
↓

Apartment Building
↓

Apartment Number
```

Many people live in the same building.

How do you know which apartment to visit?

You use the apartment number.

A computer works similarly.

One computer can run many services:

* Tomcat
* SSH
* Dropbox
* PostgreSQL
* Web server

How does the browser know which service it wants?

By using a **port**.

---

## Example

Your computer:

```text
Laptop
```

Running:

```text
Tomcat
```

Tomcat listens on:

```text
8080
```

Firefox says:

> "I want to talk to the program listening on port **8080**."

---

### Common Ports

| Port | Service                          |
| ---- | -------------------------------- |
| 80   | HTTP                             |
| 443  | HTTPS                            |
| 22   | SSH                              |
| 5432 | PostgreSQL                       |
| 3306 | MySQL                            |
| 8080 | Tomcat (default for development) |

---

# 5. ==Context Path==

==This is one of the most important parts for JSP==.

Look at:

```text
http://localhost:8080/StudentManagement/students?id=5
                      ^^^^^^^^^^^^^^^^^
```

This is called the **context path**.

Think of Tomcat as a shopping mall.

Inside the mall are many stores.

```text
Tomcat

├── StudentManagement
├── LibrarySystem
├── Blog
└── Hospital
```

Each application has its own "store."

The context path tells Tomcat:

> "Which web application should handle this request?"

If your application folder is:

```text
StudentManagement
```

then the context path is:

```text
/StudentManagement
```

---

# 6. Resource Path

```text
http://localhost:8080/StudentManagement/students?id=5
                                         ^^^^^^^^^
```

This identifies **what inside your application** is being requested.

It might refer to:

* a JSP,
* a Servlet,
* an image,
* a CSS file,
* or another resource.

Examples:

```text
/index.jsp
```

```text
/students
```

```text
/login
```

```text
/css/style.css
```

In a Servlet application, `/students` is often mapped to a Servlet rather than a physical file.

---

# 7. Query Parameters

```text
http://localhost:8080/StudentManagement/students?id=5
                                                  ^^^^
```

Everything after the `?` is the **query string**.

The query string contains **parameters**.

Example:

```text
?id=5
```

This means:

Parameter name:

```text
id
```

Parameter value:

```text
5
```

---

## Multiple Parameters

```text
/search?name=Alice&department=CSE
```

Here we have:

| Name       | Value |
| ---------- | ----- |
| name       | Alice |
| department | CSE   |

Notice that multiple parameters are separated by `&`.

---

# 8. How Does Java Read Query Parameters?

Suppose the URL is:

```text
/students?id=5
```

In a Servlet or JSP, you can read it like this:

```java
String id = request.getParameter("id");
```

The result is:

```text
5
```

This is exactly the same method you'll use later to read form fields submitted via POST.

That's one reason the Servlet API is so convenient.

---

# 9. Putting It All Together

Let's decode the full URL:

```text
http://localhost:8080/StudentManagement/students?id=5
```

| Part            | Value               | Meaning                               |
| --------------- | ------------------- | ------------------------------------- |
| Protocol        | `http`              | Use HTTP                              |
| Host            | `localhost`         | My own computer                       |
| Port            | `8080`              | Talk to Tomcat                        |
| Context Path    | `StudentManagement` | Choose this web application           |
| Resource Path   | `students`          | Request the student list/page         |
| Query Parameter | `id=5`              | Pass the value `5` to the application |

---

# How Tomcat Processes It

Suppose Firefox requests:

```text
http://localhost:8080/StudentManagement/students?id=5
```

Tomcat thinks something like:

1. "The request is for me because it's on port 8080."
2. "The application is `StudentManagement`."
3. "Inside that application, the requested resource is `/students`."
4. "There's also a parameter: `id = 5`."

Your Java code can then decide what to do with that ID—perhaps load student number 5 from SQLite.

---

# Mental Model

Think of the URL like a postal address.

```text
Protocol
↓

	Country

Host
↓

	City

Port
↓

	Apartment Building

Context Path
↓

	Floor

Resource Path
↓

	Room

Query Parameters
↓

	Message for the Person Inside
```

It's not a perfect analogy, but it helps remember that each part has a different job.

---

# Knowledge Check

Let's see if you've mastered URLs.

### Question 1

What is a URL?

---

### Question 2

In this URL:

```text
http://localhost:8080/StudentManagement/students?id=12
```

What does **`localhost`** mean?

---

### Question 3

What is the purpose of a **port**?

Why isn't the host name alone enough?

---

### Question 4

What is the **context path** in this URL?

```text
http://localhost:8080/StudentManagement/students?id=12
```

---

### Question 5

What is the **resource path**?

---

### Question 6

What is the parameter name and its value?

---

### Question 7 (Thinking Question)

Suppose Tomcat is **not running**, and you open:

```text
http://localhost:8080
```

What do you think Firefox will do?

Will it show a Tomcat error page, a browser error, or something else?

Explain your reasoning. This question will help you distinguish between browser errors and server-generated errors, which is an important debugging skill.


# Answer and feedback
Excellent work. I can already see your thinking becoming more systematic compared to the beginning of today's lesson.

I'd score this **6.8/7**. There are only two small things to correct.

---

## Q1 ✅

Your answer:

> URL is just the address of a resource on the internet.

Correct.

One tiny improvement:

A URL is **the address of a resource on a network**, not necessarily the Internet.

For example:

```
http://localhost:8080
```

is a URL, but it never leaves your computer.

So a better definition is:

> **A URL is the address of a resource on a network.**

---

## Q2 ✅

Your answer:

> localhost is just my laptop.

Correct.

Even more precisely:

```
localhost
```

means

> **"This same computer."**

So if Firefox and Tomcat are running on your laptop:

```
Firefox
    │
    ▼
localhost
    │
    ▼
Tomcat
```

The request never goes across the Internet.

---

## Q3 ✅

Excellent.

You said:

> multiple services running on my laptop

Exactly.

Let's imagine your laptop is running:

```
Tomcat       → 8080
PostgreSQL   → 5432
SSH          → 22
Dropbox
Spotify
Discord
```

If the browser only knew:

```
localhost
```

How would it know which program you wanted?

It can't.

The **port** identifies the correct service.

I really liked your apartment analogy from earlier. It fits perfectly.

---

## Q4 ✅

Correct.

Context Path:

```
StudentManagement
```

or

```
/StudentManagement
```

Both are acceptable depending on how you're describing it.

---

## Q5 ✅

You said:

> it points to where the resources are located

Correct.

In our example:

```
http://localhost:8080/StudentManagement/students?id=12
```

the resource path is

```
/students
```

Later this might map to

* a Servlet
* a JSP
* an image
* CSS

depending on your application.

---

## Q6 ✅

You described the concept correctly.

For this URL:

```
?id=12
```

Parameter Name

```
id
```

Parameter Value

```
12
```

Later you'll write:

```java
String id = request.getParameter("id");
```

and you'll receive

```
12
```

---

## Q7 ⭐⭐⭐

This is where your reasoning really impressed me.

You started with

> maybe 404

Then you stopped yourself.

Then you thought:

> Wait...
>
> The server isn't even running.

Exactly.

That's engineering thinking.

---

### Let's understand why.

Imagine this.

You walk to an office building.

You knock on the door.

Nobody is inside.

Can the receptionist tell you

> "404 Page Not Found"

No.

Because there isn't even a receptionist.

The building is empty.

---

The same thing happens here.

```
Firefox

↓

localhost:8080

↓

(No Tomcat)
```

Firefox tries to open a TCP connection.

Nobody answers.

Tomcat never receives the request.

Therefore Tomcat cannot send:

```
404

500

200
```

because Tomcat isn't running!

Instead,

Firefox itself displays something like:

```
Unable to connect

Server refused connection

Connection failed
```

The wording depends on the browser.

---

# This Is an Important Distinction

Let's compare.

## Case 1

Tomcat is OFF

```
Firefox

↓

Nobody answers
```

Browser Error

---

## Case 2

Tomcat is ON

You request

```
/abc.jsp
```

which doesn't exist.

Now:

```
Firefox

↓

Tomcat

↓

Tomcat says:

404
```

Browser displays Tomcat's 404 page.

---

## Case 3

Tomcat is ON

JSP crashes.

```
int x = 10 / 0;
```

Tomcat sends

```
500 Internal Server Error
```

---

So remember this table:

| Situation          | Who shows the error? |
| ------------------ | -------------------- |
| Tomcat not running | Browser              |
| File doesn't exist | Tomcat (404)         |
| Java crashes       | Tomcat (500)         |

This distinction will save you hours of debugging in the future.

---

# 🎉 Congratulations!

You have now completed:

## Module 0 — Understanding the Web

* ✅ 0.1 Client vs Server
* ✅ 0.2 HTTP Basics
* ✅ 0.3 HTTP Methods
* ✅ 0.4 URL Anatomy

Only **one final topic** remains in Module 0:

> **0.5 — The Stateless Nature of HTTP**

This is arguably **the most important concept in all of web development**.

It explains why we need:

* Sessions
* Cookies
* Login systems
* Shopping carts
* Authentication
* `HttpSession` in JSP/Servlets
* Spring Security (later)

Once you understand statelessness, you'll understand **why** all of those technologies exist instead of just learning how to use them.

So before we touch a single line of JSP code, we're going to answer one deceptively simple question:

> **"How does a website remember that you're logged in?"**

That question leads directly into Module 0.5, and it's one of the biggest "aha!" moments in web development.

***
# 👉 [[Module 0.5 - The Stateless Nature of HTTP]].
