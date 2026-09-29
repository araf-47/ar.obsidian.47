***

# Module 0, Lesson 0.3 - Advanced Types

**Estimated time:** 90–120 minutes. Have VS Code open with a scratch file called `lesson03.ts`.

***

## STEP 1: PREDICT

Before reading on, write down your guesses. There are no wrong answers here.

1. A function takes an `id` that might be a number (`101`) or a string (`"USR-101"`). In Java, what would you do? What do you think TypeScript offers?
2. In Java, any object reference can be `null` and you find out with a `NullPointerException` at runtime. How do you think TypeScript could help catch that at compile time?
3. If you have `let x: string | number`, can you call `x.toUpperCase()`? Why or why not?

Keep your guesses handy. We'll check them at the end of the lesson.

***

## STEP 2: THEORY

In Lessons 0.1 and 0.2 you learned basic types (`string`, `number`, `boolean`, arrays, objects). Real data is messier. A value might be one of several types, an object might combine two shapes, a field might be missing, or a value might be `null`. **Advanced types** let you describe that reality precisely.

| Concept                      | Problem it solves                                     |
| ---------------------------- | ----------------------------------------------------- |
| Union types (`A \| B`)       | A value can be one of several types                   |
| Intersection types (`A & B`) | A value must have all the properties of several types |
| Optional properties (`?`)    | A property may be absent                              |
| Null/undefined handling      | Values that may be "nothing"                          |
| Type narrowing               | Figuring out the exact type inside a union            |
| Type assertions (`as`)       | You know more than the compiler and tell it so        |

**Why Angular cares:** Angular code is full of these. HTTP responses may be an error or data. Form values may be `null`. Route parameters may be `undefined`. You'll write `string | null` constantly.

***

## STEP 3: MENTAL MODEL

Think of types as **sets of allowed values**.

* `string` is the set of all strings.
* `number` is the set of all numbers.
* `string | number` is the **union** of the two sets: ==anything in either set==.
* `A & B` is the **intersection**: ==a value must satisfy both A and B at once==.

**The key insight about unions:** when a value is `string | number`, the compiler only lets you do things that are **safe for both**. That's why `x.toUpperCase()` fails. Numbers don't have it. To use string-only features you must first prove it's a string. That proof is called **narrowing**.

**Java comparison:**

```
Java:        Object id;  // then instanceof + cast
             if (id instanceof String) { String s = (String) id; }

TypeScript:  let id: string | number;
             if (typeof id === "string") { id.toUpperCase(); }  // auto-narrowed, no cast
```

TypeScript is smarter than Java here. After the check, it *automatically* treats `id` as a string inside that block. No cast needed. Java 16+ pattern matching (`if (o instanceof String s)`) is the closest equivalent.

**A JavaScript reality check:** at runtime, all types vanish. The compiler turns your TypeScript into plain JavaScript with no type information. So narrowing must rely on real runtime checks (`typeof`, `instanceof`, `in`, comparisons). The compiler watches those checks and updates its knowledge.

***

## STEP 4: SYNTAX

### 4.1 Union Types

```typescript
let id: string | number;
id = 101;        // OK
id = "USR-101";  // OK
id = true;       // ❌ Error: boolean not allowed

function printId(id: string | number): void {
  console.log("ID:", id);   // fine, works for both
}

// Union of literal values (very common in Angular)
type Status = "loading" | "success" | "error";
let current: Status = "loading";
current = "done";  // ❌ Error: not one of the three
```
- [^1]
Literal unions replace many uses of Java `enum`s in Angular code.

### 4.2 Intersection Types

```typescript
type Person = { name: string; age: number };
type Employee = { employeeId: string; department: string };

type Staff = Person & Employee;   // has ALL four properties

const s: Staff = {
  name: "Araf",
  age: 25,
  employeeId: "E-42",
  department: "Engineering"
};
```

Java comparison: like a class implementing two interfaces at once (`class Staff implements Person, Employee`).

### 4.3 Optional Properties

```typescript
interface User {
  id: number;
  name: string;
  email?: string;   // may be missing
}

const u1: User = { id: 1, name: "Araf" };                      // OK
const u2: User = { id: 2, name: "Sam", email: "s@x.com" };     // OK
```

`email?: string` means the type is effectively `string | undefined`. Optional parameters work the same way:

```typescript
function greet(name: string, title?: string): string {
  return title ? `${title} ${name}` : name;
}
greet("Araf");           // OK
greet("Araf", "Dr.");    // OK
```

### 4.4 Null and Undefined Handling

JavaScript has **two** "nothing" values. Java only has `null`.

* `undefined`: "no value was ever assigned" (missing property, uninitialized variable)
* `null`: "intentionally empty"

With `strict` mode on (Angular projects enable this by default), the compiler refuses to let `null`/`undefined` sneak into other types:

```typescript
let name: string = null;          // ❌ Error under strict mode
let name2: string | null = null;  // ✓ explicit
```

This is TypeScript's answer to `NullPointerException`. You must handle the "nothing" case before the compiler lets you use the value.

Tools for handling it:

```typescript
const user: { address?: { city: string } } = {};

// Optional chaining  ?.  (stops and returns undefined if anything is missing)
const city = user.address?.city;          // undefined, no crash

// Nullish coalescing  ??  (default only for null/undefined)
const display = city ?? "Unknown";        // "Unknown"

// Non-null assertion  !  (you promise it's not null; use sparingly)
const definitelyCity = user.address!.city;  // crashes at runtime if you're wrong
```

**`??` vs `||`:** `||` replaces *any falsy* value (`0`, `""`, `false`). `??` replaces only `null`/`undefined`.

```typescript
const count = 0;
console.log(count || 10);   // 10   (surprising: 0 is falsy)
console.log(count ?? 10);   // 0    (correct)
```

### 4.5 Type Narrowing

Narrowing = proving to the compiler which member of a union you have.

```typescript
// typeof: for primitives
function format(value: string | number): string {
  if (typeof value === "string") {
    return value.toUpperCase();    // value is string here
  }
  return value.toFixed(2);         // value is number here
}

// truthiness check: removes null/undefined
function length(text: string | null): number {
  if (text) {
    return text.length;            // text is string here
  }
  return 0;
}

// instanceof: for classes
function describe(e: Date | string): string {
  if (e instanceof Date) {
    return e.toISOString();
  }
  return e;
}

// "in" operator: check if property exists
type Cat = { meow: () => void };
type Dog = { bark: () => void };

function speak(pet: Cat | Dog) {
  if ("meow" in pet) {
    pet.meow();
  } else {
    pet.bark();
  }
}

// Discriminated union: the most important pattern for Angular
type Result =
  | { status: "success"; data: string[] }
  | { status: "error"; message: string };

function handle(r: Result) {
  if (r.status === "success") {
    console.log(r.data);      // compiler knows data exists
  } else {
    console.log(r.message);   // compiler knows message exists
  }
}
```

The `status` field is the "discriminator." Checking it narrows the whole object. You'll see this pattern in state management later.

### 4.6 Type Assertions

An assertion tells the compiler: "Trust me, I know the type."

```typescript
const input = document.getElementById("email") as HTMLInputElement;
console.log(input.value);   // compiler now allows .value

const raw: unknown = "hello";
const len = (raw as string).length;
```

**Critical difference from Java casts:** a Java cast is *checked at runtime* (`ClassCastException`). A TypeScript assertion is **only a compile-time instruction**. It does no runtime checking and generates no code. If you're wrong, you get a crash later, with no warning.

Prefer narrowing (which proves the type) over assertions (which just claim it).

***

## STEP 5: COMMON MISTAKES

```typescript
// ❌ WRONG 1: using a string method on a union without narrowing
function shout(v: string | number) {
  return v.toUpperCase();          // Error: not on number
}
// ✓ CORRECT
function shout(v: string | number) {
  return typeof v === "string" ? v.toUpperCase() : String(v);
}
```

```typescript
// ❌ WRONG 2: using || when 0 or "" is a valid value
const quantity = input.quantity || 1;   // 0 becomes 1!
// ✓ CORRECT
const quantity = input.quantity ?? 1;
```

```typescript
// ❌ WRONG 3: overusing ! to silence the compiler
const name = getUser()!.profile!.name!;  // three ways to crash
// ✓ CORRECT
const name = getUser()?.profile?.name ?? "Guest";
```

```typescript
// ❌ WRONG 4: assertion used as if it were a conversion
const n = "42" as unknown as number;
n + 1;   // "421" at runtime! The value is still a string.
// ✓ CORRECT
const n = Number("42");
```

```typescript
// ❌ WRONG 5: intersecting conflicting primitives
type Impossible = string & number;   // becomes `never`, nothing satisfies it
```

***

## STEP 6: HANDS-ON EXERCISE

Create `exercise03.ts` and complete these tasks. Actually type the code; don't paste.

**Task A (Union + narrowing):** Write `formatValue(value: string | number | boolean): string` that returns:
* the uppercase text if it's a string
* the number with 2 decimals if it's a number
* `"YES"` or `"NO"` if it's a boolean

**Task B (Optional + null handling):** Given:

```typescript
interface Customer {
  id: number;
  name: string;
  phone?: string;
  address?: { city: string; zip?: string };
}
```

Write `getContact(c: Customer): string` that returns `"<name> - <phone> (<city>)"`, using `"no phone"` and `"no city"` as defaults when missing. Use `?.` and `??`.

**Task C (Intersection):** Define `Timestamps = { createdAt: Date; updatedAt: Date }` and `Product = { id: number; title: string }`. Create `StoredProduct` as their intersection and build one valid object.

**Task D (Discriminated union):** Define `ApiResponse` with a success shape (`status: "success"`, `data: string[]`) and an error shape (`status: "error"`, `code: number`, `message: string`). Write `render(r: ApiResponse): string` that returns the joined data on success or `"Error <code>: <message>"` on failure.

Run with `npx tsc exercise03.ts && node exercise03.js`.

***

## STEP 7: DEBUG EXERCISE

Each snippet has a bug. Find it and fix it *before* scrolling to the next lesson step. Write your answers down.

**Bug 1:**

```typescript
function getLength(value: string | null): number {
  return value.length;
}
```

**Bug 2:**

```typescript
interface Settings { volume?: number }

function getVolume(s: Settings): number {
  return s.volume || 50;
}
// Calling getVolume({ volume: 0 }) should return 0 (muted)
```

**Bug 3:**

```typescript
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; side: number };

function area(s: Shape): number {
  return s.radius * s.radius * Math.PI;
}
```

**Bug 4:**

```typescript
const data = JSON.parse('{"age": "30"}') as { age: number };
console.log(data.age + 5);   // expected 35
```

***

## STEP 8: QUICK REVIEW

Write your answers before checking the correct ones.

**Question 1**

    What does `let x: string | number` allow you to do without narrowing?
    
    A) Call `x.toUpperCase()`
    B) Call `x.toString()`
    C) Call `x.toFixed(2)`
    D) Use `x.length`

    Correct answer: B (only members common to both types are safe)

**Question 2**

    What is the result of `const r = 0 ?? 10;`?
    
    A) 10
    B) 0
    C) undefined
    D) null

    Correct answer: B (`??` only replaces null or undefined)

**Question 3**

    Which statement about `as` type assertions is true?
    
    A) They throw an error at runtime if the type is wrong
    B) They convert the value to the new type
    C) They only affect compile-time checking
    D) They are the same as Java's instanceof

    Correct answer: C

**Question 4**

    What type does `A & B` describe?
    
    A) A value that is either A or B
    B) A value that has everything from both A and B
    C) A value that has nothing in common with A or B
    D) A value that is A but not B

    Correct answer: B

**Question 5 (short answer)**

In your own words: why is a discriminated union (using a `status` or `kind` field) safer than checking properties with `if (r.data)`?

***

## STEP 9: CHECKPOINT & REBUILD FROM MEMORY

Now **close this lesson** and don't look back. Write the following from memory in a new file `checkpoint03.ts`.

**Scenario:** A user profile screen loads data from a server.

1. Define a literal union type `LoadState` with three values: `"idle"`, `"loading"`, `"loaded"`.
2. Define an interface `Profile` with `id: number`, `name: string`, and optional `bio` and `website`.
3. Define a discriminated union `ProfileResult`:
   * success: `status: "ok"`, `profile: Profile`
   * failure: `status: "failed"`, `reason: string`
4. Write `describeProfile(result: ProfileResult): string` that:
   * on success returns `"<name>: <bio>"` with the default `"No bio"` if bio is missing (use the right operator)
   * on failure returns `"Failed: <reason>"`
5. Write `getWebsiteHost(p: Profile): string | null` using narrowing. If `website` is missing return `null`, otherwise return the website in lowercase.
6. Write one line showing an intersection: `type AdminProfile = Profile & { permissions: string[] }`, and create a valid object.
7. In two sentences, explain why narrowing is better than `as` for the value returned by `JSON.parse`.

**Send me:** your answers to the Predict questions (Step 1), your exercise code (Step 6), your bug findings (Step 7), your quiz answers (Step 8), and the checkpoint code (Step 9). I'll review everything and tell you whether you're ready for Lesson 0.4.

***

**Angular preview:** In real Angular code you'll see `FormControl<string | null>`, `route.snapshot.paramMap.get('id')` returning `string | null`, and HTTP state modeled as discriminated unions. This lesson is the foundation for reading all of that.

***
# Footnote:
[^1]: [[type keyword in typescript (explanation 4m example)]].
