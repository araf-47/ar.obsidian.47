# Session 2.9 — CORS

This is an important lesson because you're about to connect your **Angular frontend** to your **Spring Boot backend**.

The situation we'll focus on is simply:

```text
Angular
localhost:4200
     │
     │ HTTP request
     ▼
Spring Boot
localhost:8080
```

***

## 1. What is CORS?

**CORS** stands for:

> **Cross-Origin Resource Sharing**

The simplest way to understand it:

**CORS is a browser rule that controls whether a webpage is allowed to make requests to a different origin.**

The important word is **origin**.

An origin is basically:

```text
protocol + host + port
```

For example:

```text
http://localhost:4200
```

and

```text
http://localhost:8080
```

are **different origins** because their ports are different.

Even though both use:

```text
localhost
```

they are still different origins.

***

# 2. Why does the browser care?

Imagine a website:

```text
http://evil-site.com
```

trying to make requests to your bank's backend:

```text
https://my-bank.com
```

without your permission.

That could be dangerous.

So browsers enforce security rules around **cross-origin requests**.

The browser basically asks:

> "Is this backend allowing this frontend to make this request?"

CORS is the mechanism through which the **server tells the browser which cross-origin requests are allowed**.

### Important distinction

CORS is primarily a **browser restriction**.

It's not that Spring Boot automatically refuses every request.

For example:

```text
Angular/browser
      │
      │ request
      ▼
Spring Boot
```

The browser may block the frontend from using the response if the backend hasn't allowed the origin.

***

# 3. Why Angular `4200` and Spring Boot `8080` cause the problem

Your Angular development server commonly runs on:

```text
http://localhost:4200
```

Your Spring Boot server commonly runs on:

```text
http://localhost:8080
```

So:

```text
Angular:
http://localhost:4200

Spring Boot:
http://localhost:8080
```

Different ports → different origins.

Therefore:

```text
Angular → Spring Boot
```

is a **cross-origin request**.

The browser checks whether Spring Boot allows it.

If Spring Boot hasn't configured CORS appropriately, you may see an error similar to:

```text
Access to XMLHttpRequest ... has been blocked by CORS policy
```

This is the classic problem you need to recognize.

***

# 4. A simple example

Suppose your Spring Boot controller is:

```java
@RestController
@RequestMapping("/products")
public class ProductController {

    @GetMapping
    public String getProducts() {
        return "Products";
    }
}
```

The backend endpoint is:

```text
GET http://localhost:8080/products
```

Your Angular application is running at:

```text
http://localhost:4200
```

Angular sends:

```text
GET http://localhost:8080/products
```

The browser sees:

```text
Frontend origin:
http://localhost:4200

Backend origin:
http://localhost:8080
```

Different origins.

So CORS becomes relevant.

***

# 5. `@CrossOrigin`

The easiest way to solve CORS for a particular controller is:

```java
@CrossOrigin
@RestController
@RequestMapping("/products")
public class ProductController {

    @GetMapping
    public String getProducts() {
        return "Products";
    }
}
```

Now Spring allows cross-origin requests for that controller.

But it's better to explicitly say which frontend is allowed:

```java
@CrossOrigin(origins = "http://localhost:4200")
@RestController
@RequestMapping("/products")
public class ProductController {

    @GetMapping
    public String getProducts() {
        return "Products";
    }
}
```

This says:

> Allow requests coming from `http://localhost:4200`.

***

## 6. Where does `@CrossOrigin` go?

You can put it on the **controller class**:

```java
@CrossOrigin(origins = "http://localhost:4200")
@RestController
@RequestMapping("/products")
public class ProductController {
```

That means the CORS rule applies to the controller's endpoints.

You can also put it on a specific method:

```java
@GetMapping
@CrossOrigin(origins = "http://localhost:4200")
public String getProducts() {
    return "Products";
}
```

Then the rule applies specifically to that endpoint.

For now, remember:

```text
@CrossOrigin
      ↓
Allow cross-origin requests
```

***

# 🧪 Exercise 1

Take one of your existing Spring Boot controllers.

Add:

```java
@CrossOrigin(origins = "http://localhost:4200")
```

Then think about what this means:

```text
Angular:
http://localhost:4200

        ↓ allowed

Spring Boot:
http://localhost:8080
```

The important part is that **4200 is the Angular origin**, not the backend origin.

***

# 7. Global CORS configuration

Imagine your application has:

```text
ProductController
TenantController
UserController
OrderController
```

You could put:

```java
@CrossOrigin(origins = "http://localhost:4200")
```

on every controller.

That works, but it becomes repetitive.

Instead, you can configure CORS **globally**.

This is where:

```java
WebMvcConfigurer
```

comes in.

Create a configuration class:
```
com.example.trial
			|
			|
			└── Config/
				└── CorsConfig.java
```

```java
@Configuration
public class CorsConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {

        registry.addMapping("/**")
                .allowedOrigins("http://localhost:4200");
    }
}
```

You'll need the relevant imports, which your IDE can usually add automatically.

***

# 8. Understand the important pieces

Don't memorize the entire code yet. Understand what each part means.

### `@Configuration`

```java
@Configuration
```

This tells Spring:

> This class contains configuration for the application.

***

### `implements WebMvcConfigurer`

```java
public class CorsConfig implements WebMvcConfigurer
```

We're using Spring MVC's configuration mechanism.

You don't need to understand every method inside `WebMvcConfigurer` for this lesson.

***

### `addCorsMappings`

```java
@Override
public void addCorsMappings(CorsRegistry registry)
```

This is where we define our global CORS rules.

***

### `addMapping("/**")`

```java
registry.addMapping("/**")
```

This means:

> Apply this CORS configuration to all paths.

For example:

```text
/products
/tenants
/users
/orders
```

***

### `allowedOrigins`

```java
.allowedOrigins("http://localhost:4200");
```

This means:

> Allow requests coming from Angular running at `localhost:4200`.

So conceptually:

```text
allowedOrigins(
    "Angular's origin"
)
```

***

# 9. `@CrossOrigin` vs global configuration

You should understand the difference.

### Option 1 — `@CrossOrigin`

```java
@CrossOrigin(origins = "http://localhost:4200")
@RestController
public class ProductController {
```

Good when you want CORS configuration for a particular controller.

### Option 2 — Global configuration

```java
@Configuration
public class CorsConfig implements WebMvcConfigurer {
```

Good when you want the same CORS rule across your application.

Think:

```text
@CrossOrigin
     ↓
specific controller/endpoint

WebMvcConfigurer
     ↓
global configuration
```

***

# 10. The most important debugging mental model

When you eventually have:

```text
Angular
localhost:4200
     │
     │ GET /products
     ▼
Spring Boot
localhost:8080
```

and Angular gives you a CORS error, ask:

### Step 1

Are the frontend and backend on different origins?

```text
4200 vs 8080
```

Yes.

### Step 2

Does the backend allow the Angular origin?

For example:

```java
@CrossOrigin(origins = "http://localhost:4200")
```

or global CORS configuration.

### Step 3

If not, configure CORS.

That's the practical skill you need from this lesson.

***

# 🧠 One important clarification

CORS does **not** mean:

> "Angular cannot talk to Spring Boot because they are on different ports."

That's too strong.

It means:

> **Because they are different origins, the browser applies CORS rules to the request.**

If the backend permits the Angular origin, the browser can allow the frontend to use the response.

***

# 🧪 Exercise 2 — Identify the problem

Suppose you have:

```text
Angular:
http://localhost:4200

Spring Boot:
http://localhost:8080
```

Angular calls:

```text
GET http://localhost:8080/products
```

and the browser reports a CORS error.

### Question:

What is the likely problem?

A. Spring Boot is running on port 8080.

B. Angular cannot make HTTP requests.

C. The browser sees the frontend and backend as different origins, and the backend hasn't allowed the Angular origin.

**Correct answer: C.**

***

# 🧪 Exercise 3 — Read this code

```java
@CrossOrigin(origins = "http://localhost:4200")
@RestController
@RequestMapping("/products")
public class ProductController {

    @GetMapping
    public String getProducts() {
        return "Products";
    }
}
```

Explain in your own words what this line means:

```java
@CrossOrigin(origins = "http://localhost:4200")
```

Don't worry about using exact terminology. I want to see whether you understand the idea.

***

# 🧠 Session 2.9 Checkpoint

Answer these **without looking back**:

### 1.

What does CORS stand for?

### 2.

Why are these two different origins?

```text
http://localhost:4200
http://localhost:8080
```

### 3.

Who primarily enforces CORS restrictions in the situation we're discussing?

```text
Angular/browser
Spring Boot
PostgreSQL
```

### 4.

What does this do?

```java
@CrossOrigin(origins = "http://localhost:4200")
```

### 5.

What is the difference between:

```text
@CrossOrigin
```

and

```text
WebMvcConfigurer
```

### 6.

Given:

```text
Angular → localhost:4200
Spring Boot → localhost:8080
```

Angular gets a CORS error.

**What is the first thing you would suspect?**
