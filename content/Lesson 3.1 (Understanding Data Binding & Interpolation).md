Excellent. I think this is the right decision.

Since you've explicitly said you want this course to be a **syllabus-driven, university-quality course** with minimal hallucination, I'm going to treat this like a textbook.

That means:

* We follow the roadmap **exactly**.
* We don't introduce future topics early.
* We don't skip important concepts.
* Every lesson builds on the previous one.
* If I need to mention a future topic, I'll clearly label it as a preview.

***

# Angular Master Course

# Module 3 — Templates & Data Binding

## Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)

### Module Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components

### Module 3 — Templates & Data Binding

* 🟨 Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)
* ⬜ Lesson 3.2 — Property Binding (`[]`)
* ⬜ Lesson 3.3 — Event Binding (`()`)
* ⬜ Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)
* ⬜ Lesson 3.5 — Template Expressions
* ⬜ Lesson 3.6 — Pipes & Built-in Pipes

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what **data binding** is.
* Explain why Angular needs data binding.
* Understand the relationship between a **component** and its **template**.
* Use **interpolation (`{{ }}`)** correctly.
* Know what kinds of values can be displayed with interpolation.
* Recognize the limitations of interpolation.

***

# Prerequisites

Before continuing, make sure you are comfortable with:

* ✅ Components
* ✅ Templates
* ✅ Component classes
* ✅ Basic TypeScript variables

You have already completed all of these.

***

# Part 1 — The Problem

Let's start with plain HTML.

```html
<h1>Welcome</h1>

<p>Angular Course</p>
```

Question:

> Where is the data coming from?

Answer:

Nowhere.

The HTML itself contains the text.

If you want to change:

```
Angular Course
```

to

```
Learning Angular
```

you must edit the HTML file.

The page is **static**.

***

# What Makes Angular Different?

Suppose your component contains:

```typescript
export class App {

    course = "Angular";

}
```

The value exists inside the TypeScript class.

Question:

How can the HTML display it?

The HTML file cannot directly access TypeScript.

Something has to connect them.

That "something" is **Angular's data binding system**.

***

# What Is Data Binding?

Definition:

> **Data binding is the mechanism Angular uses to synchronize data between a component and its template.**

Let's simplify that.

Your application has two worlds:

### World 1

The component.

It contains:

* variables
* methods
* logic

Example:

```typescript
export class App {

    course = "Angular";

    version = 20;

}
```

***

### World 2

The template.

It contains:

```html
<h1>...</h1>

<p>...</p>
```

Without Angular:

```
Component

course = "Angular"

        ❌

HTML
```

No communication.

With Angular:

```
Component

↓

Angular

↓

Template
```

Angular becomes the bridge.

***

# Real-Life Analogy

Imagine a restaurant.

The kitchen prepares food.

Customers never enter the kitchen.

Instead,

the waiter carries the food.

```
Kitchen

↓

Waiter

↓

Customer
```

Angular works similarly.

```
Component

↓

Data Binding

↓

Template
```

The template doesn't "cook" data.

It only displays it.

***

# Types of Data Binding

Angular provides four major kinds.

We'll learn each one in its own lesson.

| Type             | Direction                | Purpose                       |
| ---------------- | ------------------------ | ----------------------------- |
| Interpolation    | Component → Template     | Display text                  |
| Property Binding | Component → DOM Property | Set element properties        |
| Event Binding    | Template → Component     | Respond to user actions       |
| Two-Way Binding  | Both directions          | Keep UI and data synchronized |

Today we only study the first one.

***

# Part 2 — Interpolation

Interpolation is the simplest and most common form of data binding.

Syntax:

```html
{{ expression }}
```

Whenever Angular sees:

```html
{{ }}
```

it evaluates the expression inside and inserts the result into the page.

***

# Your First Example

Component:

```typescript
export class App {

    course = "Angular";

}
```

Template:

```html
<h1>{{ course }}</h1>
```

Browser output:

```html
<h1>Angular</h1>
```

Angular replaces:

```
{{ course }}
```

with

```
Angular
```

***

# How It Works

Imagine Angular performing these steps:

```
Read component

↓

Find variable

↓

Read template

↓

Replace {{ course }}

↓

Display HTML
```

The browser never understands:

```html
{{ course }}
```

Angular processes it first.

***

# Displaying Different Data Types

Interpolation works with many data types.

## String

```typescript
name = "Araf";
```

```html
{{ name }}
```

Output:

```
Araf
```

***

## Number

```typescript
age = 22;
```

```html
{{ age }}
```

Output:

```
22
```

***

## Boolean

```typescript
isStudent = true;
```

```html
{{ isStudent }}
```

Output:

```
true
```

***

# Displaying Multiple Variables

Component:

```typescript
firstName = "Araf";

lastName = "Rahman";
```

Template:

```html
{{ firstName }}

{{ lastName }}
```

Output:

```
Araf

Rahman
```

Or combine them:

```html
{{ firstName }} {{ lastName }}
```

Output:

```
Araf Rahman
```

***

# Interpolation Can Evaluate Simple Expressions

Interpolation isn't limited to variables.

Example:

```html
{{ 5 + 10 }}
```

Output:

```
15
```

Example:

```html
{{ 100 / 5 }}
```

Output:

```
20
```

Example:

```html
{{ "Angular " + "Course" }}
```

Output:

```
Angular Course
```

Angular evaluates the expression and displays the result.

***

# Using Component Expressions

Component:

```typescript
price = 100;

tax = 20;
```

Template:

```html
Total: {{ price + tax }}
```

Output:

```
Total: 120
```

Notice that Angular evaluates the expression in the context of the component.

***

# Calling Methods

Interpolation can also call methods defined on the component.

Component:

```typescript
export class App {

    getGreeting() {
        return "Welcome!";
    }

}
```

Template:

```html
{{ getGreeting() }}
```

Output:

```
Welcome!
```

> **Best Practice:** Keep methods used in interpolation simple and fast. Angular may evaluate template expressions multiple times during change detection. We'll learn about change detection later in the course.

***

# What Interpolation Cannot Do

Interpolation is designed for **reading values**, not performing complex work.

Avoid:

* Long calculations.
* Modifying variables.
* Calling expensive functions.
* Business logic.

Keep templates simple.

A good rule is:

> **Templates display data. Components contain the logic.**

***

# Hands-on Exercise

Open:

```
src/app/app.ts
```

Replace the class with:

```typescript
export class App {

  course = 'Angular';

  student = 'Araf';

  age = 22;

}
```

***

Open:

```
src/app/app.html
```

Replace the contents with:

```html
<h1>{{ course }}</h1>

<p>Student: {{ student }}</p>

<p>Age: {{ age }}</p>

<p>Next Year: {{ age + 1 }}</p>

<p>{{ "Welcome to Angular!" }}</p>
```

Save the files.

If `ng serve` is running, your browser updates automatically.

Experiment:

Change:

```typescript
student = "John";
```

Save.

Watch the page update automatically.

***

# Common Beginner Mistakes

## ❌ Forgetting the curly braces

Wrong:

```html
<h1>course</h1>
```

This displays the literal word:

```
course
```

Correct:

```html
<h1>{{ course }}</h1>
```

***

## ❌ Using JavaScript keywords instead of component properties

Wrong:

```html
{{ window.location }}
```

Templates do **not** have direct access to global browser objects like `window` or `document`.

They primarily work with the component's properties and methods.

***

## ❌ Putting too much logic in the template

Avoid:

```html
{{ calculateAnnualSalaryAfterBonusAndTax() }}
```

Instead, keep complex logic inside the component and expose only the final result or a simple method.

***

# Quick Review

Without looking back, answer these:

1. What is data binding?
2. What problem does interpolation solve?
3. What syntax does interpolation use?
4. Can interpolation display numbers and booleans?
5. Should complex business logic be placed inside interpolation?

***

# Lesson Summary

Today you learned:

* ✅ What data binding is.
* ✅ Why Angular needs data binding.
* ✅ How components communicate with templates.
* ✅ How interpolation (`{{ }}`) works.
* ✅ What types of values interpolation can display.
* ✅ Why templates should remain simple.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components

### Module 3 — Templates & Data Binding

* ✅ Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)
* ⬜ Lesson 3.2 — Property Binding (`[]`)
* ⬜ Lesson 3.3 — Event Binding (`()`)
* ⬜ Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)
* ⬜ Lesson 3.5 — Template Expressions
* ⬜ Lesson 3.6 — Pipes & Built-in Pipes

***

## 📚 Instructor's Note

From this lesson onward, I want to add one new habit to the course.

Whenever Angular introduces a piece of syntax, I'll tell you **three things**:

1. **What it does** (the practical purpose).
2. **How Angular processes it** (the mental model).
3. **When you should and shouldn't use it** (best practices).

This way, you're not just memorizing syntax—you'll understand *why* Angular works the way it does, which will make learning the more advanced topics (directives, services, routing, and forms) much easier.
