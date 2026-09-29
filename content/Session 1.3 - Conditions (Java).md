# Session 1.3 — Conditions

### What this session covers

* `if`
* `else`
* `else if`
* Nested conditions
* `switch`
* Basic `switch` expressions

### What this session does **NOT** cover

* Loops
* Methods
* OOP
* Collections
* Exceptions
* Spring

### Where this fits in the roadmap

You are learning how Java makes **decisions**:

```text
Java basics
   ↓
Variables / types / operators
   ↓
Conditions ← YOU ARE HERE
   ↓
Loops
   ↓
Methods
   ↓
Classes / Objects / OOP
   ↓
Interfaces / Composition
   ↓
Dependency wiring
   ↓
Spring
```

The basic idea is simple:

> **A condition allows a program to choose what to do based on whether something is true or false.**

***

# 1. `if`

The simplest condition is `if`.

```java
int age = 20;

if (age >= 18) {
    System.out.println("Adult");
}
```

Let's break it down:

```java
if (age >= 18)
```

* `if` → tells Java we want to make a decision.
* `age >= 18` → the **condition**.
* The condition produces either `true` or `false`.

If it is `true`, Java executes the code inside `{ }`.

So:

```text
age = 20

20 >= 18
   ↓
 true
   ↓
print "Adult"
```

If:

```java
int age = 15;
```

then:

```text
15 >= 18
   ↓
 false
   ↓
don't execute the block
```

### Important connection to your previous session

You just learned that comparison expressions produce boolean values.

For example:

```java
age >= 18
```

is an expression whose result is:

```java
true
```

or:

```java
false
```

`if` uses that boolean result to make a decision.

***

# 2. `if` with a boolean variable

You can also store the condition first:

```java
int age = 20;

boolean adult = age >= 18;

if (adult) {
    System.out.println("Adult");
}
```

Here:

```java
boolean adult = age >= 18;
```

means:

1. Evaluate `age >= 18`.
2. It produces `true`.
3. Store `true` in `adult`.

Then:

```java
if (adult)
```

means essentially:

> "If `adult` is `true`, execute this block."

This is useful when the condition has a meaningful name.

***

# 3. `else`

What if we want something to happen when the condition is false?

Use `else`.

```java
int age = 15;

if (age >= 18) {
    System.out.println("Adult");
} else {
    System.out.println("Not an adult");
}
```

Think of it as:

```text
IF condition is true
    do this
ELSE
    do that
```

Only **one** of the two blocks executes.

For `age = 15`:

```text
15 >= 18
   ↓
 false
   ↓
else block
   ↓
"Not an adult"
```

***

# 4. `else if`

Sometimes there are more than two possibilities.

For example, suppose we want to classify a student's mark.

```java
int mark = 75;

if (mark >= 80) {
    System.out.println("A");
} else if (mark >= 70) {
    System.out.println("B");
} else if (mark >= 60) {
    System.out.println("C");
} else {
    System.out.println("Fail");
}
```

Java checks the conditions **from top to bottom**.

For:

```java
mark = 75;
```

Java checks:

```text
75 >= 80 → false

75 >= 70 → true
```

So it prints:

```text
B
```

Then Java stops checking this `if/else if/else` chain.

### Important

This:

```java
if (...)
else if (...)
else if (...)
else
```

is one decision chain.

Java does **not** execute every true condition.

It executes the first matching branch.

***

# 5. Why order matters

Look carefully at this:

```java
int mark = 85;

if (mark >= 60) {
    System.out.println("C or above");
} else if (mark >= 80) {
    System.out.println("A");
}
```

You might expect `A`.

But Java prints:

```text
C or above
```

Why?

Because Java checks:

```java
mark >= 60
```

first.

Since:

```text
85 >= 60 → true
```

Java enters that block and never reaches the `else if`.

So with conditions like this, **the order of conditions matters**.

Usually, more specific/higher thresholds should come first:

```java
if (mark >= 80) {
    System.out.println("A");
} else if (mark >= 60) {
    System.out.println("C or above");
}
```

***

# 6. Nested conditions

A condition can contain another condition.

That is called a **nested condition**.

Example:

```java
int age = 25;
boolean hasTicket = true;

if (age >= 18) {

    if (hasTicket) {
        System.out.println("You may enter.");
    }

}
```

The outer condition is:

```java
age >= 18
```

Only if that is true do we check:

```java
hasTicket
```

So the logic is:

```text
Are you 18 or older?
       |
      yes
       ↓
Do you have a ticket?
       |
      yes
       ↓
Allow entry
```

### Why nesting exists

Sometimes the second decision only makes sense after the first decision succeeds.

For example:

```java
if (accountExists) {

    if (passwordCorrect) {
        // allow login
    }

}
```

The password check is relevant only after we know the account exists.

***

# 7. Nested `if` vs `&&`

You may sometimes see:

```java
if (age >= 18 && hasTicket) {
    System.out.println("You may enter.");
}
```

instead of:

```java
if (age >= 18) {
    if (hasTicket) {
        System.out.println("You may enter.");
    }
}
```

Both express a similar basic requirement.

But don't worry about deciding which style is "best" yet. The important thing for this session is understanding what **nested conditions** mean.

***

# 8. `switch`

`switch` is another way of making decisions.

It is particularly useful when you're comparing one value against several specific possibilities.

For example:

```java
int day = 2;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;

    case 2:
        System.out.println("Tuesday");
        break;

    case 3:
        System.out.println("Wednesday");
        break;

    default:
        System.out.println("Unknown day");
}
```

Here Java looks at:

```java
day
```

and compares it with the `case` values.

Since:

```java
day = 2
```

Java finds:

```java
case 2:
```

and prints:

```text
Tuesday
```

***

# 9. Understanding `case`

This:

```java
case 2:
```

basically means:

> "What should happen if the switch value is 2?"

So:

```java
switch (day)
```

means:

> "Make a decision based on `day`."

And:

```java
case 1:
```

means:

> "If `day` is 1..."

***

# 10. Why `break`?

This is important.

Consider:

```java
int day = 2;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;

    case 2:
        System.out.println("Tuesday");
        break;

    case 3:
        System.out.println("Wednesday");
        break;
}
```

The `break` tells the traditional `switch`:

> "I'm finished with this switch. Get out."

Without `break`, Java can continue executing subsequent cases.

For example:

```java
int day = 2;

switch (day) {
    case 1:
        System.out.println("Monday");

    case 2:
        System.out.println("Tuesday");

    case 3:
        System.out.println("Wednesday");
}
```

For `day = 2`, Java can print:

```text
Tuesday
Wednesday
```

This behavior is called **fall-through**.

For now, remember:

> In traditional `switch`, `break` normally prevents execution from falling into the next case.

***

# 11. `default`

What if none of the cases match?

Use:

```java
default
```

Example:

```java
int day = 10;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;

    case 2:
        System.out.println("Tuesday");
        break;

    default:
        System.out.println("Invalid day");
}
```

Since there is no:

```java
case 10
```

Java executes:

```java
default:
```

Think of `default` as the `switch` equivalent of:

```java
else
```

Not exactly identical in all respects, but that's a useful mental model for now.

***

# 12. `if` vs `switch`

Consider:

```java
int option = 2;

if (option == 1) {
    System.out.println("Add");
} else if (option == 2) {
    System.out.println("View");
} else if (option == 3) {
    System.out.println("Delete");
}
```

We could write this using `switch`:

```java
switch (option) {
    case 1:
        System.out.println("Add");
        break;

    case 2:
        System.out.println("View");
        break;

    case 3:
        System.out.println("Delete");
        break;

    default:
        System.out.println("Invalid option");
}
```

A useful mental distinction:

### `if`

Good when you're asking questions such as:

```text
Is age >= 18?
Is price > 1000?
Is username equal to "admin"?
Is score between two values?
```

### `switch`

Good when you're essentially asking:

```text
Which specific option/value is this?
```

For example:

```text
1 → Add
2 → View
3 → Delete
4 → Exit
```

***

# 13. Basic `switch` expressions

Modern Java also has a `switch` expression that can **produce a value**.

Example:

```java
int option = 2;

String action = switch (option) {
    case 1 -> "Add";
    case 2 -> "View";
    case 3 -> "Delete";
    default -> "Invalid";
};
```

Now:

```java
String action
```

receives the result of the `switch`.

For:

```java
option = 2
```

the result is:

```text
"View"
```

So:

```java
System.out.println(action);
```

prints:

```text
View
```

Notice the difference from traditional `switch`.

Traditional:

```java
case 2:
    System.out.println("View");
    break;
```

Switch expression:

```java
case 2 -> "View";
```

The arrow form is much less verbose.

For this session, that's enough to know about switch expressions. We don't need to go into advanced pattern matching or other modern `switch` features.

***

# 14. Practical exercise — Menu program

Now let's combine the concepts.

Create a Java program representing a simple application menu.

The user chooses an option represented by an integer:

```text
1 → Add Tenant
2 → View Tenants
3 → Delete Tenant
4 → Exit
```

Start with:

```java
public class MenuProgram {

    public static void main(String[] args) {

        int option = 2;

        // Your code here

    }
}
```

### Your task

Use a `switch` to produce:

```text
Viewing tenants...
```

when:

```java
option = 2;
```

Also handle the other options:

```text
1 → Adding tenant...
2 → Viewing tenants...
3 → Deleting tenant...
4 → Exiting...
anything else → Invalid option.
```

### Requirements

Use a **traditional `switch`** first:

* `case`
* `break`
* `default`

Don't use loops, methods, classes beyond the single class, or anything else we haven't covered.

***

## Code-reading checkpoint

Don't run this yet. Read it first:

```java
int age = 20;
boolean hasTicket = true;

if (age >= 18) {
    if (hasTicket) {
        System.out.println("Allowed");
    } else {
        System.out.println("No ticket");
    }
} else {
    System.out.println("Too young");
}
```

Tell me:

1. What is the first condition Java checks?
2. What happens if `age` is `16`?
3. What happens if `age` is `20` and `hasTicket` is `false`?
4. Which `if` is nested inside another `if`?
5. What will be printed for the values shown?

Don't run it yet—reason through it first.

***

# Session checkpoint

Answer these without looking anything up:

### 1. Conceptual

What is the difference between:

```java
if
```

and:

```java
else
```

***

### 2. Conceptual

In this code:

```java
if (score >= 80) {
    // A
} else if (score >= 60) {
    // B
} else {
    // C
}
```

If `score` is `75`, which block executes?

***

### 3. Code reading

What does this print?

```java
int option = 3;

switch (option) {
    case 1:
        System.out.println("Add");
        break;

    case 2:
        System.out.println("View");
        break;

    case 3:
        System.out.println("Delete");
        break;

    default:
        System.out.println("Invalid");
}
```

***

### 4. Important

Why does the order matter here?

```java
if (mark >= 60) {
    System.out.println("Pass");
} else if (mark >= 80) {
    System.out.println("A");
}
```

***

### 5. Code reading

In this:

```java
if (age >= 18) {
    if (hasTicket) {
        System.out.println("Allowed");
    }
}
```

Which `if` is the **outer condition**, and which is the **nested condition**?

***

### Before considering Session 1.3 complete, you should be able to explain:

* how `if` makes a decision using a boolean condition
* how `else` handles the false path
* how `else if` handles multiple possibilities
* why the order of conditions matters
* what a nested condition is
* how `switch`, `case`, `break`, and `default` work
* the basic difference between a traditional `switch` and a `switch` expression
* how to build a small menu using `switch`

**Do the menu exercise and answer the checkpoint. I won't move to the next session until we finish this one.**
