Excellent! 🎉

You've now learned the first structural directive:

* `*ngIf` → **Should this element exist?**

Now we'll learn the second one:

* `*ngFor` → **How many copies of this element should exist?**

These two directives are used together constantly in Angular applications.

***

# Angular Master Course

# Module 4 — Directives

## Lesson 4.4 — `*ngFor`

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* ✅ Lesson 4.1 — What are Directives?
* ✅ Lesson 4.2 — Structural Directives
* ✅ Lesson 4.3 — `*ngIf`
* 🟨 Lesson 4.4 — `*ngFor`
* ⬜ Lesson 4.5 — Attribute Directives
* ⬜ Lesson 4.6 — `ngClass`
* ⬜ Lesson 4.7 — `ngStyle`

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what `*ngFor` does.
* Loop through arrays in Angular templates.
* Use special variables like `index`, `first`, `last`, `even`, and `odd`.
* Understand why `trackBy` exists.
* Know when to use `*ngFor`.

***

# Prerequisites

You should already understand:

* ✅ Components
* ✅ Templates
* ✅ Data Binding
* ✅ `*ngIf`

***

# Part 1 — Motivation

Imagine you're building a university portal.

A student is enrolled in five courses:

* Database Systems
* Operating Systems
* Software Engineering
* Networking
* Artificial Intelligence

Should you write this?

```html
<li>Database Systems</li>
<li>Operating Systems</li>
<li>Software Engineering</li>
<li>Networking</li>
<li>Artificial Intelligence</li>
```

That works for **five** courses.

But what if another student has **seven** courses?

Or only **two**?

Or the course list comes from a database?

You don't know the number of items beforehand.

Instead, you want Angular to repeat the same HTML for every item in a collection.

That's exactly what `*ngFor` does.

***

# Part 2 — What is `*ngFor`?

### Definition

> `*ngFor` is a **structural directive** that repeats an HTML element once for every item in a collection.

If you have:

```text
3 items
```

Angular creates:

```text
3 HTML elements
```

If you have:

```text
100 items
```

Angular creates:

```text
100 HTML elements
```

You write the HTML **once**.

Angular repeats it automatically.

***

# Part 3 — Basic Syntax

Component:

```typescript
export class App {

  students = [
    'Alice',
    'Bob',
    'Charlie'
  ];

}
```

Template:

```html
<ul>

  <li *ngFor="let student of students">
    {{ student }}
  </li>

</ul>
```

Output:

```text
• Alice
• Bob
• Charlie
```

Let's break down the syntax:

```html
*ngFor="let student of students"
```

| Part       | Meaning                                            |
| ------- | -------------------------------------------------- |
| `let`      | Creates a local template variable.                 |
| `student`  | Represents the current item during each iteration. |
| `of`       | Reads items from a collection.                     |
| `students` | The array to loop through.                         |

Think of it like Java's enhanced `for` loop:

```java
for (String student : students) {
    System.out.println(student);
}
```

Or JavaScript:

```javascript
for (const student of students) {
    console.log(student);
}
```

The Angular syntax follows the same idea.

***

# Part 4 — Hands-on Exercise

## Step 1

Open:

```text
src/app/app.ts
```

Replace the class with:

```typescript
export class App {

  students = [
    'Alice',
    'Bob',
    'Charlie',
    'David'
  ];

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
<h1>Student List</h1>

<ul>

  <li *ngFor="let student of students">
    {{ student }}
  </li>

</ul>
```

***

## Step 3

Run the application.

You should see:

```text
Student List

• Alice
• Bob
• Charlie
• David
```

Now add another name to the array.

Angular updates the page automatically.

***

# Part 5 — Using `index`

Sometimes you need the position of each item.

Example:

```html
<li *ngFor="let student of students; index as i">
  {{ i + 1 }}. {{ student }}
</li>
```

Output:

```text
1. Alice
2. Bob
3. Charlie
4. David
```

Notice that `index` starts at **0**, so we display `i + 1` for a friendlier numbered list.

***

# Part 6 — Other Useful Variables

Angular provides several variables inside `*ngFor`.

## `first`

```html
<li *ngFor="let student of students; first as isFirst">
  {{ student }}
  <span *ngIf="isFirst">(First Student)</span>
</li>
```

***

## `last`

```html
<li *ngFor="let student of students; last as isLast">
  {{ student }}
  <span *ngIf="isLast">(Last Student)</span>
</li>
```

***

## `even`

```html
<li *ngFor="let student of students; even as isEven">
  {{ student }} - Even Row: {{ isEven }}
</li>
```

***

## `odd`

```html
<li *ngFor="let student of students; odd as isOdd">
  {{ student }} - Odd Row: {{ isOdd }}
</li>
```

These are useful for alternating row colors, labels, and styling.

***

# Part 7 — What is `trackBy`?

Imagine you have a list of 1,000 products.

One product changes.

Without extra information, Angular may have to compare many DOM elements to figure out what changed.

`trackBy` helps Angular identify items more efficiently by using a unique identifier.

Example:

```typescript
products = [
  { id: 1, name: 'Laptop' },
  { id: 2, name: 'Mouse' }
];

trackById(index: number, product: any) {
  return product.id;
}
```

Template:

```html
<li *ngFor="let product of products; trackBy: trackById">
  {{ product.name }}
</li>
```

For small practice projects, you usually don't need `trackBy`.

For larger applications with frequently changing lists, it can improve performance.

***

# Part 8 — Real-World Examples

## Student List

```html
<li *ngFor="let student of students">
  {{ student }}
</li>
```

***

## Product Catalog

```html
<div *ngFor="let product of products">
  {{ product.name }}
</div>
```

***

## Todo List

```html
<li *ngFor="let task of tasks">
  {{ task }}
</li>
```

***

## Chat Messages

```html
<p *ngFor="let message of messages">
  {{ message }}
</p>
```

***

# Under the Hood

Suppose you write:

```html
<li *ngFor="let student of students">
  {{ student }}
</li>
```

If the array contains:

```typescript
['Alice', 'Bob', 'Charlie']
```

Angular conceptually creates:

```html
<li>Alice</li>
<li>Bob</li>
<li>Charlie</li>
```

You only wrote one `<li>`.

Angular generated the rest.

***

# Common Beginner Mistakes

## ❌ Forgetting `let`

Wrong:

```html
<li *ngFor="student of students">
```

Correct:

```html
<li *ngFor="let student of students">
```

***

## ❌ Using `in` instead of `of`

Wrong:

```html
<li *ngFor="let student in students">
```

Correct:

```html
<li *ngFor="let student of students">
```

Angular uses `of`, similar to JavaScript's `for...of` loop.

***

## ❌ Modifying the loop variable

This is a template variable representing the current item.

If you need to change the data, do it in the component, not in the template.

***

## ❌ Thinking `trackBy` is always required

It isn't.

Learn the basics first.

Use `trackBy` when working with larger, frequently updated lists.

***

# Mini Challenge

Create a list of your favorite programming languages.

Component:

```typescript
languages = [
  'Java',
  'JavaScript',
  'TypeScript',
  'SQL'
];
```

Template requirements:

* Display the list using `*ngFor`.
* Show the index before each language.
* Mark the first language with `(Favorite)`.

Try to complete it without looking back.

***

# Quick Review

Without looking back:

1. What does `*ngFor` do?
2. What does `let` mean in `*ngFor`?
3. What is the purpose of `index`?
4. Name three special variables available inside `*ngFor`.
5. Why might you use `trackBy`?

***

# Lesson Summary

Today you learned:

* ✅ What `*ngFor` is.
* ✅ How to loop through arrays.
* ✅ `index`, `first`, `last`, `even`, and `odd`.
* ✅ The purpose of `trackBy`.
* ✅ Common real-world uses of `*ngFor`.

***

# Roadmap Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* ✅ Lesson 4.1 — What are Directives?
* ✅ Lesson 4.2 — Structural Directives
* ✅ Lesson 4.3 — `*ngIf`
* ✅ Lesson 4.4 — `*ngFor`
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

Think of `*ngFor` as a **photocopier**.

You hand Angular **one template**:

```html
<li>{{ student }}</li>
```

Then you hand it **a list of data**.

Angular makes one copy of that template for every item in the list and fills in the values.

* `*ngIf` answers: **"Should this element exist?"**
* `*ngFor` answers: **"How many copies of this element should exist?"**

Those two ideas together form the foundation of dynamic Angular templates and are among the most frequently used features in everyday Angular development.
