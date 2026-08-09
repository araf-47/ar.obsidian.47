Great. Now we move from **understanding the component relationship** to actually making components communicate.

# Angular Master Course

# Module 5 — Component Communication

## Lesson 5.2 — `@Input()`

### Progress

```text
Module 5 — Component Communication

✅ Lesson 5.1 — Parent and Child Components
🟨 Lesson 5.2 — @Input()
⬜ Lesson 5.3 — @Output()
⬜ Lesson 5.4 — EventEmitter
```

***

# 📌 Version Note

In modern Angular, `@Input()` is still fully relevant.

Angular also provides a newer **signal-based input API**, `input()`, but we're going to learn `@Input()` first because:

1. It is fundamental to understanding component communication.
2. You'll encounter it extensively in existing Angular applications.
3. The underlying parent → child communication concept remains the same.

We'll cover the modern `input()` API separately later as a **Modern Angular Note**, rather than mixing two concepts together right now.

***

# Lesson Objectives

By the end of this lesson, you should understand:

* What `@Input()` does.
* Why a child component needs inputs.
* How a parent passes data to a child.
* How to bind a parent's property to a child's input.
* The difference between ordinary properties and `@Input()` properties.

***

# Part 1 — The Problem

Let's say we have:

```text
AppComponent
    ↓
StudentComponent
```

The parent knows the student's name:

```typescript
studentName = 'Rahim';
```

But the child needs to display it.

How does the parent give the child that information?

That's exactly what `@Input()` is for.

> **`@Input()` allows a parent component to pass data to a child component.**

The direction is:

```text
Parent
   │
   │ data
   ↓
Child
```

Remember this direction.

**`@Input()` = Parent → Child**

***

# Part 2 — Creating the Child Component

Let's create a simple child component.

For example:

```bash
ng generate component student
```

You'll have a component roughly like:

```text
student/
├── student.ts
├── student.html
└── student.css
```

Depending on your Angular CLI version and configuration, filenames may differ slightly. That's okay—the important thing is that we have a `StudentComponent`.

***

# Part 3 — The Child Has an Input

In the child component:

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-student',
  templateUrl: './student.html'
})
export class StudentComponent {

  @Input() name = '';

}
```

The important part is:

```typescript
@Input() name = '';
```

This tells Angular:

> "The parent is allowed to provide a value for this property."

Without `@Input()`, `name` is simply an ordinary property of the child.

With `@Input()`, it becomes something the parent can provide.

***

# Part 4 — Displaying the Input

The child template can use it normally:

```html
<h2>{{ name }}</h2>
```

At this point, the child knows **how to display** the name.

But where does the actual name come from?

The parent.

***

# Part 5 — Parent Component

Suppose the parent has:

```typescript
export class AppComponent {

  studentName = 'Rahim';

}
```

And the parent template contains:

```html
<app-student></app-student>
```

The child will be created, but it doesn't know about `studentName` yet.

We need to connect them.

***

# Part 6 — Passing the Data

We use **property binding**.

```html
<app-student [name]="studentName"></app-student>
```

Let's break this down.

```text
[name]
```

means:

> Bind to the child's `name` property.

And:

```text
"studentName"
```

means:

> Get the value from the parent component.

So:

```html
[name]="studentName"
```

means:

> "Take the parent's `studentName` value and give it to the child's `name` input."

***

# Part 7 — The Complete Example

### Parent — TypeScript

```typescript
export class AppComponent {

  studentName = 'Rahim';

}
```

### Parent — HTML

```html
<h1>Student Management</h1>

<app-student [name]="studentName"></app-student>
```

### Child — TypeScript

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-student',
  templateUrl: './student.html'
})
export class StudentComponent {

  @Input() name = '';

}
```

### Child — HTML

```html
<h2>{{ name }}</h2>
```

The result is:

```text
Student Management

Rahim
```

***

# Part 8 — Follow the Data

This is extremely important.

Don't just memorize the syntax.

Follow the data.

The parent has:

```text
studentName = "Rahim"
```

Then:

```html
<app-student [name]="studentName">
```

passes it to:

```text
StudentComponent
       ↓
@Input() name
```

Then the child displays:

```html
{{ name }}
```

So the complete flow is:

```text
Parent property
     │
     │ [name]="studentName"
     ↓
Child @Input()
     │
     ↓
Child template
     │
     ↓
{{ name }}
```

That's `@Input()`.

***

# Part 9 — Don't Confuse These Two

This is a very common beginner mistake.

### Parent:

```html
<app-student [name]="studentName">
```

This is **property binding**.

The brackets:

```text
[ ]
```

tell Angular to evaluate:

```text
studentName
```

as a component property.

***

Compare that with:

```html
<app-student name="studentName">
```

This passes the literal text:

```text
studentName
```

rather than the value stored in the parent's `studentName` property.

So:

```html
[name]="studentName"
```

means:

> Give me the value.

Whereas:

```html
name="studentName"
```

means:

> Give me this text.

***

# Part 10 — Passing Numbers

Inputs aren't limited to strings.

Parent:

```typescript
rent = 15000;
```

Child:

```typescript
@Input() rent = 0;
```

Parent template:

```html
<app-tenant [rent]="rent"></app-tenant>
```

Child:

```html
<p>Rent: {{ rent }}</p>
```

The child receives:

```text
15000
```

as a number.

***

# Part 11 — Passing Objects

This is where `@Input()` becomes really useful.

Suppose the parent has:

```typescript
tenant = {
  name: 'Rahim',
  rent: 15000,
  paid: true
};
```

Child:

```typescript
@Input() tenant: any;
```

Parent:

```html
<app-tenant-card [tenant]="tenant"></app-tenant-card>
```

Child template:

```html
<h2>{{ tenant.name }}</h2>

<p>Rent: {{ tenant.rent }}</p>

<p>Paid: {{ tenant.paid }}</p>
```

Now one input can carry an entire object.

***

# Part 12 — Passing Multiple Inputs

A child can have multiple inputs.

### Child:

```typescript
@Input() name = '';
@Input() rent = 0;
@Input() paid = false;
```

### Parent:

```html
<app-tenant
  [name]="tenant.name"
  [rent]="tenant.rent"
  [paid]="tenant.paid">
</app-tenant>
```

So:

```text
Parent
 │
 ├── name ─────→ Child
 ├── rent ─────→ Child
 └── paid ─────→ Child
```

***

# Part 13 — A Better Design

Instead of passing three separate properties:

```html
<app-tenant
  [name]="tenant.name"
  [rent]="tenant.rent"
  [paid]="tenant.paid">
</app-tenant>
```

you might pass the entire object:

```html
<app-tenant [tenant]="tenant"></app-tenant>
```

Then:

```typescript
@Input() tenant!: Tenant;
```

This becomes especially useful when your object has many related properties.

We'll learn proper TypeScript typing for this later.

***

# Part 14 — Inputs Are Not Independent Data

Here's an important mental model.

Suppose:

```typescript
studentName = 'Rahim';
```

The child receives it.

Later the parent changes:

```typescript
studentName = 'Karim';
```

The child can receive the updated value.

The relationship is:

```text
Parent owns the data
        ↓
Child receives the data
```

The child isn't the owner of that information.

This distinction becomes **very important** as your applications become larger.

***

# Part 15 — `@Input()` Does Not Mean "Global Variable"

A beginner might think:

> "`@Input()` lets any component access this variable."

No.

It specifically creates a communication path between:

```text
Parent → Child
```

It doesn't make the property globally available.

***

# Part 16 — Real-World Example

Let's use your LandLord application idea.

Imagine:

```text
TenantListComponent
        │
        ├── TenantCardComponent
        ├── TenantCardComponent
        └── TenantCardComponent
```

The parent has:

```typescript
tenants = [
  { id: 1, name: 'Rahim', rent: 15000 },
  { id: 2, name: 'Karim', rent: 18000 },
  { id: 3, name: 'Hasan', rent: 12000 }
];
```

The parent loops:

```html
@for (tenant of tenants; track tenant.id) {

  <app-tenant-card
    [tenant]="tenant">
  </app-tenant-card>

}
```

The child:

```typescript
@Input() tenant!: Tenant;
```

Now each child receives **one tenant**.

So the communication looks like:

```text
TenantListComponent

tenant #1 ─────→ TenantCardComponent
tenant #2 ─────→ TenantCardComponent
tenant #3 ─────→ TenantCardComponent
```

This is a very common Angular pattern.

***

# Part 17 — `@Input()` and `@for` Together

Notice how the concepts you've already learned combine:

```html
@for (tenant of tenants; track tenant.id) {

  <app-tenant-card
    [tenant]="tenant">
  </app-tenant-card>

}
```

You already understand:

* `@for`
* `track`
* property binding

Now you're adding:

* `@Input()`

This is exactly how Angular concepts start coming together.

***

# Common Beginner Mistakes

### ❌ Forgetting `@Input`

Child:

```typescript
name = '';
```

Parent:

```html
<app-student [name]="studentName"></app-student>
```

This won't establish an input relationship.

You need:

```typescript
@Input() name = '';
```

***

### ❌ Putting `@Input()` on the parent

`@Input()` belongs to the **child property that receives the data**.

***

### ❌ Reversing the direction

Remember:

```text
@Input()

Parent
  ↓
Child
```

The child doesn't use `@Input()` to send data upward.

That's what we'll learn with `@Output()`.

***

# 💼 Real-World Developer Notes

One of the most important architectural ideas here is:

> **The component that owns the data should generally be responsible for managing that data.**

A child should usually receive what it needs through inputs rather than reaching into its parent's internal state.

For example:

```text
TenantListComponent
        │
        │ tenant
        ↓
TenantCardComponent
```

The card doesn't need to know where the tenant came from.

It only needs:

```typescript
@Input() tenant
```

That makes the card more reusable.

You could potentially use the same `TenantCardComponent` somewhere else later.

***

# Mini Challenge

Build this yourself.

### Parent

```typescript
student = {
  name: 'Rahim',
  age: 22,
  department: 'CSE'
};
```

### Child

Create:

```text
StudentCardComponent
```

The child should receive the entire student object using `@Input()`.

Then display:

```text
Name: Rahim
Age: 22
Department: CSE
```

### Your communication should look conceptually like:

```text
AppComponent
     │
     │ student
     ↓
StudentCardComponent
     │
     ↓
Display student information
```

Try implementing it yourself before looking at your notes.

***

# Quick Review

Make sure you can answer these without looking back:

1. What does `@Input()` do?
2. What direction does `@Input()` communication flow?
3. Where is `@Input()` declared?
4. What does `[name]="studentName"` mean?
5. What's the difference between `[name]="studentName"` and `name="studentName"`?
6. Can an input contain an object?
7. Can a component have multiple inputs?

If you can answer these comfortably, you understand the core of `@Input()`.

***

# Lesson Summary

Today you learned:

* ✅ `@Input()` creates a parent → child communication channel.
* ✅ The child declares the input.
* ✅ The parent provides the value using property binding.
* ✅ Inputs can contain strings, numbers, booleans, objects, arrays, etc.
* ✅ A child can have multiple inputs.
* ✅ `@Input()` works naturally with `@for`.
* ✅ The parent generally remains the owner of the data.

***

# 🎯 Mental Model

Remember this single picture:

```text
        PARENT
           │
           │
      [property]
           │
           ▼
        @Input()
           │
           ▼
         CHILD
```

Or even simpler:

> **`@Input()` = "Parent, give me some data."**

That is the fundamental idea.

***

# Roadmap Progress

```text
Module 5 — Component Communication

✅ Lesson 5.1 — Parent and Child Components
✅ Lesson 5.2 — @Input()
⬜ Lesson 5.3 — @Output()
⬜ Lesson 5.4 — EventEmitter
```

## Next: Lesson 5.3 — `@Output()`

We've learned how the **parent sends data down**.

Next we'll reverse the direction:

```text
Child
  │
  │ event
  ▼
Parent
```

That's where `@Output()` comes in.
