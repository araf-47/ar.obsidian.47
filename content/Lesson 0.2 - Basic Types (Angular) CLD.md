# Lesson 0.2: Basic Types

**Estimated time:** 90 to 120 minutes, in one sitting. Keep VS Code open and create a file called `basic-types.ts`.

***

## STEP 1: PREDICT

Before reading further, write down your guesses (in your notes, or reply to me):

1. In Java you write `int age = 25;`. What do you think the TypeScript equivalent looks like?
2. Java has `int`, `double`, `long`, and `float`. How many number types do you think TypeScript has?
3. If you write `let city = "Dhaka";` with no type, does TypeScript know it's a string?

Don't scroll on until you've committed to a guess. Being wrong here is useful.

***

## STEP 2: THEORY

**What it is.** A *type* tells the compiler what kind of value a variable holds, so it can catch mistakes before your code runs.

**Why it exists.** Plain JavaScript lets a variable hold anything at any time:

```js
let age = 25;
age = "twenty-five";  // JavaScript: fine
age.toFixed(2);       // 💥 crashes at RUNTIME
```

TypeScript catches that error while you type, not after users hit it.

**The Java bridge:**

| Concept | Java | JavaScript | TypeScript |
|---|---|---|---|
| Declare a number | `int x = 5;` | `let x = 5;` | `let x: number = 5;` |
| Declare a string | `String s = "hi";` | `let s = "hi";` | `let s: string = "hi";` |
| Constant | `final int x = 5;` | `const x = 5;` | `const x: number = 5;` |
| Type position | before the name | none | **after** the name, with `:` |

Java puts the type *before* the name. TypeScript puts it *after*, separated by a colon.

**The core primitives:**

| Type        | Meaning                                 | Java closest match                                 |
| ----------- | --------------------------------------- | -------------------------------------------------- |
| `string`    | text                                    | `String`                                           |
| `number`    | **all** numbers (integers and decimals) | `int`, `double`, `long`, `float` all in one        |
| `boolean`   | `true` / `false`                        | `boolean`                                          |
| `null`      | intentional "nothing"                   | `null`                                             |
| `undefined` | "never assigned a value"                | *(no equivalent; Java uses uninitialized or null)* |
| `bigint`    | very large integers                     | `long` / `BigInteger`                              |

You will use `string`, `number`, and `boolean` for 95% of your work.

***

## STEP 3: MENTAL MODEL

### 1. Types exist only at compile time

This is the biggest difference from Java.

```
Your .ts file  →  TypeScript compiler (tsc)  →  plain .js file
  (has types)        (checks types,               (NO types left,
                      then erases them)            just JavaScript)
```

In Java, type information survives into the bytecode and the JVM enforces it at runtime. In TypeScript, the types are a **safety net during development**. The browser only ever runs plain JavaScript.

Angular runs `tsc` for you, so you'll see type errors in your editor and terminal.

### 2. One `number` type

JavaScript has no separate `int`. Every number is a 64-bit floating-point value, like Java's `double`.

```ts
let a: number = 42;
let b: number = 3.14;
let c: number = -7;
console.log(0.1 + 0.2);  // 0.30000000000000004 (same quirk as Java doubles!)
```

### 3. ==Type inference==: the compiler reads your mind

If you assign a value at declaration, TypeScript **infers** the type:

```ts
let city = "Dhaka";   // TypeScript infers: string
city = 42;            // ❌ Error: number is not assignable to string
```

The Java parallel is `var city = "Dhaka";` (Java 10+), where the compiler infers `String`.

**`let` vs `const` changes what gets inferred:**

```ts
let x = 5;      // type: number  (could change to any number later)
const y = 5;    // type: 5       (a "literal type": can only ever be 5)
```

### 4. `any` vs `unknown`: the "I don't know the type" types

|                          | `any`                              | `unknown`                                          |
| ------------------------ | ---------------------------------- | -------------------------------------------------- |
| Meaning                  | "Turn off type checking for this"  | "Could be anything, so **prove** what it is first" |
| Can you use it directly? | Yes, anything goes                 | **No**, you must check its type first              |
| Safety                   | ❌ None                             | ✅ Full                                             |
| Java analogy             | Casting with no checks, and hoping | `Object`, where you need `instanceof` before use   |

Think of `any` as removing the seatbelt, and `unknown` as a locked box that you must inspect before opening.

***

## STEP 4: SYNTAX

### Explicit type annotations

```ts
let username: string = "araf";
let age: number = 25;
let isLoggedIn: boolean = true;
const PI: number = 3.14159;
```

### Type inference (annotation omitted)

```ts
let username = "araf";    // inferred: string
let age = 25;             // inferred: number
let isLoggedIn = true;    // inferred: boolean
```

**Rule of thumb:** ==if you assign a value right away, let inference work. Annotate only when the type isn't obvious==.

### Declaring without a value: annotation needed

```ts
let score: number;        // declared, not assigned yet
score = 100;              // ✅
score = "high";           // ❌ Error
```

### Template literals (a JavaScript feature Java lacks)

```ts
let name = "Araf";
let age = 25;
let msg = `Hello, ${name}! You are ${age} years old.`;
```

Backticks allow `${}` interpolation. In Java you'd write `"Hello, " + name` or `String.format(...)`.

### `null` and `undefined`

```ts
let middleName: string | null = null;    // "string OR null" (a union type, covered later)
let nickname: string | undefined;        // no value yet
```

With `strictNullChecks` on (the default in modern Angular projects), a `string` variable **cannot** hold `null`. This is like Java's `@NonNull`, but enforced by the compiler.

### `any`: the escape hatch

```ts
let mystery: any = 5;
mystery = "now a string";   // ✅ no error
mystery = true;             // ✅ no error
mystery.foo.bar.baz();      // ✅ compiles... 💥 crashes at runtime
```

### `unknown`: the safe version

```ts
let input: unknown = "hello";

input.toUpperCase();         // ❌ Error: 'input' is of type 'unknown'

if (typeof input === "string") {
  input.toUpperCase();       // ✅ TypeScript now knows it's a string here
}
```

Checking the type before use is called **narrowing**. You'll use it constantly.

### `typeof`: checking types at runtime

```ts
typeof "hi"       // "string"
typeof 42         // "number"
typeof true       // "boolean"
typeof undefined  // "undefined"
typeof null       // "object"  ⚠️ famous JavaScript bug, ignore it
```

### JavaScript quirks to know

```ts
// Use === (strict equality), never == 
5 == "5"     // true   😱 (JavaScript converts types silently)
5 === "5"    // false  ✅ (what you almost always want)

// var vs let vs const
var  x = 1;  // ❌ old style, avoid (function-scoped, hoisted)
let  y = 2;  // ✅ can be reassigned, block-scoped like Java locals
const z = 3; // ✅ cannot be reassigned. Default to this
```

**Modern habit:** use `const` by default, `let` only when the value must change, and never `var`.

***

## STEP 5: COMMON MISTAKES

```ts
// ❌ WRONG: capital-S String (that's the wrapper object type)
let name: String = "Araf";

// ✅ CORRECT: lowercase primitive type
let name: string = "Araf";
```
Java habit alert: `String` is correct in Java, but in TypeScript you want lowercase `string`, `number`, and `boolean`.

```ts
// ❌ WRONG: using any to "make the error go away"
let data: any = fetchUser();

// ✅ CORRECT: use a real type, or unknown if truly uncertain
let data: unknown = fetchUser();
```
`any` spreads like a virus: anything touched by an `any` also loses its type safety.

```ts
// ❌ WRONG: over-annotating what's obvious
let count: number = 0;
let title: string = "Home";

// ✅ CORRECT: let inference do it
let count = 0;
let title = "Home";
```

```ts
// ❌ WRONG: uninitialized variable with no annotation → implicit any
let total;
total = 5;
total = "oops";   // no error!

// ✅ CORRECT
let total: number;
```

```ts
// ❌ WRONG: expecting separate integer and decimal types
let price: int = 5;     // Error: no 'int' type exists
let tax: double = 0.5;  // Error

// ✅ CORRECT
let price: number = 5;
let tax: number = 0.5;
```

```ts
// ❌ WRONG: using == 
if (age == "25") { }

// ✅ CORRECT
if (age === 25) { }
```

***

## STEP 6: HANDS-ON EXERCISE

Create `basic-types.ts` and write:

1. A `const` called `appName` holding your app's name, using **inference** (no annotation).
2. A `let` called `userAge` with an **explicit** `number` annotation, set to any age.
3. A `let` called `isPremium` (boolean), initially `false`.
4. A `let` called `email` declared **without a value**, annotated as `string`. Assign an email to it on the next line.
5. A `let` called `userInput` typed as `unknown`, assigned the value `"  Hello TypeScript  "`.
6. Write an `if (typeof userInput === "string")` block that logs `userInput.trim().toUpperCase()`.
7. Build a template literal that combines `appName` and `userAge` into a sentence, and log it.
8. Deliberately write **two** lines that should produce compile errors (for example, assign a string to `userAge`) and confirm VS Code underlines them in red.

**Run it:**
```bash
npx tsc basic-types.ts
node basic-types.js
```
Compare the generated `.js` file with your `.ts` file. Notice that the types are gone.

***

## STEP 7: DEBUG EXERCISE

This code has **5 bugs**. Find each one and say how to fix it **before** asking me for the answer.

```ts
let age: number = "25";

let username = "Sara";
username = 42;

let data: unknown = "hello world";
console.log(data.toUpperCase());

let isActive: boolean;
let status: String = "active";
if (age == "25") {
  console.log("match");
}
```

Hints, without giving anything away: some bugs are type mismatches, one involves `unknown`, one is a Java habit, and one is about equality.

Reply with your list of bugs and fixes, and I'll respond with the full explanation.

***

## STEP 8: QUICK REVIEW

*Cover the answer line under each question until you've committed to your own answer.*

**Question 1:** What type does TypeScript infer for `const y = 5;`?

    A) number
    B) string
    C) 5 (the literal type)
    D) any

    Correct answer: C) 5 (the literal type). With `const`, the value can never change, so the type narrows to exactly `5`. With `let x = 5` it would be `number`.

**Question 2:** Which is the main difference between `any` and `unknown`?

    A) There is no difference
    B) `unknown` forces you to check the type before using the value
    C) `any` is only for numbers
    D) `unknown` disables type checking

    Correct answer: B) `unknown` forces you to check the type before using the value. `any` disables checks, while `unknown` keeps them and requires narrowing.

**Question 3:** Which line correctly declares a decimal price in TypeScript?

    A) `let price: double = 9.99;`
    B) `let price: float = 9.99;`
    C) `let price: number = 9.99;`
    D) `let price: decimal = 9.99;`

    Correct answer: C) `let price: number = 9.99;`. TypeScript has one `number` type for integers and decimals alike.

**Question 4:** Why should you prefer `===` over `==`?

    A) `===` is faster to type
    B) `==` doesn't exist in TypeScript
    C) `==` silently converts types (so `5 == "5"` is true), `===` does not
    D) `===` only works on strings

    Correct answer: C) `==` silently converts types, `===` does not.

**Question 5 (short answer):** In one or two sentences, explain what happens to your type annotations after the TypeScript compiler finishes. How does that differ from Java?

***

## STEP 9: CHECKPOINT & REBUILD FROM MEMORY

Close this lesson. No peeking. From memory, create a new file `checkpoint-0-2.ts` and write:

1. A `const` string using inference and a `let` number with an explicit annotation.
2. A boolean declared without a value, then assigned later.
3. A variable of type `unknown` holding a string, plus an `if` block that uses `typeof` to safely call a string method on it.
4. One line using `any`, and a comment explaining in your own words why it's dangerous.
5. A template literal that combines at least two of your variables.
6. **Explain in your own words** (as code comments):
   - the difference between `any` and `unknown`
   - why `let x = 5` and `const x = 5` get different inferred types
   - what "types are erased at compile time" means, and how that differs from Java

Paste your code here, along with your debug exercise answers and your review answers (especially Question 5). I'll evaluate all of it and either clear you for **Lesson 0.3** or give targeted help on whatever was shaky.

***

**Next up (when you pass):** Lesson 0.3, the next topic on your Module 0 roadmap.