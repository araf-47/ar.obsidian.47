Absolutely. This is the final lesson of **Module 5**, and it connects everything we've learned so far.

# Angular Master Course

# Module 5 — Component Communication

## Lesson 5.4 — `EventEmitter`

### Progress

```text
Module 5 — Component Communication

✅ Lesson 5.1 — Parent and Child Components
✅ Lesson 5.2 — @Input()
✅ Lesson 5.3 — @Output()
🟨 Lesson 5.4 — EventEmitter
```

***

# Lesson Objectives

By the end of this lesson, you should understand:

* What `EventEmitter` is.
* Why `@Output()` commonly uses `EventEmitter`.
* How `.emit()` works.
* How to send data from a child to a parent.
* How the parent receives that data.
* How `@Input()` and `@Output()` work together.

***

# Part 1 — Where We Left Off

In the previous lesson, we had:

```text
Child
  │
  │ event
  ▼
Parent
```

For example:

```typescript
@Output() delete = new EventEmitter();
```

and:

```typescript
this.delete.emit();
```

The parent could listen:

```html
<app-student-card
  (delete)="deleteStudent()">
</app-student-card>
```

That allows the child to say:

> "Something happened."

But what if the child needs to say:

> "Something happened, and here's some information about it."

That's where `EventEmitter` becomes particularly useful.

***

# Part 2 — What Is `EventEmitter`?

`EventEmitter` is an Angular class used with component outputs to **emit events and optionally carry a value with the event**.

The basic pattern is:

```typescript
@Output() somethingHappened = new EventEmitter();
```

Then:

```typescript
this.somethingHappened.emit();
```

Think of it as a little communication channel.

```text
Child
  │
  │ EventEmitter
  │
  ▼
Parent
```

***

# Part 3 — The Three Important Pieces

There are three things you need to recognize:

### 1. `@Output()`

```typescript
@Output()
```

This tells Angular:

> "This property is an output that a parent can listen to."

### 2. `EventEmitter`

```typescript
new EventEmitter()
```

This gives us something capable of emitting events.

### 3. `.emit()`

```typescript
this.someEvent.emit();
```

This actually sends the event.

So:

```text
@Output()
    +
EventEmitter
    +
emit()
    ↓
Child sends event
```

***

# Part 4 — Simple Example

Let's create:

```text
CounterComponent
```

The child has:

```typescript
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-counter',
  templateUrl: './counter.html'
})
export class CounterComponent {

  @Output() increase = new EventEmitter();

  increaseCounter() {
    this.increase.emit();
  }

}
```

The child template:

```html
<button (click)="increaseCounter()">
  Increase
</button>
```

The child now has an event called:

```text
increase
```

When the button is clicked:

```typescript
this.increase.emit();
```

fires that event.

***

# Part 5 — Parent Listens

The parent template:

```html
<app-counter
  (increase)="increaseCount()">
</app-counter>
```

The parent TypeScript:

```typescript
export class AppComponent {

  count = 0;

  increaseCount() {
    this.count++;
  }

}
```

Now the complete flow is:

```text
User clicks button
       ↓
Child increaseCounter()
       ↓
this.increase.emit()
       ↓
Parent hears (increase)
       ↓
increaseCount()
       ↓
count++
```

That's component communication.

***

# Part 6 — Sending Data

Now let's make it more interesting.

Suppose the child wants to tell the parent:

> "The user selected this student."

The child could have:

```typescript
@Output() studentSelected = new EventEmitter();
```

Then:

```typescript
selectStudent() {
  this.studentSelected.emit('Rahim');
}
```

The important part is:

```typescript
.emit('Rahim')
```

We're passing data along with the event.

***

# Part 7 — The Parent Receives the Data

Parent template:

```html
<app-student
  (studentSelected)="onStudentSelected($event)">
</app-student>
```

Notice:

```text
$event
```

This is extremely important.

`$event` represents the value emitted by the child.

So if the child does:

```typescript
this.studentSelected.emit('Rahim');
```

then:

```text
$event
```

contains:

```text
'Rahim'
```

The parent receives it:

```typescript
onStudentSelected(name: string) {
  console.log(name);
}
```

Result:

```text
Rahim
```

***

# Part 8 — Follow the Data

This is probably the most important example in this lesson.

### Child:

```typescript
this.studentSelected.emit('Rahim');
```

↓

### Parent template:

```html
(studentSelected)="onStudentSelected($event)"
```

↓

### Parent method:

```typescript
onStudentSelected(name: string) {
  console.log(name);
}
```

So:

```text
"Rahim"
   ↓
emit()
   ↓
$event
   ↓
name
```

That's how data travels from child → parent.

***

# Part 9 — Sending an Object

Usually, you'll want to send more than a string.

Suppose:

```typescript
student = {
  id: 5,
  name: 'Rahim',
  department: 'CSE'
};
```

The child can emit the entire object:

```typescript
this.studentSelected.emit(this.student);
```

The parent:

```html
<app-student
  (studentSelected)="onStudentSelected($event)">
</app-student>
```

And:

```typescript
onStudentSelected(student: Student) {
  console.log(student.name);
}
```

Now `$event` contains the entire student object.

***

# Part 10 — Typed `EventEmitter`

This is where your TypeScript knowledge becomes useful.

Instead of:

```typescript
@Output() studentSelected = new EventEmitter();
```

we can specify what kind of data the event carries:

```typescript
@Output() studentSelected = new EventEmitter<Student>();
```

Now Angular/TypeScript knows:

> This event should emit a `Student`.

Then:

```typescript
this.studentSelected.emit(this.student);
```

is appropriate.

But:

```typescript
this.studentSelected.emit(123);
```

would be a type mismatch if `123` isn't a `Student`.

***

# Part 11 — Example With a Tenant

Let's make this relevant to your LandLord application.

Suppose:

```typescript
interface Tenant {
  id: number;
  name: string;
  rent: number;
}
```

The child:

```typescript
@Output() deleteTenant = new EventEmitter<Tenant>();
```

When the user clicks Delete:

```typescript
deleteClicked() {
  this.deleteTenant.emit(this.tenant);
}
```

The parent:

```html
<app-tenant-card
  [tenant]="tenant"
  (deleteTenant)="removeTenant($event)">
</app-tenant-card>
```

The parent receives:

```typescript
removeTenant(tenant: Tenant) {
  console.log('Delete:', tenant.name);
}
```

So:

```text
TenantCardComponent
        │
        │ Tenant object
        ▼
deleteTenant.emit(tenant)
        │
        ▼
       $event
        │
        ▼
removeTenant(tenant)
```

This is a very realistic Angular pattern.

***

# Part 12 — Now Combine `@Input()` and `@Output()`

This is the big picture.

Suppose:

```text
TenantListComponent
        │
        ↓
TenantCardComponent
```

The parent sends a tenant:

```html
<app-tenant-card
  [tenant]="tenant"
  (deleteTenant)="removeTenant($event)">
</app-tenant-card>
```

So:

### Parent → Child

```text
[tenant]
```

uses:

```text
@Input()
```

### Child → Parent

```text
(deleteTenant)
```

uses:

```text
@Output()
+
EventEmitter
```

Together:

```text
              PARENT
             /      \
            /        \
      @Input()     @Output()
          ↓            ↑
          ↓            │
         CHILD ────────┘
```

***

# Part 13 — A Very Important Distinction

Don't think of `EventEmitter` as a general-purpose application communication system.

It's primarily being used here for:

> **Child → Parent component communication.**

Later, you'll learn about **services**, which solve a different problem.

For example:

```text
Component A
      │
      ↓
   Service
      ↑
      │
Component B
```

That's useful when components aren't directly parent/child.

We'll learn that in **Module 7**.

***

# Part 14 — What Happens When `.emit()` Is Called?

Suppose:

```typescript
this.deleteTenant.emit(tenant);
```

Conceptually:

```text
Child
  │
  │ emit(tenant)
  ▼
Angular event system
  │
  ▼
Parent listener
  │
  ▼
removeTenant($event)
```

The parent doesn't directly call the child's method.

The child doesn't directly call the parent's method.

They communicate through the component's output.

That's an important separation.

***

# Part 15 — `@Output()` vs `EventEmitter`

This distinction is worth understanding.

You might ask:

> "What's the difference between `@Output()` and `EventEmitter`?"

They're related but not the same thing.

### `@Output()`

Tells Angular:

> "This property is an output that a parent can subscribe to through template event binding."

### `EventEmitter`

Provides the mechanism for emitting the event.

So:

```typescript
@Output() selected = new EventEmitter<Student>();
```

has two pieces:

```text
@Output()
    ↓
Angular component output

EventEmitter<Student>
    ↓
Object that emits the event/value
```

***

# Part 16 — Don't Confuse `emit()` With a Function Call

This:

```typescript
this.studentSelected.emit(student);
```

is not the same as:

```typescript
this.parent.onStudentSelected(student);
```

The child doesn't know the parent's method.

That's the point.

The child only knows:

> "I have an output called `studentSelected`."

The parent decides what to do when it receives it.

***

# Part 17 — Real-World Example

Imagine your rental marketplace.

You have:

```text
RentalListComponent
       │
       ├── RentalCardComponent
       ├── RentalCardComponent
       └── RentalCardComponent
```

Each card displays:

```text
Apartment
৳15,000/month

[ View Details ]
```

The child can emit:

```typescript
@Output() viewDetails = new EventEmitter<Apartment>();
```

When clicked:

```typescript
this.viewDetails.emit(this.apartment);
```

The parent:

```html
<app-rental-card
  [apartment]="apartment"
  (viewDetails)="openDetails($event)">
</app-rental-card>
```

Then:

```typescript
openDetails(apartment: Apartment) {
  // do something with the selected apartment
}
```

Later, when we learn routing, that method might navigate to:

```text
/apartments/42
```

Notice how the concepts we've learned will eventually connect.

***

# Part 18 — Common Beginner Mistakes

### ❌ Forgetting `.emit()`

Declaring:

```typescript
@Output() selected = new EventEmitter();
```

doesn't automatically send anything.

You have to emit:

```typescript
this.selected.emit();
```

***

### ❌ Using the wrong `$event`

If the child emits:

```typescript
this.selected.emit(student);
```

then:

```text
$event
```

is the `student`.

Not the event name.

***

### ❌ Forgetting to listen in the parent

Child:

```typescript
@Output() selected = new EventEmitter();
```

isn't enough.

The parent needs:

```html
<app-student
  (selected)="handleSelection($event)">
</app-student>
```

***

### ❌ Directly modifying parent state

Avoid thinking:

```text
Child → directly modify Parent
```

Prefer:

```text
Child → emit event → Parent decides what to do
```

***

# 💼 Real-World Developer Notes

This pattern gives components a clean contract.

For example, a reusable `TenantCardComponent` might say:

> **Input:** Give me a tenant.

```typescript
@Input() tenant!: Tenant;
```

> **Output:** I'll tell you when the user requests deletion.

```typescript
@Output() deleteTenant = new EventEmitter<Tenant>();
```

The parent doesn't need to know how the card is implemented.

It only needs to understand its contract:

```text
Input:
Tenant

Output:
deleteTenant
```

That's a powerful component-design principle.

***

# 🧪 Mini Project

Let's put the entire module together.

Build:

## **Student List**

The component structure:

```text
AppComponent
      │
      ↓
StudentListComponent
      │
      ├── StudentCardComponent
      ├── StudentCardComponent
      └── StudentCardComponent
```

### Parent

The parent owns:

```typescript
students = [
  { id: 1, name: 'Rahim' },
  { id: 2, name: 'Karim' },
  { id: 3, name: 'Hasan' }
];
```

### Child

Each `StudentCardComponent` should receive a student using:

```typescript
@Input()
```

and display:

```text
Name: Rahim
[Select]
```

When Select is clicked, the child should emit:

```typescript
@Output()
```

with the selected student.

### Parent

The parent should receive the student through:

```text
$event
```

and display something like:

```text
Selected student: Rahim
```

***

# Your Expected Communication

Your final architecture should conceptually look like:

```text
                 StudentListComponent
                         │
                         │ @Input()
                         ↓
                 StudentCardComponent
                         │
                         │ @Output()
                         │ EventEmitter<Student>
                         ↓
                 StudentListComponent
                         │
                         ↓
                 Selected student
```

This single exercise combines:

* Components
* Parent/child relationships
* `@Input()`
* Property binding
* `@Output()`
* `EventEmitter`
* Event binding
* `$event`

That's why this is a good stopping point for Module 5.

***

# Quick Review

Make sure you can explain these:

### 1. What is `EventEmitter`?

### 2. What does `.emit()` do?

### 3. What is `$event`?

### 4. What is the difference between:

```typescript
@Input()
```

and:

```typescript
@Output()
```

### 5. What is the role of:

```typescript
EventEmitter<Student>
```

### 6. What is the complete flow when a child sends a student to its parent?

You should be able to explain:

```text
emit(student)
      ↓
$event
      ↓
parent method
```

***

# 🎯 Final Mental Model for Module 5

You now have the complete basic component communication model:

```text
                 PARENT
                /      \
               /        \
        @Input()      @Output()
           ↓              ↑
           ↓              │
         CHILD ───────────┘
                    EventEmitter
```

### `@Input()`

**Parent → Child**

> "Here is some data."

### `@Output()`

**Child → Parent**

> "Something happened."

### `EventEmitter`

The child uses it to **emit the event/value**.

### `$event`

The parent uses it to **receive the emitted value**.

***

# ✅ Module 5 Complete

```text
Module 5 — Component Communication

✅ Lesson 5.1 — Parent and Child Components
✅ Lesson 5.2 — @Input()
✅ Lesson 5.3 — @Output()
✅ Lesson 5.4 — EventEmitter
```

You've now completed the entire original **Module 5**.

And importantly, you now have a foundation for understanding why Angular needs **services** later.

**Next in the roadmap:**

# Module 6 — Forms

```text
Lesson 6.1 — Forms Overview
Lesson 6.2 — Template-driven Forms
Lesson 6.3 — Form Validation
Lesson 6.4 — Reactive Forms
Lesson 6.5 — FormBuilder
```

Before we move there, make sure you complete the **Student List mini-project** above. It will make the next modules considerably easier.
