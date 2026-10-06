# Lesson 2.5 — Component Lifecycle, `ngOnInit`, `ngOnDestroy`

***

## 1. Theory

### What is a component lifecycle?

An Angular component is **created, used, and eventually destroyed**.

For example:

```text
Component created
      ↓
Angular initializes it
      ↓
Component is displayed and used
      ↓
Component is removed
      ↓
Component destroyed
```

This sequence is called the **component lifecycle**.

Angular gives us lifecycle hooks so we can run code at important points in that lifecycle.

For this lesson, we only need two:

* `ngOnInit()` → runs when the component has been initialized.
* `ngOnDestroy()` → runs just before the component is destroyed.

Think of them as:

```text
ngOnInit()    → "The component is ready. Do setup work."
ngOnDestroy() → "The component is going away. Clean things up."
```

***

## 2. How it works internally

Suppose Angular creates this component:

```text
Angular
   │
   ├── creates component object
   │
   ├── sets up the component
   │
   ├── calls ngOnInit()
   │
   └── displays/uses the component
```

Later, if Angular removes the component:

```text
Angular
   │
   ├── component is no longer needed
   │
   ├── calls ngOnDestroy()
   │
   └── destroys component
```

You don't normally call these methods yourself.

Angular calls them at the appropriate lifecycle point.

### Important distinction

`ngOnInit()` is **not the same thing as the component constructor**.

The constructor creates the TypeScript object.

`ngOnInit()` is Angular's lifecycle hook that runs after Angular has initialized the component.

For now, the useful mental model is:

```text
constructor → object is being created

ngOnInit() → Angular has initialized the component
```

***

## 3. Syntax

### `ngOnInit()`

Import `OnInit`:

```typescript
import { Component, OnInit } from '@angular/core';
```

Then implement it:

```typescript
@Component({
  selector: 'app-example',
  template: `<p>Hello</p>`
})
export class ExampleComponent implements OnInit {

  ngOnInit(): void {
    console.log('Component initialized');
  }
}
```

The important pieces are:

```typescript
implements OnInit
```

and:

```typescript
ngOnInit(): void {
}
```

`OnInit` is an Angular interface that tells TypeScript that this class is implementing the initialization lifecycle hook.

***

### `ngOnDestroy()`

Import `OnDestroy`:

```typescript
import { Component, OnDestroy } from '@angular/core';
```

Then:

```typescript
export class ExampleComponent implements OnDestroy {

  ngOnDestroy(): void {
    console.log('Component destroyed');
  }
}
```

You can use both together:

```typescript
import { Component, OnInit, OnDestroy } from '@angular/core';

@Component({
  selector: 'app-example',
  template: `<p>Hello</p>`
})
export class ExampleComponent implements OnInit, OnDestroy {

  ngOnInit(): void {
    console.log('Component initialized');
  }

  ngOnDestroy(): void {
    console.log('Component destroyed');
  }
}
```

***

## 4. Examples

### Example 1 — `ngOnInit()`

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user',
  template: `
    <h2>{{ message }}</h2>
  `
})
export class UserComponent implements OnInit {

  message = '';

  ngOnInit(): void {
    this.message = 'Welcome!';
  }
}
```

When Angular initializes the component:

```text
ngOnInit()
   ↓
message becomes "Welcome!"
   ↓
template displays "Welcome!"
```

The main purpose is to perform **initialization work**.

For example:

```typescript
ngOnInit(): void {
  // initialize component state
}
```

Later, you will also see `ngOnInit()` used for things such as starting data-related work.

***

### Example 2 — `ngOnDestroy()`

```typescript
import { Component, OnDestroy } from '@angular/core';

@Component({
  selector: 'app-message',
  template: `
    <p>Message component</p>
  `
})
export class MessageComponent implements OnDestroy {

  ngOnDestroy(): void {
    console.log('Message component is being destroyed');
  }
}
```

When Angular removes this component, it calls:

```typescript
ngOnDestroy()
```

This is where cleanup work can happen.

For example, later in your Angular learning you may have resources that need cleanup:

```text
component created
      ↓
resource started
      ↓
component used
      ↓
component destroyed
      ↓
resource cleaned up
```

You don't need to learn the different cleanup techniques yet.

Just remember the purpose:

> **`ngOnDestroy()` is the place for cleanup before a component disappears.**

***

### Example 3 — Both together

```typescript
import { Component, OnInit, OnDestroy } from '@angular/core';

@Component({
  selector: 'app-counter',
  template: `
    <h2>Counter</h2>
  `
})
export class CounterComponent implements OnInit, OnDestroy {

  ngOnInit(): void {
    console.log('Counter started');
  }

  ngOnDestroy(): void {
    console.log('Counter stopped');
  }
}
```

The lifecycle looks like:

```text
Component created
       ↓
ngOnInit()
       ↓
Component is running
       ↓
Component removed
       ↓
ngOnDestroy()
       ↓
Component destroyed
```

***

## 5. Common mistakes

### Mistake 1 — Calling `ngOnInit()` yourself

Don't normally do this:

```typescript
this.ngOnInit();
```

Angular manages lifecycle hooks.

You define them, and Angular calls them.

***

### Mistake 2 — Thinking `ngOnInit()` runs every time the component changes

It doesn't.

`ngOnInit()` runs **once for each component instance**.

If the same component remains alive while its displayed data changes, Angular does not recreate it just because the data changed.

***

### Mistake 3 — Thinking `ngOnDestroy()` means the entire application is closing

No.

It means **that particular component instance is being destroyed**.

For example:

```text
App
 ├── Header
 ├── ProductList
 └── ProductDetails
```

If `ProductDetails` is removed, its `ngOnDestroy()` can run while the rest of the application continues running.

***

### Mistake 4 — Using `ngOnInit()` when no initialization work is needed

You don't have to use `ngOnInit()` in every component.

Use lifecycle hooks when you actually need them.

***

## 6. Hands-on exercise

Create a component called `LifecycleDemoComponent`.

It should:

1. Implement `OnInit`.
2. Implement `OnDestroy`.
3. Have a property:

```typescript
message = 'Not initialized';
```

4. In `ngOnInit()`, change it to:

```text
Component is ready!
```

5. In `ngOnDestroy()`, log:

```text
Component is being destroyed
```

6. Display the `message` in the template.

Your goal is to produce something roughly like:

```text
Component is ready!
```

and have the browser console show the appropriate lifecycle messages.

**Try writing it yourself before looking back at the examples above.**

***

## 7. Quick review

### Question 1

What is the main purpose of `ngOnInit()`?

> A. Destroy a component
> B. Perform initialization work
> C. Create a new Angular project
> D. Define a component's selector

**Correct answer: B**

`ngOnInit()` is called after Angular initializes the component.

***

### Question 2

How many times does `ngOnInit()` normally run for one component instance?

> A. Every second
> B. Every time the template changes
> C. Once
> D. Never

**Correct answer: C**

It runs once for that component instance.

***

### Question 3

When does `ngOnDestroy()` run?

> A. Before a component is destroyed
> B. Before Angular starts
> C. Every time a property changes
> D. When a component is created

**Correct answer: A**

It gives the component an opportunity to perform cleanup before it is destroyed.

***

### Question 4

Who normally calls `ngOnInit()`?

> A. You manually
> B. The browser
> C. Angular
> D. TypeScript

**Correct answer: C**

Angular manages the component lifecycle and calls the lifecycle hooks.

***

### Question 5

Which statement is correct?

> A. `ngOnInit()` and `ngOnDestroy()` are constructors
> B. `ngOnInit()` is for initialization and `ngOnDestroy()` is for cleanup
> C. `ngOnDestroy()` runs whenever a property changes
> D. `ngOnInit()` runs continuously

**Correct answer: B**

That's the core mental model for these two lifecycle hooks.

***

## Progress

**Completed:** Lesson 2.5 — Component lifecycle, `ngOnInit`, `ngOnDestroy`

**Next:** Module 3 — Templates & Data Binding → **Lesson 3.1 — Interpolation, Property binding**
