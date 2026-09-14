# Session 3.5 — Repositories

This session is about **Repositories** and, specifically, how `JpaRepository` lets your Spring application talk to the database without you writing the usual JDBC CRUD code yourself.

You already learned the pieces leading up to this:

```text
Java Object
    ↓
@Entity
Tenant
    ↓
JpaRepository
TenantRepository
    ↓
JPA / Hibernate
    ↓
Database
```

We'll keep this practical.

***

## 1. What is a Repository?

In a Spring application, a **Repository is the part responsible for accessing stored data**.

For example, suppose your database has a `tenant` table.

You might want to:

* get all tenants
* get one tenant
* save a tenant
* delete a tenant

With JDBC, you'd normally write SQL and JDBC code yourself:

```java
Connection
PreparedStatement
SQL
ResultSet
```

For example:

```sql
SELECT * FROM tenant;
```

and then manually turn the result into Java objects.

With Spring Data JPA, the Repository handles much of that work for you.

You create an interface:

```java
public interface TenantRepository
        extends JpaRepository<Tenant, Long> {
}
```

And that's it.

You haven't written:

```sql
SELECT
INSERT
UPDATE
DELETE
```

yet Spring gives you CRUD operations.

***

# 2. What is `JpaRepository`?

`JpaRepository` is a Spring Data interface that provides many common database operations.

Your code:

```java
public interface TenantRepository
        extends JpaRepository<Tenant, Long> {
}
```

means roughly:

> "Create a repository for the `Tenant` entity, whose ID is a `Long`."

The important part is:

```java
JpaRepository<Tenant, Long>
```

There are **two generic parameters** here.

***

# 3. Understanding `JpaRepository<T, ID>`

The general form is:

```java
JpaRepository<T, ID>
```

### `T` = Entity type

`T` tells Spring:

> "What kind of object does this repository work with?"

For us:

```java
JpaRepository<Tenant, Long>
```

So:

```text
T = Tenant
```

The repository works with `Tenant` objects.

***

### `ID` = ID type

`ID` tells Spring:

> "What data type is the entity's primary-key ID?"

Suppose your entity has:

```java
@Id
@GeneratedValue
private Long id;
```

Then the ID type is:

```java
Long
```

Therefore:

```java
JpaRepository<Tenant, Long>
```

### Think of it like this:

```text
JpaRepository<Tenant, Long>
               │       │
               │       └── ID is Long
               └────────── Entity is Tenant
```

***

# 4. Our `Tenant` entity

Let's use a simple entity from the previous session:

```java
@Entity
@Table(name = "tenant")
public class Tenant {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    private String email;

    // constructors, getters, setters
}
```

So our database concept is:

```text
Tenant Java object
        ↕
tenant database row
```

Now create the repository.

***

# 5. Creating `TenantRepository`

### Where?

Inside your Spring Boot project, create:

```text
src
└── main
    └── java
        └── com.lord.LandLord
            ├── Controller
            ├── Entity
            │   └── Tenant.java
            └── Repository
                └── TenantRepository.java
```

The exact package names can differ in your project, but the important part is that you have a `Repository` package.

### `TenantRepository.java`

```java
package com.lord.LandLord.Repository;

import com.lord.LandLord.Entity.Tenant;
import org.springframework.data.jpa.repository.JpaRepository;

public interface TenantRepository
        extends JpaRepository<Tenant, Long> {
}
```

Notice something interesting:

**There is no method implementation.**

No:

```java
public List<Tenant> findAll() {
    ...
}
```

No SQL.

No JDBC.

Spring Data provides the implementation for you.

***

# 6. Why is it an `interface`?

You might wonder:

> "How can an interface actually access the database?"

Normally, you would need a class that implements an interface.

But ==Spring Data JPA creates the implementation for the repository for you at runtime==.

You write:

```java
public interface TenantRepository
        extends JpaRepository<Tenant, Long> {
}
```

Spring essentially handles the implementation behind the scenes.

You don't need to write that implementation yourself.

For now, the important idea is simply:

```text
You define what repository you need
              ↓
Spring Data creates the working repository
              ↓
You use its methods
```

***

# 7. Built-in CRUD operations

Because:

```java
TenantRepository extends JpaRepository
```

your repository automatically gets methods such as:

```java
findAll()
findById()
save()
deleteById()
```

These are the methods you need to understand for this session.

***

# 8. `findAll()`

Suppose you want **all tenants**.

You can call:

```java
tenantRepository.findAll();
```

It returns a collection of `Tenant` objects.

Typically:

```java
List<Tenant> tenants = tenantRepository.findAll();
```

Conceptually:

```text
tenantRepository.findAll()
        ↓
     Database
        ↓
all tenant rows
        ↓
List<Tenant>
```

You didn't write:

```sql
SELECT * FROM tenant;
```

Spring Data/JPA handles the database interaction.

### JDBC comparison

With JDBC you might do:

```java
SELECT * FROM tenant
```

then:

```text
ResultSet
   ↓
Tenant objects
   ↓
List<Tenant>
```

With JPA:

```java
tenantRepository.findAll()
```

does much of that work for you.

***

## Small exercise

If you wanted to store all tenants in a variable, complete this:

```java
List<Tenant> tenants = ____________________;
```

**Answer:**

```java
List<Tenant> tenants = tenantRepository.findAll();
```

***

# 9. `findById()`

Now suppose you want tenant with ID `5`.

You can write:

```java
tenantRepository.findById(5L);
```

Why `5L` instead of just `5`?

Because our ID type is:

```java
Long
```

and `5L` is a Java `long` literal that can be used as a `Long` value through boxing.

The method returns:

```java
Optional<Tenant>
```

So:

```java
Optional<Tenant> tenant =
        tenantRepository.findById(5L);
```

Why `Optional`?

Because tenant `5` might **not exist**.

There are two possibilities:

```text
ID 5 exists
     ↓
Tenant object


ID 5 doesn't exist
     ↓
empty Optional
```

For this session, remember:

```java
findById()
```

means:

> Find one entity using its ID.

***

## Small exercise

Which method would you use?

> "Get the tenant whose ID is 10."

Answer:

```java
tenantRepository.findById(10L);
```

***

# 10. `save()` [^1]

Now let's create a tenant.

For example:

```java
Tenant tenant = new Tenant();

tenant.setName("Rahim");
tenant.setEmail("rahim@example.com");
```

Then:

```java
tenantRepository.save(tenant);
```

This tells JPA:

> Save this `Tenant` object in the database.

Conceptually:

```text
Tenant object
     ↓
save()
     ↓
JPA / Hibernate
     ↓
Database
```

Depending on the entity's state, `save()` ==can be used for creating or updating an entity==.

For now, the basic idea is:

```java
tenantRepository.save(tenant);
```

= **save the tenant to the database.**

***

## Small exercise

Complete this:

```java
Tenant tenant = new Tenant();
tenant.setName("Karim");

_____________________________;
```

Answer:

```java
tenantRepository.save(tenant);
```

***

# 11. `deleteById()`

Suppose you want to delete tenant ID `5`.

Use:

```java
tenantRepository.deleteById(5L);
```

Conceptually:

```text
deleteById(5L)
       ↓
find/delete database record
       ↓
tenant with ID 5 removed
```

Again, you didn't manually write:

```sql
DELETE FROM tenant
WHERE id = 5;
```

Spring Data JPA handles the database operation.

***

## Small exercise

How would you delete tenant ID `20`?

```java
tenantRepository.________________(20L);
```

Answer:

```java
tenantRepository.deleteById(20L);
```

***

# 12. The four methods together

These four methods cover the basic CRUD operations:

| Method         | Purpose                |
| -------------- | ---------------------- |
| `findAll()`    | Get all records        |
| `findById()`   | Get one record by ID   |
| `save()`       | Create/update a record |
| `deleteById()` | Delete a record by ID  |

Think:

```text
CREATE  → save()
READ    → findAll()
READ    → findById()
DELETE  → deleteById()
```

And `save()` can also handle updates.

***

# 13. What happened to SQL?

This is the important connection to your JDBC knowledge.

### JDBC

You might have written something like:

```java
String sql = "SELECT * FROM tenant";

PreparedStatement statement =
        connection.prepareStatement(sql);

ResultSet resultSet =
        statement.executeQuery();
```

You had to deal with the database interaction yourself.

### Spring Data JPA

You can instead write:

```java
List<Tenant> tenants =
        tenantRepository.findAll();
```

The framework handles the lower-level database work.

Conceptually:

```text
                 Your code
                    │
                    ▼
          TenantRepository
                    │
                    ▼
             JpaRepository
                    │
                    ▼
                  JPA
                    │
                    ▼
               Hibernate
                    │
                    ▼
               PostgreSQL
```

You don't need to memorize every layer yet. The important thing is that **your repository gives you a convenient Java API for database operations**.

***

# 14. What does the repository know about?

This line is doing a lot:

```java
public interface TenantRepository
        extends JpaRepository<Tenant, Long> {
}
```

Let's translate it into normal English:

> "This is a repository for the `Tenant` entity, and the ID of a Tenant is a `Long`."

Therefore Spring knows that:

```java
findAll()
```

should return:

```java
List<Tenant>
```

and:

```java
findById(5L)
```

should look for:

```text
Tenant with ID 5
```

and:

```java
save(tenant)
```

should save a:

```text
Tenant
```

That's why specifying:

```java
<Tenant, Long>
```

matters.

***

# 15. One important distinction

Don't confuse these three things:

### Entity

```java
Tenant
```

Represents your data/object.

### Repository

```java
TenantRepository
```

Provides access to stored `Tenant` data.

### Database

For example:

```text
PostgreSQL
```

Actually stores the data.

So:

```text
Tenant
  │
  │ represented by
  ▼
Database row

TenantRepository
  │
  │ accesses
  ▼
Database
```

The repository is **not the database**.

It is the component your application uses to access the database.

***

# 16. The core code you should remember

Your repository:

```java
public interface TenantRepository
        extends JpaRepository<Tenant, Long> {
}
```

Then the four operations:

```java
tenantRepository.findAll();
```

```java
tenantRepository.findById(5L);
```

```java
tenantRepository.save(tenant);
```

```java
tenantRepository.deleteById(5L);
```

That's the heart of Session 3.5.

***

# Practical exercise

👉 [[s3.5 Practical - Build a Tenant Repository]] 👈

Before moving on, try to answer these without looking back:

### 1.

What does this mean?

```java
JpaRepository<Tenant, Long>
```

### 2.

Which method gets **all** tenants?

```text
A. save()
B. findAll()
C. findById()
D. deleteById()
```

### 3.

Which method gets tenant ID `7`?

### 4.

Which method saves a `Tenant` object?

### 5.

Which method deletes tenant ID `7`?

### 6.

Why doesn't this repository contain SQL?

```java
public interface TenantRepository
        extends JpaRepository<Tenant, Long> {
}
```

***

## Short checkpoint

Try answering these in your own words:

> **A.** What is the job of a Repository?

> **B.** In `JpaRepository<Tenant, Long>`, what do `Tenant` and `Long` represent?

> **C.** What is the difference between `findAll()` and `findById()`?

> **D.** What does `save(tenant)` do?

> **E.** What does `deleteById(5L)` do?

Once these make sense, you understand the basic Repository layer.

# Footnote
[^1]: [[s3.5 Practical - Build a Tenant Repository]].