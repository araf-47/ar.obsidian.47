Absolutely. We've learned **Parent → Child** communication with `@Input()`. Now we're going to reverse the direction.

# Angular Master Course

# Module 5 — Component Communication

## Lesson 5.3 — `@Output()`

### Progress

```text
Module 5 — Component Communication

✅ Lesson 5.1 — Parent and Child Components
✅ Lesson 5.2 — @Input()
🟨 Lesson 5.3 — @Output()
⬜ Lesson 5.4 — EventEmitter
```

***

# 📌 Version Note

`@Output()` is still an important Angular concept and is widely used in existing applications.

Modern Angular also provides newer signal-based APIs such as `output()`. We'll learn those later as a **Modern Angular Note**.

For now, we're learning the classic `@Output()` + `EventEmitter` pattern because it teaches the fundamental idea of **child → parent communication**.

***

# Lesson Objectives

By the end of this lesson, you should understand:

* Why a child needs to communicate with its parent.
* What `@Output()` does.
* The direction of `@Output()` communication.
* How a child exposes an event to its parent.
* How the parent listens to that event.
* The difference between `@Input()` and `@Output()`.

***

# Part 1 — We Already Know One Direction

In the previous lesson:

```text
Parent
   │
   │ data
   ▼
Child
```

We used:

```typescript
@Input()
```

For example:

```html
<app-student [name]="studentName"></app-student>
```

The parent gives the child data.

***

# Part 2 — But What If the Child Needs to Tell the Parent Something?

Imagine we have:

```text
Parent
   │
   ↓
Child
```

The parent displays a student card.

The child has a button:

```text
┌──────────────────────┐
│ Student: Rahim       │
│                      │
│ [ Delete Student ]   │
└──────────────────────┘
```

The user clicks:

**Delete Student**

Who handles the actual deletion?

Usually, the parent.

Why?

Because the parent owns the list of students.

So the child needs to tell the parent:

> "The user clicked the Delete button."

That's where `@Output()` comes in.

***

# Part 3 — What Is `@Output()`?

### Definition

> `@Output()` allows a child component to communicate an event to its parent component.

The direction is:

```text
Child
  │
  │ event
  ▼
Parent
```

So remember:

```text
@Input()
Parent → Child

@Output()
Child → Parent
```

This distinction is extremely important.

***

# Part 4 — `@Output()` Works With Events

Suppose our child has:

```html
<button>Delete</button>
```

The child can expose an event such as:

```text
studentDeleted
```

The parent can listen for that event.

Conceptually:

```text
Child
  │
  │ studentDeleted
  ▼
Parent
```

The child isn't directly modifying the parent's data.

It's saying:

> "Something happened."

The parent decides what to do about it.

***

# Part 5 — The Basic Structure

A child component typically declares an output:

```typescript
@Output() somethingHappened = new EventEmitter();
```

We'll study `EventEmitter` in detail in **Lesson 5.4**.

For now, focus on the concept:

```text
@Output()
     +
EventEmitter
     ↓
Child creates an event
     ↓
Parent listens
```

***

# Part 6 — Simple Example

Let's create a child component called:

```text
StudentCardComponent
```

The child template:

```html
<button (click)="deleteStudent()">
  Delete
</button>
```

The child component:

```typescript
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-student-card',
  templateUrl: './student-card.html'
})
export class StudentCardComponent {

  @Output() delete = new EventEmitter();

  deleteStudent() {
    this.delete.emit();
  }

}
```

Don't worry about every detail yet.

The important parts are:

```typescript
@Output() delete
```

and:

```typescript
this.delete.emit();
```

The child is saying:

> "I have an event called `delete`, and I'm emitting it."

***

# Part 7 — Parent Listens

Now the parent contains:

```html
<app-student-card
  (delete)="deleteStudent()">
</app-student-card>
```

The important syntax is:

```text
(delete)
```

This is **event binding**, which you already learned in Module 3.

So:

```html
(delete)="deleteStudent()"
```

means:

> "When the child's `delete` event happens, call my `deleteStudent()` method."

***

# Part 8 — Complete Communication Flow

Now we have:

```text
                 PARENT
                   │
                   │
              @Input()
                   │
                   ▼
                 CHILD
                   │
                   │
              @Output()
                   │
                   ▼
                 PARENT
```

In our example:

```text
Parent
  │
  │ student
  ▼
StudentCard
  │
  │ delete event
  ▼
Parent
```

This is the basic pattern you'll use constantly in Angular.

***

# Part 9 — A More Realistic Example

Let's use our LandLord application again.

Imagine:

```text
TenantListComponent
       │
       ├── TenantCardComponent
       ├── TenantCardComponent
       └── TenantCardComponent
```

The parent owns:

```typescript
tenants = [
  { id: 1, name: 'Rahim' },
  { id: 2, name: 'Karim' },
  { id: 3, name: 'Hasan' }
];
```

The child displays one tenant.

The child has:

```html
<button (click)="deleteClicked()">
  Delete
</button>
```

When the user clicks Delete:

```text
TenantCardComponent
       │
       │ "Delete was clicked"
       ▼
TenantListComponent
```

The parent can then remove the tenant from its array.

***

# Part 10 — Why Doesn't the Child Just Delete the Tenant?

This is a very important architectural question.

You might think:

> "Why doesn't `TenantCardComponent` just modify the parent's `tenants` array?"

Because the child shouldn't need to know how the parent manages its data.

The child should communicate:

> "The user requested deletion."

The parent decides:

> "Okay, I'll remove that tenant."

This creates a clean separation of responsibilities.

***

# Part 11 — `@Input()` vs `@Output()`

This is one of the most important tables in this module.

| Feature     | Direction      | Purpose     |
| ----------- | -------------- | ----------- |
| `@Input()`  | Parent → Child | Pass data   |
| `@Output()` | Child → Parent | Send events |

Think:

```text
INPUT

Parent
  ↓
Child
```

and:

```text
OUTPUT

Child
  ↓
Parent
```

***

# Part 12 — Another Example: Counter

Parent:

```typescript
count = 0;
```

Child has a button:

```text
[ Increase ]
```

The child doesn't directly modify:

```typescript
parent.count
```

Instead:

```text
Child
  │
  │ increase event
  ▼
Parent
  │
  ↓
count++
```

The parent remains responsible for its own state.

***

# Part 13 — The Event Name

Suppose the child declares:

```typescript
@Output() selected = new EventEmitter();
```

The parent listens:

```html
<app-student-card
  (selected)="studentSelected()">
</app-student-card>
```

Notice:

```text
@Output() selected
```

matches:

```text
(selected)
```

The names need to correspond.

***

# Part 14 — Don't Confuse `@Output()` With `@Input()`

This is a common exam/interview question.

### `@Input()`

```typescript
@Input() student!: Student;
```

means:

> "The parent can give this component a student."

### `@Output()`

```typescript
@Output() selected = new EventEmitter();
```

means:

> "This component can notify the parent that something happened."

***

# Part 15 — What `@Output()` Does NOT Do

`@Output()` does **not**:

* Send data to the database.
* Make a variable global.
* Communicate with the backend.
* Automatically change the parent.
* Replace services.

It creates a **component event communication channel**.

That's it.

***

# Part 16 — `@Output()` + Event Binding

You already learned event binding in Module 3:

```html
<button (click)="save()">
```

The same idea applies to component outputs.

Native HTML event:

```html
<button (click)="save()">
```

Angular component event:

```html
<app-student (selected)="studentSelected()">
```

The syntax is the same because Angular treats the component's output as an event that the parent can listen to.

***

# Part 17 — Data Can Also Be Sent

An output doesn't have to communicate just:

```text
Something happened.
```

It can also communicate:

```text
Something happened + here is some data.
```

For example:

```text
Child
  │
  │ selected student
  ▼
Parent
```

The child could tell the parent:

```text
"The user selected student #5."
```

We'll see exactly how that works using `EventEmitter` in the next lesson.

***

# 💼 Real-World Developer Notes

A useful rule is:

> **The child reports events; the parent decides what those events mean.**

For example:

```text
TenantCardComponent
        │
        │ deleteRequested
        ▼
TenantListComponent
        │
        ├── remove tenant from UI
        ├── maybe call a service
        └── maybe eventually call an API
```

This becomes particularly important when we reach:

* Services
* HTTP
* Forms

You'll see that component communication is one piece of a much larger architecture.

***

# Mini Challenge

Imagine:

```text
ParentComponent
      │
      ↓
CounterComponent
```

The child contains:

```html
<button>Increase</button>
```

Your goal:

1. Create an output called `increase`.
2. When the child button is clicked, emit the event.
3. Let the parent listen to it.
4. The parent should increment its own `count`.

The communication should look like:

```text
Child button
     ↓
increase event
     ↓
Parent
     ↓
count++
```

Don't worry about passing a value yet. We'll cover that properly in Lesson 5.4.

***

# Quick Review

Make sure you can answer:

1. What does `@Output()` do?
2. What direction does `@Output()` communication flow?
3. What is the difference between `@Input()` and `@Output()`?
4. Who should generally own the application data—the parent or child?
5. What does the parent use to listen to an output?
6. Does `@Output()` communicate directly with a backend?

***

# Lesson Summary

Today you learned:

* ✅ `@Output()` creates a child → parent communication channel.
* ✅ The child emits an event.
* ✅ The parent listens for that event.
* ✅ Event binding is used to listen to component outputs.
* ✅ The parent generally remains responsible for its own state.
* ✅ `@Input()` and `@Output()` work together to establish two-way communication between components.

***

# 🎯 Mental Model

Keep this picture in your head:

```text
             PARENT
             /    \
            /      \
       @Input()   @Output()
          ↓          ↑
          ↓          │
         CHILD ──────┘
```

Or even simpler:

> **`@Input()` = "Give me something."**

> **`@Output()` = "Something happened."**

That's the foundation of component communication.

***

# Roadmap Progress

```text
Module 5 — Component Communication

✅ Lesson 5.1 — Parent and Child Components
✅ Lesson 5.2 — @Input()
✅ Lesson 5.3 — @Output()
⬜ Lesson 5.4 — EventEmitter
```

### Next: Lesson 5.4 — `EventEmitter`

This is where we'll slow down and understand the part we deliberately didn't dive deeply into today:

```typescript
new EventEmitter()
```

and:

```typescript
this.eventName.emit(...)
```

We'll learn how to **send actual data from the child to the parent**, not just a notification that something happened.
