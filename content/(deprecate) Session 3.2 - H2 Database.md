# Session 3.2 — H2 Database

Today we are doing **one specific thing**:

> Connect your Spring Boot + JPA application to an **H2 database** instead of PostgreSQL.

The goal is to make this flow understandable:

```text
Entity
   ↓
Repository
   ↓
JPA / Hibernate
   ↓
H2
```

Think of H2 as a **temporary practice database**. It lets us focus on JPA/Hibernate without worrying about PostgreSQL installation, database names, usernames, passwords, etc.

***

## 1. What is H2?

**H2 is a relational database**, just like PostgreSQL.

You can think:

```text
PostgreSQL  → real relational database
MySQL       → real relational database
H2          → lightweight relational database
```

H2 supports things you already know from SQL:

```sql
CREATE TABLE
INSERT
SELECT
UPDATE
DELETE
```

So H2 isn't some completely different database concept.

The important difference for this lesson is that H2 can run **in memory**.

***

# 2. What does "in-memory database" mean?

Normally, when you use PostgreSQL:

```text
Spring Boot
    ↓
PostgreSQL
    ↓
Data stored on disk
```

If you shut down your application, the database still exists.

With an in-memory H2 database:

```text
Spring Boot starts
       ↓
H2 database is created in memory
       ↓
Your application uses it
       ↓
Spring Boot stops
       ↓
Database disappears
```

For example, suppose we save:

```text
Tenant
id: 1
name: Rahim
```

While the application is running:

```text
H2
└── tenant
    └── 1, Rahim
```

Stop the application:

```text
H2 disappears
```

Start it again:

```text
Empty H2 database
```

### Why is that useful for learning?

Because you don't need to worry about maintaining a real database.

You can experiment freely.

For example:

> "Let me change my Entity."

Run the application.

Test it.

Break something.

Delete the application.

Start again.

You get a fresh database.

That's perfect for learning JPA.

***

# 3. Why are we using H2 now?

You already know PostgreSQL.

So why not simply use PostgreSQL?

Because right now we're trying to understand:

```text
Entity
   ↓
Repository
   ↓
JPA/Hibernate
   ↓
Database
```

If PostgreSQL configuration is also involved, you have another layer to worry about:

```text
Entity
   ↓
Repository
   ↓
JPA/Hibernate
   ↓
PostgreSQL configuration
   ↓
PostgreSQL
```

You might encounter things like:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/Practice_DB
spring.datasource.username=...
spring.datasource.password=...
```

And then wonder:

> "Is my JPA code broken, or is my PostgreSQL connection broken?"

H2 removes much of that configuration.

So:

**H2 is not replacing PostgreSQL in your knowledge.**

We're using it as a **learning environment for JPA**.

***

# 4. Add H2 to your Spring Boot project

Open your `pom.xml`.

You should already have something similar to:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

Now add H2:

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

So you have:

```xml
<dependencies>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <scope>runtime</scope>
    </dependency>

</dependencies>
```

### What does `<scope>runtime</scope>` mean?

For this lesson, don't overthink it.

It basically tells Maven that H2 is needed when the application **runs**.

You don't need to study Maven dependency scopes deeply right now.

***

# 5. Configure H2

Now open:

```text
src
└── main
    └── resources
        └── application.properties
```

Put this in it:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver

spring.jpa.hibernate.ddl-auto=create
spring.jpa.show-sql=true
```

Let's understand each important line.

***

## `spring.datasource.url`

```properties
spring.datasource.url=jdbc:h2:mem:testdb
```

This says:

> Use an H2 database called `testdb`, stored in memory.

Compare it with PostgreSQL:

```text
jdbc:postgresql://localhost:5432/Practice_DB
```

H2:

```text
jdbc:h2:mem:testdb
```

The important part is:

```text
mem
```

which means **memory**.

***

## `spring.datasource.driver-class-name`

```properties
spring.datasource.driver-class-name=org.h2.Driver
```

This tells Spring Boot which JDBC driver to use for H2.

You don't need to memorize this line yet.

***

## `spring.jpa.hibernate.ddl-auto`

```properties
spring.jpa.hibernate.ddl-auto=create
```

This tells Hibernate to create the database tables based on your Entity mappings.

For example, if you have:

```java
@Entity
public class Tenant {

    @Id
    private Long id;

    private String name;
}
```

Hibernate can create a corresponding table.

Conceptually:

```text
Tenant Entity
     ↓
Hibernate
     ↓
CREATE TABLE tenant (...)
```

We're keeping this at a **basic understanding** level for this session.

***

## `spring.jpa.show-sql`

```properties
spring.jpa.show-sql=true
```

This is useful for learning because Hibernate will show SQL in your console.

For example, you might see:

```sql
select
    t1_0.id,
    t1_0.name
from
    tenant t1_0
```

That's actually very useful for you because you already know SQL.

You can see:

> "Ah! This Java repository operation caused Hibernate to execute this SQL."

***

# 6. Let's build a tiny example

Don't use your whole Landlord project yet.

Let's make something extremely small.

Suppose we have:

```text
Product
```

Create:

```text
src/main/java
└── com.example.demo
    ├── Product.java
    └── ProductRepository.java
```

Your package structure may be different. That's fine.

***

## Product Entity

```java
package com.example.demo;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;

@Entity
public class Product {

    @Id
    private Long id;

    private String name;

    private double price;

    public Product() {
    }

    public Product(Long id, String name, double price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }

    public Long getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }
}
```

The important part for **today's lesson** is:

```java
@Entity
```

This tells JPA:

> This Java class represents something that should be persisted in the database.

And:

```java
@Id
private Long id;
```

identifies the primary key.

You learned the deeper Entity/JPA concepts in the previous session, so we're not going to restart that lesson here.

***

# 7. Create the Repository

```java
package com.example.demo;

import org.springframework.data.jpa.repository.JpaRepository;

public interface ProductRepository extends JpaRepository<Product, Long> {
}
```

Again, don't get distracted by Repository details.

The important thing today is the connection:

```text
Product
   ↓
ProductRepository
   ↓
JPA/Hibernate
   ↓
H2
```

***

# 8. How does H2 actually get used?

Here's the interesting part.

We don't write:

```java
Connection connection =
    DriverManager.getConnection(...);
```

We don't manually write:

```sql
INSERT INTO product ...
```

Instead, Spring Data JPA gives us repository operations.

For example:

```java
productRepository.save(
    new Product(1L, "Keyboard", 1200)
);
```

Conceptually:

```text
Java object
   ↓
Product
   ↓
Repository
   ↓
JPA
   ↓
Hibernate
   ↓
SQL
   ↓
H2
```

Hibernate might ultimately execute SQL similar to:

```sql
insert into product (name, price, id)
values ('Keyboard', 1200, 1);
```

**You don't write that SQL yourself.**

That's one of the major things you're learning with JPA.

***

# 9. The complete picture

This is the picture I want you to understand from this session:

```text
             Your Java code
                  │
                  ▼
             Product Entity
                  │
                  ▼
          ProductRepository
                  │
                  ▼
             Spring Data JPA
                  │
                  ▼
              Hibernate
                  │
                  ▼
                H2
             (database)
```

And H2 is simply the database at the bottom.

You could later replace H2 with PostgreSQL:

```text
Entity
   ↓
Repository
   ↓
JPA
   ↓
Hibernate
   ↓
PostgreSQL
```

Your Entity and Repository concepts don't fundamentally change just because the database changes.

**That's exactly why we're using H2 now.**

***

# 10. Practical exercise 🧪

Now I want **you** to do this instead of just reading.

### Step 1

Add the H2 dependency to `pom.xml`.

### Step 2

Configure:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.jpa.hibernate.ddl-auto=create
spring.jpa.show-sql=true
```

### Step 3

Create:

```java
@Entity
public class Product
```

with:

```text
id
name
price
```

### Step 4

Create:

```java
ProductRepository
```

extending:

```java
JpaRepository<Product, Long>
```

### Step 5

Start your Spring Boot application.

Look at the console.

You should see Hibernate doing database-related work.

You may see SQL resembling:

```sql
create table product ...
```

That is the important moment.

It means:

```text
Your Entity
      ↓
Hibernate
      ↓
H2 table
```

***

# 🧠 Checkpoint

Don't look back if possible. Answer these in your own words:

### 1.

What is H2?

### 2.

What does **in-memory database** mean?

### 3.

Why are we using H2 instead of PostgreSQL while learning JPA?

### 4.

What does this mean?

```properties
spring.datasource.url=jdbc:h2:mem:testdb
```

Especially: what does `mem` tell you?

### 5.

Complete the flow:

```text
Entity
   ↓
Repository
   ↓
__________
   ↓
H2
```

### 6.

If you stop a Spring Boot application using:

```text
jdbc:h2:mem:testdb
```

and start it again, what happens to the data?

Answer these **without looking back**. I’ll check your understanding before we move on.
