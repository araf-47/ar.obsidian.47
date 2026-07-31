Excellent. This is where you'll notice the payoff from learning `*ngIf` first.

I'm going to teach `@if` **by comparing it to `*ngIf`**, not as a completely new feature. That way, you'll see that you're really learning a **new way of writing the same idea**.

***

# Angular Master Course

# Module 4A — Modern Angular Control Flow

## Lesson M4.2 — `@if`

### Progress

### Module 4 — Directives ✅ Complete

* ✅ What are Directives
* ✅ Structural Directives
* ✅ `*ngIf`
* ✅ `*ngFor`
* ✅ Attribute Directives
* ✅ `ngClass`
* ✅ `ngStyle`

### Module 4A — Modern Angular Control Flow

* ✅ Lesson M4.1 — Why Modern Control Flow?
* 🟨 Lesson M4.2 — `@if`
* ⬜ Lesson M4.3 — `@for`
* ⬜ Lesson M4.4 — Old vs Modern Angular Syntax
* ⬜ Lesson M4.5 — Migration Guide

***

# 📌 Version Note

**Angular 17+**

`@if` is available starting with Angular 17 and is the recommended way to write conditional rendering in modern Angular projects.

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Use the `@if` block.
* Use `@else`.
* Use `@else if`.
* Compare `@if` with `*ngIf`.
* Know when to use `@if` in modern Angular applications.

***

# Prerequisites

You should already understand:

* ✅ `*ngIf`
* ✅ Structural Directives
* ✅ Data Binding

***

# Part 1 — What is `@if`?

### Definition

> `@if` is Angular's modern control flow syntax for conditionally rendering content.

Conceptually, it answers the same question as `*ngIf`:

> **Should this content exist?**

If the condition is:

* **true** → Angular renders the block.
* **false** → Angular skips the block.

The behavior is exactly the same as `*ngIf`.

Only the syntax is different.

***

# Part 2 — Your First `@if`

Suppose your component contains:

```typescript
export class App {

  isLoggedIn = true;

}
```

Instead of writing:

```html
<p *ngIf="isLoggedIn">
  Welcome back!
</p>
```

You now write:

```html
@if (isLoggedIn) {
  <p>Welcome back!</p>
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

The paragraph is not rendered.

***

# Part 3 — Side-by-Side Comparison

Old Angular:

```html
<p *ngIf="isLoggedIn">
  Welcome!
</p>
```

Modern Angular:

```html
@if (isLoggedIn) {
  <p>Welcome!</p>
}
```

Notice something?

The modern syntax looks much closer to JavaScript.

***

# JavaScript

```javascript
if (isLoggedIn) {
    console.log("Welcome");
}
```

***

# Angular

```html
@if (isLoggedIn) {
    <p>Welcome</p>
}
```

This similarity is intentional.

***

# Part 4 — Hands-on Exercise

## Step 1

`app.ts`

```typescript
export class App {

  isLoggedIn = true;

}
```

***

## Step 2

`app.html`

```html
<h1>Modern Angular</h1>

@if (isLoggedIn) {

  <p>Welcome back!</p>

}
```

Run the application.

You should see:

```text
Modern Angular

Welcome back!
```

***

## Step 3

Change:

```typescript
isLoggedIn = false;
```

The paragraph disappears.

Exactly like `*ngIf`.

***

# Part 5 — `@else`

Old Angular required:

```html
<p *ngIf="isLoggedIn; else loggedOut">
  Welcome!
</p>

<ng-template #loggedOut>
  <p>Please log in.</p>
</ng-template>
```

Notice the `<ng-template>`.

Modern Angular removes that extra ceremony.

Now you simply write:

```html
@if (isLoggedIn) {

  <p>Welcome!</p>

} @else {

  <p>Please log in.</p>

}
```

Much easier to read.

***

# Part 6 — `@else if`

This is one of the biggest improvements.

Imagine a grading system.

Old Angular often required nested `*ngIf` directives or multiple `ng-template` references.

Modern Angular looks almost exactly like JavaScript.

```html
@if (score >= 80) {

  <p>Grade A</p>

} @else if (score >= 60) {

  <p>Grade B</p>

} @else if (score >= 40) {

  <p>Grade C</p>

} @else {

  <p>Failed</p>

}
```

It's much easier to follow.

***

# Part 7 — Real-World Examples

## Login System

```html
@if (isLoggedIn) {

  <button>Logout</button>

} @else {

  <button>Login</button>

}
```

***

## Shopping Cart

```html
@if (cart.length === 0) {

  <p>Your cart is empty.</p>

}
```

***

## Admin Dashboard

```html
@if (isAdmin) {

  <app-admin-panel />

}
```

***

## Loading Screen

```html
@if (isLoading) {

  <p>Loading...</p>

} @else {

  <app-products />

}
```

***

# Part 8 — Under the Hood

Although the syntax changed, Angular still asks the same question:

```text
Condition?

↓

True?

↓

Render the block.
```

or

```text
Condition?

↓

False?

↓

Skip the block.
```

The DOM behavior hasn't changed.

Only the template syntax has.

***

# Part 9 — Comparing Old and Modern

| Old                        | Modern                    |
| -------------------------- | ------------------------- |
| `*ngIf`                    | `@if`                     |
| `else` via `<ng-template>` | Inline `@else`            |
| Multiple templates         | Single readable block     |
| Less similar to JavaScript | Much closer to JavaScript |

***

# Common Beginner Mistakes

## ❌ Mixing the syntaxes

Wrong:

```html
@if (*ngIf="isLoggedIn") {

}
```

Choose **one** style.

***

## ❌ Forgetting the braces

Wrong:

```html
@if (isLoggedIn)

<p>Welcome</p>
```

Correct:

```html
@if (isLoggedIn) {

  <p>Welcome</p>

}
```

***

## ❌ Thinking `@if` is just text

It isn't.

Angular recognizes `@if` as part of its template syntax during compilation.

***

# Mini Challenge

Build a page with:

Component:

```typescript
isPremium = true;
```

Requirements:

If the user is premium:

```text
⭐ Premium Member
```

Otherwise:

```text
Regular Member
```

Then extend it by adding another variable:

```typescript
isAdmin = true;
```

Use `@else if` so the page can display:

* Administrator
* Premium Member
* Regular Member

***

# Quick Review

Without looking back:

1. What problem does `@if` solve?
2. How is `@if` different from `*ngIf`?
3. Why is `@else` easier to read than the old syntax?
4. What new capability makes multiple conditions cleaner?
5. Does `@if` change the DOM behavior compared with `*ngIf`?

***

# Lesson Summary

Today you learned:

* ✅ The basic `@if` syntax.
* ✅ `@else`.
* ✅ `@else if`.
* ✅ Side-by-side comparisons with `*ngIf`.
* ✅ Why the new syntax is easier to read.

***

# Roadmap Progress

### Module 4A — Modern Angular Control Flow

* ✅ Lesson M4.1 — Why Modern Control Flow?
* ✅ Lesson M4.2 — `@if`
* ⬜ Lesson M4.3 — `@for`
* ⬜ Lesson M4.4 — Old vs Modern Angular Syntax
* ⬜ Lesson M4.5 — Migration Guide

***

# 🎯 Mental Model

Think of `@if` as Angular finally speaking the same "language" as JavaScript.

In JavaScript, you already know:

```javascript
if (condition) {
    // do something
} else {
    // do something else
}
```

Now Angular templates follow that same structure:

```html
@if (condition) {
  <!-- render this -->
} @else {
  <!-- render that -->
}
```

The **idea** hasn't changed from `*ngIf`—only the **way you express it** has.

***

## 💡 One Important Note

From this point onward, when I introduce new Angular features (services, routing, forms, HTTP, etc.), I'll usually show **both** syntaxes when conditional rendering is needed:

* The **modern** `@if` version (recommended for new Angular 17+ projects).
* The **classic** `*ngIf` version when it's helpful for understanding or for maintaining older code.

That way, you'll be comfortable working with both modern and legacy Angular applications.
