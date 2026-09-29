# Lesson 0.1: TypeScript Fundamentals

***

## STEP 1: PREDICT

Before I explain, think about these (jot down guesses, no peeking):

1. In Java, you write `int x = 5;` and the compiler checks types. What do you think TypeScript adds to JavaScript?
2. Browsers can only run JavaScript. So how do you think a `.ts` file ends up running in a browser?
3. Angular could have been written in plain JavaScript. Why do you think the Angular team chose TypeScript?

***

## STEP 2: THEORY

### What is TypeScript?

TypeScript is **JavaScript plus a type system**. Every valid JavaScript file is already valid TypeScript. TypeScript just lets you add type annotations, and a compiler checks them **before your code runs**.

Important: browsers and Node.js **cannot run TypeScript**. TypeScript is compiled ("transpiled") to plain JavaScript, and the types are erased.

```
hello.ts  ──(tsc compiler)──►  hello.js  ──►  runs in browser / Node
 (types)                      (no types)
```

### The problem it solves

JavaScript is dynamically typed, so bugs show up at runtime, often in front of a user:

```javascript
function add(a, b) { return a + b; }
add(5, "10");   // "510"  (string concatenation, no error!)
```

TypeScript catches this while you type, in the editor:

```typescript
function add(a: number, b: number): number { return a + b; }
add(5, "10");   // ❌ Compile error: string is not assignable to number
```

### Why Angular uses TypeScript

* **Large apps need safety:** types catch bugs in big codebases early
* **Great tooling:** autocomplete, refactoring, and jump-to-definition
* **Decorators and classes:** Angular's `@Component` and `@Injectable` rely on TypeScript features
* **Dependency Injection:** Angular reads constructor and `inject()` types to know what to provide
* **It feels like Java:** classes, interfaces, generics, access modifiers

***

## STEP 3: MENTAL MODEL

### Java vs JavaScript vs TypeScript

```
Java:        int x = 5;              // type checked at compile time, enforced at runtime
JavaScript:  let x = 5;              // no type checking at all
TypeScript:  let x: number = 5;      // type checked at compile time, ERASED at runtime
```

The key idea, which is different from Java: **TypeScript types exist only at compile time.** After compilation, the JavaScript output has no idea what a `number` annotation was. In Java, the JVM still knows types at runtime (mostly). Here, JavaScript never does.

So TypeScript is like a very strict **code reviewer** that reads your code, complains, then hands the clean JavaScript to the runtime.

### The compile pipeline

1. You write `app.ts`
2. `tsc` (the TypeScript compiler) **type-checks** it
3. `tsc` **emits** `app.js`
4. Node or the browser runs `app.js`

Even if type errors exist, `tsc` will still emit the JS by default. The errors are warnings to you, not blockers, unless you configure otherwise (`noEmitOnError`).

### Angular connection

When you run `ng serve`, Angular's build tooling runs the TypeScript compiler and bundler for you. You almost never call `tsc` by hand in Angular projects. But you must understand it now, since that is what happens underneath, like knowing that Spring Boot runs `javac` behind Maven.

***

## STEP 4: SYNTAX

### Installing TypeScript

**Prerequisite:** Node.js (this also installs `npm`).

```bash
node --version
npm --version
```

If those print versions, install TypeScript globally:

```bash
npm install -g typescript
tsc --version
```

`tsc` is the TypeScript compiler command. (Analogy: `javac`.)

### Your first compile

Create `hello.ts`:

```typescript
let message: string = "Hello, TypeScript!";
let year: number = 2026;
let isLearning: boolean = true;

function greet(name: string): string {
  return `Hello, ${name}! Welcome to ${year}.`;
}

console.log(greet("Learner"));
console.log(message, isLearning);
```

Compile and run:

```bash
tsc hello.ts        # produces hello.js
node hello.js       # runs the JavaScript
```

Open `hello.js` and notice the annotations are gone. Depending on your `target` setting, the output may look slightly different, but the types will be removed.

### Basic types (quick tour)

```typescript
let count: number = 10;              // all numbers (no int/double split)
let title: string = "Angular";       // text
let done: boolean = false;           // true/false
let scores: number[] = [90, 85];     // array (like List<Integer>)
let anything: any = "risky";         // turns OFF type checking, avoid it
let inferred = 42;                   // type inferred as number
```

==Type inference means you don't always have to write the type==. `let inferred = 42;` is already a `number`, similar to Java's `var`.

### Project setup with tsconfig

```bash
tsc --init
```

This creates `tsconfig.json`, the compiler's config file (like `pom.xml` for compiler settings). Key options:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "strict": true,
    "outDir": "./dist"
  }
}
```

* `target`: which JavaScript version to output
* `strict`: turns on all strict checks (Angular projects use this)
* `outDir`: where compiled `.js` files go

With a `tsconfig.json` present, just run `tsc` with no filename to compile the whole project. Add `tsc --watch` to recompile on every save.

***

## STEP 5: COMMON MISTAKES

**Mistake 1: Trying to run a `.ts` file directly**

```bash
node hello.ts     # ❌ Node doesn't understand TypeScript syntax (older setups fail)
```

Fix: compile first with `tsc hello.ts`, then `node hello.js`.

**Mistake 2: Overusing `any`**

```typescript
let user: any = "Ali";
user.foo.bar();   // ❌ no compile error, crashes at runtime
```

`any` throws away the whole point of TypeScript. Use a real type.

**Mistake 3: Thinking types exist at runtime**

```typescript
let x: number = 5;
if (typeof x === "number") { }   // ✓ works, this is a JS check
// You can NOT do: if (x instanceof number)   ❌
```

Types are erased. You cannot inspect them while the program runs.

**Mistake 4: Ignoring compile errors because the `.js` still got created**

`tsc` may emit JS even with errors. Always read the errors and fix them.

**Mistake 5: Editing the generated `.js` file**

It gets overwritten on the next compile. Always edit the `.ts` file.

***

## STEP 6: HANDS-ON EXERCISE

**Task:** Set up TypeScript and compile a small program.

1. Create a folder `ts-lab`
2. Run `npm install -g typescript` (if not already installed)
3. Create `profile.ts` with:
   * A `string` variable for your name
   * A `number` variable for the number of lessons completed
   * A `boolean` variable `isReady`
   * A `number[]` array of three scores
   * A function `summary(name: string, lessons: number): string` that returns a sentence
4. Log the result with `console.log`
5. Compile with `tsc profile.ts` and run with `node profile.js`
6. Then deliberately break it: call `summary("Ali", "three")` and read the error message

**Deliverable:** paste your code plus the exact error message from step 6.

Skeleton:

```typescript
let name: string = "____";
let lessons: number = ____;

function summary(name: string, lessons: number): string {
  // return a sentence using a template string
}

console.log(summary(name, lessons));
```

***

## STEP 7: DEBUG EXERCISE

Here is code someone wrote. It has **three problems**. Find them before reading on.

```typescript
let course: string = "Angular";
let lessons: number = "12";

function describe(title: string, count: number) {
  return title + " has " + count + " lessons";
}

console.log(describe(course));
```

Think about: what does the compiler complain about on each line?

**Answers (try first!):**

1. `let lessons: number = "12";` assigns a string to a `number` variable. Fix: `12`
2. `describe(course)` is missing the second argument. In TypeScript, all parameters are required unless marked optional (`count?: number`). Java would also refuse this.
3. Not a compile error, but `describe` has no declared return type. It is inferred as `string`, but writing `: string` explicitly is good practice for readable APIs.

***

## STEP 8: QUICK REVIEW

> **Question 1:** What happens to type annotations after compilation?
>
>A) They are converted to Java-style types
>B) They are removed from the JavaScript output
>C) They are kept as comments
>D) They are checked again at runtime
>
> **Correct answer: B**

> **Question 2:** Which command compiles `app.ts`?
>
> &nbsp;&nbsp;&nbsp;&nbsp;A) `node app.ts`
> &nbsp;&nbsp;&nbsp;&nbsp;B) `tsc app.ts`
> &nbsp;&nbsp;&nbsp;&nbsp;C) `npm compile app.ts`
> &nbsp;&nbsp;&nbsp;&nbsp;D) `javac app.ts`
>
> **Correct answer: B**

> **Question 3:** What is the main danger of using `any`?
>
> &nbsp;&nbsp;&nbsp;&nbsp;A) It makes code slower
> &nbsp;&nbsp;&nbsp;&nbsp;B) It disables type checking for that value
> &nbsp;&nbsp;&nbsp;&nbsp;C) It only works with numbers
> &nbsp;&nbsp;&nbsp;&nbsp;D) It cannot be used in functions
>
> **Correct answer: B**

> **Question 4:** What does `tsc --init` create?
>
> &nbsp;&nbsp;&nbsp;&nbsp;A) A new Angular project
> &nbsp;&nbsp;&nbsp;&nbsp;B) A `package.json`
> &nbsp;&nbsp;&nbsp;&nbsp;C) A `tsconfig.json`
> &nbsp;&nbsp;&nbsp;&nbsp;D) A `main.ts` file
>
> **Correct answer: C**

> **Question 5 (short answer):** Give two reasons Angular uses TypeScript instead of plain JavaScript.

> **Question 6 (what would happen?):** If `tsc` reports a type error, is the `.js` file still produced by default? Why does that matter?

(Answer 5 and 6 yourself, then compare with Steps 2, 3, and 5.)

***

## STEP 9: CHECKPOINT AND REBUILD FROM MEMORY

Close this lesson. **Type B and C combined:**

1. **Explain in your own words** (3 to 5 sentences): what TypeScript is, and why a browser can't run it directly.
2. **From memory**, write down the commands to:
   * Check that Node is installed
   * Install TypeScript
   * Generate a `tsconfig.json`
   * Compile a file called `library.ts` and run the output
3. **Build from memory**: `library.ts` with
   * A `string` book title, a `number` page count, and a `boolean` `isAvailable`
   * A function `bookInfo(title: string, pages: number): string`
   * One deliberate type error that you fix after reading the compiler message

Send me your explanation, commands, code, and the error message you got. I'll evaluate it and tell you whether you're ready for **Lesson 0.2**.

***

Take your time. Attempt the predict questions and the debug exercise before checking my answers. When you're done, paste your checkpoint here.