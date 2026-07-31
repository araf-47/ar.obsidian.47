Excellent! You're moving through the roadmap steadily. 🎉

This next lesson introduces one of the biggest improvements in modern Angular. If `@if` felt like a cleaner `*ngIf`, then `@for` is a cleaner and more powerful `*ngFor`.

***

# Angular Master Course

# Module 4A — Modern Angular Control Flow

## Lesson M4.3 — `@for`

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
* 🟨 Lesson M4.3 — `@for`
* ⬜ Lesson M4.4 — Old vs Modern Angular Syntax
* ⬜ Lesson M4.5 — Migration Guide

***

# 📌 Version Note

**Angular 17+**

`@for` is the modern replacement for `*ngFor`.

It keeps the same core concept—repeating elements—but introduces a cleaner syntax and encourages better performance through explicit tracking.

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Use the `@for` block.
* Understand the `track` expression.
* Use contextual variables like `$index`, `$first`, `$last`, `$even`, and `$odd`.
* Compare `@for` with `*ngFor`.
* Know why `track` matters.

***

# Prerequisites

You should already understand:

* ✅ `*ngFor`
* ✅ Arrays
* ✅ Interpolation
* ✅ Modern `@if`

***

# Part 1 — What is `@for`?

### Definition

> `@for` is Angular's modern control flow syntax for repeating a block of HTML for every item in a collection.

If your component has:

```typescript
students = ['Alice', 'Bob', 'Charlie'];
```

Angular will repeat the HTML block **three times**.

***

# Part 2 — Your First `@for`

Component:

```typescript
export class App {
  students = ['Alice', 'Bob', 'Charlie'];
}
```

Old Angular:

```html
<ul>
  <li *ngFor="let student of students">
    {{ student }}
  </li>
</ul>
```

Modern Angular:

```html
<ul>
  @for (student of students; track student) {
    <li>{{ student }}</li>
  }
</ul>
```

Output:

```text
• Alice
• Bob
• Charlie
```

The result is identical.

Only the syntax has changed.

***

# Part 3 — Understanding `track`

This is the biggest difference between `*ngFor` and `@for`.

Imagine this list:

```typescript
students = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' },
  { id: 3, name: 'Charlie' }
];
```

You write:

```html
@for (student of students; track student.id) {
  <li>{{ student.name }}</li>
}
```

The important part is:

```text
track student.id
```

You're telling Angular:

> "Each student is uniquely identified by their `id`."

This helps Angular efficiently determine which items changed when the list is updated.

***

# Why does `track` matter?

Suppose your list is:

```text
1 Alice
2 Bob
3 Charlie
```

Now you insert:

```text
0 David
```

Without tracking, Angular may think many items have changed.

With:

```html
track student.id
```

Angular knows:

* Alice is still Alice.
* Bob is still Bob.
* Charlie is still Charlie.
* Only David is new.

This lets Angular update the DOM more efficiently.

***

# Part 4 — Hands-on Exercise

Component:

```typescript
export class App {
  fruits = [
    { id: 1, name: 'Apple' },
    { id: 2, name: 'Orange' },
    { id: 3, name: 'Banana' }
  ];
}
```

Template:

```html
<ul>
  @for (fruit of fruits; track fruit.id) {
    <li>{{ fruit.name }}</li>
  }
</ul>
```

Run it.

Then try adding another fruit to the array and observe that the new item appears.

***

# Part 5 — Contextual Variables

Just like `*ngFor`, `@for` provides useful information about each iteration.

## `$index`

```html
@for (student of students; track student.id; let i = $index) {
  <p>{{ i }} - {{ student.name }}</p>
}
```

Output:

```text
0 - Alice
1 - Bob
2 - Charlie
```

***

## `$first`

```html
@for (student of students; track student.id; let first = $first) {

  @if (first) {
    <strong>{{ student.name }}</strong>
  } @else {
    {{ student.name }}
  }

}
```

`$first` is `true` only for the first item.

***

## `$last`

```html
let last = $last
```

True only for the last item.

***

## `$even`

```html
let even = $even
```

True for even-numbered iterations (based on the zero-based index).

***

## `$odd`

```html
let odd = $odd
```

True for odd-numbered iterations.

***

# Part 6 — Empty Lists

What if there are no students?

Angular provides an elegant solution:

```html
<ul>
  @for (student of students; track student.id) {
    <li>{{ student.name }}</li>
  } @empty {
    <li>No students found.</li>
  }
</ul>
```

If `students` is empty, Angular renders:

```text
No students found.
```

This replaces the common older pattern of combining `*ngIf` with `*ngFor`.

***

# Part 7 — Comparing Old and Modern

Old Angular:

```html
<li *ngFor="let student of students">
  {{ student }}
</li>
```

Modern Angular:

```html
@for (student of students; track student) {
  <li>{{ student }}</li>
}
```

***

With index:

Old:

```html
<li *ngFor="let student of students; let i = index">
  {{ i }} {{ student }}
</li>
```

Modern:

```html
@for (student of students; track student; let i = $index) {
  <li>{{ i }} {{ student }}</li>
}
```

Notice how the contextual variable names now start with `$`, making them easier to recognize as Angular-provided values.

***

# Part 8 — Real-World Examples

## Student List

```html
@for (student of students; track student.id) {
  <app-student-card [student]="student" />
}
```

***

## Shopping Cart

```html
@for (item of cart; track item.id) {
  <app-cart-item [item]="item" />
}
```

***

## Comments

```html
@for (comment of comments; track comment.id) {
  <app-comment [comment]="comment" />
}
```

***

## Notifications

```html
@for (notification of notifications; track notification.id) {
  <app-notification [notification]="notification" />
} @empty {
  <p>No notifications.</p>
}
```

***

# Common Beginner Mistakes

## ❌ Forgetting `track`

Technically you can track by the item itself:

```html
track student
```

But when working with objects, a stable unique identifier like `student.id` is usually the better choice.

***

## ❌ Using `$index` as the identity

You may see:

```html
track $index
```

This can work for lists that never change order, but it's not a good default for lists where items can be inserted, removed, or reordered.

Prefer a real unique identifier whenever one exists.

***

## ❌ Forgetting `@empty`

Instead of writing extra `@if` blocks to check whether a list is empty, remember that `@empty` is built into `@for`.

***

# Mini Challenge

Component:

```typescript
books = [
  { id: 1, title: 'Angular Basics' },
  { id: 2, title: 'Learning TypeScript' },
  { id: 3, title: 'Spring Boot Guide' }
];
```

Create a template that:

* Displays all book titles using `@for`.
* Tracks each book by `book.id`.
* Shows the row number using `$index`.
* Displays "Library is empty." using `@empty` if the list has no books.

Try solving it before checking the examples.

***

# Quick Review

Without looking back:

1. What does `@for` do?
2. What is the purpose of `track`?
3. Why is `track item.id` usually better than `track $index`?
4. What does `$index` provide?
5. What does `@empty` do?

***

# Lesson Summary

Today you learned:

* ✅ The basic `@for` syntax.
* ✅ Why `track` improves performance.
* ✅ Contextual variables like `$index`, `$first`, `$last`, `$even`, and `$odd`.
* ✅ The `@empty` block.
* ✅ How `@for` compares to `*ngFor`.

***

# Roadmap Progress

### Module 4A — Modern Angular Control Flow

* ✅ Lesson M4.1 — Why Modern Control Flow?
* ✅ Lesson M4.2 — `@if`
* ✅ Lesson M4.3 — `@for`
* ⬜ Lesson M4.4 — Old vs Modern Angular Syntax
* ⬜ Lesson M4.5 — Migration Guide

***

# 🎯 Mental Model

Imagine you're a teacher handing back exam papers.

Each paper has a **student ID**.

When students line up in a different order, you don't identify them by where they're standing in the line—you identify them by their **student ID**.

That's exactly what `track` does.

* `track student.id` → "This is the same student, even if they moved."
* `track $index` → "I only know their position in the line."

When lists change frequently, tracking by a stable ID lets Angular update only what's necessary, making your application more efficient.

***

## 📌 Looking Ahead

Next we'll cover **Lesson M4.4 — Old vs. Modern Angular Syntax**, where we'll place `*ngIf` beside `@if` and `*ngFor` beside `@for` in a comprehensive comparison. By the end of that lesson, you'll be able to switch between legacy and modern Angular templates confidently.
