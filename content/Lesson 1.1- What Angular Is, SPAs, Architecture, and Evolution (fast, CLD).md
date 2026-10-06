# Lesson 1.1: What Angular Is, SPAs, Architecture, and Evolution

The latest stable version is **Angular 22**, released June 3, 2026. Everything below uses the modern style.

***

## 1. Theory

**Angular** is a framework for building web applications in **TypeScript**. It is made and maintained by Google.

A framework gives you a complete toolkit: a way to build UI, move between pages, talk to servers, handle forms, and test your code. You follow its structure instead of assembling everything yourself.

**Single Page Application (SPA):**

- In a traditional website, every click asks the server for a new HTML page, and the browser reloads.
- In a SPA, the browser loads **one HTML page once**. After that, JavaScript changes what you see on screen without a reload.
- The app fetches only **data** (usually JSON) from a server, not whole pages.

Result: the app feels fast and smooth, like a desktop or phone app.

***

## 2. How it works internally

The mental model has four steps:

1. The browser requests your site and gets **one small HTML file** with an empty placeholder tag.
2. It downloads your compiled Angular JavaScript.
3. Angular **starts up** and fills the placeholder with your root component.
4. When the user clicks a link, Angular's **router** swaps which components are on screen and updates the URL. No page reload happens. If data is needed, Angular calls an API, gets JSON, and updates the screen.

```
Browser → index.html (empty shell) → Angular JS loads
        → root component renders → user clicks
        → router swaps components → fetch JSON if needed → screen updates
```

**Angular architecture overview.** An Angular app is built from a few main pieces. Each one gets its own lesson later.

- **Component:** a piece of UI. It is a TypeScript class plus an HTML template. An app is a tree of components.
- **Template:** the HTML of a component, with Angular's extra syntax for showing data and reacting to clicks.
- **Signals:** values that tell Angular automatically when they change, so the screen updates.
- **Services:** classes that hold shared logic or data, like calling an API.
- **Dependency injection (DI):** how Angular hands services to the places that need them.
- **Router:** maps URLs to components.
- **Directives and pipes:** small tools to change behavior or format displayed values.
- **Angular CLI:** the command line tool that creates, runs, and builds your project.

***

## 3. Syntax

Here is the smallest modern Angular app structure. You don't need to memorize it yet. Just see the shape.

**A component:**

```ts
import { Component, signal } from '@angular/core';

@Component({
  selector: 'app-counter',
  template: `
    <p>Count: {{ count() }}</p>
    <button (click)="increment()">Add</button>
  `,
})
export class Counter {
  count = signal(0);

  increment() {
    this.count.update(n => n + 1);
  }
}
```

**Starting the app (in `main.ts`):**

```ts
import { bootstrapApplication } from '@angular/platform-browser';
import { App } from './app/app';
import { appConfig } from './app/app.config';

bootstrapApplication(App, appConfig);
```

***

## 4. Examples

**Reading the component above:**

- `@Component({...})` is a **decorator**. It tells Angular "this class is a component."
- `selector` is the custom HTML tag name, so you can write `<app-counter />`.
- `template` is the HTML shown on screen.
- `{{ count() }}` shows the current value of the signal. The `()` reads it.
- `(click)="increment()"` runs the method when the button is clicked.
- `signal(0)` creates a value that starts at 0. When it changes, Angular updates the screen.

Recent Angular style drops the word "Component" from class names, so we write `Counter` instead of `CounterComponent`.

**Reading `bootstrapApplication(App, appConfig)`:** it starts Angular with `App` as the **root component**. Every other component lives inside it.

**Evolution: NgModules → Standalone → Signals**

|Era|What changed|
|:--|:--|
|**AngularJS (2010)**|The original framework. A completely different, older product. Not covered in this course.|
|**Angular 2+ (2016)**|Rewritten in TypeScript, built on components and **NgModules**.|
|**Standalone (v14 to v19)**|Components work on their own, with no NgModule needed. It became the default in v19.|
|**Signals (v16 onward)**|A simpler way to track changing data and update the screen. Now the core of modern Angular.|

🕰️ **Legacy side note: NgModules.** Old code wraps components in a module like this:

```ts
@NgModule({
  declarations: [Counter],
  imports: [BrowserModule],
  bootstrap: [Counter],
})
export class AppModule {}
```

You will see this in older projects and tutorials. New projects don't need it. We cover it in a Legacy Reference lesson later.

***

## 5. Common mistakes

- **Confusing AngularJS with Angular.** If a tutorial mentions `$scope` or `angular.module`, it is AngularJS. Skip it.
- **Copying old tutorials.** If you see `NgModule`, `*ngIf` or `@Input()` as the main approach, the tutorial is older than the modern style. Check the date.
- **Thinking a SPA never talks to a server.** It still does. It just asks for data, not full pages.
- **Forgetting `()` when reading a signal.** `count` is the signal itself. `count()` is its value.
- **Thinking Angular is a library.** Angular is a full framework with strong opinions about structure. That is why it feels bigger to learn at first.

***

## 6. Hands-on exercise

No installation yet. Setup comes in the next lesson. Do this on paper or in Obsidian:

1. Write **in your own words**, in 2 or 3 sentences, how a SPA differs from a traditional website.
2. Look at the `Counter` component in section 3. Label these parts: the decorator, the selector, the template, the signal, the click handler.
3. Draw the four-step flow from section 2, from the browser request to the screen updating.

Paste your answers here if you want me to check them.

***

## 7. Quick review

**Question 1.** What is a Single Page Application?

```
    A) A website with only one HTML link  
    B) An app that loads one HTML page and updates the screen with JavaScript, without full page reloads  
    C) A website that has no JavaScript  
    D) An app that never contacts a server
```

**Answer: B.** A SPA loads once, then updates the view in place and only fetches data when needed.

**Question 2.** What is an Angular component made of?

```
    A) A database and a server  
    B) Only a CSS file  
    C) A TypeScript class plus an HTML template  
    D) A single JSON file
```

**Answer: C.** A component combines a class (the logic) with a template (the HTML shown on screen).

**Question 3.** What does `{{ count() }}` do in a template?

```
    A) Declares a new signal  
    B) Shows the current value of the `count` signal  
    C) Runs a click handler  
    D) Imports a component
```

**Answer: B.** The double curly braces display a value, and the `()` reads the signal's current value.

**Question 4.** What is the correct order of Angular's evolution?

```
    A) Signals → NgModules → Standalone  
    B) Standalone → Signals → NgModules  
    C) NgModules → Standalone → Signals  
    D) NgModules → Signals → Standalone
```

**Answer: C.** Angular moved from NgModules to Standalone components, then added Signals as the modern way to track data.

**Question 5.** Which of these is the root component's job in `bootstrapApplication(App, appConfig)`?

```
    A) It is the starting component that all other components live inside  
    B) It deletes old components  
    C) It replaces the router  
    D) It runs only on the server
```

**Answer: A.** `App` is the top of the component tree, and every other component sits inside it.

***

## Progress

- ✅ **Done:** Lesson 1.1
- ⏭️ **Next:** Lesson 1.2

Say **"next"** to continue, **"explain again"** for a different example, or **"quiz me"** for 5 new questions.