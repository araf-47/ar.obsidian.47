# Session 3.3 — Entities

In this session, we are going to make **one Java class represent one database table**.

You already know Java classes and SQL tables, so the main thing to understand is how JPA/Hibernate connects the two.

We will keep this at the **basic, usable level** needed for your LandLord project.

***

## 1. What is an Entity?

An **Entity** is a Java class that JPA/Hibernate can connect to a database table.

For example, suppose our database has a table:

```sql
tenant
-------------------------
id       | name | phone
-------------------------
1        | John | 12345
2        | Alex | 67890
```

We can create a Java class:

```java
public class Tenant {

    private int id;
    private String name;
    private String phone;

}
```

The idea is:

```text
Java                          Database

Tenant object       ↔         tenant row
```

For example:

```text
Tenant object
id = 1
name = "John"
phone = "12345"

            ↕
            
Database row
1 | John | 12345
```

This is the basic idea behind an entity.

### Important distinction

A normal Java class is **not automatically** an entity.

This:

```java
public class Tenant {
    private int id;
    private String name;
}
```

is simply a Java class.

When we add:

```java
@Entity
```

we are telling JPA:

> "Treat this class as an entity that can be mapped to database data."

***

# 2. `@Entity`

`@Entity` marks a Java class as a JPA entity.

Example:

```java
import jakarta.persistence.Entity;

@Entity
public class Tenant {

    private int id;
    private String name;
    private String phone;
}
```

Now JPA knows:

```text
Tenant
   ↓
Entity
   ↓
can be mapped to database
```

### Where does `@Entity` come from?

For modern Spring Boot projects:

```java
import jakarta.persistence.Entity;
```

Notice that it is **`jakarta.persistence`**, not Spring.

JPA provides these annotations.

***

## Small exercise

Look at this:

```java
public class Product {
    private int id;
    private String name;
}
```

Is `Product` currently an entity?

**Answer: No.**

Why?

Because it doesn't have:

```java
@Entity
```

***

# 3. `@Table`

`@Table` lets us specify the database table that the entity [[correspond]]s to.

For example:

```java
@Entity
@Table(name = "tenant")
public class Tenant {
    
}
```

This means:

```text
Java class                 Database table

Tenant          ↔          tenant
```

The `name` is the actual table name.

### Do we always need `@Table`?

No.

For example:

```java
@Entity
public class Tenant {
}
```

is already enough for JPA to map the class to a table using its naming conventions.

But using `@Table` makes the relationship explicit:

```java
@Entity
@Table(name = "tenant")
```

For learning, I want you to use it.

***

# 4. `@Id`

Now we need to identify the **primary key**.

In SQL you already know:

```sql
CREATE TABLE tenant (
    id INTEGER PRIMARY KEY,
    name VARCHAR(100)
);
```

The `id` uniquely identifies each row.

In our Java entity:

```java
@Entity
@Table(name = "tenant")
public class Tenant {

    @Id
    private int id;

    private String name;
}
```

`@Id` means:

> This field is the entity's identifier / primary key.

So:

```java
@Id
private int id;
```

corresponds roughly to:

```sql
id INTEGER PRIMARY KEY
```

***

# 5. ⚠️ `@GeneratedValue` < not working on H2

Usually, we don't want to manually assign every tenant's ID.

For example, we don't want to write:

```java
Tenant tenant = new Tenant();

tenant.setId(1);
```

then the next one:

```java
tenant.setId(2);
```

Instead, we want the database/JPA to generate the ID.

That's what `@GeneratedValue` is for.

```java
@Id
@GeneratedValue
private int id;
```

Together:

```java
@Id
@GeneratedValue
private int id;
```

means:

> `id` is the primary key, and its value should be generated automatically.

Conceptually:

```text
Create Tenant
      ↓
Don't provide ID
      ↓
Database/JPA generates ID
      ↓
1
```

Then another tenant:

```text
Create Tenant
      ↓
Generated ID
      ↓
2
```

### Important

You don't need to study the different ID-generation strategies yet.

For this session, understand only:

```java
@GeneratedValue
```

= **automatically generate the ID**.

***

# 6. `@Column`

`@Column` lets us configure how a Java field maps to a database column.

For example:

```java
@Column(name = "full_name")
private String name;
```

means:

```text
Java field                 Database column

name              ↔       full_name
```

Without `@Column`, JPA normally maps the field based on its naming conventions.

So:

```java
private String name;
```

can correspond to:

```text
name
```

You use `@Column` when you want to explicitly specify/configure the column.

For example:

```java
@Column(name = "phone_number")
private String phone;
```

***

# 7. Putting the annotations together

Now let's combine everything.

Our database conceptually has:

```text
tenant
--------------------------------
id       name       phone_number
--------------------------------
1        John       12345
2        Alex       67890
```

Our Java entity:

```java
@Entity
@Table(name = "tenant")
public class Tenant {

    @Id
    @GeneratedValue
    private int id;

    @Column(name = "name")
    private String name;

    @Column(name = "phone_number")
    private String phone;
}
```

The important mapping is:

```text
Tenant class
      ↓
tenant table

id field
      ↓
id column
      ↓
PRIMARY KEY
      ↓
@GeneratedValue

name field
      ↓
name column

phone field
      ↓
phone_number column
```

***

# 8. The Java Object ↔ Database Row idea

This is the most important part of today's lesson.

Suppose we have:

```java
Tenant tenant = new Tenant();
```

and eventually the object contains:

```text
id = 1
name = "John"
phone = "12345"
```

Think of it as representing this database row:

```text
┌────┬──────┬───────┐
│ id │ name │ phone │
├────┼──────┼───────┤
│ 1  │ John │ 12345 │
└────┴──────┴───────┘
```

So:

```text
Java Object
     ↕
Database Row
```

This is **not** saying that the Java object literally becomes the row.

Rather, JPA/Hibernate understands the mapping between them.

***

# 9. Let's build our `Tenant` entity

Now let's actually create it in your Spring Boot project.

Your structure can be:

```text
src
└── main
    └── java
        └── com.lord.LandLord
            ├── Controller
            ├── Entity
            │   └── Tenant.java
            └── ...
```

Create:

```text
Entity/Tenant.java
```

Put this inside:

```java
package com.lord.LandLord.Entity;

import jakarta.persistence.Entity;
import jakarta.persistence.Table;
import jakarta.persistence.Id;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.Column;

@Entity
@Table(name = "tenant")
public class Tenant {

    @Id
    @GeneratedValue
    private int id;

    @Column(name = "name")
    private String name;

    @Column(name = "phone_number")
    private String phone;

}
```

### What each line does

```java
@Entity
```

> This Java class is a JPA entity.

```java
@Table(name = "tenant")
```

> Map this entity to the `tenant` database table.

```java
@Id
```

> This field is the primary key.

```java
@GeneratedValue
```

> Generate the primary-key value automatically.

```java
@Column(name = "name")
```

> Map this Java field to the `name` column.

```java
@Column(name = "phone_number")
```

> Map this Java field to the `phone_number` column.

***

# 10. One important Java issue: getters/setters

Right now our fields are:

```java
private int id;
private String name;
private String phone;
```

Because they're `private`, other classes can't directly access them.

Normally we'll have getters and setters:

```java
public int getId() {
    return id;
}

public void setId(int id) {
    this.id = id;
}

public String getName() {
    return name;
}

public void setName(String name) {
    this.name = name;
}

public String getPhone() {
    return phone;
}

public void setPhone(String phone) {
    this.phone = phone;
}
```

So our complete basic entity becomes:

```java
package com.lord.LandLord.Entity;

import jakarta.persistence.Entity;
import jakarta.persistence.Table;
import jakarta.persistence.Id;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.Column;

@Entity
@Table(name = "tenant")
public class Tenant {

    @Id
    @GeneratedValue
    private int id;

    @Column(name = "name")
    private String name;

    @Column(name = "phone_number")
    private String phone;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }
}
```

Don't worry about repositories or services yet. **Those are later topics.** For this session, we're focusing on what an entity is and how its fields map to database columns.

***

# 11. One thing to notice about `id`

Notice that we don't normally do this when creating a new tenant:

```java
tenant.setId(1);
```

because we have:

```java
@Id
@GeneratedValue
private int id;
```

The ID is supposed to be generated automatically.

You would provide things such as:

```java
tenant.setName("John");
tenant.setPhone("12345");
```

while the ID is generated when the data is persisted.

***

# 12. Your mental model for today

You don't need to memorize complicated JPA terminology.

Remember this:

```text
@Entity
   ↓
"This Java class represents database data."

@Table
   ↓
"Use this database table."

@Id
   ↓
"This field is the primary key."

@GeneratedValue
   ↓
"Generate the primary key automatically."

@Column
   ↓
"Configure which database column this field maps to."
```

And the overall picture:

```text
              JPA / Hibernate
                   │
                   ↕
        ┌─────────────────────┐
        │     Tenant.java     │
        │                     │
        │ id                  │
        │ name                │
        │ phone               │
        └─────────────────────┘
                   ↕
        ┌─────────────────────┐
        │   database: tenant  │
        │                     │
        │ id                  │
        │ name                │
        │ phone_number        │
        └─────────────────────┘
```

That's the core of **Session 3.3**.

***

## Small practical exercise

Before moving on, look at this entity:

```java
@Entity
@Table(name = "tenant")
public class Tenant {

    @Id
    @GeneratedValue
    private int id;

    @Column(name = "full_name")
    private String name;

    private String email;
}
```

Tell me what each of these means:

1. `@Entity`
2. `@Table(name = "tenant")`
3. `@Id`
4. `@GeneratedValue`
5. `@Column(name = "full_name")`
6. What database column does `email` map to?

Once you answer those, I'll check your understanding before we continue.
