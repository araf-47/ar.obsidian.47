## Session 1.2 — Operators & Expressions

### What this session covers

We will learn only:

* Arithmetic operators
* Assignment operators
* Comparison operators
* Logical operators
* Increment/decrement
* Expressions
* Operator precedence
* A small calculation program

### What this session does **NOT** cover

We will **not** teach:

* Methods
* Classes
* Objects
* OOP
* Collections
* Spring

If one of those becomes relevant, we will leave it for a later session.

### Where this fits in the roadmap

You are rebuilding the basic Java language layer first:

**Java basics → Operators & Expressions → Classes/Objects → OOP → Interfaces → Composition → Collections → Exceptions → Dependency wiring → Spring**

Operators and expressions are fundamental because Spring code is still Java code. Before reading something like:

```java
if (user.getAge() >= 18 && user.isActive()) {
    ...
}
```

you need to be completely comfortable understanding the operators involved.

***

# 1. What is an operator?

An **operator** is a symbol that tells Java to perform an operation.

For example:

```java
10 + 5
```

Here:

```text
10    → value
+     → operator
5     → value
```

Java evaluates this and produces:

```text
15
```

Some common operators:

```text
+       addition
-       subtraction
*       multiplication
/       division
%       remainder

=       assignment
==      equality comparison
!=      not equal
>       greater than
<       less than
>=      greater than or equal
<=      less than or equal

&&      AND
||      OR
!       NOT
```

***

# 2. Arithmetic Operators

These perform mathematical calculations.

| Operator | Meaning        | Example  |
| -------- | -------------- | -------- |
| `+`      | addition       | `10 + 3` |
| `-`      | subtraction    | `10 - 3` |
| `*`      | multiplication | `10 * 3` |
| `/`      | division       | `10 / 3` |
| `%`      | remainder      | `10 % 3` |

Let's see them in Java:

```java
int a = 10;
int b = 3;

System.out.println(a + b);
System.out.println(a - b);
System.out.println(a * b);
System.out.println(a / b);
System.out.println(a % b);
```

Output:

```text
13
7
30
3
1
```

### Why is `10 / 3` equal to `3`?

Because both `10` and `3` are `int`.

Integer division discards the decimal portion.

```java
10 / 3
```

mathematically:

```text
3.333...
```

But Java's integer division gives:

```text
3
```

This is an important practical detail.

Compare:

```java
System.out.println(10 / 3);
System.out.println(10.0 / 3);
```

Output:

```text
3
3.3333333333333335
```

The second calculation involves a decimal value, so Java performs floating-point division.

***

# 3. The `%` operator — remainder

This one is particularly important.

```java
10 % 3
```

means:

> After dividing 10 by 3, what is left over?

```text
10 ÷ 3

3 × 3 = 9
remainder = 1
```

Therefore:

```java
10 % 3
```

produces:

```text
1
```

Another example:

```java
20 % 5
```

produces:

```text
0
```

because 20 divides evenly by 5.

You'll frequently encounter `%` when checking things such as:

```java
number % 2 == 0
```

which means:

> Is the number divisible by 2?

***

# 4. Assignment Operator

The basic assignment operator is:

```java
=
```

For example:

```java
int age = 25;
```

This does **not** mean "age is equal to 25" in the mathematical sense.

It means:

> Put the value `25` into the variable `age`.

Think of:

```java
int age = 25;
```

as:

```text
create an int variable called age
        ↓
put 25 into it
```

You can then change its value:

```java
age = 30;
```

Now:

```text
age → 30
```

***

# 5. Assignment vs comparison

This is one of the most important distinctions.

### Assignment

```java
age = 30;
```

Means:

> Store 30 in `age`.

### Comparison

```java
age == 30
```

Means:

> Is `age` equal to 30?

The two equal signs are completely different from one equal sign.

```text
=    assignment
==   comparison
```

For example:

```java
int age = 30;

System.out.println(age == 30);
```

Output:

```text
true
```

But:

```java
age = 40;
```

changes the value.

***

# 6. Compound Assignment Operators

Java provides shortcuts for modifying a variable.

Suppose:

```java
int price = 100;
```

You could write:

```java
price = price + 20;
```

Now:

```text
price = 120
```

Java provides a shorter form:

```java
price += 20;
```

Same basic effect.

Other compound assignment operators:

```java
price -= 20;
price *= 2;
price /= 2;
price %= 3;
```

For example:

```java
int number = 10;

number += 5;
System.out.println(number);
```

Output:

```text
15
```

Conceptually:

```java
number += 5;
```

means:

```java
number = number + 5;
```

Similarly:

```java
number -= 3;
```

means:

```java
number = number - 3;
```

***

# 7. Comparison Operators

Comparison operators compare values.

The result is a **boolean**:

```text
true
```

or:

```text
false
```

For example:

```java
int age = 25;

System.out.println(age > 18);
```

Result:

```text
true
```

Because 25 is greater than 18.

### Main comparison operators

| Operator | Meaning                  |
| -------- | ------------------------ |
| `==`     | equal to                 |
| `!=`     | not equal to             |
| `>`      | greater than             |
| `<`      | less than                |
| `>=`     | greater than or equal to |
| `<=`     | less than or equal to    |

Examples:

```java
int age = 25;

System.out.println(age == 25);  // true
System.out.println(age != 25);  // false
System.out.println(age > 20);   // true
System.out.println(age < 20);   // false
System.out.println(age >= 25);  // true
System.out.println(age <= 25);  // true
```

The important mental model is:

```java
age > 20
```

is an **expression** that produces a value:

```text
true
```

or:

```text
false
```

***

# 8. Logical Operators

Logical operators combine boolean expressions.

The three you need here are:

```text
&&    AND
||    OR
!     NOT
```

## `&&` — AND

Both conditions must be true.

```java
int age = 25;
boolean hasTicket = true;

System.out.println(age >= 18 && hasTicket);
```

Break it down:

```text
age >= 18
    ↓
true

hasTicket
    ↓
true

true && true
    ↓
true
```

So the result is:

```text
true
```

But:

```java
int age = 16;
boolean hasTicket = true;

System.out.println(age >= 18 && hasTicket);
```

becomes:

```text
false && true
```

Therefore:

```text
false
```

### AND rule

```text
true  && true  → true
true  && false → false
false && true  → false
false && false → false
```

***

# 9. `||` — OR

At least **one** condition must be true.

```java
boolean isAdmin = false;
boolean isManager = true;

System.out.println(isAdmin || isManager);
```

Becomes:

```text
false || true
```

Result:

```text
true
```

### OR rule

```text
true  || true  → true
true  || false → true
false || true  → true
false || false → false
```

***

# 10. `!` — NOT

`!` reverses a boolean value.

```java
boolean active = true;

System.out.println(!active);
```

Result:

```text
false
```

Because:

```text
!true → false
!false → true
```

For example:

```java
boolean loggedIn = false;

System.out.println(!loggedIn);
```

Result:

```text
true
```

Read it as:

> NOT logged in.

***

# 11. Increment and Decrement

These are used to increase or decrease a number by one.

### Increment

```java
int count = 5;

count++;
```

Now:

```text
count = 6
```

This:

```java
count++;
```

is essentially:

```java
count = count + 1;
```

### Decrement

```java
count--;
```

is essentially:

```java
count = count - 1;
```

So:

```java
int count = 5;

count++;
count++;

System.out.println(count);
```

produces:

```text
7
```

***

# 12. `++` before vs after

There is one detail worth learning now because you'll encounter it in real Java code.

These are different:

```java
++count
```

and:

```java
count++
```

The difference matters when the increment is part of a larger expression.

Example:

```java
int count = 5;

int result = count++;

System.out.println(result);
System.out.println(count);
```

The output is:

```text
5
6
```

Why?

`count++` means:

> Use the current value first, then increment.

So:

```text
result gets 5
count becomes 6
```

Now:

```java
int count = 5;

int result = ++count;

System.out.println(result);
System.out.println(count);
```

Output:

```text
6
6
```

Because:

```text
increment first
then use the value
```

For now, remember:

```text
count++ → use, then increase
++count → increase, then use
```

The same idea applies to `--`.

***

# 13. What is an Expression?

This is an important term.

An **expression** is a piece of Java code that is evaluated to produce a value.

For example:

```java
10 + 5
```

is an expression.

Its result is:

```text
15
```

This is also an expression:

```java
age > 18
```

Its result is:

```text
true
```

And:

```java
price * quantity
```

produces a numeric value.

You can therefore have expressions of different types.

### Numeric expression

```java
10 + 5
```

produces:

```text
15
```

### Boolean expression

```java
age >= 18
```

produces:

```text
true
```

### More complicated expression

```java
age >= 18 && hasTicket
```

produces:

```text
true
```

or:

```text
false
```

The key idea:

> **An expression is something Java evaluates to produce a value.**

***

# 14. Expressions can be stored

For example:

```java
int price = 100;
int quantity = 3;

int total = price * quantity;
```

Look at:

```java
price * quantity
```

That is an expression.

Java evaluates it:

```text
100 * 3
   ↓
300
```

Then:

```java
total = 300;
```

So:

```java
int total = price * quantity;
```

contains an expression on the right-hand side.

***

# 15. Operator Precedence

Now we need to answer an important question:

What happens when an expression contains multiple operators?

For example:

```java
int result = 10 + 5 * 2;
```

Does Java calculate:

```text
(10 + 5) * 2
```

or:

```text
10 + (5 * 2)
```

The answer is:

```text
20
```

because multiplication has higher precedence than addition.

So Java evaluates:

```text
10 + (5 * 2)
```

then:

```text
10 + 10
```

then:

```text
20
```

***

# 16. Basic precedence to remember

For this session, remember this simplified order:

```text
1. Parentheses
2. * / %
3. + -
4. Comparisons
5. &&
6. ||
7. Assignment
```

For example:

```java
int result = 10 + 5 * 2;
```

`*` happens before `+`.

***

## Parentheses can make your intention explicit

Instead of:

```java
int result = 10 + 5 * 2;
```

you can write:

```java
int result = 10 + (5 * 2);
```

Or if you actually want addition first:

```java
int result = (10 + 5) * 2;
```

Now the result is:

```text
30
```

### Good habit

==When an expression becomes complicated, use parentheses to make your intention obvious==.

Don't rely on your memory of precedence when parentheses can make the code clearer.

***

# 17. Putting operators together

Consider:

```java
int age = 25;
int minimumAge = 18;
boolean hasID = true;

boolean allowed = age >= minimumAge && hasID;
```

Let's break down:

### First:

```java
age >= minimumAge
```

becomes:

```text
25 >= 18
```

which produces:

```text
true
```

### Second:

```java
hasID
```

is:

```text
true
```

### Then:

```java
true && true
```

produces:

```text
true
```

Therefore:

```java
allowed
```

contains:

```text
true
```

This type of expression is extremely common in application code.

***

# 18. Practical Program

Now let's build the small calculation program requested for this session.

We'll make a **shopping bill calculator**.

It will calculate:

* item price
* quantity
* subtotal
* discount
* final total
* whether the customer qualifies for free delivery

```java
public class Calculator {

    public static void main(String[] args) {

        double price = 120.50;
        int quantity = 3;

        double subtotal = price * quantity;

        double discount = 50.00;

        double finalTotal = subtotal - discount;

        boolean freeDelivery = finalTotal >= 300;

        System.out.println("Price: " + price);
        System.out.println("Quantity: " + quantity);
        System.out.println("Subtotal: " + subtotal);
        System.out.println("Discount: " + discount);
        System.out.println("Final Total: " + finalTotal);
        System.out.println("Free Delivery: " + freeDelivery);
    }
}
```

### What happens?

Start with:

```java
double price = 120.50;
```

The variable:

```text
price
```

contains:

```text
120.50
```

Then:

```java
int quantity = 3;
```

contains:

```text
3
```

Then:

```java
double subtotal = price * quantity;
```

The expression:

```java
price * quantity
```

becomes:

```text
120.50 * 3
```

which produces:

```text
361.50
```

Then:

```java
double finalTotal = subtotal - discount;
```

becomes:

```text
361.50 - 50.00
```

result:

```text
311.50
```

Finally:

```java
boolean freeDelivery = finalTotal >= 300;
```

becomes:

```text
311.50 >= 300
```

which is:

```text
true
```

***

# Your Practical Exercise

Create your own program called:

```text
SalaryCalculator
```

Use these variables:

```java
double monthlySalary = 50000;
double bonus = 10000;
double tax = 5000;
```

Calculate:

1. Gross salary:

```text
monthlySalary + bonus
```

2. Final salary:

```text
gross salary - tax
```

3. Whether the employee earns at least `50000` after tax.

Your program should print something similar to:

```text
Monthly Salary: 50000
Bonus: 10000
Gross Salary: 60000
Tax: 5000
Final Salary: 55000
Earns at least 50000: true
```

### One extra challenge

Add:

```java
int months = 12;
```

and calculate the annual final salary.

That will give you practice with several arithmetic expressions.

***

# Code-reading checkpoint

Don't run this yet. Read it first:

```java
int price = 100;
int quantity = 4;

int total = price * quantity;

boolean expensive = total > 300;
```

Tell me:

1. What value does `total` contain?
2. What value does `expensive` contain?
3. Which line contains an arithmetic expression?
4. Which line contains a comparison expression?
5. What would happen if this were changed to:

```java
boolean expensive = total >= 400;
```

***

# Session Checkpoint

Answer these without looking back if possible:

### 1.

What's the difference between:

```java
=
```

and:

```java
==
```

### 2.

What does this produce?

```java
17 % 5
```

### 3.

What is the result?

```java
10 + 2 * 5
```

And why?

### 4.

What is the difference between:

```java
count++
```

and:

```java
++count
```

when they are used inside a larger expression?

### 5.

What does this mean?

```java
age >= 18 && hasID
```

***

## Before considering Session 1.2 complete

You should be able to explain, in your own words:

* what an operator is
* what an expression is
* how `+`, `-`, `*`, `/`, `%` work
* the difference between `=` and `==`
* how `&&`, `||`, and `!` work
* what `++` and `--` do
* why parentheses matter
* basic operator precedence
* how Java evaluates a multi-operator expression

**Don't move to the next session yet.** First do the `SalaryCalculator` exercise and answer the checkpoint questions.
