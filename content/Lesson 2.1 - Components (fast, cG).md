# Lesson 2.1 — Components

## 1. Theory

### What is a component?

A **component** is a building block of an Angular application.

A component controls **one part of the screen**.

For example, imagine a website like this:

```text
---------------------------------
|         Header                |
---------------------------------
|                               |
|        Product List           |
|                               |
|   [ Product ] [ Product ]     |
|                               |
---------------------------------
|         Footer                |
---------------------------------
```

You could make each part a component:

```text
AppComponent
├── HeaderComponent
├── ProductListComponent
│   ├── ProductComponent
│   └── ProductComponent
└── FooterComponent
```

So instead of putting the entire application's UI into one huge file, Angular lets you divide the UI into **small, reusable components**.

A component usually has three important responsibilities:

1. **Define what appears on the screen**
2. **Define the data/logic for that screen part**
3. **Connect the logic with the HTML template**

***

## 2. How a component works internally

The easiest mental model is:

```text
Component
   │
   ├── TypeScript
   │      ↓
   │    Data + Logic
   │
   ├── Template
   │      ↓
   │    HTML / UI
   │
   └── Styles
          ↓
        Appearance
```

For example:

```text
ProductComponent
```

might contain:

```text
TypeScript
    productName = "Laptop"
    price = 800

        ↓

Template
    <h2>Laptop</h2>
    <p>$800</p>

        ↓

Browser
    Laptop
    $800
```

Angular connects the TypeScript component class to its template.

You can think of the component as:

> **"The code responsible for this particular piece of the UI."**

***

# 3. Component Anatomy

A modern Angular component commonly looks like this:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-product',
  template: `
    <h2>{{ name }}</h2>
    <p>Price: ${{ price }}</p>
  `
})
export class ProductComponent {
  name = 'Laptop';
  price = 800;
}
```

There are several parts here.

### 1. Import

```typescript
import { Component } from '@angular/core';
```

This imports Angular's `Component` decorator.

You need it to tell Angular:

> "This class is an Angular component."

***

### 2. `@Component`

```typescript
@Component({
  ...
})
```

`@Component` is called a **decorator**.

It gives Angular information about the class below it.

For example:

```typescript
@Component({
  selector: 'app-product',
  template: `<h2>Product</h2>`
})
```

It tells Angular things such as:

* What selector the component uses
* What HTML template it uses
* What styles it uses
* Other component configuration

You don't need to learn every configuration option yet.

***

### 3. Selector

```typescript
selector: 'app-product'
```

The selector defines the HTML element used to place the component.

For example:

```html
<app-product></app-product>
```

Angular sees:

```html
<app-product>
```

and knows:

> "Render the ProductComponent here."

Think of the selector as the component's **HTML name**.

***

### 4. Template

```typescript
template: `
  <h2>{{ name }}</h2>
  <p>Price: ${{ price }}</p>
`
```

The template describes **what the component displays**.

Here:

```html
<h2>{{ name }}</h2>
<p>Price: ${{ price }}</p>
```

The component's TypeScript contains:

```typescript
name = 'Laptop';
price = 800;
```

So Angular renders:

```text
Laptop
Price: $800
```

We'll study the template syntax and data binding in detail later.

***

### 5. Component class

```typescript
export class ProductComponent {
  name = 'Laptop';
  price = 800;
}
```

This is the **TypeScript class** containing the component's data and logic.

For now, think of it as:

```text
Class
 ├── data
 └── logic
```

For example:

```typescript
export class ProductComponent {
  name = 'Laptop';
  price = 800;

  getPrice() {
    return this.price;
  }
}
```

The class is the programming side of the component.

***

### 6. Styles

A component can also have its own CSS.

For example:

```typescript
@Component({
  selector: 'app-product',
  template: `
    <h2>{{ name }}</h2>
    <p>Price: ${{ price }}</p>
  `,
  styles: `
    h2 {
      color: blue;
    }
  `
})
export class ProductComponent {
  name = 'Laptop';
  price = 800;
}
```

The styles control the component's appearance.

In real Angular projects, the template and styles are often placed in separate files:

```text
product.component.ts
product.component.html
product.component.css
```

For example:

```typescript
@Component({
  selector: 'app-product',
  templateUrl: './product.component.html',
  styleUrl: './product.component.css'
})
export class ProductComponent {
  name = 'Laptop';
  price = 800;
}
```

We'll use this structure frequently as the application becomes larger.

***

# 4. Examples

## Example 1 — Simple component

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-greeting',
  template: `
    <h1>Hello!</h1>
    <p>Welcome to Angular.</p>
  `
})
export class GreetingComponent {
}
```

Its selector is:

```text
app-greeting
```

So another template could use:

```html
<app-greeting></app-greeting>
```

The result is:

```text
Hello!

Welcome to Angular.
```

***

## Example 2 — Component with data

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-user',
  template: `
    <h2>{{ name }}</h2>
    <p>Age: {{ age }}</p>
  `
})
export class UserComponent {
  name = 'Rahim';
  age = 25;
}
```

The important relationship is:

```text
UserComponent class
        │
        ├── name = "Rahim"
        └── age = 25
                ↓
             template
                ↓
        <h2>{{ name }}</h2>
        <p>{{ age }}</p>
                ↓
             browser
```

The `{{ ... }}` syntax will be properly covered in **Lesson 3.1**.

***

## Example 3 — Separate files

A component might look like this:

```text
product/
├── product.component.ts
├── product.component.html
└── product.component.css
```

### `product.component.ts`

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-product',
  templateUrl: './product.component.html',
  styleUrl: './product.component.css'
})
export class ProductComponent {
  name = 'Laptop';
  price = 800;
}
```

### `product.component.html`

```html
<h2>{{ name }}</h2>
<p>Price: ${{ price }}</p>
```

### `product.component.css`

```css
h2 {
  color: blue;
}
```

The three files work together as **one component**.

***

# 5. Common mistakes

### Mistake 1 — Thinking a component is only HTML

A component isn't just HTML.

It combines:

```text
TypeScript + Template + Styles
```

***

### Mistake 2 — Confusing selector with class name

These are different:

```typescript
selector: 'app-product'
```

and:

```typescript
export class ProductComponent
```

The class is the TypeScript class.

The selector is the HTML name used to place the component.

```html
<app-product></app-product>
```

***

### Mistake 3 — Forgetting that the selector is how a component is used

If you have:

```typescript
selector: 'app-product'
```

you use it as:

```html
<app-product></app-product>
```

Not:

```html
<ProductComponent></ProductComponent>
```

***

### Mistake 4 — Putting application-wide thinking into every component

A component should generally represent **one meaningful piece of UI**.

For example:

```text
Header
Product List
Product Card
Login Form
Footer
```

This makes applications easier to understand and maintain.

***

# 6. Hands-on exercise

Create a component called `UserCardComponent`.

It should display:

```text
Name: Alice
Age: 25
```

### Requirements

Your component should have:

```typescript
selector: 'app-user-card'
```

and these properties:

```typescript
name = 'Alice';
age = 25;
```

Its template should display both values.

**Do not worry about Angular CLI yet.** Just write the component code yourself.

Paste your code here when you're finished, and I'll review it.

***

# 7. Quick review

### Question 1

What is an Angular component?

> A. A database table
> B. A building block of the UI
> C. A TypeScript compiler
> D. An HTTP request

**Correct answer: B**

A component controls a particular part of an Angular application's UI.

***

### Question 2

What does `selector` define?

> A. The component's CSS
> B. The component's TypeScript class
> C. The HTML element used to place the component
> D. The component's database name

**Correct answer: C**

For `selector: 'app-product'`, you use:

```html
<app-product></app-product>
```

***

### Question 3

What is the purpose of `@Component`?

> A. It tells Angular that the class is a component and provides its configuration
> B. It creates a database
> C. It starts the Angular server
> D. It defines a TypeScript variable

**Correct answer: A**

`@Component` provides Angular with the component's metadata/configuration.

***

### Question 4

Which part usually contains the component's data and logic?

> A. CSS
> B. HTML template
> C. TypeScript class
> D. Selector

**Correct answer: C**

The component class contains the programming logic and data.

***

### Question 5

Which parts can make up an Angular component?

> A. TypeScript class
> B. Template
> C. Styles
> D. All of the above

**Correct answer: D**

A component brings its programming logic, UI template, and styling together.

***

## Progress

**Completed:** Lesson 2.1 — What is a component? + Component anatomy

**Next:** Lesson 2.2 — Component metadata, selector, standalone components, and the `imports` array.
