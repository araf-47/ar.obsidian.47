# Lesson 2.2 — Component Metadata, Selector, and Standalone `imports`

***

## 1. Theory

In the previous lesson, you learned that an Angular **component** is a TypeScript class connected to a template and styles.

But Angular needs some additional information about the component:

* What HTML tag represents this component?
* Where is its template?
* Where are its styles?
* What other Angular components/directives/pipes can it use?

This information is called **component metadata**.

Angular provides this metadata through the `@Component()` decorator.

A basic modern component looks like this:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-user',
  template: '<h1>Hello</h1>'
})
export class UserComponent {
}
```

Here:

```ts
@Component({
  ...
})
```

is the **component metadata**.

***

## 2. How It Works Internally

Think of the `@Component()` metadata as instructions that tell Angular:

> "This TypeScript class should be treated as an Angular component, and here is how this component should behave."

For example:

```ts
@Component({
  selector: 'app-user',
  template: '<h1>Hello</h1>'
})
export class UserComponent {
}
```

Angular sees:

```text
UserComponent
     ↓
@Component metadata
     ↓
Angular knows:
- this is a component
- its HTML tag is <app-user>
- its template is <h1>Hello</h1>
```

The class contains the **component's logic**.

The metadata describes **how Angular should use that class**.

***

## 3. Syntax

The most important metadata properties for this lesson are:

```ts
@Component({
  selector: 'app-user',
  template: '<h1>Hello</h1>',
  imports: []
})
export class UserComponent {
}
```

Let's look at them one by one.

### `selector`

Defines the HTML element used to place the component.

```ts
selector: 'app-user'
```

You can then use:

```html
<app-user></app-user>
```

Angular recognizes that element as your `UserComponent`.

***

### `template`

Defines the HTML for the component.

```ts
template: '<h1>Hello</h1>'
```

==For larger templates, Angular normally uses a separate HTML file==:

```ts
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html'
})
export class UserComponent {
}
```

You will work with templates more deeply in Module 3.

***

### `styleUrl`

Defines the component's stylesheet.

```ts
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrl: './user.component.css'
})
export class UserComponent {
}
```

So a component can look like:

```text
user.component.ts
user.component.html
user.component.css
```

***

## 4. Selector

The selector tells Angular:

> "When you see this HTML element, use this component."

For example:

```ts
@Component({
  selector: 'app-user',
  template: '<p>User component</p>'
})
export class UserComponent {
}
```

You can place it in another template:

```html
<app-user></app-user>
```

Angular connects the two:

```text
<app-user>
     ↓
UserComponent
     ↓
<p>User component</p>
```

### Why `app-`?

Angular CLI commonly generates selectors beginning with `app-`.

For example:

```text
app-user
app-product
app-navbar
```

It helps distinguish your custom elements from normal HTML elements.

The exact prefix is configurable, though.

***

## 5. Standalone Components and `imports`

Modern Angular uses **standalone components**.

A standalone component can directly declare which Angular components, directives, and pipes it needs through its `imports` array.

Example:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-user',
  imports: [],
  template: '<h1>Hello</h1>'
})
export class UserComponent {
}
```

The important idea is:

```text
UserComponent
     │
     └── imports
           ├── Component
           ├── Directive
           └── Pipe
```

The `imports` array answers:

> "What Angular building blocks can this component use in its template?"

***

## 6. A Simple Example

Suppose we have another component:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-header',
  template: '<h1>My Website</h1>'
})
export class HeaderComponent {
}
```

Now we want to use `HeaderComponent` inside another component.

We import the class:

```ts
import { Component } from '@angular/core';
import { HeaderComponent } from './header.component';

@Component({
  selector: 'app-root',
  imports: [HeaderComponent],
  template: `
    <app-header></app-header>
    <p>Home page</p>
  `
})
export class AppComponent {
}
```

Notice there are **two different kinds of imports** here.

### TypeScript `import`

```ts
import { HeaderComponent } from './header.component';
```

This makes the `HeaderComponent` class available in this TypeScript file.

### Angular `imports`

```ts
imports: [HeaderComponent]
```

This tells Angular:

> "This component is allowed to use `HeaderComponent` in its template."

These are related, but they are **not the same thing**.

You need both.

***

## 7. `imports` with Angular Features

The same idea applies to Angular directives and pipes.

For example, suppose a component wants to use `@if`.

You can import the required Angular functionality:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-user',
  imports: [],
  template: `
    @if (isLoggedIn) {
      <p>Welcome!</p>
    }
  `
})
export class UserComponent {
  isLoggedIn = true;
}
```

Modern Angular control-flow blocks such as `@if` are built into the template syntax, so you don't need to add `NgIf` to `imports`.

This is one reason modern Angular is cleaner than the older directive-based syntax.

***

## 8. Common Mistakes

### Mistake 1 — Confusing `selector` with the class name

```ts
selector: 'app-user'
```

does **not** mean the class must be named `AppUser`.

The selector and class name are separate:

```ts
selector: 'app-user'
export class UserComponent {
}
```

***

### Mistake 2 — Forgetting the component in `imports`

If you want to use another standalone component:

```html
<app-header></app-header>
```

you need to make that component available:

```ts
imports: [HeaderComponent]
```

Otherwise Angular doesn't know that `HeaderComponent` is available in this template.

***

### Mistake 3 — Confusing TypeScript imports with Angular imports

This:

```ts
import { HeaderComponent } from './header.component';
```

and this:

```ts
imports: [HeaderComponent]
```

serve different purposes.

Think:

```text
TypeScript import
    ↓
"Give me access to this class."

Angular imports array
    ↓
"Allow this component to use it in its template."
```

***

### Mistake 4 — Using old NgModule thinking

🕰️ Older Angular applications commonly organized components through **NgModules**.

Modern Angular primarily uses standalone components.

For this roadmap, think:

```text
Component
   ↓
imports: [...]
```

rather than starting with:

```text
NgModule
   ↓
declarations
   ↓
imports
```

You only need the old approach when reading legacy Angular code.

***

## 9. Hands-on Exercise

Create a simple `HeaderComponent` mentally or in your Angular project.

It should have:

```text
Class name: HeaderComponent
Selector: app-header
Template: <h1>My Website</h1>
```

Then create/use another component called `HomeComponent`.

Your goal is to make this work:

```html
<app-header></app-header>

<p>Welcome to the home page.</p>
```

And make sure `HomeComponent` has:

```ts
imports: [HeaderComponent]
```

**Your task:** write the `HeaderComponent` and `HomeComponent` TypeScript code yourself.

Don't worry about making the project perfect. The goal is to practice the relationship between:

```text
@Component
selector
imports
template
```

***

## 10. Quick Review

### Question 1

What does `selector` define?

> A. The TypeScript class name
> B. The HTML element used to place the component
> C. The component's CSS file
> D. The component's constructor

**Correct answer: B**

The selector determines how the component is referenced in HTML, such as `<app-user>`.

***

### Question 2

What is the purpose of `@Component()`?

> A. It creates a database
> B. It tells Angular that a class is a component and provides its metadata
> C. It creates an HTML file
> D. It starts the Angular server

**Correct answer: B**

`@Component()` provides Angular with information about the component.

***

### Question 3

What does the `imports` array of a standalone component control?

> A. Which TypeScript files are compiled
> B. Which components, directives, and pipes the component can use in its template
> C. Which CSS files are loaded globally
> D. Which routes exist in the application

**Correct answer: B**

The `imports` array makes Angular building blocks available to that component's template.

***

### Question 4

Why might you have both of these?

```ts
import { HeaderComponent } from './header.component';
```

and:

```ts
imports: [HeaderComponent]
```

> A. They do exactly the same thing
> B. The first is TypeScript importing; the second makes it available to the Angular template
> C. The first imports CSS; the second imports TypeScript
> D. They are both required only for routing

**Correct answer: B**

They operate at different levels: TypeScript and Angular template configuration.

***

### Question 5

Which is the modern Angular approach?

> A. Put every component inside an NgModule
> B. Use standalone components and their `imports` array
> C. Avoid component metadata
> D. Put all components in `app.module.ts`

**Correct answer: B**

Modern Angular uses standalone components as the primary approach.

***

## Progress

**Completed:** Lesson 2.2 — Component metadata, selector, standalone components and `imports`

**Next:** Lesson 2.3 — Component template and component styles
