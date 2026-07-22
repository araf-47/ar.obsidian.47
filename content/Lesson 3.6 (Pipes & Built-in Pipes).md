Excellent! 🎉

This is the final lesson of **Module 3**.

You've learned how to display data, update the UI, respond to user actions, and synchronize data between the component and the view.

Now you'll learn how to **format** that data before displaying it.

Instead of changing the original data in your component, Angular lets you transform it **only for display** using **Pipes**.

***

# Angular Master Course

# Module 3 — Templates & Data Binding

## Lesson 3.6 — Pipes & Built-in Pipes

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components

### Module 3 — Templates & Data Binding

* ✅ Lesson 3.1 — Understanding Data Binding & Interpolation (`{{ }}`)
* ✅ Lesson 3.2 — Property Binding (`[]`)
* ✅ Lesson 3.3 — Event Binding (`()`)
* ✅ Lesson 3.4 — Two-Way Binding (`[(ngModel)]`)
* ✅ Lesson 3.5 — Template Expressions
* 🟨 Lesson 3.6 — Pipes & Built-in Pipes

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what a pipe is.
* Understand why pipes exist.
* Use Angular's built-in pipes.
* Pass parameters to pipes.
* Chain multiple pipes together.
* Know when to use pipes instead of modifying data in the component.

***

# Prerequisites

You should already understand:

* ✅ Interpolation
* ✅ Property Binding
* ✅ Event Binding
* ✅ Two-Way Binding
* ✅ Template Expressions

***

# Part 1 — The Problem

Suppose your component contains:

```typescript
export class App {
  username = 'araf';
}
```

Template:

```html
<p>{{ username }}</p>
```

Output:

```
araf
```

But what if you want:

```
ARAF
```

Should you change the component?

```typescript
username = 'ARAF';
```

Maybe.

But what if you still need the original value elsewhere?

Changing the data just for display isn't a good idea.

Angular gives us **Pipes**.

***

# What Is a Pipe?

**Definition:**

> A pipe transforms data in a template without changing the original value.

Think of it like a water filter.

```
Original Data

↓

Pipe

↓

Formatted Data
```

The original data stays the same.

Only the displayed value changes.

***

# Pipe Syntax

General syntax:

```html
{{ expression | pipeName }}
```

Notice the vertical bar:

```
|
```

This symbol means:

> "Take the value on the left and pass it through the pipe on the right."

Example:

```html
{{ username | uppercase }}
```

Output:

```
ARAF
```

***

# Example

Component:

```typescript
export class App {
  username = 'araf';
}
```

Template:

```html
<p>{{ username | uppercase }}</p>
```

Output:

```
ARAF
```

The component variable is still:

```typescript
username = 'araf';
```

Only the display changes.

***

# Built-in Pipes

Angular includes many useful pipes.

We'll cover the most common ones.

***

# 1. UpperCasePipe

Converts text to uppercase.

Component:

```typescript
username = 'araf';
```

Template:

```html
{{ username | uppercase }}
```

Output:

```
ARAF
```

***

# 2. LowerCasePipe

Converts text to lowercase.

```html
{{ username | lowercase }}
```

Output:

```
araf
```

***

# 3. TitleCasePipe

Capitalizes the first letter of each word.

Component:

```typescript
course = 'angular master course';
```

Template:

```html
{{ course | titlecase }}
```

Output:

```
Angular Master Course
```

***

# 4. DatePipe

Formats dates.

Component:

```typescript
today = new Date();
```

Template:

```html
{{ today | date }}
```

Example output:

```
Jul 21, 2026
```

You can specify a format:

```html
{{ today | date:'fullDate' }}
```

Example:

```
Tuesday, July 21, 2026
```

Other common formats:

```html
{{ today | date:'short' }}
```

```html
{{ today | date:'medium' }}
```

```html
{{ today | date:'longDate' }}
```

***

# 5. CurrencyPipe

Formats numbers as currency.

Component:

```typescript
price = 500;
```

Template:

```html
{{ price | currency }}
```

Example output (depends on locale):

```
$500.00
```

Specify a currency:

```html
{{ price | currency:'BDT' }}
```

Depending on your application's locale, this may display the Bangladeshi Taka currency code or symbol.

> We'll learn more about localization (locale) in a later module.

***

# 6. PercentPipe

Component:

```typescript
score = 0.85;
```

Template:

```html
{{ score | percent }}
```

Output:

```
85%
```

***

# 7. NumberPipe

Formats numbers.

Component:

```typescript
population = 1234567.89;
```

Template:

```html
{{ population | number }}
```

Output:

```
1,234,567.89
```

You can also control formatting:

```html
{{ population | number:'1.2-2' }}
```

For now, just know that the string controls the number of integer and decimal digits.

We'll revisit advanced formatting later if needed.

***

# Passing Parameters

Some pipes accept parameters.

General syntax:

```html
{{ value | pipe:parameter }}
```

Example:

```html
{{ today | date:'fullDate' }}
```

Here:

```
date
```

is the pipe.

```
fullDate
```

is its parameter.

***

# Chaining Pipes

You can use multiple pipes together.

Example:

```html
{{ username | uppercase | slice:0:2 }}
```

Imagine:

```
araf

↓

uppercase

↓

ARAF

↓

slice

↓

AR
```

Each pipe receives the output of the previous one.

***

# Hands-on Exercise

## Step 1

Open:

```
src/app/app.ts
```

Replace the class with:

```typescript
export class App {

  username = 'araf';

  course = 'angular master course';

  today = new Date();

  price = 1500;

  score = 0.92;

  population = 1234567.89;

}
```

***

## Step 2

Open:

```
src/app/app.html
```

Replace the contents with:

```html
<h2>{{ username }}</h2>

<h2>{{ username | uppercase }}</h2>

<h2>{{ username | lowercase }}</h2>

<h2>{{ course | titlecase }}</h2>

<hr>

<p>{{ today | date }}</p>

<p>{{ today | date:'fullDate' }}</p>

<hr>

<p>{{ price | currency }}</p>

<p>{{ price | currency:'BDT' }}</p>

<hr>

<p>{{ score | percent }}</p>

<p>{{ population | number }}</p>
```

***

## Step 3

Save the files.

Observe how the same data is displayed in different formats without changing the original values in your component.

***

# Common Beginner Mistakes

## ❌ Thinking pipes change the original data

They don't.

Pipes only transform the displayed value.

***

## ❌ Forgetting the pipe symbol

Wrong:

```html
{{ username uppercase }}
```

Correct:

```html
{{ username | uppercase }}
```

***

## ❌ Putting pipes in the component

Pipes belong in the **template**, not in your TypeScript class.

***

# Quick Review

Without looking back:

1. What is a pipe?
2. What symbol is used to apply a pipe?
3. Name four built-in pipes.
4. Do pipes change the original data?
5. Can multiple pipes be chained together?

***

# Lesson Summary

Today you learned:

* ✅ What pipes are.
* ✅ Why Angular uses pipes.
* ✅ How to use built-in pipes.
* ✅ How to pass parameters to pipes.
* ✅ How to chain multiple pipes together.
* ✅ That pipes format data without changing the original value.

***

# 🎉 Module 3 Complete!

Congratulations! You have now completed one of the most important modules in Angular.

You now understand how a component and its template communicate in every direction.

### What you've learned in Module 3

* ✅ Interpolation (`{{ }}`)
* ✅ Property Binding (`[]`)
* ✅ Event Binding (`()`)
* ✅ Two-Way Binding (`[(ngModel)]`)
* ✅ Template Expressions
* ✅ Pipes

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding
* ⬜ Module 4 — Directives
* ⬜ Module 5 — Services & Dependency Injection
* ⬜ Module 6 — Routing
* ⬜ Module 7 — HTTP & APIs
* ⬜ Module 8 — Forms

***

## 📌 A Note About Modern Angular

The built-in pipes you've learned (`uppercase`, `date`, `currency`, `number`, etc.) are stable and widely used across Angular applications.

In newer versions of Angular, you'll also encounter newer reactive features like **signals**, but they **complement** pipes rather than replace them. Pipes remain the standard way to format data in templates, so what you've learned here is both current and practical.

***

### Next Module Preview: Directives

So far, your templates have displayed data and responded to events.

In **Module 4**, you'll learn how to **change the structure and appearance of the DOM** itself using **directives**.

You'll answer questions like:

* Should this element exist?
* How do I repeat an element for every item in a list?
* How can I change an element's CSS class dynamically?

Those capabilities are what make Angular templates truly dynamic.
