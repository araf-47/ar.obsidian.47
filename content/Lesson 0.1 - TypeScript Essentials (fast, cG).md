# Lesson 0.1 — TypeScript Essentials

## 1. Theory

### What is TypeScript?

**TypeScript is a programming language built on top of JavaScript.**

You can think of it like this:

```text
TypeScript
    ↓
JavaScript + additional features
    ↓
JavaScript
    ↓
Browser / Node.js
```

The most important additional feature for us is **static typing**.

For example, JavaScript allows:

```javascript
let age = 25;
age = "hello";
```

TypeScript can detect that problem:

```typescript
let age: number = 25;

age = "hello"; // Error
```

The `: number` tells TypeScript:

> This variable is supposed to contain a number.

***

### TypeScript does not run directly in the browser

Browsers understand JavaScript.

They do not normally execute TypeScript directly.

So TypeScript code is **compiled/transpiled into JavaScript**:

```text
app.ts
  ↓
TypeScript compiler
  ↓
app.js
  ↓
JavaScript runtime
```

For example:

```typescript
let message: string = "Hello Angular";
console.log(message);
```

becomes JavaScript similar to:

```javascript
let message = "Hello Angular";
console.log(message);
```

The type information is mainly useful during development and compilation.

***

## 2. Why Angular uses TypeScript

Angular is built around TypeScript.

One major reason is that Angular applications can become large and complex. Types help you catch many mistakes while writing code rather than discovering them later at runtime.

For example:

```typescript
function add(a: number, b: number): number {
    return a + b;
}
```

TypeScript knows:

```text
a → number
b → number
return value → number
```

So this is valid:

```typescript
add(10, 20);
```

But this produces a type error:

```typescript
add(10, "20");
```

This becomes particularly useful in Angular when working with:

* Components
* Services
* Forms
* HTTP responses
* Objects
* Functions
* Signals

You will gradually see these benefits throughout the roadmap.

### Important mental model

Don't think:

> "Angular is a completely different language."

Think:

> **Angular uses TypeScript to write application code. TypeScript adds useful features to JavaScript and is compiled to JavaScript.**

***

## 3. Installing TypeScript

TypeScript is installed through **npm**, the Node.js package manager.

First check whether Node.js and npm are installed:

```bash
node --version
```

```bash
npm --version
```

Then install TypeScript globally:

```bash
npm install -g typescript
```

Check the installation:

```bash
tsc --version
```

`tsc` means **TypeScript Compiler**.

For example:

```text
Version 5.x.x
```

The exact version may differ.

### One important distinction

There are two different things here:

```text
TypeScript
    ↓
Programming language

tsc
    ↓
TypeScript compiler
```

You **write** TypeScript.

You use `tsc` to **compile** TypeScript.

***

## 4. Compiling `.ts` files

Let's create a very small TypeScript program.

Create a file:

```text
hello.ts
```

Put this inside:

```typescript
let message: string = "Hello TypeScript";

console.log(message);
```

Now compile it:

```bash
tsc hello.ts
```

You should get:

```text
hello.js
```

So your directory becomes:

```text
hello.ts
hello.js
```

The `.ts` file is your TypeScript source.

The `.js` file is the JavaScript output.

You can then run the JavaScript using Node:

```bash
node hello.js
```

Output:

```text
Hello TypeScript
```

### The complete process

```text
You write:

hello.ts
   ↓
tsc hello.ts
   ↓
hello.js
   ↓
node hello.js
   ↓
Hello TypeScript
```

### Try a type error

Change your file to:

```typescript
let age: number = 25;

age = "twenty";
```

Then run:

```bash
tsc hello.ts
```

TypeScript should report an error because `"twenty"` is a string while `age` was declared as a number.

This is one of the main reasons TypeScript is useful.

***

## 5. Common mistakes

### Mistake 1 — Thinking `.ts` runs directly

```text
hello.ts → browser
```

Not normally.

Instead:

```text
hello.ts → TypeScript compiler → hello.js → JavaScript runtime
```

***

### Mistake 2 — Thinking TypeScript replaces JavaScript

TypeScript is closely based on JavaScript.

Most normal JavaScript code is also valid TypeScript.

For example:

```typescript
console.log("Hello");
```

is perfectly valid TypeScript.

***

### Mistake 3 — Confusing `tsc` with TypeScript

```bash
tsc hello.ts
```

`tsc` is the **compiler command**, not the language itself.

***

### Mistake 4 — Expecting type annotations in the final JavaScript

You write:

```typescript
let age: number = 25;
```

But the generated JavaScript will not need:

```javascript
let age: number = 25;
```

The type annotation is removed during compilation.

***

## 6. Hands-on exercise

Create:

```text
lesson01.ts
```

Write a small TypeScript program containing:

1. A variable called `name` that contains your name.
2. A variable called `age` that contains your age.
3. A variable called `isLearning` that contains `true`.
4. Print all three values using `console.log()`.

For example, the structure should look like:

```typescript
let name: string = "...";
let age: number = ...;
let isLearning: boolean = true;

console.log(name);
console.log(age);
console.log(isLearning);
```

Then compile it:

```bash
tsc lesson01.ts
```

Check that `lesson01.js` was created.

Finally run:

```bash
node lesson01.js
```

**Don't move to the next lesson yet.** Paste your `.ts` code and, if possible, the compiler/output here. I'll check it.

***

## 7. Quick review

### Question 1

> What is TypeScript?

> A. A database
> B. A programming language built on JavaScript
> C. A web browser
> D. An operating system

**Correct answer: B**

TypeScript extends JavaScript with features such as static typing.

***

### Question 2

> What does `tsc` do?

> A. Runs Angular
> B. Runs JavaScript in a browser
> C. Compiles TypeScript into JavaScript
> D. Installs Node.js

**Correct answer: C**

`tsc` is the TypeScript compiler.

***

### Question 3

> What does this mean?

> ```typescript
> let age: number = 25;
> ```

> A. `age` must contain a number
> B. `age` must contain a string
> C. `age` can only contain `true` or `false`
> D. `age` is an Angular component

**Correct answer: A**

`: number` specifies the variable's type.

***

### Question 4

> Why does TypeScript eventually become JavaScript?

> A. Browsers primarily execute JavaScript
> B. JavaScript is faster than TypeScript
> C. Angular cannot use TypeScript
> D. TypeScript is a database language

**Correct answer: A**

The TypeScript compiler converts TypeScript into JavaScript that can be executed by JavaScript runtimes.

***

### Question 5

> Which sequence is correct?

> A. `.js → .ts → browser`
> B. `.ts → tsc → .js → JavaScript runtime`
> C. `.ts → browser → tsc`
> D. `.ts → Angular → database`

**Correct answer: B**

That is the basic TypeScript development flow.

***

### Progress

**Completed:** Lesson 0.1 — TypeScript Essentials

**Next:** Lesson 0.2 — Variables, Primitive Types, Type Inference, `any`, `unknown`
