# Lesson 2.4 — Angular CLI Component Generation

***

## 1. Theory

### What is Angular CLI?

**Angular CLI** (Command Line Interface) is a command-line tool for creating and managing Angular applications.

Instead of manually creating all the files needed for a component, you can tell Angular CLI:

```bash
ng generate component user-card
```

Angular CLI creates the component structure for you.

The shorter version is:

```bash
ng g c user-card
```

Both commands do the same thing.

### Why use it?

A component usually needs several things:

* A TypeScript class
* A template
* A stylesheet
* Component metadata

The CLI creates these files with the correct Angular structure and configuration.

***

## 2. How it works internally

Think of the CLI command as asking Angular:

> "Create a new component named `user-card` and configure it as an Angular component."

For example:

```bash
ng generate component user-card
```

Angular CLI creates something like:

```text
src/
└── app/
    ├── user-card/
    │   ├── user-card.ts
    │   ├── user-card.html
    │   └── user-card.css
    └── ...
```

The exact generated files can vary depending on your Angular version and project configuration.

The important idea is:

```text
CLI command
     ↓
Angular CLI generator
     ↓
Creates component files
     ↓
Configures the component
```

You don't need to manually create the component from scratch.

***

## 3. Syntax

### Full command

```bash
ng generate component component-name
```

For example:

```bash
ng generate component product-card
```

### Short command

```bash
ng g c product-card
```

Here:

```text
ng        → Angular CLI
g         → generate
c         → component
product-card → component name
```

### Generate inside a folder

You can also specify a path:

```bash
ng g c components/product-card
```

This creates the component under:

```text
src/app/components/product-card/
```

assuming the command is run from the Angular project root.

***

## 4. Examples

### Example 1 — Create a `user-card`

From your Angular project directory:

```bash
ng g c user-card
```

You will get a component directory such as:

```text
user-card/
├── user-card.ts
├── user-card.html
└── user-card.css
```

The generated TypeScript will have Angular component metadata similar to:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-user-card',
  imports: [],
  templateUrl: './user-card.html',
  styleUrl: './user-card.css'
})
export class UserCard {

}
```

Notice that the CLI has already created the `@Component` configuration for you.

You don't have to remember the entire structure every time.

***

### Example 2 — Create a component in a folder

```bash
ng g c components/product-card
```

Structure:

```text
src/
└── app/
    └── components/
        └── product-card/
            ├── product-card.ts
            ├── product-card.html
            └── product-card.css
```

This is useful for keeping larger applications organized.

***

### Example 3 — Generate without the separate stylesheet

Angular CLI supports options that change what it generates.

For example:

```bash
ng g c product-card --inline-style
```

The CSS is placed directly in the component metadata instead of creating a separate CSS file.

Similarly:

```bash
ng g c product-card --inline-template
```

puts the HTML template directly into the TypeScript file.

You don't need to memorize these options now. The important thing is that **CLI generators have options for customizing what they create**.

***

## 5. Common mistakes

### Mistake 1 — Running the command outside the Angular project

If you run:

```bash
ng g c user-card
```

from the wrong directory, Angular CLI may not know which project you mean.

Usually, first move into your project:

```bash
cd my-angular-app
```

Then:

```bash
ng g c user-card
```

***

### Mistake 2 — Confusing the component name with the selector

If you generate:

```bash
ng g c user-card
```

the component class is:

```typescript
export class UserCard {

}
```

while its selector is typically:

```text
app-user-card
```

These are different things.

```text
Component class → UserCard
Selector         → app-user-card
Folder           → user-card
```

***

### Mistake 3 — Thinking CLI is required for Angular

It isn't.

You can create a component manually.

The CLI is simply a tool that makes the process faster and less error-prone.

***

### Mistake 4 — Assuming every generated project looks exactly the same

Angular's generated structure and defaults can change between versions and project configurations.

So focus on the **purpose of the CLI command**, rather than memorizing every generated file.

***

## 6. Hands-on exercise

Inside your Angular project, create a component called `profile-card`.

Run:

```bash
ng g c profile-card
```

Then inspect the generated files.

You should be able to identify:

```text
profile-card.ts
profile-card.html
profile-card.css
```

Open `profile-card.ts` and answer these questions for yourself:

1. What is the component class called?
2. What is its selector?
3. Which file is used as its template?
4. Which file is used for its styles?

**Don't change the generated code yet.** The goal here is simply to understand what the CLI generated.

***

## 7. Quick review

**1. What does `ng g c product-card` do?**

> A. Starts the Angular development server
> B. Generates a component
> C. Builds the Angular application
> D. Creates a service

**Correct answer: B — Generates a component.**

***

**2. What is the full form of `ng g c`?**

> A. `ng get config`
> B. `ng generate component`
> C. `ng generate class`
> D. `ng global component`

**Correct answer: B — `ng generate component`.**

***

**3. Where should you normally run an Angular CLI component-generation command?**

> A. Inside the Angular project
> B. Inside the browser
> C. Inside the `node_modules` folder
> D. Inside the TypeScript compiler

**Correct answer: A — Inside the Angular project.**

***

**4. What is the main purpose of Angular CLI component generation?**

> A. To replace Angular components
> B. To automatically write application business logic
> C. To quickly create the files and structure for a component
> D. To connect Angular to a database

**Correct answer: C — It automates component creation.**

***

## Progress

**Completed:** Lesson 2.4 — Angular CLI component generation

**Next:** Lesson 2.5 — Component lifecycle, `ngOnInit`, `ngOnDestroy`
