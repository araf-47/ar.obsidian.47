These three words describe **three different roles in a typical Spring application**:

```text
Controller
   ↓
Service
   ↓
Repository
   ↓
Database
```

Think of them as **three layers**, where each layer has a different job.

***

## 1. Controller — handles the request

The **Controller** is the part that receives a request from the client.

For example, Angular sends:

```http
GET /tenants
```

The Controller receives that request.

```java
@RestController
public class TenantController {

    public List<Tenant> getTenants() {
        // ...
    }
}
```

So:

> **Controller = receives HTTP requests and sends HTTP responses.**

Since you know Angular and HTTP, you can think of it roughly like:

```text
Angular
   ↓ HTTP request
Controller
```

The Controller should mainly deal with **HTTP/API-related things**.

***

# 2. Service — contains the application logic

The **Service** is where you put the actual work/rules of your application.

For example:

> "Find all tenants whose rent is overdue."

The Controller shouldn't normally contain all that logic.

Instead:

```text
Controller
    ↓
Service
```

Example:

```java
@Service
public class TenantService {

    public List<Tenant> getOverdueTenants() {
        // application logic
    }
}
```

So:

> **Service = performs the application's business/application logic.**

For example:

```text
Controller:
"Someone requested overdue tenants."

Service:
"Okay, I need to figure out which tenants are overdue."

Repository:
"Give me the tenant data from the database."
```

***

# 3. Repository — talks to the database

The **Repository** is responsible for accessing stored data.

```text
Service
   ↓
Repository
   ↓
Database
```

For example:

```java
@Repository
public class TenantRepository {

    public List<Tenant> findAll() {
        // get tenant data from database
    }
}
```

So:

> **Repository = handles data access.**

Since you've used JDBC, this should feel familiar.

With JDBC, you might have written:

```java
Connection connection = ...;

PreparedStatement statement =
    connection.prepareStatement("SELECT * FROM tenants");

ResultSet result = statement.executeQuery();
```

That kind of database-access code belongs conceptually in the **Repository layer**.

***

# Put them together

Imagine your landlord application has this request:

```http
GET /tenants
```

The flow is:

```text
Angular
   │
   │ GET /tenants
   ↓
Controller
   │
   │ "Give me the tenants"
   ↓
Service
   │
   │ "I need tenant data"
   ↓
Repository
   │
   │ SQL / database access
   ↓
PostgreSQL
```

Then the result comes back:

```text
PostgreSQL
   ↓
Repository
   ↓
Service
   ↓
Controller
   ↓
Angular
```

***

## A simple analogy

Imagine a restaurant:

| Spring layer   | Restaurant analogy                      |
| -------------- | --------------------------------------- |
| **Controller** | Waiter                                  |
| **Service**    | Chef                                    |
| **Repository** | Person getting ingredients from storage |
| **Database**   | Storage room                            |

Customer says:

> "I want chicken biryani."

**Controller / Waiter:**

> "Okay, I'll take your order."

**Service / Chef:**

> "I need to prepare chicken biryani."

**Repository:**

> "I'll get the chicken, rice, spices, etc. from storage."

**Database:**

> Contains the stored ingredients/data.

The important idea is **separation of responsibilities**.

***

## Why not just put everything in Controller?

You *could* write something like:

```java
@RestController
public class TenantController {

    public List<Tenant> getTenants() {

        // connect to PostgreSQL

        // execute SQL

        // process results

        // business logic

        // return response
    }
}
```

But now one class is doing **everything**.

Instead:

```text
Controller
    ↓
Service
    ↓
Repository
    ↓
Database
```

Each class has a focused responsibility.

***

### The three definitions to remember

For now, remember just this:

```text
Controller  → handles HTTP/API requests

Service     → handles application/business logic

Repository  → handles database/data access
```

And the typical relationship is:

```text
Client/Angular
      ↓
 Controller
      ↓
   Service
      ↓
 Repository
      ↓
  Database
```

**Important:** These are not special Java keywords. They are **roles/architectural layers** commonly used in Spring applications. `@Controller`, `@Service`, and `@Repository` are Spring annotations that help mark classes for those roles.
