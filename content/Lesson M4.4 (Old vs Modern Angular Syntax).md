Excellent. This lesson is one of the most valuable in the entire roadmap.

Why?

Because after today, you'll be able to open almost **any Angular project**—whether it's Angular 12, Angular 16, Angular 17, or Angular 20—and understand what's happening.

This is the lesson that bridges **legacy Angular** and **modern Angular**.

***

# Angular Master Course

# Module 4A — Modern Angular Control Flow

## Lesson M4.4 — Old vs. Modern Angular Syntax

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
* ✅ Lesson M4.2 — `@if`
* ✅ Lesson M4.3 — `@for`
* 🟨 Lesson M4.4 — Old vs. Modern Angular Syntax
* ⬜ Lesson M4.5 — Migration Guide

***

# 📌 Version Note

* **Angular 16 and earlier:** Mostly use `*ngIf` and `*ngFor`.
* **Angular 17+:** Supports the new control flow syntax (`@if`, `@for`).
* **Angular 20+:** The new syntax is the recommended approach for new projects.

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Read both old and modern Angular templates.
* Convert old syntax into modern syntax.
* Convert modern syntax back into old syntax.
* Decide which syntax to use in different situations.

***

# Part 1 — The Big Picture

Remember this:

> **Angular did not invent new concepts.**
>
> It introduced a **new way to write the same concepts.**

Think of it like two dialects of the same language.

If you know one, you can learn the other quickly.

***

# Part 2 — Conditional Rendering

## Old Angular

```html
<p *ngIf="isLoggedIn">
  Welcome!
</p>
```

***

## Modern Angular

```html
@if (isLoggedIn) {
  <p>Welcome!</p>
}
```

***

### Same Meaning

Both ask:

> Should this paragraph exist?

If the answer is **yes**, Angular renders it.

If the answer is **no**, Angular skips it.

***

# Part 3 — Else Blocks

## Old Angular

```html
<p *ngIf="isLoggedIn; else loginTemplate">
  Welcome!
</p>

<ng-template #loginTemplate>
  <p>Please log in.</p>
</ng-template>
```

***

## Modern Angular

```html
@if (isLoggedIn) {

  <p>Welcome!</p>

} @else {

  <p>Please log in.</p>

}
```

***

### Which is easier?

Most developers find the modern version easier because everything is in one place.

***

# Part 4 — Multiple Conditions

## Old Angular

This often requires multiple templates or nested conditions.

```html
<div *ngIf="score >= 80; else nextGrade">
  Grade A
</div>

<ng-template #nextGrade>
  ...
</ng-template>
```

As the number of conditions grows, the template becomes harder to follow.

***

## Modern Angular

```html
@if (score >= 80) {

  Grade A

} @else if (score >= 60) {

  Grade B

} @else {

  Failed

}
```

This closely resembles JavaScript.

***

# Part 5 — Repeating Lists

## Old Angular

```html
<ul>

  <li *ngFor="let student of students">
    {{ student }}
  </li>

</ul>
```

***

## Modern Angular

```html
<ul>

  @for (student of students; track student) {

    <li>{{ student }}</li>

  }

</ul>
```

***

### Same Meaning

Both repeat the `<li>` for every student in the array.

***

# Part 6 — Tracking Items

## Old Angular

```html
<li *ngFor="let student of students; trackBy: trackStudent">
```

Component:

```typescript
trackStudent(index: number, student: Student) {
  return student.id;
}
```

Notice that you had to write a separate method.

***

## Modern Angular

```html
@for (student of students; track student.id) {

  <li>{{ student.name }}</li>

}
```

No helper function is needed.

The tracking expression is written directly where it's used.

This is one of the nicest improvements in the new syntax.

***

# Part 7 — Empty Lists

## Old Angular

Many developers combined `*ngIf` and `*ngFor`:

```html
@if (students.length === 0) {

  <p>No students.</p>

}
```

Or in older projects:

```html
<p *ngIf="students.length === 0">
  No students.
</p>

<ul>
  <li *ngFor="let student of students">
    {{ student }}
  </li>
</ul>
```

***

## Modern Angular

```html
<ul>

  @for (student of students; track student.id) {

    <li>{{ student.name }}</li>

  } @empty {

    <li>No students.</li>

  }

</ul>
```

Cleaner.

Everything stays together.

***

# Part 8 — Side-by-Side Cheat Sheet

| Task         | Old Angular        | Modern Angular     |
| ------------ | ------------------ | ------------------ |
| Show content | `*ngIf`            | `@if`              |
| Else         | `<ng-template>`    | `@else`            |
| Else if      | Multiple templates | `@else if`         |
| Loop         | `*ngFor`           | `@for`             |
| Track items  | `trackBy` function | `track` expression |
| Empty list   | Extra `*ngIf`      | `@empty`           |

Save this table mentally—it summarizes the transition from legacy to modern Angular.

***

# Part 9 — When Will You See Each?

## University Courses

Often still teach:

```html
*ngIf
*ngFor
```

because they work across many Angular versions.

***

## Older YouTube Tutorials

Usually:

```html
*ngIf
*ngFor
```

***

## Recent Documentation

Usually:

```html
@if
@for
```

***

## Company Projects

It depends on when the project started.

A project from 2022 may still use the classic syntax.

A project started recently may use the modern syntax throughout.

***

# Part 10 — How Should *You* Write Angular?

Based on where you are in your learning journey:

### When reading:

Learn to recognize **both** styles.

### When writing new practice projects:

Prefer:

```html
@if
```

and

```html
@for
```

### When fixing bugs in an existing project:

Follow the style already used by that project unless your team is actively migrating.

Consistency within a codebase is important.

***

# Real-World Example

Imagine you join a company.

Your team says:

> "We're maintaining an Angular 15 application."

You'll likely work with:

```html
*ngIf
*ngFor
```

Later, the company starts a new Angular 20 project.

Now you'll write:

```html
@if
@for
```

Because you've learned both, switching between them won't be a problem.

***

# Common Beginner Mistakes

## ❌ Thinking modern syntax changes how Angular works

It doesn't.

It changes how **you write** the template, not how Angular decides what to render.

***

## ❌ Refusing to learn the old syntax

Many production applications still use it.

Knowing only the modern syntax would make maintaining older projects harder.

***

## ❌ Converting code just because you can

If you're contributing to an existing project, follow the team's conventions.

Don't rewrite working code unless the team has planned a migration.

***

# Mini Challenge

Convert each old example into modern syntax.

### Example 1

```html
<p *ngIf="loggedIn">
  Welcome
</p>
```

***

### Example 2

```html
<li *ngFor="let course of courses">
  {{ course }}
</li>
```

***

### Example 3

```html
<p *ngIf="cart.length === 0">
  Cart is empty
</p>
```

Try converting them before checking your notes.

***

# Quick Review

Without looking back:

1. What replaced `*ngIf` in modern Angular?
2. What replaced `*ngFor`?
3. What replaces `trackBy`?
4. Which modern feature handles empty lists elegantly?
5. Should you know both syntaxes?

***

# Lesson Summary

Today you learned:

* ✅ How to translate between old and modern Angular syntax.
* ✅ The improvements in readability.
* ✅ The new `track` expression.
* ✅ The `@empty` block.
* ✅ When you'll encounter each syntax in real projects.

***

# Roadmap Progress

### Module 4A — Modern Angular Control Flow

* ✅ Lesson M4.1 — Why Modern Control Flow?
* ✅ Lesson M4.2 — `@if`
* ✅ Lesson M4.3 — `@for`
* ✅ Lesson M4.4 — Old vs. Modern Angular Syntax
* ⬜ Lesson M4.5 — Migration Guide

***

# 🎯 Mental Model

Imagine you've learned to drive a **manual transmission** car.

Later, you learn an **automatic transmission**.

The controls are different:

* Manual → clutch + gear stick.
* Automatic → no clutch.

But the goal is exactly the same:

* Start the car.
* Drive safely.
* Reach your destination.

Old Angular and modern Angular are like that.

* `*ngIf` and `*ngFor` are the "manual transmission."
* `@if` and `@for` are the "automatic transmission."

The **mechanics of writing the code** changed, but the **fundamental concepts**—conditional rendering and repeating content—are exactly the same.

***

## 📌 Looking Ahead

Next is the final lesson of this mini-module:

**Lesson M4.5 — Migration Guide**

This is a practical lesson where we'll answer questions like:

* Should you still use `*ngIf`?
* How do you migrate an existing project?
* What should you use in interviews?
* What if you're following an old tutorial?
* What do companies actually do?

By the end of that lesson, you'll know not just **how** to write Angular templates, but also **when** to choose each approach in real-world development.
