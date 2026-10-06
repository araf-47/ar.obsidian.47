# Lesson 1.3 — Modern Angular Project Structure

In this lesson, we are going to understand **where an Angular application starts, where the root component lives, where configuration lives, and what the important project-level files do**.

We are using the current standalone-style Angular structure. Angular's current supported major version is **Angular 22**. ([Angular][1])

***

## 1. Theory

When you create an Angular project, you get many files.

At first, this can look confusing:

```text
my-app/
├── angular.json
├── package.json
├── tsconfig.json
├── src/
│   ├── index.html
│   ├── main.ts
│   ├── styles.css
│   └── app/
│       ├── app.ts
│       ├── app.html
│       ├── app.css
│       ├── app.config.ts
│       └── app.routes.ts
```

You do **not** need to memorize every file.

For this lesson, build this mental model:

```text
Angular application
│
├── main.ts
│      ↓
│   starts Angular
│
├── Root component
│      ↓
│   first component displayed
│
├── app.config.ts
│      ↓
│   application-wide configuration
│
├── app.routes.ts
│      ↓
│   URL → component rules
│
├── angular.json
│      ↓
│   Angular CLI/build configuration
│
└── tsconfig.json
       ↓
    TypeScript configuration
```

The most important distinction is:

> **Your application code lives mainly inside `src/`. Configuration for the workspace/tooling mostly lives outside `src/`.** ([Angular][2])

***

# 2. How It Works Internally

Let's follow what happens when you start an Angular application.

### Step 1 — The browser loads the application

Angular has an HTML entry point:

```text
src/index.html
```

But Angular itself needs to be started.

That's the job of:

```text
src/main.ts
```

### Step 2 — `main.ts` starts Angular

Conceptually:

```text
main.ts
   ↓
bootstrapApplication()
   ↓
Root component
   ↓
Angular application
```

### Step 3 — The root component becomes the starting point

Angular creates the root component.

The root component then becomes the top of your component tree.

Later, your application might look conceptually like:

```text
Root Component
│
├── Header
├── Navigation
├── Home
│   ├── ProductList
│   └── ProductCard
└── Footer
```

So the **root component is the starting component of your UI**.

### Step 4 — Configuration is supplied

Angular can also receive application-wide configuration through `app.config.ts`.

For example:

```text
main.ts
   │
   ├── Root component
   │
   └── app.config.ts
           │
           └── application providers/configuration
```

This is one of the important differences between the modern standalone approach and older Angular applications.

There is no `AppModule` in the modern standalone structure. Angular's standalone migration documentation shows the old `AppModule` bootstrap being replaced by `bootstrapApplication()`. ([Angular][3])

***

# 3. Syntax

## 3.1 `main.ts` and `bootstrapApplication()`

A modern Angular application has a `main.ts` entry point.

A simplified version looks like:

```ts
import { bootstrapApplication } from '@angular/platform-browser';
import { App } from './app/app';
import { appConfig } from './app/app.config';

bootstrapApplication(App, appConfig);
```

There are three important pieces.

### `bootstrapApplication`

```ts
bootstrapApplication(...)
```

means roughly:

> "Start an Angular application using this root component."

### `App`

```ts
App
```

is the root component.

### `appConfig`

```ts
appConfig
```

contains application-level configuration.

So:

```ts
bootstrapApplication(App, appConfig);
```

can be mentally read as:

> **Start Angular with `App` as the root component and use this application configuration.**

Angular's documentation identifies `main.ts` as the main entry point and `bootstrapApplication()` as the modern standalone bootstrap mechanism. ([Angular][2])

***

## 3.2 Root Component

The root component is the component at the top of your application's component hierarchy.

A modern root component might look like:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {}
```

Its template might contain:

```html
<h1>My Angular App</h1>
```

The important idea is:

```text
App
 ↓
app.html
 ↓
<h1>My Angular App</h1>
```

Angular's current CLI-generated structure uses an `app` root component inside `src/app/`. ([Angular][2])

> **Note:** Current Angular CLI versions may use names such as `app.ts` and `app.html` rather than the older `app.component.ts` / `app.component.html` naming you may see in tutorials.

Don't let the filename confuse you. It is still a component.

***

## 3.3 `app.config.ts`

This file contains application-level configuration.

For example:

```ts
import { ApplicationConfig } from '@angular/core';

export const appConfig: ApplicationConfig = {
  providers: []
};
```

The important part is:

```ts
ApplicationConfig
```

and:

```ts
providers: []
```

You will later put things such as application-wide providers here.

For example, routing can be configured through a provider:

```ts
import { ApplicationConfig } from '@angular/core';
import { provideRouter } from '@angular/router';
import { routes } from './app.routes';

export const appConfig: ApplicationConfig = {
  providers: [
    provideRouter(routes)
  ]
};
```

Don't worry about `provideRouter()` yet. Routing is a later module.

For now, remember:

> **`app.config.ts` = application configuration.**

Angular defines `ApplicationConfig` as the configuration available during application bootstrap, including providers available to the root component and its children. ([Angular][4])

***

## 3.4 `app.routes.ts`

This file contains your application's routing configuration.

For example:

```ts
import { Routes } from '@angular/router';

export const routes: Routes = [
  {
    path: '',
    component: HomeComponent
  }
];
```

Conceptually:

```text
URL
 ↓
Route
 ↓
Component
```

For example:

```text
/products
     ↓
ProductComponent
```

So `app.routes.ts` answers questions such as:

> "Which component should Angular display for this URL?"

Angular's documentation describes routes as the fundamental building blocks for navigation and recommends keeping route definitions in a routes file such as `src/app/app.routes.ts`. ([Angular][5])

You don't need to learn routing itself yet.

For this lesson, just understand **where routing configuration lives**.

***

## 3.5 `angular.json`

Now we leave the application's main source code and look at the Angular workspace.

At the project root:

```text
angular.json
```

This file configures the Angular CLI.

For example, it contains configuration related to:

* building
* serving
* testing
* project settings
* assets
* styles
* scripts

Conceptually:

```text
angular.json
     ↓
Angular CLI
     ↓
Build / Serve / Test
```

For example, when you run:

```bash
ng serve
```

Angular CLI uses project configuration to determine how the application should be served.

When you run:

```bash
ng build
```

the CLI uses the project's build configuration.

Angular's documentation describes `angular.json` as the workspace-wide and project-specific configuration file used by Angular CLI tools. ([Angular][6])

### Important

You usually **don't edit `angular.json` every day**.

You should understand what it is before changing it.

***

## 3.6 `tsconfig.json`

This file belongs to TypeScript.

```text
tsconfig.json
```

It tells TypeScript how the project should be treated.

For example, it can configure things such as:

* compiler options
* included files
* module settings
* TypeScript behavior

Conceptually:

```text
tsconfig.json
       ↓
TypeScript compiler
       ↓
How TypeScript is compiled/checked
```

Angular's workspace documentation describes the root `tsconfig.json` as the base TypeScript configuration for the projects in the workspace. ([Angular][2])

You may also see:

```text
tsconfig.app.json
```

This provides application-specific TypeScript configuration and inherits from the base configuration. ([Angular][2])

For now, don't worry about individual compiler options.

Remember:

> **`tsconfig.json` = TypeScript configuration.**

***

# 4. Examples

Let's put everything together.

A modern Angular project might look like this:

```text
my-app/
│
├── angular.json
├── package.json
├── tsconfig.json
│
└── src/
    ├── index.html
    ├── main.ts
    ├── styles.css
    │
    └── app/
        ├── app.ts
        ├── app.html
        ├── app.css
        ├── app.config.ts
        └── app.routes.ts
```

Now imagine the application starts here:

### `main.ts`

```ts
import { bootstrapApplication } from '@angular/platform-browser';
import { App } from './app/app';
import { appConfig } from './app/app.config';

bootstrapApplication(App, appConfig);
```

This gives us:

```text
main.ts
   ↓
bootstrapApplication()
   ↓
App
```

Then `App` uses:

```text
app.html
```

for its template.

And:

```text
app.css
```

for its component styles.

Meanwhile:

```text
app.config.ts
```

contains application configuration.

And:

```text
app.routes.ts
```

contains route definitions.

Outside `src/`:

```text
angular.json
```

controls Angular CLI behavior.

And:

```text
tsconfig.json
```

controls TypeScript configuration.

***

## The easiest mental model

If you forget everything else, remember this:

```text
                    Angular Project
                          │
             ┌────────────┴────────────┐
             │                         │
        Application                 Tooling
             │                         │
            src/               angular.json
             │                 tsconfig.json
             │
       ┌─────┴─────┐
       │           │
    main.ts      app/
       │           │
       │      ┌────┼─────────────┐
       │      │    │             │
       │    root  config       routes
       │   component
       │
       └── starts Angular
```

### One-line definitions

| File            | Remember it as                          |
| --------------- | --------------------------------------- |
| `main.ts`       | **Starts the Angular application**      |
| Root component  | **Top-level component of the UI**       |
| `app.config.ts` | **Application configuration**           |
| `app.routes.ts` | **URL → component routing rules**       |
| `angular.json`  | **Angular CLI/workspace configuration** |
| `tsconfig.json` | **TypeScript configuration**            |

The official Angular project structure documentation confirms these roles and locations. ([Angular][2])

***

# 5. Common Mistakes

### Mistake 1 — Thinking `angular.json` starts the application

It doesn't.

```text
angular.json
```

is configuration for Angular's tooling.

The application entry point is:

```text
src/main.ts
```

***

### Mistake 2 — Thinking `app.config.ts` is the root component

It isn't.

The root component is something like:

```ts
export class App {}
```

while:

```text
app.config.ts
```

contains configuration.

```text
App              → component
app.config.ts    → configuration
```

***

### Mistake 3 — Thinking `app.routes.ts` displays the UI

It doesn't directly display the UI.

It defines routing rules.

For example:

```text
/products → ProductComponent
```

The router uses those rules to determine what should be displayed.

***

### Mistake 4 — Thinking `tsconfig.json` is an Angular configuration file

It is primarily **TypeScript configuration**.

Angular uses TypeScript, but these are different concepts:

```text
Angular configuration → angular.json
TypeScript configuration → tsconfig.json
```

***

### Mistake 5 — Getting confused by `app.ts`

You may find older tutorials showing:

```text
app.component.ts
```

while a newer Angular project may use:

```text
app.ts
```

Don't assume they represent different Angular concepts.

They can both represent the root component.

The current Angular CLI's generated structure uses the root component files inside `src/app/`. ([Angular][2])

***

# 6. Hands-on Exercise

Open the Angular project you created in **Lesson 1.2**.

Don't change anything.

Find these files:

```text
src/main.ts
src/app/app.ts
src/app/app.config.ts
src/app/app.routes.ts
angular.json
tsconfig.json
```

For each file, answer this in your own words:

```text
1. main.ts:
2. app.ts:
3. app.config.ts:
4. app.routes.ts:
5. angular.json:
6. tsconfig.json:
```

Then answer this:

> **What is the path Angular follows from starting the application to displaying the root component?**

Try to express it like:

```text
_____ → _____ → _____
```

**Don't look for the answer yet.** This exercise is mainly to make sure you can identify the role of each file.

***

# 7. Quick Review

### Question 1

What is the main entry point of a modern Angular application?

> A. `angular.json`
> B. `main.ts`
> C. `app.config.ts`
> D. `tsconfig.json`

**Correct answer: B — `main.ts`**

`main.ts` is the application's main entry point. ([Angular][2])

***

### Question 2

What does `bootstrapApplication()` do?

> A. Compiles TypeScript
> B. Configures the Angular CLI
> C. Starts an Angular application with a root component
> D. Creates a route

**Correct answer: C**

It bootstraps the Angular application using the root component.

***

### Question 3

What is `app.config.ts` mainly used for?

> A. Application configuration
> B. HTML markup
> C. TypeScript compilation
> D. CSS styling

**Correct answer: A**

It contains application-level configuration such as providers.

***

### Question 4

What is `angular.json` mainly responsible for?

> A. Defining components
> B. Defining Angular CLI/workspace configuration
> C. Defining TypeScript types
> D. Defining HTML

**Correct answer: B**

It contains workspace and project configuration used by Angular CLI tools. ([Angular][6])

***

### Question 5

What is `tsconfig.json`?

> A. Angular's routing configuration
> B. The root component
> C. TypeScript configuration
> D. Angular CLI configuration

**Correct answer: C**

It provides the base TypeScript configuration for the workspace. ([Angular][2])

***

# Progress

**Completed:** Lesson 1.3 — Modern Project Structure

**Next:** Lesson 1.4 — Running the application

* Development server
* Build process

[1]: https://angular.dev/reference/releases?utm_source=chatgpt.com "Versioning and releases • Angular"
[2]: https://angular.dev/reference/configs/file-structure?utm_source=chatgpt.com "File structure • Angular"
[3]: https://angular.dev/reference/migrations/standalone?utm_source=chatgpt.com "Standalone • Angular"
[4]: https://angular.dev/api/core/ApplicationConfig?utm_source=chatgpt.com "ApplicationConfig • Angular"
[5]: https://angular.dev/guide/routing/define-routes?utm_source=chatgpt.com "Define routes • Angular"
[6]: https://angular.dev/reference/configs/workspace-config?utm_source=chatgpt.com "Workspace configuration • Angular"
