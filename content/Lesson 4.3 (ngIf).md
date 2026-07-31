This is one of the most important lessons in Angular.

If someone asks:

> "What is the first Angular feature you use to make a page dynamic?"

The answer is almost always **`*ngIf`**.

You'll use it constantly in real-world Angular applications.

***

# Angular Master Course

# Module 4 — Directives

## Lesson 4.3 — `*ngIf`

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* ✅ Lesson 4.1 — What are Directives?
* ✅ Lesson 4.2 — Structural Directives
* 🟨 Lesson 4.3 — `*ngIf`
* ⬜ Lesson 4.4 — `*ngFor`
* ⬜ Lesson 4.5 — Attribute Directives
* ⬜ Lesson 4.6 — `ngClass`
* ⬜ Lesson 4.7 — `ngStyle`

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what `*ngIf` does.
* Use `*ngIf` to conditionally display elements.
* Understand truthy and falsy values.
* Use `else` blocks.
* Use `then` and `else` together.
* Know when `*ngIf` should and shouldn't be used.

***

# Prerequisites

You should already understand:

* ✅ Components
* ✅ Templates
* ✅ Data Binding
* ✅ Structural Directives

***

# Part 1 — Motivation

Imagine you're building a university portal.

Students should only see the **Exam Results** section after the results are published.

Before publication:

```text
Student Dashboard

Assignments

Attendance
```

After publication:

```text
Student Dashboard

Assignments

Attendance

Exam Results
```

How do we tell Angular:

> "Only create this section when the results are available."

This is exactly what `*ngIf` does.

***

# Part 2 — What is `*ngIf`?

### Definition

> `*ngIf` is a **structural directive** that creates or removes an element based on a condition.

If the condition is:

* **true** → Angular creates the element.
* **false** → Angular removes the element from the DOM.

Notice the wording:

It does **not** hide the element.

It **removes** it.

***

# Part 3 — Basic Syntax

General syntax:

```html
<element *ngIf="condition">
    Content
</element>
```

Example:

```html
<p *ngIf="isLoggedIn">
    Welcome back!
</p>
```

Component:

```typescript
export class App {
    isLoggedIn = true;
}
```

Output:

```text
Welcome back!
```

Now change:

```typescript
isLoggedIn = false;
```

Output:

Nothing.

Angular doesn't render the `<p>` element.

***

# Part 4 — First Hands-on Exercise

## Step 1

Open:

```text
src/app/app.ts
```

Replace your class with:

```typescript
export class App {

  isLoggedIn = true;

}
```

***

## Step 2

Open:

```text
src/app/app.html
```

Replace everything with:

```html
<h1>Angular *ngIf Demo</h1>

<p *ngIf="isLoggedIn">
  Welcome back!
</p>
```

***

## Step 3

Run the application.

You should see:

```text
Angular *ngIf Demo

Welcome back!
```

***

## Step 4

Now change:

```typescript
isLoggedIn = false;
```

Save.

Now the page should display:

```text
Angular *ngIf Demo
```

The paragraph is gone.

***

# Part 5 — Understanding Truthy and Falsy

`*ngIf` doesn't only work with `true` and `false`.

Angular evaluates expressions using JavaScript truthiness rules.

Examples:

```typescript
isLoggedIn = true;
```

Shows the element.

***

```typescript
isLoggedIn = false;
```

Doesn't show it.

***

```typescript
username = "Araf";
```

Non-empty strings are truthy.

***

```typescript
username = "";
```

Empty strings are falsy.

***

```typescript
count = 5;
```

Non-zero numbers are truthy.

***

```typescript
count = 0;
```

Zero is falsy.

***

```typescript
items = [];
```

An empty array is **truthy** in JavaScript.

That often surprises beginners.

If you want to know whether an array has elements, check its length instead:

```html
<div *ngIf="items.length > 0">
  Items found!
</div>
```

***

# Part 6 — Using Expressions

The condition doesn't have to be a variable.

Example:

```html
<p *ngIf="age >= 18">
    Adult
</p>
```

Or:

```html
<p *ngIf="score > 50">
    Passed
</p>
```

Any expression that evaluates to true or false can be used.

***

# Part 7 — `else`

Instead of showing nothing when the condition is false, you can show different content.

Template:

```html
<p *ngIf="isLoggedIn; else loggedOut">
  Welcome back!
</p>

<ng-template #loggedOut>
  <p>Please log in.</p>
</ng-template>
```

If:

```typescript
isLoggedIn = true;
```

Output:

```text
Welcome back!
```

If:

```typescript
isLoggedIn = false;
```

Output:

```text
Please log in.
```

***

# What is `<ng-template>`?

`<ng-template>` is a special Angular element.

It is **not rendered immediately**.

Angular only renders it when instructed.

Think of it as a stored template waiting to be used.

***

# Part 8 — `then` and `else`

Angular also supports explicit `then` and `else` templates.

Example:

```html
<div *ngIf="isLoggedIn; then welcome; else login"></div>

<ng-template #welcome>
  <h2>Welcome!</h2>
</ng-template>

<ng-template #login>
  <h2>Please log in.</h2>
</ng-template>
```

This is useful when the templates are large or reused.

For simple conditions, `*ngIf` with `else` is usually easier to read.

***

# Part 9 — Real-World Examples

### Login System

```html
<button *ngIf="!isLoggedIn">
  Login
</button>

<button *ngIf="isLoggedIn">
  Logout
</button>
```

***

### Shopping Cart

```html
<p *ngIf="cart.length === 0">
  Your cart is empty.
</p>
```

***

### Admin Panel

```html
<div *ngIf="isAdmin">
  Admin Dashboard
</div>
```

***

### Error Message

```html
<p *ngIf="hasError">
  Something went wrong.
</p>
```

***

# Under the Hood

When Angular sees:

```html
<p *ngIf="isLoggedIn">
  Welcome
</p>
```

You might imagine it simply hiding the paragraph.

It doesn't.

Conceptually, Angular does something like this:

If `isLoggedIn` is true:

```text
Create the <p> element.
Insert it into the DOM.
```

If `isLoggedIn` is false:

```text
Remove the <p> element from the DOM.
```

The DOM itself changes.

That's why `*ngIf` is called a **structural** directive.

***

# Common Beginner Mistakes

## ❌ Forgetting the `*`

Wrong:

```html
<p ngIf="isLoggedIn">
```

Correct:

```html
<p *ngIf="isLoggedIn">
```

***

## ❌ Thinking `*ngIf` hides elements

It doesn't.

It removes or creates them.

***

## ❌ Using an empty array as "false"

This is incorrect:

```html
<div *ngIf="items">
```

Because:

```typescript
items = [];
```

is still truthy.

Instead:

```html
<div *ngIf="items.length > 0">
```

***

## ❌ Making complex conditions directly in the template

This is valid:

```html
<div *ngIf="age >= 18 && hasPaid && !isBlocked">
```

But if the condition becomes very long, move the logic into the component:

```typescript
get canAccessPortal(): boolean {
  return this.age >= 18 && this.hasPaid && !this.isBlocked;
}
```

Then your template stays readable:

```html
<div *ngIf="canAccessPortal">
```

***

# Mini Challenge

Build a small page with:

* A variable named `isStudent`.
* If `true`, show:

```text
Welcome Student!
```

* Otherwise, show:

```text
Please register first.
```

Try it yourself before looking back at the examples.

***

# Quick Review

Without looking back:

1. What does `*ngIf` do?
2. Does `*ngIf` hide elements or remove them?
3. What is `<ng-template>` used for?
4. Can `*ngIf` use expressions?
5. Why is `*ngIf` called a structural directive?

***

# Lesson Summary

Today you learned:

* ✅ What `*ngIf` is.
* ✅ How to conditionally render elements.
* ✅ Truthy and falsy values.
* ✅ `else` templates.
* ✅ `then` and `else`.
* ✅ Real-world uses of `*ngIf`.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* ✅ Lesson 4.1 — What are Directives?
* ✅ Lesson 4.2 — Structural Directives
* ✅ Lesson 4.3 — `*ngIf`
* ⬜ Lesson 4.4 — `*ngFor`
* ⬜ Lesson 4.5 — Attribute Directives
* ⬜ Lesson 4.6 — `ngClass`
* ⬜ Lesson 4.7 — `ngStyle`

⭐ **Appendix (Modern Angular Notes)**

* `@if`
* `@for`
* Reading old vs. new Angular syntax
* Migration overview

***

## 🎯 Mental Model

Think of `*ngIf` as a **security guard** at the entrance to your page.

Every time Angular renders the template, the guard asks one question:

> **"Does this element have permission to exist?"**

* If the answer is **yes**, the element enters the DOM.
* If the answer is **no**, the element never appears.

That's the essence of `*ngIf`: it controls the **existence** of elements, not just their visibility.

***

### 📌 Looking Ahead

The next lesson, **Lesson 4.4 — `*ngFor`**, answers a different question.

`*ngIf` asks:

> **"Should this element exist?"**

`*ngFor` asks:

> **"How many copies of this element should Angular create?"**

You'll see that these two structural directives often work together to build dynamic user interfaces.
