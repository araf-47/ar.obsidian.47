
```typescript
// Java style:
// public int add(int a, int b) { return a + b; }

// TypeScript:
function add(a: number, b: number): number {
  return a + b;
}

// With arrow function (modern):
const multiply = (a: number, b: number): number => a * b;

// Function with optional parameter
function greet(name: string, greeting?: string): string {
  const msg = greeting || "Hello";
  return `${msg}, ${name}`;
}

greet("Araf");              // ✓ Works
greet("Araf", "Hi");        // ✓ Works
greet("Araf", 42);          // ❌ Error: 42 is not a string
```

***
# The explanation

An **optional parameter** in TypeScript is a parameter that a function caller can choose to provide or leave out.

The question mark (`?`) attached to `greeting?: string` tells TypeScript: **"The caller must provide a `name`, but passing a `greeting` is entirely optional."**

***

### 1. The Core Problem It Solves

Normally, TypeScript is very strict about function arguments. If you define a function with two parameters without `?`:

```typescript
function greet(name: string, greeting: string): string { ... }

```

TypeScript will give you a compiler error if you forget or don't want to pass the second argument:

```typescript
greet("Alice"); // ❌ Error: Expected 2 arguments, but got 1.

```

Adding `?` makes TypeScript allow both calls:

```typescript
greet("Alice", "Good morning"); // ✅ Allowed -> returns "Good morning, Alice"
greet("Alice");                  // ✅ Allowed -> returns "Hello, Alice"

```

***

### 2. What Happens Behind the Scenes?

When you mark a parameter with `?`:

1. **Its type automatically includes `undefined`:**
`greeting?: string` means the value inside the function will be either a `string` OR `undefined`.
2. **Handling the missing value:**
When the caller omits `greeting`, its value is `undefined`.
In your code:
```typescript
const msg = greeting || "Hello";

```


If `greeting` is undefined (or an empty string `""`), the `||` (OR) operator falls back to `"Hello"`.

***

### 3. Two Rules You Must Know

* **Optional parameters must come last:**
You cannot put an optional parameter before a required one because TypeScript wouldn't know which argument you omitted.
```typescript
// ❌ Invalid
function greet(greeting?: string, name: string) {}

// ✅ Valid
function greet(name: string, greeting?: string) {}

```


* **Default Parameters (A cleaner modern alternative):**
Instead of writing `greeting?: string` and checking it with `||`, JavaScript and TypeScript allow you to set a default value directly in the parameter list. It automatically makes the parameter optional:
```typescript
function greet(name: string, greeting: string = "Hello"): string {
  return `${greeting}, ${name}`;
}

```


Both approaches make the argument optional for the caller, but default parameters eliminate the need for manual fallback logic inside the function body.