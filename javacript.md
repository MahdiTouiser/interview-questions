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

## ❓ Question 4: Is JavaScript async by itself? If not, how does it get handled?

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
console.log('Start');

setTimeout(() => {
  console.log('Timeout 1');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise 1');
}).then(() => {
  console.log('Promise 2');
});

setTimeout(() => {
  console.log('Timeout 2');
}, 0);

console.log('End');


answers :
Start
End
Promise 1
Promise 2
Timeout 1
Timeout 2

```

## ❓ Question 5: What are the differences between regular functions and arrow functions in JavaScript?

### ✅ Answer:

In JavaScript, both **regular functions** and **arrow functions** are used to define functions, but they have several key differences in behavior.

### 🧠 Key Differences:

| Feature                  | **Regular Function**                               | **Arrow Function**                              |
|--------------------------|----------------------------------------------------|-------------------------------------------------|
| **Syntax**               | `function foo() { ... }`                         | `const foo = () => { ... }`                    |
| **`this` Binding**       | Binds its own `this` (depends on how the function is called) | Does not bind its own `this`; inherits it from the surrounding scope (lexical scoping) |
| **Arguments Object**     | Has an `arguments` object that contains all passed parameters | Does not have its own `arguments` object        |
| **Constructor**          | Can be used as a constructor with `new` keyword   | Cannot be used as a constructor (throws an error) |
| **Method of an Object**  | Can be used as a method within an object          | Cannot be used as a method of an object (because `this` would not refer to the object) |
| **Return Value**         | Must use `return` explicitly if needed            | Implicit return for single expression functions |
| **Hoisting**             | Hoisted to the top of the scope (can be called before declaration) | Not hoisted (must be defined before use)        |

### 💡 Examples:

1. **Regular Function:**

```js
function regularFunction() {
  console.log(this); // 'this' is bound to the object or context that calls the function
}

const obj = { 
  name: 'John',
  greet: regularFunction
};
obj.greet(); // 'this' refers to 'obj' here


const arrowFunction = () => {
  console.log(this); // 'this' is inherited from the surrounding scope
};

const obj = { 
  name: 'John',
  greet: arrowFunction
};
obj.greet(); // 'this' refers to the surrounding context (likely window or global object in non-strict mode)


const add = (a, b) => a + b;  // Returns the result of a + b implicitly
console.log(add(2, 3)); // 5

```

## ❓ Question 6: What is the difference between value types and reference types in JavaScript?

### ✅ Answer:

In JavaScript, data types are divided into two categories: **value types** and **reference types**. Understanding the distinction between these types is crucial because it affects how values are stored, passed, and manipulated in memory.

### 🧠 Key Differences:

| Feature                | **Value Types**                               | **Reference Types**                              |
|------------------------|-----------------------------------------------|--------------------------------------------------|
| **Types**              | Primitive types: `undefined`, `null`, `boolean`, `number`, `bigint`, `string`, `symbol` | Objects: `Object`, `Array`, `Function`, `Date`, etc. |
| **Storage**            | Stored directly in memory                      | Stored as a reference to the memory location     |
| **Assignment Behavior**| When assigned, a **copy** of the value is created | When assigned, a **reference** to the original object is created |
| **Passing to Functions**| Passed by **value** — a copy of the data is passed | Passed by **reference** — a reference to the original object is passed |
| **Immutability**       | Immutable — the value cannot be changed after being assigned | Mutable — the properties or elements of the object can be modified |
| **Equality**           | Comparison is based on the actual value | Comparison is based on memory location (reference) |

### 💡 Examples:

1. **Value Types:**

```js
let x = 10;
let y = x; // Copy of the value is made

x = 20; // Changes 'x', but 'y' remains unchanged

console.log(x); // 20
console.log(y); // 10

let obj1 = { name: 'Alice' };
let obj2 = obj1; // Reference to the same object in memory

obj1.name = 'Bob'; // Modifies the original object

console.log(obj1.name); // 'Bob'
console.log(obj2.name); // 'Bob'
```
## ❓ Question 7: What are the heap and memory in JavaScript?

### ✅ Answer:

In JavaScript, memory management is crucial for understanding how values are stored and how they are managed in the context of execution. **Heap** is a part of the memory structure, and understanding it helps in optimizing performance and preventing memory leaks.

### 🧠 Memory in JavaScript:

JavaScript uses two types of memory for storing data: the **stack** and the **heap**. 

- **Stack Memory**: 
  - Used for storing **primitive** data types (such as `number`, `string`, `boolean`, etc.).
  - It operates in a **Last In, First Out (LIFO)** order.
  - Each time a function is called, a new memory block is added to the stack. When the function finishes, the memory is cleared.
  - **Fixed-size** and **fast** memory storage.

- **Heap Memory**: 
  - Used for storing **reference** types (such as `objects`, `arrays`, `functions`, etc.).
  - It operates on a **dynamic allocation** system, meaning memory is allocated when needed and released when no longer in use.
  - Heap memory is **larger** and **slower** than stack memory because it allows for more complex data structures like objects and arrays.

### 🧠 Heap vs. Stack:

| Feature                  | **Stack**                                      | **Heap**                                     |
|--------------------------|------------------------------------------------|----------------------------------------------|
| **Used for**             | Primitive types (`number`, `boolean`, `string`) | Reference types (`objects`, `arrays`, `functions`) |
| **Memory Allocation**    | Static and fixed size                          | Dynamic allocation (can grow or shrink)      |
| **Storage**              | Fast, but limited in size                     | Larger, but slower                          |
| **LIFO** (Last In, First Out) | Yes                                          | No                                           |
| **Lifetime**             | Tied to the execution context (function calls) | Until the object is no longer referenced (garbage collection) |
| **Speed**                | Very fast                                      | Slower compared to stack                    |

### 💡 Example of Stack and Heap:

1. **Stack Example (Primitive Types)**:

```js
let a = 5;  // Stored in stack
let b = a;  // Copy of 'a' is made in stack

a = 10;  // 'a' is updated, but 'b' remains 5
console.log(a); // 10
console.log(b); // 5

2. **Heap Example (Reference Types)**:
let obj1 = { name: 'John' };  // Stored in heap
let obj2 = obj1;              // Both obj1 and obj2 point to the same memory location in the heap

obj1.name = 'Jane';  // Both 'obj1' and 'obj2' are modified

console.log(obj1.name); // 'Jane'
console.log(obj2.name); // 'Jane'

```
