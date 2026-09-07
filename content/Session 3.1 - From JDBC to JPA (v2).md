# Session 3.1 — From JDBC to JPA

You already know the basic JDBC flow, so we're going to use that as the starting point.

The main goal of this lesson is **not to learn JPA coding yet**. It's to understand what these three names mean and how they fit together:

```text
JPA
 ↓
Hibernate
 ↓
Spring Data JPA
```

But there's an important correction to that diagram:

> **JPA is not something that sits "above" Hibernate in a strict execution chain.**
> JPA is a specification, Hibernate is an implementation, and Spring Data JPA is a Spring abstraction that makes working with JPA easier.

Let's build that understanding step by step.

***

## 1. First: What you already know — JDBC

Suppose you have a PostgreSQL table:

```sql
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    price NUMERIC
);
```

And you want to retrieve products using JDBC.

Conceptually, you do something like:

```text
Java code
   ↓
Connection
   ↓
PreparedStatement
   ↓
SQL
   ↓
ResultSet
   ↓
Java Product object
```

For example:

```java
String sql = "SELECT id, name, price FROM products";

PreparedStatement ps = connection.prepareStatement(sql);

ResultSet rs = ps.executeQuery();

while (rs.next()) {

    Product product = new Product();

    product.setId(rs.getInt("id"));
    product.setName(rs.getString("name"));
    product.setPrice(rs.getDouble("price"));
}
```

Notice what **you** are doing.

You are explicitly telling Java:

> "Execute this SQL."

Then:

> "Take the `id` column from the ResultSet and put it into the Product object's `id`."

Then:

> "Take the `name` column and put it into the Product object's `name`."

So JDBC makes you deal fairly directly with the database.

***

# 2. What if Java could work with objects more directly?

Imagine you have:

```java
Product product = new Product();

product.setName("Laptop");
product.setPrice(80000);
```

You want to save this object into the database.

With JDBC, you would typically write SQL yourself:

```sql
INSERT INTO products (name, price)
VALUES (?, ?);
```

Then:

```java
PreparedStatement ps =
    connection.prepareStatement(sql);

ps.setString(1, product.getName());
ps.setDouble(2, product.getPrice());

ps.executeUpdate();
```

There's a lot of database plumbing.

JPA was created around the idea of:

> **Map Java objects to database data.**

This is where **JPA** comes in.

***

# 3. What is JPA?

**JPA = Jakarta Persistence API**

For our purposes, think of JPA as:

> **A standard/specification that defines how Java objects can be mapped to relational database tables.**

The important word is **specification**.

JPA itself is **not the actual database implementation**.

Think of it like this:

```text
JPA
=
Rules / standard / API
```

It defines concepts such as:

```text
Java Object  ↔  Database Row
Java Class   ↔  Database Table
Java Field   ↔  Database Column
```

For example:

```java
class Product {

    int id;
    String name;
    double price;
}
```

can conceptually correspond to:

```text
products
-----------------
id
name
price
```

This process is called **Object-Relational Mapping (ORM)**.

You don't need to study ORM deeply right now. Just remember:

> **ORM means mapping Java objects to relational database data.**

***

## 4. JPA is a specification — not the engine

This is probably the most important part of today's lesson.

Suppose someone creates a specification saying:

> "Here are the standard rules and APIs for Java persistence."

That's JPA.

But someone still needs to **actually implement those rules**.

That's where Hibernate comes in.

***

# 5. What is Hibernate?

Hibernate ORM is an implementation of the JPA specification.

In simple terms:

> **JPA tells us what should be possible. Hibernate actually does the work.**

Think about an interface in Java.

You might have:

```java
interface PaymentService {
    void pay();
}
```

The interface defines what must exist.

Then:

```java
class BkashPaymentService implements PaymentService {

    public void pay() {
        // actual implementation
    }
}
```

`PaymentService` is the contract.

`BkashPaymentService` provides the implementation.

Similarly, conceptually:

```text
JPA
↓
Specification / standard

Hibernate
↓
Implementation
```

So:

```text
JPA says:
"Here is the standard way to do persistence."

Hibernate says:
"Okay, I'll implement that standard."
```

### Important

Don't memorize:

> "JPA = Hibernate"

They are **not the same thing**.

Instead:

```text
JPA       → specification
Hibernate → implementation
```

***

# 6. Where does Spring Data JPA come in?

Now we add the third piece:

**Spring Data JPA**

Its purpose is to make working with JPA much easier in a Spring application.

Without Spring Data JPA, you may have to deal with more JPA-related code yourself.

Spring Data JPA gives you convenient repository abstractions.

For example, eventually you can have something conceptually like:

```java
public interface ProductRepository
        extends JpaRepository<Product, Integer> {
}
```

And then you can use methods such as:

```java
productRepository.findAll();
```

or:

```java
productRepository.findById(id);
```

or:

```java
productRepository.save(product);
```

You didn't write the SQL yourself.

You didn't manually create a `PreparedStatement`.

You didn't manually process a `ResultSet`.

Spring Data JPA provides a lot of that infrastructure for you.

**Don't worry about `JpaRepository` yet.** That's a later coding topic. For today's lesson, just understand why it exists.

***

# 7. So how do the three relate?

Here's the mental model I want you to remember:

```text
                 YOUR SPRING APPLICATION
                         │
                         ▼
                 Spring Data JPA
                         │
                         ▼
                       JPA
                         │
                         ▼
                    Hibernate
                         │
                         ▼
                    JDBC / Driver
                         │
                         ▼
                    PostgreSQL
```

But don't interpret this as:

> "JPA directly calls Hibernate."

Instead, think:

```text
Spring Data JPA
    ↓
makes JPA easier to use

JPA
    ↓
defines the standard persistence API

Hibernate
    ↓
implements JPA and performs ORM/database work

JDBC
    ↓
provides lower-level database communication

PostgreSQL
    ↓
actual database
```

That's the relationship.

***

# 8. JDBC vs JPA approach

Let's compare the mindset.

### JDBC

You think primarily in terms of:

```text
Database
   ↓
SQL
   ↓
ResultSet
   ↓
Java Object
```

For example:

```java
String sql = "SELECT * FROM products";
```

You're directly working with SQL.

***

### JPA

You start thinking more in terms of:

```text
Java Object
      ↕
Database data
```

For example, conceptually:

```java
Product product
```

represents database data.

JPA/Hibernate handles much of the translation between the object world and relational database world.

***

# 9. A useful analogy

Since you know Angular, here's a rough analogy.

Imagine you have:

```text
Angular
   ↓
HttpClient
   ↓
HTTP
   ↓
Backend
```

`HttpClient` makes HTTP communication easier for your Angular code.

Similarly, in the Spring world:

```text
Spring Data JPA
      ↓
      JPA
      ↓
   Hibernate
      ↓
     JDBC
      ↓
  PostgreSQL
```

Spring Data JPA gives you a convenient way to work with persistence.

But remember: this is only an analogy. Angular's `HttpClient` and Spring Data JPA aren't equivalent technologies.

***

# 10. The big picture

Let's put everything together.

### With JDBC

You might manually handle:

```text
Java
 ↓
Connection
 ↓
PreparedStatement
 ↓
SQL
 ↓
ResultSet
 ↓
Java Object
```

### With JPA/Hibernate/Spring Data JPA

The goal becomes more like:

```text
Java Object
     ↕
JPA
     ↕
Hibernate
     ↓
JDBC
     ↓
PostgreSQL
```

And Spring Data JPA gives you a convenient Spring programming model around JPA.

So the responsibilities are roughly:

| Technology          | What it is                                            |
| ------------------- | ----------------------------------------------------- |
| **JPA**             | Standard/specification for Java persistence           |
| **Hibernate**       | Implementation of JPA; performs ORM work              |
| **Spring Data JPA** | Spring abstraction that makes JPA easier to use       |
| **JDBC**            | Lower-level Java API for communicating with databases |
| **PostgreSQL**      | Your actual relational database                       |

***

# 🧠 One thing you absolutely must remember

If I ask:

### "Is JPA a library like Hibernate?"

Your answer should be:

> **No. JPA is a specification/API standard. Hibernate is an implementation of that specification.**

And:

### "What is Spring Data JPA?"

> **It's a Spring project/abstraction that makes working with JPA much easier, especially through repository-based database operations.**

That's enough for this session.

***

# 🛠️ Small Practical Exercise

Don't code yet.

Look at this stack:

```text
Product.java
     ↓
Spring Data JPA
     ↓
JPA
     ↓
Hibernate
     ↓
JDBC
     ↓
PostgreSQL
```

Now try to explain **in your own words** what each layer is doing.

For example:

```text
Product.java
→ ?

Spring Data JPA
→ ?

JPA
→ ?

Hibernate
→ ?

JDBC
→ ?

PostgreSQL
→ ?
```

Don't look back while answering if you can avoid it.

***

# 🧠 Checkpoint

Answer these **without looking back**:

### 1.

What is JPA?

### 2.

Is JPA an implementation or a specification?

### 3.

What is Hibernate?

### 4.

What is the relationship between JPA and Hibernate?

### 5.

What is Spring Data JPA?

### 6.

In your own words, explain this:

```text
Spring Data JPA
       ↓
      JPA
       ↓
   Hibernate
       ↓
      JDBC
       ↓
  PostgreSQL
```

Once you answer these, I'll check your understanding before we move to the next topic.
