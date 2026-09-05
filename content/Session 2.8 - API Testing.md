# Session 2.8 — API Testing

This session is about **testing your Spring Boot API before involving Angular**.

The main idea is very simple:

```text
Spring Boot backend
       ↓
    API endpoint
       ↓
   Test it directly
       ↓
 Backend confirmed working
       ↓
    Angular later
```

Why do this?

Because if Angular later fails to get data, you want to know:

> **Is my Spring Boot API broken, or is Angular/CORS the problem?**

API testing lets us answer that first.

***

# 1. What does "test an API" mean?

Suppose you have already built this endpoint:

```java
@GetMapping
public String getProduct() {
    return "Product list";
}
```

and your controller has:

```java
@RequestMapping("/products")
```

Then your endpoint is:

```text
GET http://localhost:8080/products
```

Testing the API simply means:

> **Send a request to that endpoint and see what the backend returns.**

We don't need Angular for this.

We can use:

* Browser
* Postman
* `curl`

***

# 2. Testing a GET request with the browser

For a simple `GET` endpoint, the browser is the easiest tool.

If your Spring Boot application is running, open:

```text
http://localhost:8080/products
```

Your browser sends:

```http
GET /products
```

Spring finds:

```java
@GetMapping
public String getProduct() {
    return "Product list";
}
```

and responds:

```text
Product list
```

So:

```text
Browser
   |
   | GET /products
   ↓
Spring Boot
   |
   | "Product list"
   ↓
Browser
```

### Important

The browser isn't doing anything special here.

It is simply acting as an **HTTP client**.

You already know HTTP, so think of it like this:

```text
Angular        → HTTP client
Postman        → HTTP client
curl           → HTTP client
Browser        → HTTP client
```

They are different tools for sending requests.

***

# 3. Why use Postman?

The browser is useful for simple GET requests.

But APIs aren't only GET requests.

You will eventually have:

```text
GET
POST
PUT
DELETE
```

For example:

```text
GET    /products
POST   /products
PUT    /products/5
DELETE /products/5
```

The browser isn't convenient for manually testing all of these.

That's where **Postman** becomes useful.

Postman allows you to explicitly choose:

```text
HTTP method
URL
Headers
Request body
```

and then send the request.

For this session, don't worry about advanced Postman features.

The important idea is:

> **Postman lets you manually send HTTP requests to your API and inspect the response.**

***

# 4. Your first Postman test

Let's use the endpoint you've already been working with.

Suppose your controller is:

```java
@RestController
@RequestMapping("/products")
public class ProductController {

    @GetMapping
    public String getProduct() {
        return "Product list";
    }
}
```

Start Spring Boot.

Then open Postman.

Create a request:

```text
Method: GET
URL: http://localhost:8080/products
```

Click:

```text
Send
```

You should get:

```text
Product list
```

That's your first API test.

### What actually happened?

Postman sent:

```http
GET http://localhost:8080/products
```

Spring Boot received it.

Spring matched:

```java
@GetMapping
```

and executed:

```java
getProduct()
```

The response went back to Postman.

***

# 5. Testing with `curl`

`curl` does the same basic thing, but from your terminal.

Run:

```bash
curl http://localhost:8080/products
```

You should see:

```text
Product list
```

That's it.

Conceptually:

```text
Browser       ──┐
Postman       ──┼──→ HTTP request → Spring Boot
curl          ──┘
```

All three can test your API.

***

# 6. Why test with three different tools?

You don't necessarily need all three every time.

Each has a convenient use.

### Browser

Good for:

```text
Simple GET
```

Example:

```text
http://localhost:8080/products
```

### Postman

Good for:

```text
GET
POST
PUT
DELETE
```

and examining requests/responses.

### curl

Good for:

```text
Quick terminal testing
```

For example:

```bash
curl http://localhost:8080/products
```

***

# 7. The important debugging workflow

This is the **main lesson of this session**.

Imagine you eventually have:

```text
Angular
   |
   | HTTP request
   ↓
Spring Boot
   |
   ↓
Database
```

Angular says:

> "I can't get the products!"

There are several possible problems.

Maybe:

```text
Spring endpoint is wrong
```

or:

```text
Spring application isn't running
```

or:

```text
Angular request is wrong
```

or:

```text
CORS problem
```

Instead of immediately blaming Angular, test the backend independently.

### Step 1 — Build endpoint

For example:

```text
GET /products
```

### Step 2 — Test endpoint

Use Postman:

```text
GET http://localhost:8080/products
```

### Step 3 — Confirm backend works

If Postman returns:

```text
Product list
```

you know:

> The backend endpoint is working.

### Step 4 — Connect Angular

Only now should Angular call:

```text
http://localhost:8080/products
```

This separates the problems.

***

# 8. What if Postman gets an error?

This is actually useful.

Suppose you test:

```text
GET http://localhost:8080/products
```

and receive:

```text
404 Not Found
```

That tells you:

> The request reached the server, but Spring couldn't find that endpoint.

You can investigate the **backend** first.

You don't need to involve Angular.

Similarly, if the Spring Boot application isn't running, you might get a connection error.

Again:

> That's a backend/server problem, not an Angular problem.

***

# 9. Small practical exercise 🛠️

Let's test your existing API.

### Exercise 1 — Browser

With Spring Boot running, visit:

```text
http://localhost:8080/products
```

Confirm what you receive.

***

### Exercise 2 — curl

In your terminal:

```bash
curl http://localhost:8080/products
```

Confirm that you receive the same response.

***

### Exercise 3 — Postman

Create:

```text
GET
http://localhost:8080/products
```

Click **Send**.

Confirm that Postman gives you the same response.

***

### Exercise 4 — Deliberately make a mistake

Change the URL to:

```text
http://localhost:8080/product
```

Notice the difference.

You have:

```text
/products
```

but requested:

```text
/product
```

You should get an error such as:

```text
404
```

This is useful practice because you're learning to interpret API failures.

Then change it back to:

```text
/products
```

***

# The one thing I want you to remember

Don't memorize Postman buttons.

Remember this workflow:

```text
Build API
    ↓
Test API independently
    ↓
Does it work?
    ↓
YES ♦️ ──→ Connect Angular
    │
    NO
    ↓
Fix backend
```

**Postman/curl are basically tools that allow you to talk directly to your Spring Boot backend without Angular in the middle.**

***

# 🧠 Checkpoint

Answer these **without looking back**:

### 1.

If you have:

```java
@GetMapping
public String getProduct() {
    return "Product list";
}
```

and:

```java
@RequestMapping("/products")
```

what URL would you test?

***

### 2.

Why can a browser test a simple `GET` API?

***

### 3.

What is the main advantage of using Postman instead of the browser?

***

### 4.

What does this command do?

```bash
curl http://localhost:8080/products
```

***

### 5.

Why should we test the Spring Boot API with Postman **before** connecting Angular?

Answer these five, and I'll check your understanding before we move on.
