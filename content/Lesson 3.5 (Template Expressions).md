Excellent! You're making steady progress.

Now we're moving to a lesson that many beginners underestimate.

At first glance, **template expressions** seem like "just writing JavaScript inside `{{ }}`," but that's **not** how Angular works.

Angular has its **own expression language** with rules about what is allowed and what is not. Understanding those rules will help you write cleaner templates and avoid confusing errors.

***

# Angular Master Course

# Module 3 — Templates & Data Binding

## Lesson 3.5 — Template Expressions

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components

### Module 3 — Templates & Data Binding

* ✅ Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)
* ✅ Lesson 3.2 — Property Binding (`[]`)
* ✅ Lesson 3.3 — Event Binding (`()`)
* ✅ Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)
* 🟨 Lesson 3.5 — Template Expressions
* ⬜ Lesson 3.6 — Pipes & Built-in Pipes

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what a template expression is.
* Know where template expressions can be used.
* Understand what Angular allows inside template expressions.
* Understand what Angular does **not** allow.
* Follow best practices for writing readable templates.

***

# Prerequisites

You should already understand:

* ✅ Interpolation (`{{ }}`)
* ✅ Property Binding (`[]`)
* ✅ Event Binding (`()`)
* ✅ Two-Way Binding (`[(ngModel)]`)

***

# Part 1 — What Is a Template Expression?

A **template expression** is an expression that Angular evaluates inside a template.

You've already been using them.

For example:

```html
<h1>{{ title }}</h1>
```

The expression is:

```text
title
```

Angular evaluates it and displays its value.

Another example:

```html
<p>{{ age + 1 }}</p>
```

The expression is:

```text
age + 1
```

Angular evaluates it and displays the result.

So a template expression is simply **the code inside Angular bindings that Angular evaluates**.

***

# Where Can Template Expressions Be Used?

You'll commonly see them in:

### 1. Interpolation

```html
{{ username }}
```

***

### 2. Property Binding

```html
<img [src]="imageUrl">
```

Here, the expression is:

```text
imageUrl
```

***

### 3. Two-Way Binding

```html
<input [(ngModel)]="username">
```

Here, `username` is also part of Angular's template binding system.

***

# Part 2 — What Can You Put Inside a Template Expression?

## Variables

```html
{{ username }}
```

***

## Numbers

```html
{{ age }}
```

***

## Strings

```html
{{ "Angular" }}
```

***

## Arithmetic

```html
{{ 10 + 20 }}
```

```html
{{ price * quantity }}
```

```html
{{ age + 1 }}
```

***

## String Concatenation

```html
{{ firstName + " " + lastName }}
```

Output:

```text
Araf Rahman
```

***

## Boolean Expressions

```html
{{ age >= 18 }}
```

Output:

```text
true
```

***

## Ternary Operator

Angular supports the ternary operator.

Component:

```typescript
age = 20;
```

Template:

```html
{{ age >= 18 ? "Adult" : "Minor" }}
```

Output:

```text
Adult
```

This is very common in Angular templates.

***

## Calling Simple Methods

Component:

```typescript
export class App {

  getGreeting() {
    return 'Welcome!';
  }

}
```

Template:

```html
{{ getGreeting() }}
```

Output:

```text
Welcome!
```

This works.

However...

***

# Best Practice

Methods inside template expressions should be:

* Simple
* Fast
* Free of side effects

Avoid expensive calculations because Angular may evaluate template expressions multiple times while checking for changes.

***

# Part 3 — What Should You Avoid?

## ❌ Complex Logic

Avoid:

```html
{{ calculateFinalSalaryAfterTaxAndBonus() }}
```

Better:

```typescript
finalSalary = 50000;
```

Then:

```html
{{ finalSalary }}
```

***

## ❌ Assignments

Don't write:

```html
{{ age = 25 }}
```

Template expressions are for **reading values**, not assigning them.

***

## ❌ Creating Objects or Arrays

Avoid doing work like:

```html
{{ { name: 'Araf' } }}
```

or

```html
{{ [1, 2, 3] }}
```

Keep object and array creation inside the component.

***

## ❌ Accessing Global Browser Objects

Don't expect this to work:

```html
{{ window.location.href }}
```

or

```html
{{ document.title }}
```

Angular templates don't have direct access to global objects like `window` or `document`.

If you need that information, access it in your component and expose the value through a property.

***

# Part 4 — Safe Navigation Operator (`?.`)

Sometimes a value may not exist yet.

Example:

```typescript
user = undefined;
```

If you write:

```html
{{ user.name }}
```

Angular will try to read `name` from `undefined`, which causes an error.

Instead, use the safe navigation operator:

```html
{{ user?.name }}
```

Meaning:

> "If `user` exists, show the name. Otherwise, show nothing."

This is especially useful when working with data loaded from an API.

***

# Part 5 — Template Expressions Are Not Full JavaScript

A common beginner misconception is:

> "Anything that works in JavaScript should work inside `{{ }}`."

That's not true.

Angular template expressions are intentionally limited.

This keeps templates:

* Easier to read
* More secure
* Easier for Angular to optimize

Think of templates as a place to **display** data, not to write application logic.

***

# Hands-on Exercise

## Step 1

Open:

```text
src/app/app.ts
```

Replace the class with:

```typescript
export class App {

  firstName = 'Araf';

  lastName = 'Rahman';

  age = 22;

  price = 50;

  quantity = 3;

  user = {
    name: 'Araf'
  };

  getGreeting() {
    return 'Welcome to Angular!';
  }

}
```

***

## Step 2

Open:

```text
src/app/app.html
```

Replace the contents with:

```html
<h1>{{ getGreeting() }}</h1>

<p>Name: {{ firstName + " " + lastName }}</p>

<p>Age Next Year: {{ age + 1 }}</p>

<p>Total: {{ price * quantity }}</p>

<p>Status: {{ age >= 18 ? "Adult" : "Minor" }}</p>

<p>User: {{ user?.name }}</p>
```

***

## Step 3

Save the files.

Verify that everything displays correctly.

Then experiment by changing values in your component.

For example:

```typescript
age = 15;
```

Observe how the "Status" changes automatically.

***

# Common Beginner Mistakes

## ❌ Confusing JavaScript with Angular template expressions

Templates support many familiar JavaScript-like expressions, but **not all JavaScript syntax**.

***

## ❌ Writing complex business logic in the template

Keep templates focused on presentation.

Put calculations and business rules in the component.

***

## ❌ Forgetting the safe navigation operator

If a value might be `null` or `undefined`, use:

```html
{{ user?.name }}
```

instead of:

```html
{{ user.name }}
```

***

# Quick Review

Without looking back:

1. What is a template expression?
2. Name three places where template expressions are used.
3. Can you use arithmetic inside template expressions?
4. Why should template expressions stay simple?
5. What does `?.` do?

***

# Lesson Summary

Today you learned:

* ✅ What template expressions are.
* ✅ Where Angular uses them.
* ✅ What kinds of expressions Angular supports.
* ✅ What should be avoided in templates.
* ✅ How to use the safe navigation operator (`?.`).

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components

### Module 3 — Templates & Data Binding

* ✅ Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)
* ✅ Lesson 3.2 — Property Binding (`[]`)
* ✅ Lesson 3.3 — Event Binding (`()`)
* ✅ Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)
* ✅ Lesson 3.5 — Template Expressions
* ⬜ Lesson 3.6 — Pipes & Built-in Pipes

***

## 📌 One Important Clarification

Earlier in the course, we used simple expressions like:

```html
{{ age + 1 }}
```

without calling them "template expressions."

Now you know the proper term: **everything Angular evaluates inside bindings is a template expression**.

This lesson wasn't about learning new syntax as much as understanding **the rules** for writing expressions in Angular templates. Those rules become especially important as your applications grow larger and your templates become more complex.

Next, we'll finish Module 3 by learning **Pipes**, one of Angular's most useful features for formatting data without cluttering your component code.
