You forgot the **Angular concept of query parameters**, 🫩>(seriously, that was easy as hell.)

Okay — **`?city=Dhaka` is the same general HTTP concept you encountered in Angular.**

### In Angular

You may have seen something conceptually like:

```text
/api/tenants?city=Dhaka
```

The:

```text
city=Dhaka
```

is the **query parameter**.

The `?` means:

> "The query parameters start here."

So:

```text
/api/tenants?city=Dhaka
            ↑
       query parameter
```

And there can be multiple:

```text
/api/tenants?city=Dhaka&status=active
```

Here there are **two query parameters**:

```text
city=Dhaka
status=active
```

### Now connect Angular → Spring

Think of it this way:

```text
Angular
   │
   │ sends HTTP request
   ↓
GET /api/tenants?city=Dhaka
                         │
                         ↓
                    Spring Boot
                         │
                         ↓
                  @RequestParam
```

So when you see:

```java
@RequestParam String city
```

you should think:

> **"Spring is taking the query parameter that Angular/client put in the URL."**

That's the connection I should have made instead of treating **query parameters** like a completely new concept.
