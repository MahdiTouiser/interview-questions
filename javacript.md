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

