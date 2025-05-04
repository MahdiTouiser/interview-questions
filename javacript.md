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
```


2. **Heap Example (Reference Types)**:
```js

let obj1 = { name: 'John' };  // Stored in heap
let obj2 = obj1;              // Both obj1 and obj2 point to the same memory location in the heap

obj1.name = 'Jane';  // Both 'obj1' and 'obj2' are modified

console.log(obj1.name); // 'Jane'
console.log(obj2.name); // 'Jane'

```

## ❓ Question 8: What is Garbage Collection and Memory Leak in JavaScript?

### ✅ Answer:

In JavaScript, **garbage collection** is a mechanism that automatically manages memory by removing objects that are no longer needed or accessible. **Memory leaks** occur when memory is not properly released, causing the application to consume more memory over time, which can lead to performance issues.

### 🧠 **Garbage Collection in JavaScript**:

Garbage collection is the process of **automatically** identifying and cleaning up objects that are no longer reachable or referenced by the program. JavaScript engines, such as V8 (used by Chrome and Node.js), use **automatic memory management** to handle this process.

#### How Garbage Collection Works:
1. **Reachability**:
   - JavaScript identifies objects that are **reachable**, meaning they can still be accessed by the program. If an object is no longer reachable (i.e., no references point to it), it becomes eligible for garbage collection.
   
2. **Mark-and-Sweep Algorithm**:
   - The **Mark-and-Sweep** algorithm is the most common garbage collection technique used in JavaScript.
     1. **Mark**: The garbage collector starts from the root objects (global objects, local variables, etc.) and marks all objects that can be reached from there.
     2. **Sweep**: Once marking is complete, the garbage collector sweeps through memory, clearing all unmarked objects (those that are no longer reachable).

3. **Memory Management**:
   - When an object becomes unreachable, the memory allocated to it is freed, making space for new objects.

### 💡 Example of Garbage Collection:

```js
function createObject() {
  let obj = { name: 'Alice' };  // 'obj' is a reference to an object
  return obj;
}

let ref = createObject();  // 'ref' holds a reference to the object
ref = null;  // 'ref' no longer holds the reference, making the object eligible for GC
```

## ❓ Question: What is Hoisting in JavaScript?

### ✅ Answer:

**Hoisting** is a JavaScript mechanism where **variable and function declarations** are moved to the top of their containing scope during the compile phase, before the code has been executed. However, only the declarations are hoisted, not the initializations.

### 🧠 Key Points of Hoisting:

- **Variable Hoisting**:
  - **`var`** declarations are hoisted and initialized with `undefined`.
  - **`let`** and **`const`** declarations are hoisted but not initialized, meaning they enter a **temporal dead zone** (TDZ) where they cannot be accessed before their declaration is executed.

- **Function Hoisting**:
  - **Function declarations** are hoisted completely (both the declaration and the body) to the top of their scope.
  - **Function expressions** (including arrow functions) are **not hoisted** in the same way and are treated like variables.

### 🧠 Examples of Hoisting:

```js
console.log(x); // undefined
var x = 5;
console.log(x); // 5

console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 10;

foo(); // "Hello"
function foo() {
  console.log("Hello");
}

baz(); // TypeError: baz is not a function
var baz = () => {
  console.log("Arrow function");
};


bar(); // TypeError: bar is not a function
var bar = function() {
  console.log("World");
};

```
## ❓ Question 9: What is a Promise in JavaScript, and how do the methods like `Promise.all()`, `Promise.race()`, and `Promise.allSettled()` work?

### ✅ Answer:

A **Promise** in JavaScript is an object representing the eventual completion (or failure) of an asynchronous operation and its resulting value. It allows you to write asynchronous code in a more readable manner, without the "callback hell."

Promises have three states:
1. **Pending**: The promise is still in progress.
2. **Fulfilled**: The promise has been completed successfully.
3. **Rejected**: The promise has failed.

### 🧠 **Creating a Promise**:

You can create a promise using the `new Promise()` constructor, which takes a function called the *executor* as an argument. This function receives two parameters: `resolve` (for fulfilling the promise) and `reject` (for rejecting the promise).

```js
const myPromise = new Promise((resolve, reject) => {
  const success = true;
  
  if (success) {
    resolve('Promise fulfilled');
  } else {
    reject('Promise rejected');
  }
});

```
### 🧠 Promise Methods:

```js
myPromise.then(result => {
  console.log(result);  // "Promise fulfilled"
}).catch(error => {
  console.log(error);  // Handle rejection if any
});

myPromise.catch(error => {
  console.log(error);  // "Promise rejected"
});

myPromise.finally(() => {
  console.log('Promise completed');  // Runs regardless of promise outcome
});


```

### 🧠 Promise Static Methods:
`Promise.all()` takes an iterable (usually an array) of promises and returns a single promise. This promise resolves when all promises in the iterable are resolved, or rejects if any of the promises in the array is rejected.
```js
const promise1 = Promise.resolve(3);
const promise2 = new Promise((resolve, reject) => setTimeout(resolve, 100, 'foo'));
const promise3 = 42;

Promise.all([promise1, promise2, promise3])
  .then(values => {
    console.log(values);  // [3, "foo", 42]
  })
  .catch(error => {
    console.log(error);  // If any promise is rejected, it enters this block
  });


```
If any of the promises rejects, the entire `Promise.all()` call rejects immediately with that error.

---

`Promise.allSettled()` returns a promise that resolves after all of the given promises have either been fulfilled or rejected. It always resolves with an array of objects that describe the outcome of each promise.
```js

const promise1 = Promise.resolve(3);
const promise2 = new Promise((resolve, reject) => setTimeout(reject, 100, 'Error'));
const promise3 = Promise.resolve(42);

Promise.allSettled([promise1, promise2, promise3])
  .then(results => {
    console.log(results);
    // [
    //   { status: "fulfilled", value: 3 },
    //   { status: "rejected", reason: "Error" },
    //   { status: "fulfilled", value: 42 }
    // ]
  });
```
Unlike `Promise.all()`, `Promise.allSettled()` does not reject if any of the promises fail. It returns the outcome of each promise.

---

`Promise.race()` takes an iterable of promises and returns a promise that resolves or rejects as soon as one of the promises resolves or rejects, whichever happens first.
```js
const promise1 = new Promise((resolve, reject) => setTimeout(resolve, 100, 'First'));
const promise2 = new Promise((resolve, reject) => setTimeout(resolve, 50, 'Second'));

Promise.race([promise1, promise2])
  .then(result => {
    console.log(result);  // "Second" (because promise2 resolves first)
  })
  .catch(error => {
    console.log(error);
  });
```

`Promise.race()` resolves or rejects as soon as the first promise settles, making it useful for scenarios like timeouts.

---

### 🧠 Summary:
`Promise.all()`: Resolves when all promises are fulfilled or rejects if any promise is rejected.

`Promise.allSettled()`: Resolves when all promises are settled (fulfilled or rejected) and returns the outcome of each promise.

`Promise.race()`: Resolves as soon as the first promise settles, either resolved or rejected.

`then()`: Handles the fulfillment of a promise.

`catch()`: Handles the rejection of a promise.

`finally()`: Executes code after the promise is settled, regardless of the outcome.


## ❓ Question 10: What is the difference between `setTimeout()` and `setInterval()` in JavaScript?

### ✅ Answer:

Both `setTimeout()` and `setInterval()` are timing functions used to schedule asynchronous operations, but they behave differently.

---

### ⏱ `setTimeout()`

- Executes a function **once** after a specified delay.
- Returns a timeout ID that can be used with `clearTimeout()`.

#### 💡 Example:

```js
console.log("Start");

setTimeout(() => {
  console.log("This runs after 2 seconds");
}, 2000);

console.log("End");
```
---

### 🔁 setInterval()
- Repeatedly executes a function every specified interval.
- Returns an interval ID that can be used with `clearInterval()`.

### 💡 Example:


```js
let count = 0;

const intervalId = setInterval(() => {
  count++;
  console.log(`Interval count: ${count}`);
  
  if (count === 3) {
    clearInterval(intervalId); // Stops after 3 executions
  }
}, 1000);

```

| Feature       | `setTimeout()`     | `setInterval()`        |
| ------------- | ------------------ | ---------------------- |
| Runs          | Once after delay   | Repeats every interval |
| Cancel method | `clearTimeout(id)` | `clearInterval(id)`    |
| Use case      | Delayed task       | Repeated task          |

---

 ## ❓ Question 11 : What is Implicit and Explicit Type Coercion in JavaScript?

### ✅ Answer:

**Type coercion** in JavaScript refers to the automatic or manual conversion of values from one data type to another (like string to number, boolean to string, etc.).

---

### 🔄 Implicit Type Coercion

JavaScript automatically converts types during operations when needed. This is also known as **type conversion behind the scenes**.

#### 💡 Examples:

```js
console.log("5" + 2);      // "52" (number 2 is converted to string)
console.log("5" - 2);      // 3   (string "5" is converted to number)
console.log(true + 1);     // 2   (true is converted to 1)
console.log(false == 0);   // true (false is coerced to 0)
```
+ triggers string conversion when one operand is a string.
-, *, / convert both operands to numbers.

---

### ✋ Explicit Type Coercion
You manually convert one data type to another using built-in functions like Number(), String(), or Boolean().

### 💡 Examples:
```js
console.log(Number("123"));     // 123
console.log(String(123));       // "123"
console.log(Boolean(0));        // false
console.log(Boolean("hello"));  // true
```
| Coercion Type | Triggered By             | Example           |
| ------------- | ------------------------ | ----------------- |
| Implicit      | JavaScript engine (auto) | `"5" + 1 → "51"`  |
| Explicit      | Developer (manual)       | `Number("5") → 5` |

---
## ❓ Question 12: What is the difference between `bind()`, `call()`, and `apply()` in JavaScript?

### ✅ Answer:

All three methods — `bind()`, `call()`, and `apply()` — are used to **explicitly set the `this` context** of a function in JavaScript.

---

### 🔗 `bind()`

- Returns a **new function** with the specified `this` value.
- Does **not** invoke the function immediately.

#### 💡 Example:
```js
const user = { name: "Alice" };

function greet(greeting) {
  return `${greeting}, ${this.name}`;
}

const greetAlice = greet.bind(user);
console.log(greetAlice("Hello")); // "Hello, Alice"
```

### ☎️ `call()` 
- Invokes the function immediately, with this and arguments passed individually.
```js
const user = { name: "Bob" };

function greet(greeting) {
  console.log(`${greeting}, ${this.name}`);
}

greet.call(user, "Hi"); // "Hi, Bob"
```

### 📞 `apply()` 
- Invokes the function immediately, like call(), but arguments are passed as an array.
```js
const user = { name: "Charlie" };

function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

greet.apply(user, ["Hey", "!"]); // "Hey, Charlie!"
```
| Method    | Invokes Immediately? | Arguments Format | Returns      |
| --------- | -------------------- | ---------------- | ------------ |
| `bind()`  | ❌ No                 | Individually     | New function |
| `call()`  | ✅ Yes                | Individually     | Return value |
| `apply()` | ✅ Yes                | Array            | Return value |


---


## ❓ Question 13: What is the `reduce()` method in JavaScript?

### ✅ Answer:

The `reduce()` method executes a **reducer function** on each element of the array, resulting in a **single output value**.

---

### 🔧 Syntax:

```js
array.reduce((accumulator, currentValue, index, array) => {
  // return updated accumulator
}, initialValue);
```
accumulator: Accumulates the return values.

currentValue: Current element being processed.

initialValue: (Optional) Initial value for the accumulator.

### Example :
```js
const numbers = [1, 2, 3, 4];

const sum = numbers.reduce((acc, curr) => acc + curr, 0);

console.log(sum); // 10
```

---

## ❓ Question 14: What is a Higher-Order Function (HOF) in JavaScript?

### ✅ Answer:

A **Higher-Order Function (HOF)** is a function that either:

1. **Takes one or more functions as arguments**, or
2. **Returns a function as its result**.

This enables powerful patterns like function composition, callbacks, and currying.

---

### 💡 Example 1: A Function That Takes Another Function as an Argument

```js
function greet(name) {
  return `Hello, ${name}`;
}

function processUser(name, callback) {
  return callback(name);
}

console.log(processUser("Alice", greet)); // "Hello, Alice"
```

### 💡 Example 2: A Function That Returns Another Function
```js
function multiplier(factor) {
  return function (number) {
    return number * factor;
  };
}

const double = multiplier(2);
console.log(double(5)); // 10
```
### ✅ Built-in Higher-Order Functions in JavaScript:
Array.prototype.map()

Array.prototype.filter()

Array.prototype.reduce()

Array.prototype.forEach()

| Feature                 | Description                                      |
| ----------------------- | ------------------------------------------------ |
| Takes function as input | Yes                                              |
| Returns function        | Yes                                              |
| Used for                | Reusability, composition, abstraction            |
| Examples                | `map`, `filter`, `reduce`, custom callback funcs |


---


## ❓ Question 15: What is an IIFE (Immediately Invoked Function Expression) in JavaScript?

### ✅ Answer:

An **IIFE** (Immediately Invoked Function Expression) is a function that is **defined and executed immediately** after its creation.

It is often used to create a private scope and avoid polluting the global namespace.

---

### 🔧 Syntax:

```js
(function () {
  // code inside this function runs immediately
})();
```

OR 

```js

(() => {
  // code runs immediately
})();

```
### Example :

```js
(function () {
  const message = "This runs immediately!";
  console.log(message);
})();

// Output: This runs immediately!

```

| Feature              | Description                             |
| -------------------- | --------------------------------------- |
| Stands for           | Immediately Invoked Function Expression |
| Purpose              | Encapsulation, private scope            |
| Executed Immediately | Yes                                     |
| Uses                 | Avoid global scope pollution            |


---

## ❓ Question 16: What are Generator Functions in JavaScript?

### ✅ Answer:

A **Generator function** is a special type of function in JavaScript that can be **paused and resumed**, allowing you to generate values on demand.

They are defined using the `function*` syntax and use the `yield` keyword to pause execution.

---

### 🔧 Syntax:

```js
function* generatorFunc() {
  yield value1;
  yield value2;
  // ...
}
```

### To run the generator, you call it and use `.next()` :
const gen = generatorFunc();
gen.next(); // { value: value1, done: false }
gen.next(); // { value: value2, done: false }
gen.next(); // { value: undefined, done: true }

```js
###function* countToThree() {
  yield 1;
  yield 2;
  yield 3;
}

const counter = countToThree();

console.log(counter.next()); // { value: 1, done: false }
console.log(counter.next()); // { value: 2, done: false }
console.log(counter.next()); // { value: 3, done: false }
console.log(counter.next()); // { value: undefined, done: true }
```

## ❓ Question 17: What are `Set` and `Map` in JavaScript?

### ✅ Answer:

In JavaScript, `Set` and `Map` are built-in data structures introduced in ES6 to handle **collections of values** more efficiently and flexibly than plain objects or arrays.

---

## 🔷 `Set`

A `Set` is a **collection of unique values**. It automatically removes duplicates.

### 🔧 Syntax:

```js
const mySet = new Set([1, 2, 3, 3, 4]);
console.log(mySet); // Set(4) { 1, 2, 3, 4 }
```

| Method          | Description                    |
| --------------- | ------------------------------ |
| `add(value)`    | Adds a new value               |
| `delete(value)` | Removes a value                |
| `has(value)`    | Checks if a value exists       |
| `clear()`       | Removes all elements           |
| `size`          | Returns the number of elements |

### Example :

``` js
const ids = new Set();
ids.add(1);
ids.add(2);
ids.add(1); // Duplicate, ignored
console.log(ids); // Set { 1, 2 }
```

### 🔶 Map
A Map is a collection of key-value pairs where keys can be any type (not just strings).
```js
const myMap = new Map();
myMap.set('name', 'Alice');
myMap.set(1, 'One');
console.log(myMap); // Map(2) { 'name' => 'Alice', 1 => 'One' }

```

| Method            | Description                    |
| ----------------- | ------------------------------ |
| `set(key, value)` | Adds or updates a value by key |
| `get(key)`        | Gets the value for a given key |
| `has(key)`        | Checks if a key exists         |
| `delete(key)`     | Removes a key-value pair       |
| `clear()`         | Clears all entries             |
| `size`            | Returns the number of entries  |


### Example :
```js

const user = new Map();
user.set('name', 'Bob');
user.set('age', 25);

console.log(user.get('name')); // Bob
console.log(user.has('age'));  // true

```

| Feature   | `Set`                        | `Map`                        |
| --------- | ---------------------------- | ---------------------------- |
| Stores    | Unique values                | Key-value pairs              |
| Keys      | Not applicable               | Can be any type              |
| Order     | Insertion order is preserved | Insertion order is preserved |
| Iteration | `for...of`, `.forEach()`     | `for...of`, `.forEach()`     |

---

## ❓ Question 17: What is the `this` keyword in JavaScript?

### ✅ Answer:

In JavaScript, the `this` keyword refers to the **execution context** of a function, meaning it determines what "object" the function is a method of or what context the function is being executed in. It is used to access properties or methods of the current object.

### 🧠 Key Points:

1. **Global Context**: In the global scope, `this` refers to the global object (`window` in browsers).
2. **Object Context**: Inside a method, `this` refers to the object the method is a property of.
3. **Function Context**: Inside a regular function, `this` refers to the global object (`window` in browsers) in non-strict mode, and `undefined` in strict mode.
4. **Arrow Functions**: Arrow functions **do not** have their own `this` and inherit it from the surrounding (lexical) context.

---

### 🏠 `this` in Global Context

In the global execution context (outside of any function or object), `this` refers to the global object.

```js
console.log(this); // In a browser, this will refer to the `window` object
```


### 🧑‍💻 this in Object Context
Inside an object method, this refers to the object that the method is a part of.
```js
const person = {
  name: "Alice",
  greet: function () {
    console.log(`Hello, ${this.name}`);
  }
};

person.greet(); // "Hello, Alice"
```
In this case, this inside the greet method refers to the person object.

---
### 🔄 this in Regular Function Context
In regular functions (not inside an object), this refers to the global object (window in browsers) in non-strict mode.
```js
function showThis() {
  console.log(this); // In non-strict mode, this refers to the global object (window in browsers)
}

showThis();
```
### 🏃 this in Constructor Functions
When using constructor functions to create new objects, this refers to the new instance being created.
```js
function Person(name) {
  this.name = name;
}

const alice = new Person("Alice");
console.log(alice.name); // "Alice"

```
In this case, this refers to the newly created alice object.

| Context                       | `this` refers to                                              |
| ----------------------------- | ------------------------------------------------------------- |
| Global Scope                  | The global object (`window` in browsers, `global` in Node.js) |
| Object Method                 | The object the method is a property of                        |
| Regular Function              | The global object (or `undefined` in strict mode)             |
| Constructor Function          | The newly created object                                      |
| Arrow Functions               | Inherited `this` from the surrounding context                 |
| `bind()`, `call()`, `apply()` | Explicitly sets the value of `this`                           |


---

## ❓ Question 18: What is the difference between `Object.seal()` and `Object.freeze()` in JavaScript?

### ✅ Answer:

Both `Object.seal()` and `Object.freeze()` are used to control the mutability of objects in JavaScript, but they have different levels of restriction.

---

### 🔒 `Object.seal()`

- **Prevents adding or removing properties** from the object.
- **Allows modification of existing property values** (if writable).
- Existing properties become **non-configurable** (cannot be deleted or reconfigured).

#### 💡 Example:

```js
const user = {
  name: "Alice"
};

Object.seal(user);

user.name = "Bob";     // ✅ Allowed
user.age = 25;         // ❌ Not added
delete user.name;      // ❌ Not deleted

console.log(user);     // { name: "Bob" }
```
### Object.freeze()
Prevents adding, removing, or modifying properties.
All existing properties become non-configurable and non-writable.
Makes the object completely immutable (shallow freeze).

```js
const user = {
  name: "Alice"
};

Object.freeze(user);

user.name = "Bob";     // ❌ Not changed
user.age = 25;         // ❌ Not added
delete user.name;      // ❌ Not deleted

console.log(user);     // { name: "Alice" }
```

| Feature                          | `Object.seal()`         | `Object.freeze()` |
| -------------------------------- | ----------------------- | ----------------- |
| Add new properties               | ❌ Not allowed           | ❌ Not allowed     |
| Delete properties                | ❌ Not allowed           | ❌ Not allowed     |
| Modify existing properties       | ✅ Allowed (if writable) | ❌ Not allowed     |
| Make properties non-configurable | ✅ Yes                   | ✅ Yes             |
| Make properties non-writable     | ❌ No                    | ✅ Yes             |
| Shallow or deep                  | Shallow                 | Shallow           |


---

## ❓ Question 19: What is the difference between **shallow clone** and **deep clone** in JavaScript?

### ✅ Answer:

Cloning an object means creating a new object with the same properties as the original. The difference between **shallow** and **deep** cloning lies in how nested objects are handled.

---

### 🧪 Shallow Clone

- Copies only the **top-level** properties.
- If a property is a **reference (like an object or array)**, only the reference is copied, **not the actual nested object**.
- Changes to nested objects affect the original.

#### 💡 Example (Shallow Clone):

```js
const original = {
  name: "Alice",
  address: {
    city: "Paris"
  }
};

const shallowCopy = { ...original };

shallowCopy.name = "Bob";                // ✅ Independent
shallowCopy.address.city = "London";     // 🔴 Affects `original.address.city`

console.log(original.address.city);      // "London"
```

### ✅ Common Shallow Clone Methods
```js
const copy1 = Object.assign({}, original);
const copy2 = { ...original };
```

### 🔁 Deep Clone
Recursively copies all levels of the object.
Ensures nested objects or arrays are also cloned.
Changes to nested objects do not affect the original.

```js
const original = {
  name: "Alice",
  address: {
    city: "Paris"
  }
};

// Deep clone using structuredClone (ES2021+)
const deepCopy = structuredClone(original);

deepCopy.address.city = "London";

console.log(original.address.city); // "Paris" ✅ Original is unaffected
```

| Feature            | Shallow Clone           | Deep Clone                     |
| ------------------ | ----------------------- | ------------------------------ |
| Top-level copy     | ✅ Yes                   | ✅ Yes                          |
| Nested object copy | ❌ No (shared reference) | ✅ Yes (fully independent)      |
| Performance        | ⚡ Faster                | 🐢 Slower (recursive)          |
| Use cases          | Simple objects          | Complex/nested data structures |


---


