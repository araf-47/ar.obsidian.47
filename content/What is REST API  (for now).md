**REST API** means an API that allows applications to communicate with each other over **HTTP** using a common style of design.

Since you already know HTTP, let's make it very simple.

### Think about your Angular + Spring Boot project

You might have:

```text
Angular frontend
      ↓
   HTTP request
      ↓
Spring Boot backend
      ↓
   PostgreSQL
```

The **REST API is the interface between Angular and your Spring Boot backend**.

For example, Angular might ask:

```http
GET /api/tenants
```

Spring Boot receives that request and might respond with:

```json
[
  {
    "id": 1,
    "name": "Rahim"
  },
  {
    "id": 2,
    "name": "Karim"
  }
]
```

So:

> **REST API = a set of HTTP endpoints through which another application can communicate with your backend.**

### A few common examples

```http
GET    /api/tenants       → get tenants
GET    /api/tenants/5     → get tenant #5
POST   /api/tenants       → create a tenant
PUT    /api/tenants/5     → update tenant #5
DELETE /api/tenants/5     → delete tenant #5
```

You already know HTTP methods, so you can think of REST APIs as **using HTTP requests in a structured way to work with backend data/resources**.

### Why did I mention it in the previous lesson?

Because when you use:

```text
spring-boot-starter-web
```

one of the major things you can build with Spring Boot is a **REST API**.

However, **REST API itself is not a topic we need to study in Session 2.1**. I only mentioned it as an example of what Spring Boot's web functionality is commonly used for.

We'll study it when it appears in your syllabus.
