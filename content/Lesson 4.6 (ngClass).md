Excellent! This is one of the most practical Angular lessons you'll learn.

Before this lesson, you've already used **property binding**:

```html
<img [src]="imageUrl">
```

Today you'll discover that `ngClass` is really just **property binding applied to CSS classes**.

Once you understand that connection, `ngClass` becomes much easier to remember.

***

# Angular Master Course

# Module 4 — Directives

## Lesson 4.6 — `ngClass`

### Progress

* ✅ Module 1 — Angular Introduction
* ✅ Module 2 — Components
* ✅ Module 3 — Templates & Data Binding

### Module 4 — Directives

* ✅ Lesson 4.1 — What are Directives?
* ✅ Lesson 4.2 — Structural Directives
* ✅ Lesson 4.3 — `*ngIf`
* ✅ Lesson 4.4 — `*ngFor`
* ✅ Lesson 4.5 — Attribute Directives
* 🟨 Lesson 4.6 — `ngClass`
* ⬜ Lesson 4.7 — `ngStyle`

***

# Lesson Objectives

By the end of this lesson, you will be able to:

* Explain what `ngClass` does.
* Apply CSS classes dynamically.
* Use strings, arrays, and objects with `ngClass`.
* Compare `class`, `[class]`, and `[ngClass]`.
* Know when to use `ngClass`.

***

# Prerequisites

You should already understand:

* ✅ CSS classes
* ✅ Property binding (`[]`)
* ✅ Attribute directives

***

# Part 1 — Motivation

Imagine you're building a university portal.

A student's score is displayed like this:

```text
Score: 85
```

The teacher says:

> "Students who pass should have green scores."

Another teacher says:

> "Students who fail should have red scores."

You could manually edit the HTML every time a score changes...

But Angular can do it automatically.

That's exactly what `ngClass` is for.

***

# Part 2 — What is `ngClass`?

### Definition

> `ngClass` is an **attribute directive** that adds or removes CSS classes dynamically.

It does **not**:

* Create elements
* Remove elements
* Repeat elements

It only changes the CSS classes attached to an existing element.

***

# Part 3 — First Example

Component:

```typescript
export class App {

  isPassed = true;

}
```

Template:

```html
<p [ngClass]="isPassed ? 'pass' : 'fail'">
  Final Result
</p>
```

CSS:

```css
.pass {
  color: green;
}

.fail {
  color: red;
}
```

If:

```typescript
isPassed = true;
```

Output:

**Green text**

If:

```typescript
isPassed = false;
```

Output:

**Red text**

Angular changes the class automatically.

***

# Part 4 — Your First Hands-on Exercise

## Step 1

`app.ts`

```typescript
export class App {

  isPassed = true;

}
```

***

## Step 2

`app.html`

```html
<h2>Exam Result</h2>

<p [ngClass]="isPassed ? 'pass' : 'fail'">
  Angular Examination
</p>
```

***

## Step 3

`app.css`

```css
.pass {
  color: green;
}

.fail {
  color: red;
}
```

Run it.

Now change

```typescript
isPassed = false;
```

Watch the color change automatically.

***

# Part 5 — The Three Ways to Use `ngClass`

Angular accepts **three common formats**.

## 1. String (Single or Multiple Class Names)

```html
<p [ngClass]="'highlight'">
  Hello
</p>
```

Or multiple classes:

```html
<p [ngClass]="'highlight bold'">
  Hello
</p>
```

Useful when you already know exactly which class names you want.

***

## 2. Array

```html
<p [ngClass]="['highlight', 'bold']">
  Hello
</p>
```

Angular applies every class in the array.

This is handy when your component builds the list of classes.

***

## 3. Object (Most Common)

```html
<p [ngClass]="{
  pass: score >= 50,
  fail: score < 50
}">
  {{ score }}
</p>
```

Suppose:

```typescript
score = 80;
```

Angular evaluates:

```text
pass  → true
fail  → false
```

Result:

Only the `pass` class is added.

If:

```typescript
score = 20;
```

Result:

Only the `fail` class is added.

This object syntax is the one you'll see most often in Angular projects.

***

# Part 6 — `class` vs `[class]` vs `[ngClass]`

These three are related but serve different purposes.

## Plain `class`

```html
<p class="highlight">
  Hello
</p>
```

The class is fixed.

It never changes.

***

## Property Binding `[class]`

```html
<p [class]="currentClass">
  Hello
</p>
```

Angular replaces the entire class attribute with the value of `currentClass`.

Example:

```typescript
currentClass = 'highlight';
```

***

## `ngClass`

```html
<p [ngClass]="{
  highlight: isHighlighted,
  bold: isBold
}">
  Hello
</p>
```

Angular decides which classes to add or remove individually.

This is much more flexible.

***

# Part 7 — Real-World Examples

## Student Result

```html
<p [ngClass]="{
  pass: marks >= 50,
  fail: marks < 50
}">
  {{ marks }}
</p>
```

***

## Active Navigation

```html
<a [ngClass]="{
  active: currentPage === 'home'
}">
  Home
</a>
```

***

## Todo App

```html
<li [ngClass]="{
  completed: task.done
}">
  {{ task.name }}
</li>
```

***

## Online Store

```html
<div [ngClass]="{
  outOfStock: product.quantity === 0
}">
  {{ product.name }}
</div>
```

***

# Under the Hood

Suppose you write:

```html
<p [ngClass]="{
  pass: true,
  fail: false
}">
```

Angular evaluates the object:

```text
pass → true
fail → false
```

Then it updates the DOM.

Conceptually:

```text
Add class "pass"

Remove class "fail"
```

Angular isn't changing the HTML source file—it is updating the DOM after your application is running.

***

# Common Beginner Mistakes

## ❌ Forgetting the square brackets

Wrong:

```html
<p ngClass="pass">
```

Correct:

```html
<p [ngClass]="'pass'">
```

Without `[]`, Angular treats it as a plain HTML attribute instead of evaluating an expression.

***

## ❌ Confusing `class` with `ngClass`

```html
class="pass"
```

Always applies the class.

```html
[ngClass]
```

Applies classes dynamically.

***

## ❌ Using `ngClass` for inline styles

If you need to change things like:

* color
* font size
* background

without creating CSS classes, use `ngStyle` instead.

That's our next lesson.

***

# Mini Challenge

Build a page with:

Component:

```typescript
isOnline = true;
```

CSS:

```css
.online {
  color: green;
}

.offline {
  color: red;
}
```

Template requirements:

* Display the text:

```text
Server Status
```

* When `isOnline` is `true`, use the `online` class.
* When `isOnline` is `false`, use the `offline` class.

Try solving it yourself before checking the earlier examples.

***

# Quick Review

Without looking back:

1. What does `ngClass` do?
2. Is `ngClass` a structural or attribute directive?
3. What are the three common ways to use `ngClass`?
4. What is the difference between `class` and `[ngClass]`?
5. When would you choose `ngClass` over `[class]`?

***

# Lesson Summary

Today you learned:

* ✅ What `ngClass` is.
* ✅ How to add CSS classes dynamically.
* ✅ String, array, and object syntax.
* ✅ The difference between `class`, `[class]`, and `[ngClass]`.
* ✅ Common real-world uses.

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
* ✅ Lesson 4.5 — Attribute Directives
* ✅ Lesson 4.6 — `ngClass`
* ⬜ Lesson 4.7 — `ngStyle`

⭐ **Appendix (Modern Angular Notes)**

* `@if`
* `@for`
* Reading old vs. new Angular syntax
* Migration overview

***

# 🎯 Mental Model

Imagine every HTML element has a **name tag** that lists its CSS classes.

For example:

```text
Button

Name Tag:
-------------
primary
large
rounded
-------------
```

`ngClass` is the person updating that name tag.

If your application state changes, Angular checks your `ngClass` expression and asks:

* "Should I add the `active` class?"
* "Should I remove the `disabled` class?"

It doesn't rebuild the button or create a new one. It simply updates the list of classes attached to the existing element.

***

### 📌 Looking Ahead

In the next lesson, **`ngStyle`**, you'll learn the same idea but for **inline CSS styles** instead of CSS classes.

A good way to remember the difference is:

* **`ngClass`** → *Which CSS classes should this element have?*
* **`ngStyle`** → *What specific CSS property values should this element have right now?*
