# Lesson 0.4: Collections & Generics

## First, the side note: what are these two ideas?

**Collection:** a container that holds many values instead of one. A shopping list holds many items, not just "milk". In code, that's an array, a list, a set, and so on.

**Generics:** a way to write code once so it works with many types, while TypeScript still tracks which type is involved. Think of a labeled box. A `Box<string>` is a box for strings and a `Box<number>` is a box for numbers. The box design is written once, and the label `<T>` is a placeholder filled in later.

The two ideas go together. A collection needs to know what it holds, so you write `string[]` or `Array<string>`, and that `Array<string>` is generics.

You already know this from Java: `List<String>`, `Map<String, User>`, `ResponseEntity<List<User>>`. Same idea, so you're closer than you think.

***

## STEP 1: PREDICT

Before reading on, take a minute and guess:

1. In Java, `String[]` has a fixed size. Do you think a TypeScript array `string[]` is fixed-size too?
2. What do you think `<T>` in `function identity<T>(x: T): T` means?
3. Java has no tuple. What do you think a tuple would be?

Jot your guesses down, then continue.

***

## STEP 2: THEORY

**Arrays** are ordered lists of values. In TypeScript the type says what they hold: `number[]` holds only numbers.

**Tuples** are arrays with a fixed length and a fixed type per position. `[string, number]` means the first item is a string and the second is a number. It's for small, fixed-shape groups like `["Araf", 25]`.

**Generics** solve this problem: you want a function that works for any type, but you don't want to lose type safety.

Without generics you'd write one of these:

```typescript
function firstItem(items: any[]): any { return items[0]; }
```

`any` switches off type checking, so the result could be anything and TypeScript can't help you. Generics fix that:

```typescript
function firstItem<T>(items: T[]): T { return items[0]; }
```

Pass in `string[]` and you get back a `string`. Pass in `User[]` and you get back a `User`. One function, full safety.

**Generic constraints** limit what `T` may be. "Any type" is sometimes too loose. If your function reads `item.id`, then `T` must be something that has an `id`, and you express that with `T extends { id: number }`.

***

## STEP 3: MENTAL MODEL

**Java to JavaScript to TypeScript:**

Java:        `String[]` (fixed size), or `ArrayList<String>` (resizable)
JavaScript:  arrays are always resizable and can hold mixed values
TypeScript:  `string[]`, which is a JavaScript array plus a type label

So the answer to Predict question 1 is that TypeScript arrays are **not** fixed-size. They behave like Java's `ArrayList`: `push`, `pop` and `length` all work.

**Types disappear at runtime.** TypeScript compiles to plain JavaScript and erases every type label, just like Java's type erasure for generics. So:
- A tuple becomes a plain array at runtime.
- `<T>` vanishes completely.
- Types protect you only while you write and compile the code.

That's why you can't write `new T()` or check `typeof T` in TypeScript. `T` doesn't exist at runtime.

**Angular bridge:** you'll see generics constantly in Angular code:

Spring:   `ResponseEntity<List<User>>`
Angular:  `Observable<User[]>`

Spring:   `List<User>`
Angular:  `User[]`, `signal<User[]>([])`, `http.get<User[]>(url)`

***

## STEP 4: SYNTAX

### Arrays

```typescript
let nums: number[] = [1, 2, 3];
let names: Array<string> = ["Araf", "Sam"];   // same thing, generic form

nums.push(4);          // OK, arrays are resizable
nums.push("five");     // ERROR: string is not a number

let mixed: (string | number)[] = [1, "two", 3];   // union type

const list: number[] = [1, 2];
list.push(3);          // OK! const protects the variable, not the contents
```

**Readonly arrays** are like Java's unmodifiable list:

```typescript
const fixed: readonly number[] = [1, 2, 3];
fixed.push(4);         // ERROR
```

**Common array methods** (like Java streams, but built in):

```typescript
const nums = [1, 2, 3, 4, 5];

nums.map(n => n * 2);              // [2, 4, 6, 8, 10]   (like stream().map)
nums.filter(n => n % 2 === 0);     // [2, 4]             (like stream().filter)
nums.find(n => n > 3);             // 4 (type: number | undefined)
nums.includes(3);                  // true
nums.reduce((sum, n) => sum + n, 0); // 15

const copy = [...nums, 6];         // spread: new array with an extra item
```

### Tuples

```typescript
let person: [string, number] = ["Araf", 25];

person[0];                 // "Araf" (type: string)
person[1];                 // 25 (type: number)
person = [25, "Araf"];     // ERROR: wrong order
person = ["Araf", 25, 1];  // ERROR: too many items

// Destructuring
const [name, age] = person;

// Labeled tuple (clearer)
let user: [name: string, age: number] = ["Araf", 25];
```

### Generics: functions

```typescript
function identity<T>(value: T): T {
  return value;
}

identity<string>("hello");   // explicit
identity(42);                // T inferred as number
```

### Generics: interfaces and classes

```typescript
interface ApiResponse<T> {
  data: T;
  status: number;
}

const res: ApiResponse<string[]> = { data: ["a", "b"], status: 200 };

class Box<T> {
  constructor(private content: T) {}
  get(): T { return this.content; }
}

const numBox = new Box<number>(5);
const strBox = new Box("hi");   // T inferred as string
```

### Generic constraints

```typescript
interface HasId {
  id: number;
}

function findById<T extends HasId>(items: T[], id: number): T | undefined {
  return items.find(item => item.id === id);
}

interface User { id: number; name: string; }
const users: User[] = [{ id: 1, name: "Araf" }];
findById(users, 1);          // OK, returns User | undefined
findById([1, 2, 3], 1);      // ERROR: number has no id
```

Java comparison: `<T extends HasId>` is the same idea as Java's `<T extends Comparable<T>>`.

One more useful constraint, `keyof`:

```typescript
function getProp<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const u = { id: 1, name: "Araf" };
getProp(u, "name");    // string
getProp(u, "email");   // ERROR: "email" is not a key of u
```

***

## STEP 5: COMMON MISTAKES

```typescript
// ❌ WRONG: any[] throws away type safety
let items: any[] = [1, "a", true];

// ✓ CORRECT: be specific
let items: number[] = [1, 2, 3];
```

```typescript
// ❌ WRONG: assuming find() always returns a value
const user = users.find(u => u.id === 99);
console.log(user.name);        // ERROR: user might be undefined

// ✓ CORRECT: handle the undefined case
if (user) { console.log(user.name); }
```

```typescript
// ❌ WRONG: using T's properties without a constraint
function show<T>(item: T) { console.log(item.id); }   // ERROR

// ✓ CORRECT
function show<T extends { id: number }>(item: T) { console.log(item.id); }
```

```typescript
// ❌ WRONG: expecting T to exist at runtime
function create<T>(): T { return new T(); }   // ERROR
```

```typescript
// ❌ WRONG: thinking const makes the array immutable
const arr = [1, 2];
arr.push(3);                   // allowed!

// ✓ CORRECT: use readonly if you want protection
const arr: readonly number[] = [1, 2];
```

```typescript
// ❌ WRONG: a tuple for something with many fields
let user: [string, number, string, boolean, string];   // unreadable

// ✓ CORRECT: use an interface
interface User { name: string; age: number; email: string; }
```

***

## STEP 6: HANDS-ON EXERCISE

Open VS Code and create `lesson04.ts`.

**Task A:** Build a generic `Stack<T>` class, like Java's `Stack<T>`:
- a private array `items: T[]`
- `push(item: T): void`
- `pop(): T | undefined`
- `peek(): T | undefined` (look at the top without removing it)
- `size(): number`

Test it with `Stack<number>` and `Stack<string>`.

**Task B:** Write `findById<T extends { id: number }>(items: T[], id: number): T | undefined` and test it with an array of `Product` objects (`id`, `title`, `price`).

**Task C:** Write a function `minMax(nums: number[]): [number, number]` that returns the smallest and largest numbers as a tuple. Destructure the result when you call it.

Run with `npx ts-node lesson04.ts` (or `tsc lesson04.ts` then `node lesson04.js`).

***

## STEP 7: DEBUG EXERCISE

Two bugs are hiding here. Find and fix them **before** looking for hints.

```typescript
function printId<T>(item: T): void {
  console.log(item.id);
}

const point: [number, number] = [1, 2, 3];
```

Hint: one error is about *what T is allowed to be*. The other is about *tuple length*.

*Answer (try first!):*
1. `T` could be anything, so `item.id` isn't guaranteed to exist. Fix it with `<T extends { id: number }>`.
2. The tuple type allows exactly two numbers, but three were given. Remove the extra value or change the type to `[number, number, number]`.

***

## STEP 8: QUICK REVIEW

Answers are printed after each question. Try it yourself first, then check.

**Question 1**

    What does `T` mean in `function identity<T>(x: T): T`?

    A) A fixed type called T
    B) A placeholder for a type, decided when the function is used
    C) A keyword that turns off type checking
    D) A runtime value

    Correct answer: B

**Question 2**

    What is the type of `const x = [1, 2, 3].find(n => n > 5)`?

    A) number
    B) number[]
    C) number | undefined
    D) boolean

    Correct answer: C

**Question 3**

    Which declaration correctly describes exactly one string followed by one number?

    A) `(string | number)[]`
    B) `[string, number]`
    C) `Array<any>`
    D) `string[] | number[]`

    Correct answer: B

**Question 4 (short answer):** Why can't you write `new T()` inside a generic function?

Answer: Types, including `T`, are erased when TypeScript compiles to JavaScript, so `T` doesn't exist at runtime.

**Question 5 (short answer):** What does `T extends { id: number }` allow you to do inside the function that plain `T` doesn't?

Answer: Access `item.id` safely, because every valid `T` is guaranteed to have an `id`.

***

## STEP 9: CHECKPOINT & REBUILD FROM MEMORY

Close this lesson. Without looking back, write:

1. A generic class `Repository<T extends { id: number }>` with:
   - a private `items: T[]`
   - `add(item: T): void`
   - `getById(id: number): T | undefined`
   - `getAll(): readonly T[]`
2. A function `minMax(nums: number[]): [number, number]`
3. Test both: a `Repository<User>` and one call to `minMax`
4. In two sentences, in your own words: what problem do generics solve?

Send me your code and your two-sentence explanation. I'll review it and tell you whether you're ready for **Lesson 0.5**.

If any part of Collections or Generics still feels fuzzy, tell me which one before you start the checkpoint and I'll re-explain just that part.