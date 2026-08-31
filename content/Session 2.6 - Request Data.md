# Session 2.6 — Request Data

This session is about **how data from an HTTP request gets into your Spring Boot Java method**.

You already know HTTP, so let's connect it directly to what you've learned.

Suppose Angular sends:

```text
GET /api/tenants/5
```

Spring needs to get that `5` into your Java code.

Or Angular sends:

```text
GET /api/tenants?city=Dhaka
```

Spring needs to get `"Dhaka"` into your Java code.

Or Angular sends:

```http
POST /api/tenants
Content-Type: application/json
```

with:

```json
{
  "name": "Rahim",
  "city": "Dhaka"
}
```

Spring needs to turn that JSON into a Java object.

That's what these three annotations help us do:

```java
@PathVariable
@RequestParam
@RequestBody
```

***

# 1. The Big Picture

Remember this from REST:

```text
HTTP Request
     ↓
Spring Controller
     ↓
Java method
```

For example:

```text
GET /api/tenants/5
```

might reach:

```java
@GetMapping("/api/tenants/{id}")
public Tenant getTenant(...) {
    ...
}
```

The question is:

> How do we get the `5` from the URL into the `id` variable?

Answer:

```java
@PathVariable
```

Similarly:

| Request data          | Annotation      |
| --------------------- | --------------- |
| `/tenants/5`          | `@PathVariable` |
| `/tenants?city=Dhaka` | `@RequestParam` |
| JSON body             | `@RequestBody`  |

The most important thing to understand today is **where the data comes from**.

***

# 2. `@PathVariable`

## What is a path variable?

Look at:

```text
GET /api/tenants/5
```

The `5` is part of the **URL path**.

We can define the endpoint like this:

```java
@GetMapping("/api/tenants/{id}")
```

Here:

```text
/api/tenants/{id}
              ↑
         path variable
```

Then we use:

```java
@PathVariable
```

to get that value.

### Example

```java
@GetMapping("/api/tenants/{id}")
public String getTenant(@PathVariable int id) {

    return "Tenant ID = " + id;
}
```

Now imagine the browser/client sends:

```text
GET /api/tenants/5
```

Spring sees:

```text
{id} = 5
```

and gives your Java method:

```java
id = 5
```

So the result would be:

```text
Tenant ID = 5
```

***

## Let's look at the two pieces together

```java
@GetMapping("/api/tenants/{id}")
public String getTenant(@PathVariable int id) {
    return "Tenant ID = " + id;
}
```

There are two important parts:

```java
"{id}"
```

and:

```java
@PathVariable int id
```

They correspond to each other.

Think:

```text
URL
/api/tenants/5
             ↓
         {id} = 5
             ↓
@PathVariable int id
             ↓
          id = 5
```

***

## Explicitly naming the variable

You can also write:

```java
@GetMapping("/api/tenants/{id}")
public String getTenant(@PathVariable("id") int tenantId) {

    return "Tenant ID = " + tenantId;
}
```

Here:

```java
@PathVariable("id")
```

means:

> Take the `{id}` value from the URL.

and put it into:

```java
tenantId
```

This can be useful when the Java variable has a different name.

***

## Practical Exercise 1

Add this to your controller:

```java
@GetMapping("/api/tenants/{id}")
public String getTenant(@PathVariable int id) {
    return "You requested tenant " + id;
}
```

Run your Spring Boot application.

Then visit:

```text
http://localhost:8080/api/tenants/5
```

You should get:

```text
You requested tenant 5
```

Try:

```text
http://localhost:8080/api/tenants/10
```

You should get:

```text
You requested tenant 10
```

### Notice

You didn't write:

```java
int id = 5;
```

Spring extracted `5` from the URL and supplied it to your method.

***

# 3. `@RequestParam`

Now look at a different URL:

```text
GET /api/tenants?city=Dhaka
```

Here `city=Dhaka` is a **query parameter**.

You may remember query parameters from HTTP/Angular.

The structure is:

```text
/api/tenants?city=Dhaka
             └─────────┘
             query parameter
```

We use:

```java
@RequestParam
```

to retrieve it.

### Example

```java
@GetMapping("/api/tenants")
public String getTenants(@RequestParam String city) {

    return "Searching tenants in " + city;
}
```

Request:

```text
GET /api/tenants?city=Dhaka
```

Spring gives:

```java
city = "Dhaka"
```

So the result is:

```text
Searching tenants in Dhaka
```

***

# 4. Path Variable vs Request Parameter

This distinction is **very important**.

Compare:

### Path variable

```text
/api/tenants/5
```

```java
@GetMapping("/api/tenants/{id}")
public String getTenant(@PathVariable int id) {
    ...
}
```

The `5` identifies something in the URL path.

***

### Request parameter

```text
/api/tenants?city=Dhaka
```

```java
@GetMapping("/api/tenants")
public String getTenants(@RequestParam String city) {
    ...
}
```

The `city=Dhaka` is a query parameter.

A useful mental model:

```text
/api/tenants/5
              ↑
         "which tenant?"
         @PathVariable


/api/tenants?city=Dhaka
              ↑
         "filter/search by city"
         @RequestParam
```

For your landlord/tenant example:

```text
GET /api/tenants/5
```

could mean:

> Give me tenant number 5.

While:

```text
GET /api/tenants?city=Dhaka
```

could mean:

> Give me tenants whose city is Dhaka.

***

# 5. Multiple `@RequestParam`s

You can have more than one.

For example:

```text
GET /api/tenants?city=Dhaka&status=active
```

Controller:

```java
@GetMapping("/api/tenants")
public String getTenants(
        @RequestParam String city,
        @RequestParam String status) {

    return "City = " + city + ", Status = " + status;
}
```

Spring extracts:

```java
city = "Dhaka"
status = "active"
```

Result:

```text
City = Dhaka, Status = active
```

***

# 6. What if the parameter is missing?

Suppose your controller says:

```java
@GetMapping("/api/tenants")
public String getTenants(@RequestParam String city) {
    return city;
}
```

But the client sends:

```text
GET /api/tenants
```

There is no:

```text
?city=...
```

By default, Spring expects `city` to be present.

For now, just understand this concept:

> `@RequestParam` normally expects the query parameter to exist.

We don't need to go into advanced optional/default-value handling in this session.

***

# 7. Practical Exercise 2

Create:

```java
@GetMapping("/api/tenants/search")
public String searchTenants(@RequestParam String city) {

    return "Searching for tenants in " + city;
}
```

Now visit:

```text
http://localhost:8080/api/tenants/search?city=Dhaka
```

Expected:

```text
Searching for tenants in Dhaka
```

Then try:

```text
http://localhost:8080/api/tenants/search?city=Chittagong
```

Expected:

```text
Searching for tenants in Chittagong
```

***

# 8. `@RequestBody`

Now we have a different situation.

Suppose we want to **create a tenant**.

We send:

```text
POST /api/tenants
```

The URL doesn't contain the tenant information.

Instead, the information is in the **HTTP request body**.

For example:

```json
{
    "name": "Rahim",
    "city": "Dhaka"
}
```

This is where:

```java
@RequestBody
```

comes in.

It tells Spring:

> Take the JSON data from the HTTP request body and convert it into a Java object.

***

# 9. A Java Class for the Tenant

For a simple example:

```java
public class Tenant {

    private String name;
    private String city;

    public Tenant() {
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getCity() {
        return city;
    }

    public void setCity(String city) {
        this.city = city;
    }
}
```

Don't worry about Spring terminology here. This is simply a Java class representing tenant data.

The incoming JSON:

```json
{
    "name": "Rahim",
    "city": "Dhaka"
}
```

can become:

```java
Tenant tenant
```

with:

```java
tenant.getName()
```

giving:

```text
Rahim
```

and:

```java
tenant.getCity()
```

giving:

```text
Dhaka
```

***

# 10. Using `@RequestBody`

Controller:

```java
@PostMapping("/api/tenants")
public String createTenant(@RequestBody Tenant tenant) {

    return "Tenant: " + tenant.getName()
            + ", City: " + tenant.getCity();
}
```

The client sends:

```http
POST /api/tenants
Content-Type: application/json
```

Body:

```json
{
    "name": "Rahim",
    "city": "Dhaka"
}
```

Spring essentially does the conversion for you:

```text
JSON
 ↓
{
  "name": "Rahim",
  "city": "Dhaka"
}
 ↓
Tenant object
 ↓
Java method
```

So inside the method:

```java
tenant.getName()
```

is:

```text
Rahim
```

and:

```java
tenant.getCity()
```

is:

```text
Dhaka
```

***

# 11. The Three Together

This is the most important part of today's lesson.

Imagine these three requests:

### A. Get one tenant

```text
GET /api/tenants/5
```

The `5` comes from the **path**:

```java
@PathVariable
```

Example:

```java
@GetMapping("/api/tenants/{id}")
public Tenant getTenant(@PathVariable int id) {
    ...
}
```

***

### B. Search/filter tenants

```text
GET /api/tenants?city=Dhaka
```

The `Dhaka` comes from the **query parameter**:

```java
@RequestParam
```

Example:

```java
@GetMapping("/api/tenants")
public List<Tenant> getTenants(@RequestParam String city) {
    ...
}
```

***

### C. Create a tenant

```text
POST /api/tenants
```

JSON comes from the **request body**:

```java
@RequestBody
```

Example:

```java
@PostMapping("/api/tenants")
public Tenant createTenant(@RequestBody Tenant tenant) {
    ...
}
```

***

# 12. Easy Mental Model

Whenever you receive data in a Controller, ask:

> **Where is the data located in the HTTP request?**

### In the URL path?

```text
/api/tenants/5
```

Use:

```java
@PathVariable
```

### In the query string?

```text
/api/tenants?city=Dhaka
```

Use:

```java
@RequestParam
```

### In the request body?

```json
{
    "name": "Rahim",
    "city": "Dhaka"
}
```

Use:

```java
@RequestBody
```

So:

```text
                 HTTP REQUEST
                      │
          ┌───────────┼───────────┐
          ↓           ↓           ↓
       URL path    Query       Body
          │        parameter      │
          ↓           ↓           ↓
   @PathVariable  @RequestParam  @RequestBody
```

***

# 13. Angular Connection

Since you're learning Angular, this will eventually make a lot of sense when Angular calls your Spring Boot API.

For example, Angular might request:

```text
GET /api/tenants/5
```

Spring:

```java
@GetMapping("/api/tenants/{id}")
public Tenant getTenant(@PathVariable int id) {
    ...
}
```

Or Angular might request:

```text
GET /api/tenants?city=Dhaka
```

Spring:

```java
@GetMapping("/api/tenants")
public List<Tenant> getTenants(@RequestParam String city) {
    ...
}
```

Or Angular might send a tenant object as JSON:

```json
{
    "name": "Rahim",
    "city": "Dhaka"
}
```

Spring:

```java
@PostMapping("/api/tenants")
public Tenant createTenant(@RequestBody Tenant tenant) {
    ...
}
```

You can think of the Spring Controller as **receiving and unpacking the HTTP request**.

***

# Practical Exercise 3 — All Three

Create these three endpoints in your controller.

### 1. Path variable

```java
@GetMapping("/api/tenants/{id}")
public String getTenant(@PathVariable int id) {
    return "Tenant ID = " + id;
}
```

### 2. Request parameter

```java
@GetMapping("/api/tenants/search")
public String searchTenants(@RequestParam String city) {
    return "Searching in " + city;
}
```

### 3. Request body

Using your `Tenant` class:

```java
@PostMapping("/api/tenants")
public String createTenant(@RequestBody Tenant tenant) {
    return "Created tenant " + tenant.getName()
            + " from " + tenant.getCity();
}
```

Test:

```text
GET /api/tenants/5
```

```text
GET /api/tenants/search?city=Dhaka
```

And send a POST request to:

```text
POST /api/tenants
```

with:

```json
{
    "name": "Rahim",
    "city": "Dhaka"
}
```

***

# Checkpoint 🧠

Don't look back at the explanations if you can avoid it.

### 1. What would you use for this?

```text
GET /api/tenants/25
```

Specifically, how would you get `25` into:

```java
int id
```

***

### 2. What would you use for:

```text
GET /api/tenants?city=Dhaka
```

How would you get `"Dhaka"` into:

```java
String city
```

***

### 3. What would you use for this JSON?

```json
{
    "name": "Karim",
    "city": "Dhaka"
}
```

You want Spring to convert it into:

```java
Tenant tenant
```

***

### 4. Fill in the blanks:

```java
@GetMapping("/api/tenants/{id}")
public String test(________ int id) {
    return "ID = " + id;
}
```

```java
@GetMapping("/api/tenants")
public String test(________ String city) {
    return "City = " + city;
}
```

```java
@PostMapping("/api/tenants")
public String test(________ Tenant tenant) {
    return tenant.getName();
}
```

**Answer with your answers to 1–4.** I'll check them before we move on.
