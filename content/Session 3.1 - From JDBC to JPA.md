# Session 3.1 — From JDBC to JPA

This session is about understanding **what JPA, Hibernate, and Spring Data JPA are**, and most importantly, **how they fit together**.

You already know JDBC, so we'll use that as the starting point.

***

## 1. First: What happens with JDBC?

Suppose you have a `Tenant` table:

```text
tenant
----------------
id
name
rent
```

With JDBC, you might write something like:

```java
Connection connection = ...;

PreparedStatement statement =
    connection.prepareStatement(
        "SELECT id, name, rent FROM tenant"
    );

ResultSet result = statement.executeQuery();

while (result.next()) {

    Tenant tenant = new Tenant();

    tenant.setId(result.getInt("id"));
    tenant.setName(result.getString("name"));
    tenant.setRent(result.getDouble("rent"));

}
```

Notice what **you** are doing:

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
Java object
```

You explicitly tell Java:

> Connect to the database, execute this SQL, get the result, and put each column into my Java object.

That's JDBC.

***

# 2. So what is JPA?

**JPA = Java Persistence API**

The important word here is **persistence**.

Persistence basically means:

> Keeping Java objects' data in a database so that the data survives after the program stops.

For example:

```java
Tenant tenant = new Tenant();

tenant.setName("Rahim");
tenant.setRent(15000);
```

This is a Java object.

JPA gives Java a **standard way to map Java objects to database data**.

Conceptually:

```text
Java Object                 Database
-----------                 --------

Tenant          ←→         tenant table

id              ←→         id
name            ←→         name
rent            ←→         rent
```

This is called **Object-Relational Mapping (ORM)**.

You don't need to study ORM deeply yet. For this session, just remember:

> **JPA lets us work with database data through Java objects instead of manually handling everything with JDBC and SQL.**

***

# 3. JPA is NOT Hibernate

This distinction is extremely important.

Think of JPA as a **standard/specification**.

It defines rules for things like:

> "A Java class can represent a database table."

> "A Java field can represent a database column."

> "There should be a way to save, find, update, and delete persistent objects."

But JPA itself isn't the program doing all that work.

That's where **Hibernate** comes in.

***

# 4. What is Hibernate?

**Hibernate is an implementation of JPA.**

In simple terms:

```text
JPA
↓
Rules / standard

Hibernate
↓
Software that implements those rules
```

A useful analogy:

### JDBC

You already know:

```text
JDBC API
   ↓
PostgreSQL JDBC Driver
   ↓
PostgreSQL
```

JDBC defines a standard way for Java to communicate with databases.

The PostgreSQL driver actually implements that communication for PostgreSQL.

Similarly:

```text
JPA
 ↓
Hibernate
 ↓
Database
```

JPA defines the standard.

Hibernate does the actual work.

***

# 5. Then what is Spring Data JPA?

Now we add Spring.

Spring Data JPA sits **on top of JPA** and makes working with JPA much easier.

Think of the layers like this:

```text
Your Spring Boot application
          ↓
   Spring Data JPA
          ↓
         JPA
          ↓
      Hibernate
          ↓
      PostgreSQL
```

Each layer has a different role.

### JPA

Defines the standard way of working with persistent Java objects.

### Hibernate

Actually implements that JPA standard.

### Spring Data JPA

Provides convenient Spring-based tools so you don't have to write as much JPA-related code yourself.

***

# 6. The big picture

Compare what you've already learned with what we're moving toward.

### JDBC approach

```text
Your Java code
      ↓
     JDBC
      ↓
    SQL
      ↓
 PostgreSQL
```

You manually deal with things such as:

```java
PreparedStatement
ResultSet
SQL
```

***

### Spring Data JPA approach

```text
Your Java code
      ↓
Spring Data JPA
      ↓
     JPA
      ↓
  Hibernate
      ↓
 PostgreSQL
```

Now you can work much more directly with Java objects.

For example, conceptually:

```java
Tenant tenant = ...;

repository.save(tenant);
```

Instead of manually writing:

```sql
INSERT INTO tenant ...
```

and manually handling:

```java
PreparedStatement
```

and:

```java
ResultSet
```

Spring Data JPA + JPA + Hibernate handle much of that work underneath.

**Don't worry yet about exactly how `repository.save()` works.** That's a later topic.

For this session, understand the layers.

***

# 7. A very important clarification

Don't think:

> "JPA replaces the database."

It doesn't.

Your PostgreSQL database is still there.

Don't think:

> "Hibernate is a database."

It isn't.

Hibernate communicates with the database.

And don't think:

> "Spring Data JPA is another database technology."

It isn't.

It's a tool that makes JPA-based database access easier in Spring.

***

# 8. One simple mental model

Imagine you're ordering food.

```text
You
 ↓
Waiter
 ↓
Restaurant system
 ↓
Kitchen
 ↓
Food
```

In our case:

```text
Your application
      ↓
Spring Data JPA
      ↓
JPA
      ↓
Hibernate
      ↓
PostgreSQL
```

But remember: this is only an analogy for understanding the roles, **not a literal execution sequence for every database operation**.

***

# 9. Practical example

Let's make a very small Java model:

```java
public class Tenant {

    private int id;
    private String name;
    private double rent;

}
```

Our database has:

```text
tenant
----------------
id
name
rent
```

The basic idea behind JPA is:

```text
Tenant class
     ↕
tenant table
```

And:

```text
Tenant.id
     ↕
tenant.id

Tenant.name
     ↕
tenant.name

Tenant.rent
     ↕
tenant.rent
```

This mapping between the **Java object world** and the **database table world** is the fundamental idea you need to understand before moving forward.

***

# 10. JDBC vs JPA — the key difference

### JDBC

You think primarily in terms of:

```text
SQL
↓
ResultSet
↓
Java objects
```

You manually connect the database results to your Java objects.

### JPA

You think more in terms of:

```text
Java objects
↓
database data
```

The JPA/Hibernate machinery handles much of the mapping between them.

So the mindset changes from:

> "How do I execute this SQL and read the ResultSet?"

toward:

> "How do I work with my Java entity/object and let the persistence framework handle the database mapping?"

That's the major reason JPA is useful.

***

# 11. Don't memorize this incorrectly

The relationship is:

```text
Spring Data JPA
       ↓
      JPA
       ↓
   Hibernate
       ↓
   Database
```

But **JPA and Hibernate aren't competing technologies**.

Instead:

```text
JPA = standard/specification
Hibernate = implementation
Spring Data JPA = Spring abstraction/tooling built around JPA
```

That's the core of Session 3.1.

***

# 🧪 Small Exercise

Don't write any Spring code yet.

Answer these in your own words:

### 1.

You already know JDBC. What does JDBC make you work with when retrieving database data?

### 2.

What problem is JPA trying to make easier?

### 3.

Is JPA a database?

### 4.

Is Hibernate the same thing as JPA?

### 5.

Complete this:

```text
Spring Data JPA
       ↓
      _____
       ↓
    Hibernate
       ↓
   PostgreSQL
```

### 6.

If you have:

```java
Tenant
```

and:

```text
tenant table
```

what is JPA helping establish between them?

Answer these **without looking back**. Then I'll check your understanding before we move on.
