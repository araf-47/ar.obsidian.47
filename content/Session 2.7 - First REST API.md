# Session 2.7 — First REST API

This is an important session because we're going to connect several things you've already learned:

```text
Angular / browser
       ↓
   HTTP request
       ↓
 Spring Controller
       ↓
    Java code
       ↓
   JSON response
```

And **we will NOT use a database yet**.

We'll keep the data inside a Java collection.

***

## 1. What are we building?

Let's build a tiny **Tenant API**.

It will have these endpoints:

```text
GET  /api/hello
GET  /api/tenants
POST /api/tenants
```

Eventually, you'll be able to do things like:

```text
GET /api/hello
```

and receive:

```json
{
  "message": "Hello from Spring Boot!"
}
```

Or:

```text
GET /api/tenants
```

and receive:

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

Notice something important:

**There is no PostgreSQL involved.**

The tenants will simply live in a Java collection while the application is running.

***

# 2. First, understand the request flow

Suppose the browser sends:

```http
GET /api/hello
```

The flow is:

```text
Browser / Angular
       │
       │ GET /api/hello
       ↓
Spring Boot
       │
       ↓
Controller
       │
       ↓
Java method
       │
       ↓
Response
       │
       ↓
JSON
```

The **Controller** is the part of our application that receives the HTTP request.

You've already worked with mappings such as:

```java
@GetMapping
```

Now we're going to use it for a real API.

***

# 3. Create the Controller

Create:

```text
TenantController.java
```

For now:

```java
package com.lord.LandLord.Controller;

import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.RequestMapping;

@RestController
@RequestMapping("/api")
public class TenantController {

}
```

Let's understand the two annotations.

### `@RestController`

```java
@RestController
```

means:

> This class handles HTTP requests and its methods can return data as the HTTP response.

That's exactly what we need for a REST API.

***

### `@RequestMapping("/api")`

```java
@RequestMapping("/api")
```

sets a common URL prefix for this controller.

So if we later write:

```java
@GetMapping("/hello")
```

the complete endpoint becomes:

```text
/api/hello
```

because:

```text
/api
 +
/hello
 =
/api/hello
```

***

# 4. Our first API endpoint

Add this method:

```java
@GetMapping("/hello")
public String hello() {
    return "Hello from Spring Boot!";
}
```

So the complete class is:

```java
package com.lord.LandLord.Controller;

import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.GetMapping;

@RestController
@RequestMapping("/api")
public class TenantController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello from Spring Boot!";
    }
}
```

Run your Spring Boot application.

Then visit:

```text
http://localhost:8080/api/hello
```

You should see:

```text
Hello from Spring Boot!
```

***

# 5. What actually happened?

You requested:

```text
GET /api/hello
```

Spring looked at your controller.

It found:

```java
@GetMapping("/hello")
```

and called:

```java
hello()
```

The method returned:

```java
"Hello from Spring Boot!"
```

Spring sent that back as the HTTP response.

So:

```text
GET /api/hello
       ↓
@GetMapping("/hello")
       ↓
hello()
       ↓
"Hello from Spring Boot!"
```

### 🧪 Mini exercise

Before continuing, change:

```java
return "Hello from Spring Boot!";
```

to something of your own.

For example:

```java
return "Hello from my LandLord API!";
```

Then refresh:

```text
http://localhost:8080/api/hello
```

Make sure you understand **why** that URL reaches that particular Java method.

***

# 6. Now let's return JSON

A REST API normally doesn't just return plain text.

It commonly returns **JSON**.

For example:

```json
{
    "message": "Hello from Spring Boot!"
}
```

We can create a Java class to represent that data.

Create:

```text
Message.java
```

```java
package com.lord.LandLord;

public class Message {

    private String message;

    public Message(String message) {
        this.message = message;
    }

    public String getMessage() {
        return message;
    }
}
```

Then change our controller:

```java
@GetMapping("/hello")
public Message hello() {
    return new Message("Hello from Spring Boot!");
}
```

Now:

```java
@GetMapping("/hello")
public Message hello() {
    return new Message("Hello from Spring Boot!");
}
```

returns a **Java object**.

Spring Boot converts that Java object into JSON for the HTTP response.

So conceptually:

```text
Java object
    ↓
Spring Boot
    ↓
JSON
```

The response becomes:

```json
{
    "message": "Hello from Spring Boot!"
}
```

You don't manually write:

```json
{
    "message": "Hello from Spring Boot!"
}
```

in the controller.

You return the Java object.

Spring handles the conversion.

***

# 7. Now let's create tenants

Create a simple Java class:

```java
package com.lord.LandLord;

public class Tenant {

    private int id;
    private String name;

    public Tenant(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }
}
```

We're keeping this deliberately simple.

A tenant has:

```text
id
name
```

For example:

```java
new Tenant(1, "Rahim")
```

represents:

```json
{
    "id": 1,
    "name": "Rahim"
}
```

***

# 8. Store tenants in memory

Now let's use a Java collection.

Inside the controller:

```java
private List<Tenant> tenants = new ArrayList<>();
```

You'll need:

```java
import java.util.List;
import java.util.ArrayList;
```

Then initialize it:

```java
private List<Tenant> tenants = new ArrayList<>();

public TenantController() {
    tenants.add(new Tenant(1, "Rahim"));
    tenants.add(new Tenant(2, "Karim"));
}
```

So our controller now has some data stored **inside the application**.

Think of it like:

```text
Java application memory

tenants
   ↓
[ Tenant(1, "Rahim"),
  Tenant(2, "Karim") ]
```

There is no PostgreSQL table.

There is no SQL query.

There is no JDBC.

Just a Java `List`.

***

# 9. GET `/api/tenants`

Now add:

```java
@GetMapping("/tenants")
public List<Tenant> getTenants() {
    return tenants;
}
```

Complete relevant part:

```java
@GetMapping("/tenants")
public List<Tenant> getTenants() {
    return tenants;
}
```

Now visit:

```text
http://localhost:8080/api/tenants
```

You should get something like:

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

***

# 10. Understand this very carefully

This:

```java
@GetMapping("/tenants")
public List<Tenant> getTenants() {
    return tenants;
}
```

does **not** mean we're returning JSON ourselves.

We're returning:

```java
List<Tenant>
```

which is a Java object.

Spring Boot converts it into JSON for the HTTP response.

Therefore:

```text
Java List<Tenant>
       ↓
Spring Boot
       ↓
JSON
```

This is one of the most important ideas in today's lesson.

***

# 11. Now POST `/api/tenants`

We've learned:

```text
GET /api/tenants
```

means:

> Give me the tenants.

Now we want:

```text
POST /api/tenants
```

to mean:

> Add a new tenant.

We'll use a request body containing JSON.

For example:

```json
{
    "id": 3,
    "name": "Hasan"
}
```

The client sends that to:

```text
POST /api/tenants
```

Our controller needs to receive it.

Add:

```java
@PostMapping("/tenants")
public Tenant addTenant(@RequestBody Tenant tenant) {

    tenants.add(tenant);

    return tenant;
}
```

You'll need:

```java
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
```

***

# 12. What is `@RequestBody` doing?

This is worth understanding carefully.

The client sends:

```json
{
    "id": 3,
    "name": "Hasan"
}
```

Spring receives that JSON.

Because we wrote:

```java
@RequestBody Tenant tenant
```

Spring converts the JSON into a Java `Tenant` object.

Conceptually:

```text
JSON request body
       ↓
Spring
       ↓
Tenant object
```

So inside:

```java
public Tenant addTenant(@RequestBody Tenant tenant)
```

`tenant` is a normal Java object.

We can therefore do:

```java
tenants.add(tenant);
```

because `tenants` is:

```java
List<Tenant>
```

***

# 13. The complete flow

Now we have both directions.

### GET

Client asks:

```text
GET /api/tenants
```

Spring:

```text
HTTP request
     ↓
Controller
     ↓
Java List<Tenant>
     ↓
JSON response
```

### POST

Client sends:

```text
POST /api/tenants

{
    "id": 3,
    "name": "Hasan"
}
```

Spring:

```text
HTTP request
     ↓
@RequestBody
     ↓
Java Tenant object
     ↓
tenants.add(tenant)
     ↓
JSON response
```

This is the core of your **first REST API**.

***

# 14. Your controller should now look roughly like this

```java
package com.lord.LandLord.Controller;

import java.util.ArrayList;
import java.util.List;

import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;

import com.lord.LandLord.Tenant;

@RestController
@RequestMapping("/api")
public class TenantController {

    private List<Tenant> tenants = new ArrayList<>();

    public TenantController() {
        tenants.add(new Tenant(1, "Rahim"));
        tenants.add(new Tenant(2, "Karim"));
    }

    @GetMapping("/hello")
    public String hello() {
        return "Hello from Spring Boot!";
    }

    @GetMapping("/tenants")
    public List<Tenant> getTenants() {
        return tenants;
    }

    @PostMapping("/tenants")
    public Tenant addTenant(@RequestBody Tenant tenant) {
        tenants.add(tenant);
        return tenant;
    }
}
```

And `Tenant.java`:

```java
package com.lord.LandLord;

public class Tenant {

    private int id;
    private String name;

    public Tenant(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }
}
```

***

# 15. Test it

You can test GET directly from the browser:

```text
http://localhost:8080/api/hello
```

and:

```text
http://localhost:8080/api/tenants
```

For POST, you'll need an HTTP client such as Postman [^1] or `curl`.

Send:

```http
POST http://localhost:8080/api/tenants
```

with JSON:

```json
{
    "id": 3,
    "name": "Hasan"
}
```

Then call:

```http
GET http://localhost:8080/api/tenants
```

You should now see:

```json
[
    {
        "id": 1,
        "name": "Rahim"
    },
    {
        "id": 2,
        "name": "Karim"
    },
    {
        "id": 3,
        "name": "Hasan"
    }
]
```

### One important limitation

Because this is an **in-memory collection**, restarting Spring Boot destroys the data.

After restarting:

```text
Rahim
Karim
```

will be there again, but:

```text
Hasan
```

will be gone.

That's because nothing was saved to PostgreSQL.

***

# 🧠 Session 2.7 Checkpoint

Don't look back while answering.

### 1.

What happens when a client sends:

```text
GET /api/tenants
```

Describe the flow from the HTTP request to the JSON response.

***

### 2.

What does this do?

```java
@GetMapping("/tenants")
public List<Tenant> getTenants() {
    return tenants;
}
```

***

### 3.

If the client sends:

```json
{
    "id": 3,
    "name": "Hasan"
}
```

to:

```text
POST /api/tenants
```

what is the purpose of:

```java
@RequestBody Tenant tenant
```

***

### 4.

Where are our tenants actually stored in this lesson?

A. PostgreSQL
B. A Java `List` in application memory
C. Browser local storage
D. Tomcat

***

### 5.

Why does the newly added tenant disappear when we restart Spring Boot?

Answer these five in your own words. I’ll check your understanding **before we move to the next session**.

***

# Footnote
[^1]: [[How the heck do I get Postman and use it (s2.7-frapi)]].
