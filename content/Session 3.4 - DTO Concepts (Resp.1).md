# Session 3.4 — DTO Concepts

In the previous sessions, you learned the basic relationship:

```text
Java Object
    ↕
Database Row
```

Using JPA, we made that Java object an **Entity**.

For example, imagine our `Tenant` entity:

```java
@Entity
@Table(name = "tenants")
public class Tenant {

    @Id
    @GeneratedValue
    private Long id;

    private String name;
    private String email;
}
```

The basic idea is:

```text
Tenant Java Object
        ↓
JPA / Hibernate
        ↓
tenants table in database
```

Now we need to introduce another kind of object:

> **DTO**

***

# 1. What is a DTO?

DTO stands for:

> **Data Transfer Object**

A DTO is a Java object whose main purpose is to **carry data from one part of the application to another**.

For example:

```java
public class TenantDTO {

    private Long id;
    private String name;
    private String email;
}
```

At first glance, you might think:

> "This looks almost exactly like my `Tenant` entity. Why create another class?"

That is exactly the question DTOs solve.

***

# 2. Entity vs DTO

Let's compare them.

## Entity

An Entity represents data that belongs to the **database**.

```java
@Entity
@Table(name = "tenants")
public class Tenant {

    @Id
    @GeneratedValue
    private Long id;

    private String name;
    private String email;
}
```

Its job is roughly:

```text
Java Object ↔ Database
```

JPA/Hibernate uses the Entity to work with database data.

***

## DTO

A DTO represents data that we want to **transfer**, especially between our backend and frontend.

```java
public class TenantDTO {

    private Long id;
    private String name;
    private String email;
}
```

Its job is roughly:

```text
Backend ↔ Frontend
```

For our REST API:

```text
Spring Boot
    ↓
DTO
    ↓
JSON
    ↓
Angular
```

So the important distinction is:

| Entity                                           | DTO                                                |
| ------------------------------------------------ | -------------------------------------------------- |
| Represents database data                         | Represents transferred data                        |
| Usually connected to a database table            | Usually not directly connected to a database table |
| Uses JPA annotations such as `@Entity` and `@Id` | Usually just contains the data being transferred   |
| Used internally for persistence                  | Used for sending/receiving API data                |

A simple way to remember it:

```text
Entity = Database representation

DTO = Data transfer representation
```

***

# 3. Why not just send the Entity directly?

Let's say our database contains this:

```text
tenants
-------------------------------------------------
id | name  | email              | password
-------------------------------------------------
1  | Rafi  | rafi@example.com   | secret123
```

Your Entity might look like this:

```java
@Entity
public class Tenant {

    @Id
    private Long id;

    private String name;
    private String email;
    private String password;
}
```

Now imagine your controller directly returns the Entity:

```java
@GetMapping("/tenants")
public Tenant getTenant() {
    return tenant;
}
```

Spring Boot can convert that object into JSON:

```json
{
    "id": 1,
    "name": "Rafi",
    "email": "rafi@example.com",
    "password": "secret123"
}
```

The problem:

> The frontend received the password.

Even if the frontend does not need that information.

This is one reason why exposing Entities directly is not always ideal.

***

# 4. Using a DTO instead

Suppose we create this:

```java
public class TenantDTO {

    private Long id;
    private String name;
    private String email;
}
```

Notice:

```text
Tenant Entity                 TenantDTO
-------------                 ---------
id                            id
name                          name
email                         email
password                      ❌ not included
```

Now the API can send this data instead:

```json
{
    "id": 1,
    "name": "Rafi",
    "email": "rafi@example.com"
}
```

The password remains inside the backend.

So the DTO lets us control:

> **What data leaves or enters the application.**

***

# 5. The basic data flow

This is the main concept you need to understand in this session:

```text
Database
   ↓
Entity
   ↓
DTO
   ↓
JSON
```

Let's walk through it.

### Step 1: Database

Your database has a row:

```text
id = 1
name = Rafi
email = rafi@example.com
password = secret123
```

↓

### Step 2: Entity

JPA/Hibernate represents that row as:

```java
Tenant tenant
```

Containing:

```java
tenant.getId();
tenant.getName();
tenant.getEmail();
tenant.getPassword();
```

↓

### Step 3: DTO

Before sending data outside the backend, we can create:

```java
TenantDTO tenantDTO
```

Containing only:

```java
id
name
email
```

↓

### Step 4: JSON

Spring Boot sends:

```json
{
    "id": 1,
    "name": "Rafi",
    "email": "rafi@example.com"
}
```

↓

### Step 5: Angular

Later, Angular receives that JSON.

```text
Database
    ↓
Tenant Entity
    ↓
TenantDTO
    ↓
JSON response
    ↓
Angular
```

***

# 6. A JDBC comparison

You already know JDBC, so think about it this way.

With JDBC, you might write:

```java
ResultSet resultSet = statement.executeQuery();
```

Then manually take the database values:

```java
String name = resultSet.getString("name");
String email = resultSet.getString("email");
```

And put them into a Java object.

With JPA:

```text
Database Row
      ↓
JPA/Hibernate
      ↓
Entity Object
```

With DTOs, there is another step:

```text
Database Row
      ↓
Entity
      ↓
DTO
      ↓
JSON
```

The Entity handles the application's representation of persisted data, while the DTO can represent the **specific data you want to transfer**.

***

# 7. Why might Entity and DTO be different?

They do **not** have to contain the same fields.

For example:

## Database / Entity

```java
Tenant
```

```text
id
name
email
password
phoneNumber
monthlyRent
internalNotes
```
# Session 3.4 — DTO Concepts
But maybe Angular only needs:

```java
TenantDTO
```

```text
id
name
email
phoneNumber
```

So:

```text
ENTITY                         DTO
------                         ---
id                 →          id
name               →          name
email              →          email
password           →          ❌
phoneNumber        →          phoneNumber
monthlyRent        →          ❌
internalNotes      →          ❌
```

The DTO is designed around:

> **What data needs to be transferred?**

Not necessarily:

> **What columns exist in the database?**

This is an important idea.

***

# 8. Basic example in code

We are **not building the full DTO architecture yet**. Day 4 will deal with the proper implementation.

For now, let's just see the basic idea.

## Entity

```java
@Entity
public class Tenant {

    @Id
    @GeneratedValue
    private Long id;

    private String name;
    private String email;
    private String password;
}
```

## DTO

```java
public class TenantDTO {

    private Long id;
    private String name;
    private String email;
}
```

Conceptually, we can copy selected data:

```java
TenantDTO dto = new TenantDTO();

dto.setId(tenant.getId());
dto.setName(tenant.getName());
dto.setEmail(tenant.getEmail());
```

Notice that we did **not** copy:

```java
tenant.getPassword();
```

So the transformation is:

```text
Tenant Entity
      ↓
Choose the data we want
      ↓
TenantDTO
```

Then Spring Boot can eventually turn the DTO into JSON.

***

# 9. Important: DTO does not automatically mean security only

The password example is easy to understand, but DTOs are useful for more than hiding sensitive data.

Suppose your Entity contains:

```text
id
name
email
phoneNumber
monthlyRent
internalNotes
createdAt
updatedAt
```

But one API endpoint only needs:

```text
name
email
```

You could use a DTO representing only those values.

So DTOs can help us:

* control what data is transferred
* avoid sending unnecessary data
* separate database structure from API structure
* prevent exposing fields that should stay internal

You do **not** need to memorize advanced DTO patterns yet.

Just understand the basic purpose.

***

# 10. Entity and DTO are not enemies

Don't think:

> Entity = wrong
> DTO = correct

Instead:

```text
Entity → used for persistence/database work

DTO → used for transferring data
```

They can work together.

For example:

```text
PostgreSQL
    ↓
Tenant Entity
    ↓
TenantDTO
    ↓
JSON
    ↓
Angular
```

And when data comes from the frontend, the direction can also be:

```text
Angular
    ↓
JSON
    ↓
DTO
    ↓
Entity
    ↓
Database
```

You do not need to implement that full process yet. Just understand that **DTOs can carry data in either direction**.

***

# Small practical exercise

Suppose your database Entity is:

```java
@Entity
public class Tenant {

    @Id
    private Long id;

    private String name;
    private String email;
    private String password;
    private String internalNotes;
}
```

Your API should send only:

* `id`
* `name`
* `email`

### Question

What should the DTO contain?

Think about it before looking:

```java
public class TenantDTO {

    private Long id;
    private String name;
    private String email;
}
```

It should **not** contain:

```text
password
internalNotes
```

Because those are not part of the data we want to transfer to the frontend.

***

# Session 3.4 Summary

The main idea is:

```text
Entity
  =
Object representing database data
```

```text
DTO
 =
Object representing data being transferred
```

Typical API flow:

```text
Database
   ↓
Entity
   ↓
DTO
   ↓
JSON
   ↓
Angular
```

And the reverse direction can be:

```text
Angular
   ↓
JSON
   ↓
DTO
   ↓
Entity
   ↓
Database
```

### The most important thing to remember

> **An Entity describes persisted/database data, while a DTO describes the data you want to transfer between parts of your application.**

***

# Quick checkpoint

Answer these without looking back:

1. What does **DTO** stand for?
2. What is the main difference between an **Entity** and a **DTO**?
3. If your `Tenant` Entity contains a `password`, why might you not want that field inside a `TenantDTO`?
4. Complete this flow:

```text
Database
   ↓
?
   ↓
?
   ↓
JSON
```

Once you're comfortable with those answers, you've understood the **conceptual goal of Session 3.4**. The actual fuller DTO implementation can wait until Day 4, exactly as your syllabus intends.
