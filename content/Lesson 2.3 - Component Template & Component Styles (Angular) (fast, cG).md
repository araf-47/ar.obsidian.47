# Lesson 2.3 — Component Template & Component Styles

A component has three main parts:

* **TypeScript class** → component logic
* **Template** → what appears on the screen
* **Styles** → how that screen looks

In this lesson, we focus on the last two.

***

## 1. Theory

### Component template

A **component template** is the HTML that defines what the component displays.

For example:

```ts
@Component({
  selector: 'app-user',
  template: `
    <h2>Hello!</h2>
    <p>Welcome to my application.</p>
  `
})
export class UserComponent {}
```

The template contains HTML:

```html
<h2>Hello!</h2>
<p>Welcome to my application.</p>
```

Angular takes this template and renders it as part of the application's UI.

A template can contain ordinary HTML, but Angular templates can also contain Angular-specific features such as:

```html
<h2>{{ name }}</h2>
```

or:

```html
@if (isLoggedIn) {
  <p>Welcome!</p>
}
```

You will learn those features in later lessons.

### Component styles

Component styles define the appearance of the HTML inside that component.

For example:

```css
h2 {
  color: blue;
}

p {
  font-size: 18px;
}
```

Angular associates these styles with the component.

***

## 2. How it works internally

Think of a component like this:

```text
Component
│
├── TypeScript class
│     └── Logic / data
│
├── Template
│     └── What the user sees
│
└── Styles
      └── How it looks
```

For example:

```text
UserComponent
│
├── user.component.ts
│     └── name = "Alice"
│
├── user.component.html
│     └── <h2>{{ name }}</h2>
│
└── user.component.css
      └── h2 { color: blue; }
```

Angular connects these pieces together.

The important mental model is:

> **The class provides the data and logic, the template displays it, and the styles control its appearance.**

***

## 3. Syntax

Angular provides two common ways to specify a component template.

### Inline template

The HTML is written directly inside `template`:

```ts
@Component({
  selector: 'app-user',
  template: `
    <h2>User Profile</h2>
    <p>Welcome!</p>
  `
})
export class UserComponent {}
```

The backticks allow the template to contain multiple lines.

***

### External template

For larger templates, you can put the HTML in a separate file:

```ts
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html'
})
export class UserComponent {}
```

Then:

```text
user.component.ts
user.component.html
```

The HTML file:

```html
<h2>User Profile</h2>
<p>Welcome!</p>
```

The two approaches do the same basic job.

**Inline:**

```ts
template: `...`
```

**External:**

```ts
templateUrl: './user.component.html'
```

Modern Angular projects commonly use external HTML files for components with more than a very small template.

***

### Inline styles

You can put CSS directly in the component:

```ts
@Component({
  selector: 'app-user',
  template: `
    <h2>User Profile</h2>
  `,
  styles: `
    h2 {
      color: blue;
    }
  `
})
export class UserComponent {}
```

***

### External styles

You can put CSS in a separate file:

```ts
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrl: './user.component.css'
})
export class UserComponent {}
```

Then:

```text
user.component.ts
user.component.html
user.component.css
```

And the CSS file:

```css
h2 {
  color: blue;
}
```

So remember:

```text
template      → inline HTML
templateUrl   → external HTML

styles        → inline CSS
styleUrl      → external CSS
```

***

## 4. Examples

Let's create a small component.

### `user.component.ts`

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrl: './user.component.css'
})
export class UserComponent {}
```

### `user.component.html`

```html
<h2>User Profile</h2>
<p>This is my user component.</p>
<button>View Profile</button>
```

### `user.component.css`

```css
h2 {
  color: blue;
}

p {
  font-size: 18px;
}

button {
  padding: 8px 16px;
}
```

Angular connects them:

```text
user.component.ts
       │
       ├──── templateUrl ────→ user.component.html
       │
       └──── styleUrl ───────→ user.component.css
```

The browser ultimately displays the HTML, with the component's CSS applied to it.

***

### Component styles are scoped

One important Angular behavior is that component styles are normally **scoped to that component**.

Suppose `UserComponent` has:

```css
p {
  color: blue;
}
```

That doesn't normally mean:

> "Make every `<p>` in the entire Angular application blue."

It means:

> "Style the `<p>` elements belonging to this component."

This helps prevent one component's styles from accidentally affecting another component.

For example:

```text
UserComponent
    ↓
<p>        ← blue

ProductComponent
    ↓
<p>        ← not automatically blue
```

This behavior is one of the useful differences between component CSS and a global stylesheet.

***

## 5. Common mistakes

### Mistake 1: Using `templateUrl` for an inline template

Wrong:

```ts
templateUrl: `
  <h2>Hello</h2>
`
```

`templateUrl` expects a **file path**.

Correct:

```ts
templateUrl: './user.component.html'
```

For inline HTML, use:

```ts
template: `
  <h2>Hello</h2>
`
```

***

### Mistake 2: Using `styleUrl` for CSS code

Wrong:

```ts
styleUrl: `
  h2 {
    color: blue;
  }
`
```

`styleUrl` expects a **CSS file path**.

Correct:

```ts
styleUrl: './user.component.css'
```

For inline CSS, use:

```ts
styles: `
  h2 {
    color: blue;
  }
`
```

***

### Mistake 3: Confusing HTML and CSS

Template:

```html
<h2>Hello</h2>
```

Style:

```css
h2 {
  color: blue;
}
```

The template says **what exists**.

The style says **how it looks**.

***

### Mistake 4: Expecting component CSS to style everything

If you write:

```css
button {
  background: black;
}
```

inside `UserComponent`, don't assume every button in the application will receive that style.

Component styles are normally scoped to that component.

***

## 6. Hands-on exercise

Create a component called `profile`.

Your component should have:

### TypeScript

Use an external template and external stylesheet.

```text
profile.component.ts
profile.component.html
profile.component.css
```

### Template requirements

Display:

```text
My Profile
I am learning Angular.
```

and add a button:

```text
Click Me
```

### Style requirements

* Make the heading blue.
* Make the paragraph larger.
* Add some padding to the button.

**Try writing the three files yourself before looking for an answer.**

***

## 7. Quick review

### Question 1

What does a component's template primarily define?

> A. Database structure
> B. What the component displays
> C. TypeScript configuration
> D. Angular CLI commands

**Correct answer: B — What the component displays.**

***

### Question 2

Which property references an external HTML template?

> A. `template`
> B. `htmlUrl`
> C. `templateUrl`
> D. `viewUrl`

**Correct answer: C — `templateUrl` references the HTML file.**

***

### Question 3

Which property references an external CSS file?

> A. `styleUrl`
> B. `css`
> C. `stylesUrl`
> D. `styleFile`

**Correct answer: A — `styleUrl` references the stylesheet.**

***

### Question 4

What is the main purpose of component styles?

> A. Store component data
> B. Control the component's appearance
> C. Create routes
> D. Send HTTP requests

**Correct answer: B — Component styles control appearance.**

***

### Question 5

What is the basic relationship between these three parts?

> A. Template provides logic, class provides CSS, styles provide data
> B. Class provides logic/data, template displays it, styles control appearance
> C. Template provides routes, styles provide logic, class provides HTML
> D. They are completely independent

**Correct answer: B — The class provides logic/data, the template displays it, and styles control appearance.**

***

## Progress

**Completed:** Lesson 2.3 — Component Template & Component Styles

**Next:** Lesson 2.4 — Angular CLI component generation
