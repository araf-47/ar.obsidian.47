Ah — yes. I mentioned **Postman / `curl` without teaching you how to use them**. Let's fix that.

For this lesson, I recommend **Postman**, because you're learning REST APIs and it makes the request visible.

## Option 1 — Use Postman

### 1. Install Postman

Go to the official Postman website:
[Postman](https://www.postman.com/downloads/) 

or Install it from [Flathub](https://flathub.org/en/apps/com.getpostman.Postman)

Install it for Linux.

***

### 2. Open Postman

Create a new HTTP request.

You'll see something roughly like:

```text
GET    [ URL                         ]  Send
```

Change `GET` to:

```text
POST
```

Then enter:

```text
http://localhost:8080/api/tenants
```

So you have:

```text
POST http://localhost:8080/api/tenants
```

***

### 3. Tell Postman we're sending JSON

Find the **Body** section.

Select:

```text
Body
  → raw
  → JSON
```

Then enter:

```json
{
    "id": 3,
    "name": "Hasan"
}
```

Click **Send**.

Your Spring Boot application must already be running.

***

### 4. What should happen?

Your controller receives the request:

```text
POST /api/tenants
```

This method gets called:

```java
@PostMapping("/tenants")
public Tenant addTenant(@RequestBody Tenant tenant) {

    tenants.add(tenant);

    return tenant;
}
```

Spring takes:

```json
{
    "id": 3,
    "name": "Hasan"
}
```

and turns it into:

```java
Tenant tenant
```

Then:

```java
tenants.add(tenant);
```

adds it to your Java `List`.

Finally:

```java
return tenant;
```

causes Spring to send JSON back:

```json
{
    "id": 3,
    "name": "Hasan"
}
```

***

## 5. Now check the result

Open another request in Postman:

```text
GET http://localhost:8080/api/tenants
```

Click **Send**.

You should get:

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

So you have just done a complete REST API interaction:

```text
POST
  ↓
JSON sent by client
  ↓
Spring Controller
  ↓
Java Tenant object
  ↓
Java List
  ↓
GET
  ↓
JSON returned to client
```

### One thing I want you to do now

**Don't continue with the checkpoint yet.**

First, install/open Postman and try:

```text
POST http://localhost:8080/api/tenants
```

with:

```json
{
    "id": 3,
    "name": "Hasan"
}
```

If you get an error, **show me the error** and we'll fix it together.
