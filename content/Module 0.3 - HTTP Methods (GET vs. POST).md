Excellent. This is one of the most important modules in JSP because **almost every JSP page and every Servlet you'll write will handle either a GET request or a POST request.**

By the end of this lesson, you'll know **why** GET and POST exist—not just when to use them.

---

# Day 1 - Module 0.3

# HTTP Methods (GET vs POST)

---

# Learning Objectives

By the end of this lesson, you should be able to answer:

* What is an HTTP Method?
* Why are there different methods?
* What is GET?
* What is POST?
* When should each be used?
* Why shouldn't passwords be sent using GET?
* What happens when you click a link?
* What happens when you submit a form?

---

# 1. What is an HTTP Method?

Remember from the previous lesson:

The browser sends an HTTP Request.

Example:

```http
GET /students HTTP/1.1
Host: localhost:8080
```

Notice the first word:

```text
GET
```

That first word is called the **HTTP Method**.

Think of it as the **verb** in a sentence.

For example:

* Read a book
* Write a letter
* Delete a file

The verbs are:

* Read
* Write
* Delete

HTTP works the same way.

The method tells the server:

> **"What do you want me to do?"**

---

# 2. Why Do We Need Different Methods?

Imagine you go to a library.

Sometimes you want to:

* Read a book
* Borrow a book
* Return a book

These are different actions.

It would be confusing if you always just said:

> "Book!"

The librarian wouldn't know what you wanted.

Similarly, when a browser talks to a server, it should be clear whether it wants to:

* Read data
* Submit data
* Update data
* Delete data

HTTP methods make that intent explicit.

---

# 3. The Four Main HTTP Methods

There are many HTTP methods, but you'll mainly encounter these four:

| Method | Purpose             | CRUD Equivalent |
| ------ | ------------------- | --------------- |
| GET    | Retrieve data       | Read            |
| POST   | Submit new data     | Create          |
| PUT    | Replace/update data | Update          |
| DELETE | Delete data         | Delete          |

For JSP and Servlets, you'll spend most of your time with **GET** and **POST**.

We'll mention PUT and DELETE again when you learn REST APIs and Spring Boot.
                               
---

# 4. GET — "Please Give Me Something"

GET is used when you want to **retrieve** information.

Examples:

* Open the home page.
* View a student's profile.
* Search for a book.
* Read an article.

Nothing is being changed on the server.

You're just asking for information.

---

## Example

You type:

```text
http://localhost:8080/students
```

The browser sends:

```http
GET /students HTTP/1.1
Host: localhost:8080
```

Tomcat receives the request.

Your Servlet queries SQLite.

The server sends back an HTML page listing students.

---

# Visual Flow

```text
Browser
↓
GET /students
↓
Tomcat
↓
SQLite
↓
Student List
↓
HTML
↓
Browser
```

No data was modified.

---

# 5. POST — "Here Is Some Data"

POST is used when the browser sends **new data** to the server.

Examples:

* Login
* Registration
* Add Student
* Upload File
* Send Feedback

Here, the browser isn't just asking for a page—it is also sending information.

---

## Example

You fill out this form:

```text
Name: Alice
Department: CSE
```

Then click **Submit**.

The browser sends:

```http
POST /student/add HTTP/1.1
Host: localhost:8080

name=Alice&department=CSE
```

Tomcat receives it.

Your Java code reads the data.

JDBC inserts a new record into SQLite.

---

# Visual Flow

```text
Browser
↓
POST
↓
Tomcat
↓
JDBC
↓
SQLite
↓
Student Added
↓
HTML
↓
Browser
```

Unlike GET, POST usually changes something on the server.

---

# 6. ==Where Does the Data Go?==

This is one of the biggest differences.

## GET

Data is appended to the URL.

Example:

```text
http://localhost:8080/search?name=Alice
```

Notice:

```text
?name=Alice
```

Everything after the `?` is called the **query string**.

The browser sends:

```http
GET /search?name=Alice HTTP/1.1
```

The data is visible in the address bar.

---

## POST

The URL stays clean:

```text
http://localhost:8080/login
```

The submitted data is placed in the **request body**, not the URL.

```http
POST /login HTTP/1.1

username=alice
password=secret123
```

The browser address bar still shows:

```text
http://localhost:8080/login
```

---

# 7. Why Not Use GET for Passwords?

Imagine logging in like this:

```text
http://localhost:8080/login?username=alice&password=secret123
```

Problems:

* The password is visible in the address bar.
* It may appear in browser history.
* It may be logged by servers or proxies.
* It can be accidentally shared if the URL is copied.

==Using POST doesn't encrypt the password by itself (that's the job of HTTPS), but it avoids exposing it in the URL==.

---

# 8. ==Can GET Change Data==?

Technically, yes.

Nothing stops you from writing Java code that deletes records when it receives a GET request.

==But that is considered== **bad design**==.==

By convention:

* GET should **not** have side effects.
* GET should be safe to repeat.

Why?

Because browsers, bookmarks, crawlers, and caches assume GET is for reading.

Imagine a search engine crawler visiting:

```text
/deleteStudent?id=5
```

==If your application deletes the student just because someone visited the URL, that's a serious bug==.

---

# 9. Browser Behavior

## Clicking a Link

```html
<a href="/students">Students</a>
```

==Clicking the link sends a==:

> **GET request**

==Always.==

---

## Typing a URL

Typing:

```text
http://localhost:8080/
```

also sends a:

> **GET request**

---

## HTML Form

A form chooses the method explicitly.

Example:

```html
<form method="post">
```

or

```html
<form method="get">
```

The `method` attribute tells the browser which HTTP method to use.

---

# 10. How Does Java Read the Data?

Whether the request is GET or POST, your Java code often retrieves form fields the same way:

```java
String name = request.getParameter("name");
```

This method asks:

> "What value was submitted for the parameter named `name`?"

You don't need to know *where* the data came from (query string or request body); the Servlet API handles that for you.

---

# GET vs. POST Comparison

| Feature                | GET                | POST                                |
| ---------------------- | ------------------ | ----------------------------------- |
| Purpose                | Retrieve data      | Submit data                         |
| Changes server data?   | Should not         | Usually yes                         |
| Data location          | URL (query string) | Request body                        |
| Visible in address bar | Yes                | No                                  |
| Good for bookmarks     | Yes                | Usually no                          |
| Common examples        | View pages, search | Login, registration, create records |

---

# Student Management Example

Suppose we build:

```text
Student Management System
```

Viewing all students:

```text
GET /students
```

Searching:

```text
GET /students?department=CSE
```

Adding a student:

```text
POST /student/add
```

Editing a student:

```text
POST /student/update
```

Deleting a student (in a simple JSP app):

```text
POST /student/delete
```

Later, in Spring Boot, you'll often see PUT and DELETE used for updates and deletions in REST APIs.

---

# Mental Model

When you're unsure which method to use, ask yourself one question:

> **"Am I only reading data, or am I changing something?"**

* Reading → GET
* Creating or changing → POST (or later, PUT/DELETE in REST)

---

# Knowledge Check

Answer these without looking back.

### Question 1

What is an HTTP method?

---

### Question 2

You click this link:

```html
<a href="/students">Students</a>
```

Which HTTP method is sent?

Why?

---

### Question 3

You submit a login form with:

* Username
* Password

Should you use GET or POST?

Explain your reasoning.

---

### Question 4

Which method usually places data in the URL?

---

### Question 5

Where does POST place submitted data?

---

### Question 6

Suppose a page only displays all students from the database.

Should it use GET or POST?

Why?

---

### Question 7 (Thinking Question)

Suppose you accidentally refresh the browser **after submitting a POST request** that adds a new student.

What do you think might happen?

Don't worry if you're not sure—we'll discuss the answer together. This behavior is something every web developer encounters.

# Answer and feedback
This was another excellent attempt. I'd score it **6/7**.

You have the core ideas down. There are just two important corrections that will make your understanding much more precise.

---

## Question 1 ✅

Your answer:

> HTTP methods are the way to invoke whether I send request to just get information or update information.

Very good.

I'd phrase it like this:

> **An HTTP method tells the server what kind of action the client wants to perform.**

Examples:

* GET → retrieve data
* POST → submit data
* PUT → update data
* DELETE → delete data

Think of it as the **verb** of the HTTP request.

---

## Question 2 ✅

Correct.

> Clicking on a link always sends a GET request.

Exactly.

Whenever you click:

```html
<a href="/students">Students</a>
```

the browser sends:

```http
GET /students HTTP/1.1
```

No exceptions in standard HTML.

---

## Question 3 ✅

Excellent.

You gave **both** correct reasons:

✔ Password shouldn't appear in the URL.

✔ Login is not just reading information—you're submitting credentials to the server.

One small clarification:

POST is **not encryption**.

If you're using plain HTTP (not HTTPS), someone on the network could still intercept the request.

POST simply keeps the data **out of the URL**.

Encryption comes from **HTTPS**, which we'll study later.

---

## Question 4 ✅

Correct.

GET puts data in the URL.

Example:

```text
/search?name=Alice
```

---

## Question 5 ❌ (Very Important)

You answered:

> inside response payload

This is the one mistake.

Remember:

We're talking about **POST requests**.

POST sends data inside the **request body**, **not** the response.

Let's compare them.

### GET

```http
GET /search?name=Alice HTTP/1.1
```

The data is in the URL.

---

### POST

```http
POST /login HTTP/1.1

username=alice
password=secret
```

Notice:

The data is **inside the request body**.

Then the server sends back a **response**.

A simple memory trick:

* **Request body** → Browser ➜ Server
* **Response body** → Server ➜ Browser

The browser sends the request.

The server sends the response.

---

## Question 6 ✅

Correct.

Displaying students is reading data.

Therefore:

GET.

---

## Question 7 ⭐

This is where things get interesting.

You answered:

> Refreshing won't change anything.

This is exactly what **most beginners think**.

But in reality...

It often **does**.

Let's walk through it.

---

### Scenario

Suppose you submit this form:

```
Name: Alice
Department: CSE
```

Browser sends:

```
POST /student/add
```

Your server executes:

```sql
INSERT INTO students ...
```

Now the student is stored.

---

#### Then you press Refresh (F5)

What page are you refreshing?

The page that came **after the POST request**.

The browser thinks:

> "The last thing I did was send a POST request."

So many browsers show something like:

> **Confirm Form Resubmission**

Have you ever seen this message?

---

If you click:

```
Continue
```

the browser sends the **same POST request again**.

Result:

```
Alice
Alice
```

Two records!

---

This is one of the oldest problems in web development.

It's called **Form Resubmission**.

Later, we'll learn the professional solution:

```
POST
↓
Server saves data
↓
Redirect
↓
GET
↓
Success Page
```

This pattern is called **Post/Redirect/Get (PRG)**.

Every good web framework—including Spring Boot—uses it.

---

# The Most Important Correction Today

I want you to permanently remember this picture.

```
                    Browser

     ------------------------------
     Request
     ------------------------------

URL
Headers
Body (POST data)

↓

↓

Tomcat

↓

↓

Response

Status Code
Headers
Body (HTML)
```

Notice there are **two bodies**:

* Request Body
* Response Body

You mixed those up once today, which is completely normal. Now you'll never forget the distinction.

---

# 🧠 Mini Exercise (No Notes)

Let's make sure this distinction sticks.

Suppose you submit this login form:

```html
<form action="/login" method="post">
    Username: Alice
    Password: secret123
</form>
```

Answer these four questions:

1. Who creates the **request body**?
2. Who reads the **request body**?
3. Who creates the **response body**?
4. Who reads the **response body**?

Once you answer those, we'll move to **Module 0.4: URL Anatomy**, where you'll learn exactly what every part of a URL means (`http://localhost:8080/student/list?id=5`) and why it matters in JSP and Servlets.

# Answer and feedback
🎉 **Perfect! 4/4.**

You just understood one of the most important ideas in web development.

Let's make it crystal clear.

---

## Request Body

Suppose you type:

```
Username: Alice
Password: secret123
```

and click **Login**.

Who creates the request body?

✅ **Browser**

The browser takes the form values and packages them into an HTTP request.

For example:

```http
POST /login HTTP/1.1
Host: localhost:8080

username=Alice&password=secret123
```

The highlighted part is the **request body**.

---

## Who Reads It?

The request reaches Tomcat.

Tomcat creates an `HttpServletRequest` object.

Then your Servlet (or JSP) does:

```java
String username = request.getParameter("username");
```

So the answer is:

✅ **Server (Tomcat + your Java application)**

---

## Response Body

After processing the login:

* Tomcat executes your Servlet/JSP.
* The JSP generates HTML.

For example:

```html
<html>
<body>

<h1>Welcome Alice</h1>

</body>
</html>
```

That HTML becomes the **response body**.

Who created it?

✅ **Server**

---

## Who Reads It?

Firefox receives the response.

It parses the HTML.

It renders the page on your screen.

So:

✅ **Browser**

---

# The Complete Journey

This diagram summarizes everything you've learned so far:

```text
                USER
                  │
                  ▼
             Types Data
                  │
                  ▼
             Browser (Client)
                  │
                  │ Creates HTTP Request
                  │
                  ▼
        +----------------------+
        | Request Headers      |
        | Request Body         |
        +----------------------+
                  │
                  ▼
          Tomcat (Server)
                  │
                  ▼
        Servlet / JSP
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
                  ▼
        +----------------------+
        | Response Headers     |
        | Response Body (HTML) |
        +----------------------+
                  │
                  ▼
           Browser Renders Page
                  │
                  ▼
                 USER
```

This is **the architecture** you'll keep using throughout JSP, Servlets, and even Spring Boot.

---

# 🧠 A Tiny Correction to Your Mental Model

There's one small wording change I'd like you to adopt from now on.

Instead of saying:

> "The server reads the request body."

Say:

> **"Tomcat receives the request, then my Java web application reads the request through the Servlet API."**

Why?

Because Tomcat itself doesn't know what `username` means.

Tomcat's job is to:

* receive the HTTP request,
* create the `HttpServletRequest` object,
* invoke the correct Servlet or JSP.

**Your Java code** then decides what to do with:

```java
request.getParameter("username")
```

That distinction will become important when we start writing Servlets.

---

# 📚 Progress Check

Here's where you are in the syllabus:

### Module 0 – Understanding the Web

* ✅ 0.1 Client vs Server
* ✅ 0.2 HTTP Basics
* ✅ 0.3 HTTP Methods (GET & POST)
* ⏳ 0.4 URL Anatomy
* ⏳ 0.5 Stateless Nature of HTTP

You're building a solid foundation. Most beginners jump straight into writing JSP files without understanding any of this, which is why they often struggle later.

By the time we start coding, you'll understand **why** each line exists—not just how to type it.

I'm especially happy that you're asking and answering the reasoning questions instead of rushing ahead. That approach will pay off when we reach Servlets and Spring Boot. Next, we'll decode URLs piece by piece in **Module 0.4: URL Anatomy**.

# 👉 [[Module 0.4 - URL Anatomy]].