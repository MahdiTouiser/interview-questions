# JavaScript Interview Questions

## ❓ Question 1: What is the difference between `undefined` and `null` in JavaScript?

### ✅ Answer:

- `undefined` means a variable has been declared but has not yet been assigned a value.
- `null` is an assignment value that represents "no value" or "nothing." It is intentionally set by the programmer.

### 🧠 Key Differences:

| Feature         | `undefined`                         | `null`                              |
|-----------------|-------------------------------------|--------------------------------------|
| Type            | `undefined`                         | `object`                             |
| Default Value   | Yes, default for uninitialized vars | No, must be explicitly assigned      |
| Usage Context   | Uninitialized vars, missing params  | Intentional absence of value         |
| Equality        | `undefined == null` → `true`        | `undefined === null` → `false`       |

### 💡 Example:

```js
let a;
console.log(a); // undefined

let b = null;
console.log(b); // null
```


## ❓ Question 2: What is the difference between `var`, `let`, and `const` in JavaScript?

### ✅ Answer:

| Feature           | `var`                          | `let`                           | `const`                         |
|-------------------|--------------------------------|----------------------------------|----------------------------------|
| Scope             | Function-scoped                | Block-scoped                    | Block-scoped                    |
| Hoisting          | Yes (initialized as `undefined`) | Yes (but not initialized)       | Yes (but not initialized)       |
| Reassignment      | Allowed                        | Allowed                          | ❌ Not allowed                   |
| Redeclaration     | Allowed                        | ❌ Not allowed (in same scope)   | ❌ Not allowed                   |
| Temporal Dead Zone| No                             | Yes                              | Yes                              |

### 💡 Example:

```js
function test() {
  if (true) {
    var x = 10;
    let y = 20;
    const z = 30;

    console.log("Inside block:");
    console.log("x:", x); // 10
    console.log("y:", y); // 20
    console.log("z:", z); // 30
  }

  console.log("Outside block:");
  console.log("x:", x); // 10 (accessible — var is function-scoped)
  console.log("y:", typeof y); // undefined (ReferenceError in real code — let is block-scoped)
  console.log("z:", typeof z); // undefined (ReferenceError in real code — const is block-scoped)
}

test();

```


## ❓ Question 3: Explain the concept of closure in JavaScript.

### ✅ Answer:

A **closure** is created when a function remembers and has access to variables from its **outer (enclosing) function scope**, even after the outer function has finished executing.

In simpler terms, a closure gives you access to an outer function’s variables from an inner function — even after the outer function has returned.

### 💡 Example:

```js
function outer() {
  let count = 0;

  return function inner() {
    count++;
    console.log(count);
  };
}

const counter = outer();
counter(); // 1
counter(); // 2
counter(); // 3
```

## ❓ Question: Is JavaScript async by itself? If not, how does it get handled?

### ✅ Answer:

No, JavaScript is not inherently asynchronous. It is **single-threaded**, meaning it executes code **sequentially** (one line at a time) on a single thread. However, JavaScript provides **asynchronous mechanisms** that allow it to perform non-blocking operations like fetching data, timers, and handling events.

### 🧠 How It Gets Handled:

1. **Event Loop**: JavaScript uses the **event loop** to handle asynchronous code. When an asynchronous operation (like a network request or a timer) is encountered, the event loop allows the program to continue executing other tasks while waiting for the operation to complete.

2. **Call Stack**: The call stack contains the functions that are currently being executed. Synchronous code runs on the call stack. When asynchronous operations are encountered, they are pushed to the **callback queue** and then executed after the synchronous code finishes.

3. **Web APIs**: These are built-in features of the browser (or Node.js environment) that allow asynchronous operations. For example, `setTimeout()`, `fetch()`, and `addEventListener()` are Web APIs that handle tasks like waiting for a timer or making network requests without blocking the main thread.

4. **Promises**: Promises are an abstraction for handling asynchronous operations. They are used to handle eventual completion (or failure) of asynchronous tasks in a more readable way, avoiding "callback hell."

5. **Async/Await**: `async` and `await` are syntactic sugar built on top of promises. They allow you to write asynchronous code in a way that looks and behaves like synchronous code, making it easier to manage.

### 💡 Example (Async with setTimeout and Promise):

```js
console.log("Start");

setTimeout(() => {
  console.log("Async operation complete");
}, 1000);

console.log("End");
```
