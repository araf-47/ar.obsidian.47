# Session 1.1 — Variables & Data Types

### What this session covers

Only these topics:

* Variables
* Primitive data types
* `int`
* `double`
* `boolean`
* `char`
* `byte`
* `short`
* `long`
* `float`
* `String`
* Variable declaration
* Initialization
* Assignment
* `final`
* Basic type conversion/casting

### What this session does **NOT** cover

We will **not** teach:

* Classes
* Objects
* References
* Methods
* Collections
* OOP
* Spring

Those come later in the roadmap.

### Where this fits

Your current path is:

**Java foundation → Classes → Objects → References → Constructors → OOP → Interfaces → Polymorphism → Composition → Collections → Exceptions → Application structure → Manual dependency wiring → Spring**

Variables and types are the foundation underneath all of those.

***

# 1. What is a variable?

The simplest useful definition is:

> **A variable is a named place in a program that holds a value.**

For example:

```java
int age = 25;
```

You can mentally read this as:

> "Create a variable called `age` that can hold an `int`, and put `25` into it."

There are several pieces here:

```java
int age = 25;
```

| Part  | Meaning             |
| ----- | ------------------- |
| `int` | the type            |
| `age` | variable name       |
| `=`   | assignment operator |
| `25`  | value               |
| `;`   | end of statement    |

The important relationship is:

**type → determines what kind of value the variable can hold**

**name → gives us a way to refer to that variable**

**value → the actual data currently stored there**

***

# 2. What is a type?

A **type** tells Java what kind of data something represents and what kind of values are allowed.

For example:

```java
int age = 25;
```

`int` tells Java:

> `age` is an integer variable.

So this is valid:

```java
int age = 25;
```

But this is not:

```java
int age = "hello";
```

because `"hello"` is text, not an integer.

Similarly:

```java
boolean active = true;
```

means `active` stores a boolean value.

***

# 3. Declaration vs initialization

These two terms are worth understanding precisely.

## Declaration

Declaration means:

> Tell Java that a variable exists and tell Java its type.

```java
int age;
```

We have declared `age`.

At this point we have **not given it a value ourselves**.

***

## Initialization

Initialization means:

> Give a variable its initial value.

```java
int age = 25;
```

Here:

```java
int age;
```

is the declaration.

Then:

```java
age = 25;
```

initializes it.

You can also do both at once:

```java
int age = 25;
```

That's extremely common.

### Important distinction

```java
int age = 25;
```

is both:

**declaration + initialization**

***

# 4. Assignment

Assignment means putting a value into a variable.

Example:

```java
int age = 25;

age = 26;
```

The first line creates and initializes the variable.

The second line **assigns a new value** to it.

After:

```java
age = 26;
```

the value associated with `age` is `26`.

You can assign again:

```java
age = 27;
```

Now it is `27`.

So a normal variable can change its value.

***

# 5. `int`

`int` is used for whole numbers.

```java
int age = 25;
int students = 30;
int marks = 85;
```

Examples of integer values:

```text
0
5
25
-10
1000
```

No decimal portion.

So:

```java
int price = 500;
```

is valid.

But:

```java
int price = 500.50;
```

is not valid because `500.50` is not an `int`.

### Typical use

```java
int tenantCount = 4;
int roomNumber = 12;
int quantity = 5;
```

For ordinary whole-number values, `int` is usually the first integer type you reach for.

***

# 6. `double`

`double` represents decimal numbers.

```java
double price = 499.99;
double height = 1.75;
double temperature = 32.5;
```

Unlike `int`:

```java
int age = 25;
```

stores a whole number.

While:

```java
double price = 25.50;
```

can store a fractional value.

For your current level, think:

```text
int    → whole numbers
double → decimal numbers
```

***

# 7. `boolean`

A `boolean` represents one of exactly two values:

```java
true
false
```

Example:

```java
boolean student = true;
boolean paid = false;
boolean active = true;
```

You cannot put an arbitrary number into a boolean:

```java
boolean active = 1;    // invalid
```

And you don't put quotes around `true`:

```java
boolean active = "true";   // invalid
```

This:

```java
true
```

is a boolean value.

This:

```java
"true"
```

is text (`String`).

That distinction matters.

***

# 8. `char`

`char` represents a **single character**.

```java
char grade = 'A';
char firstLetter = 'F';
char symbol = '$';
```

Notice the **single quotes**:

```java
'A'
```

A `char` contains one character.

This is valid:

```java
char grade = 'A';
```

This is not:

```java
char grade = 'AB';
```

because that's two characters.

And this is also different:

```java
String grade = "A";
```

`String` and `char` are not the same type.

Compare:

```java
char letter = 'A';
String word = "A";
```

The first is one `char`.

The second is a `String` containing text.

***

# 9. `String`

`String` represents text.

```java
String name = "Araf";
String city = "Dhaka";
String university = "ABC University";
```

Strings use **double quotes**:

```java
"Araf"
```

while a `char` uses single quotes:

```java
'A'
```

So remember:

```java
char   → 'A'
String → "Araf"
```

For your Spring preparation, you'll encounter `String` constantly—for example, names, usernames, IDs represented as text, URLs, JSON values, etc.

For this session, just understand it as:

> **`String` stores text.**

***

# 10. The remaining primitive numeric types

Java has several primitive numeric types.

You don't need to memorize their exact limits right now, but you should understand their purpose.

## `byte`

Very small integer type.

```java
byte age = 25;
```

Range:

```text
-128 to 127
```

It's an integer type, but with a much smaller range than `int`.

***

## `short`

A larger integer type than `byte`, but smaller than `int`.

```java
short year = 2026;
```

***

## `long`

Used for integers that may be larger than the normal `int` range.

```java
long population = 170000000L;
```

Notice the `L`:

```java
170000000L
```

That tells Java to treat the literal as a `long`.

You don't need to worry about `long` constantly at this stage. Just understand:

```text
byte → small integer
short → somewhat larger integer
int → normal integer
long → very large integer
```

***

# 11. `float`

`float` is another decimal type.

```java
float temperature = 36.5f;
```

Notice the `f`.

```java
36.5f
```

Without the `f`, Java normally treats a decimal literal such as `36.5` as a `double`.

So:

```java
float temperature = 36.5f;
```

works.

Whereas:

```java
float temperature = 36.5;
```

does not work without a conversion.

For ordinary Java programming, you'll commonly encounter `double` more than `float`.

For this session, remember:

```text
double → decimal
float  → decimal, but lower precision
```

***

# 12. Quick type map

Here's the mental model I want you to have:

```text
                    Java data types

Numbers
│
├── Whole numbers
│   ├── byte
│   ├── short
│   ├── int
│   └── long
│
└── Decimal numbers
    ├── float
    └── double

Other primitive types
│
├── boolean → true / false
└── char    → one character

Text
└── String  → text
```

One important technical detail:

**`String` is not a primitive type.**

The others listed above (`byte`, `short`, `int`, `long`, `float`, `double`, `boolean`, `char`) are primitive types.

You don't need to learn what `String` technically is beyond that distinction yet.

***

# 13. `final`

Normally, a variable can be changed:

```java
int age = 20;

age = 21;
```

That's fine.

But sometimes you want a value that should not be reassigned.

Use `final`:

```java
final int MAX_STUDENTS = 50;
```

Now this is illegal:

```java
MAX_STUDENTS = 100;
```

because a `final` variable cannot be assigned a new value after initialization.

Think:

```text
normal variable → can be reassigned

final variable → cannot be reassigned
```

For example:

```java
final double PI = 3.14159;
```

You don't want:

```java
PI = 4.5;
```

So `final` prevents reassignment.

### Breaking this line down

```java
final int MAX_STUDENTS = 50;
```

* `final` → cannot be reassigned
* `int` → type
* `MAX_STUDENTS` → variable name
* `=` → assignment
* `50` → value

***

# 14. Basic type conversion

Sometimes you have one numeric type and need another.

For example:

```java
int age = 25;
double value = age;
```

Java can automatically convert the `int` to a `double`.

The result is:

```text
25 → 25.0
```

This is called **widening conversion**.

You don't need to write a cast here.

***

## Narrowing conversion

Going the other direction can lose information.

```java
double price = 99.99;
int number = (int) price;
```

The:

```java
(int)
```

is a **cast**.

It tells Java:

> Convert this value to `int`.

The result is:

```text
99
```

The `.99` is discarded.

It does **not** round to `100`.

So:

```java
(int) 99.99
```

produces:

```text
99
```

***

# 15. Why casting can matter

Consider:

```java
int price = 100;
int quantity = 3;
```

You might want:

```text
price / quantity
```

But integer division gives:

```java
100 / 3
```

as:

```text
33
```

because both operands are integers.

If you want a decimal result:

```java
double result = (double) price / quantity;
```

Now Java effectively calculates:

```text
100.0 / 3
```

giving approximately:

```text
33.333...
```

This is a simple but important example of why types affect program behavior.

***

# 16. A very important mental model

Don't think of a variable as simply:

> "a box."

That analogy can be useful initially, but understand the actual programming idea:

```java
int age = 25;
```

means Java knows:

1. There is a variable named `age`.
2. Its type is `int`.
3. Its current value is `25`.
4. Because its type is `int`, Java applies the rules for an integer to it.
5. Since it isn't `final`, we can later assign another compatible value.

That relationship between **name + type + value** is what I want you to understand.

***

# 17. Practical exercise — Student Information Program

Now let's make something runnable.

Create a file:

```text
StudentInfo.java
```

For now, don't worry about the class syntax itself. We are not studying classes in this session. You need a runnable Java file, so use this structure exactly.

```java
public class StudentInfo {

    public static void main(String[] args) {

        String name = "Araf";
        int age = 22;
        double gpa = 3.75;
        boolean enrolled = true;
        char grade = 'A';

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("GPA: " + gpa);
        System.out.println("Enrolled: " + enrolled);
        System.out.println("Grade: " + grade);
    }
}
```

### Important

We are **not** studying:

```java
public class StudentInfo
```

or:

```java
public static void main(String[] args)
```

today.

Those belong to the later Java structure/classes part of the roadmap.

For this exercise, treat them as the minimal wrapper required to run Java code.

Our focus is everything **inside `main`**.

***

## Your task

Create and run that program.

Then change the information:

```java
String name = "Your Name";
int age = ...;
double gpa = ...;
boolean enrolled = ...;
char grade = ...;
```

Then add these variables:

```java
long studentId = ...;
byte semester = ...;
short year = ...;
float attendance = ...;
```

Print all of them.

For example, conceptually:

```text
Name: ...
Age: ...
GPA: ...
Enrolled: ...
Grade: ...
Student ID: ...
Semester: ...
Year: ...
Attendance: ...
```

### One important restriction

Don't copy a random value without thinking about its type.

Ask yourself:

> **What type of data am I trying to store here?**

For example:

```text
age        → int
gpa        → double
enrolled   → boolean
grade      → char
name       → String
```

That's the actual skill we're practicing.

***

# 18. Your first code-reading checkpoint

Look at this:

```java
final double tuitionFee = 50000.0;
int studentCount = 30;

studentCount = 35;
```

Without running it, identify:

1. What is the type of `tuitionFee`?
2. What is the variable name?
3. What does `final` do?
4. What is the type of `studentCount`?
5. Which variable can be reassigned?
6. What is the value of `studentCount` after the last line?

Don't answer by memorizing definitions—explain what Java is actually doing.

***

# Session checkpoint

Before considering **Session 1.1 complete**, you should be able to explain in your own words:

1. What is a variable?
2. What is a type?
3. What's the difference between declaration, initialization, and assignment?
4. What's the difference between `int`, `double`, `boolean`, `char`, and `String`?
5. What are `byte`, `short`, `long`, and `float` used for?
6. What does `final` prevent?
7. Why does `(int) 99.99` produce `99`?
8. Why can an `int` generally be assigned to a `double` without explicitly casting?

And you should be comfortable looking at:

```java
final int studentCount = 30;
```

and immediately identifying:

```text
final        → modifier
int          → type
studentCount → variable name
=            → assignment
30           → value
```

**Do the Student Information exercise and answer the checkpoint questions. Don't move to the next session yet.**
