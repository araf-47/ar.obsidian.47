You're right. **I introduced `{id}` without teaching it first.** That's my mistake.

Let's fix that before continuing with `@PathVariable`.

## What is `{id}`?

You already know that an endpoint can be:

```text
GET /api/tenants
```

Now suppose we want an endpoint for **one particular tenant**.

We could conceptually have:

```text
GET /api/tenants/1
GET /api/tenants/2
GET /api/tenants/3
GET /api/tenants/4
GET /api/tenants/5
```

We obviously don't want to write five different controller methods.

So Spring lets us write a **placeholder** in the endpoint:

```java
@GetMapping("/api/tenants/{id}")
```

The `{id}` means:

> **"This part of the URL can contain a value."**

It is a placeholder, not the actual value `id`.

So:

```text
/api/tenants/{id}
```

can match:

```text
/api/tenants/5
```

or:

```text
/api/tenants/10
```

or:

```text
/api/tenants/27
```

The actual request determines the value.

### Think of it like this

```text
/api/tenants/{id}
             ↑
          placeholder
```

Request:

```text
/api/tenants/5
             ↑
        actual value
```

Therefore:

```text
{id} → 5
```

***

## Then `@PathVariable` makes sense

Once we have:

```java
@GetMapping("/api/tenants/{id}")
```

we want the `5` to become a Java variable:

```java
int id
```

That's what this does:

```java
@PathVariable int id
```

Together:

```java
@GetMapping("/api/tenants/{id}")
public String getTenant(@PathVariable int id) {
    return "Tenant ID = " + id;
}
```

The flow is:

```text
Client
   │
   │ GET /api/tenants/5
   ↓
Spring sees:
   /api/tenants/{id}
             ↓
          id = 5
             ↓
@PathVariable int id
             ↓
        Java method
```

So **`{id}` is the URL placeholder**, while **`@PathVariable` is how Spring gives that placeholder's actual value to your Java method**.

That's the missing piece I should have explained first.

**Don't worry about the rest of `@PathVariable` yet.** This `{id}` concept needs to be clear first.
