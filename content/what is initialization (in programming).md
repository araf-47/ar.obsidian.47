In programming, **initialized** means:

> **A variable has been given its initial value.**

Think of it as **creating a variable and giving it a starting value**.

### Example in Java

```java
int age = 25;
```

Here:

* `int` → the type
* `age` → the variable
* `25` → the initial value
* `age` is **initialized to 25**

So you can say:

> "`age` has been initialized with the value `25`."

***

### Declaration vs initialization

This distinction is important:

```java
int age;
```

This is **declaration**.

You are saying:

> "I want a variable called `age` that can hold an integer."

Then:

```java
age = 25;
```

This is **initialization** (more precisely, assigning its first value).

Together:

```java
int age = 25;
```

This **declares and initializes** `age` in one statement.

***

### Another example with an object

This is especially important for Spring and Java:

```java
EmailService emailService = new EmailService();
```

Here:

```java
EmailService emailService;
```

declares the variable.

Then:

```java
new EmailService()
```

creates an `EmailService` object, and:

```java
emailService = new EmailService();
```

assigns that object to the variable.

So we can say:

> "`emailService` has been initialized with an `EmailService` object."

### Simple mental model

Think of a variable as a **box**:

```text
int age = 25;

┌───────────┐
│ age       │
│    25     │
└───────────┘
```

**Declaration** = make the box.

**Initialization** = put the first value into the box.

**Assignment** = put/change a value in the box.

This word **initialized** will come up constantly in Java, especially when you start learning constructors, objects, and Spring dependency injection.
