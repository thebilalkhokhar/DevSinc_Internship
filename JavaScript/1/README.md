### **1. Comparison Operators**

Comparison operators are used to compare two values. They return a **boolean** (`true` or `false`).

| Operator | Meaning                            | Example     | Result  |
| -------- | ---------------------------------- | ----------- | ------- |
| `==`     | Equal to (checks value only)       | `5 == "5"`  | `true`  |
| `===`    | Strict equal (checks value + type) | `5 === "5"` | `false` |
| `!=`     | Not equal to (value only)          | `5 != "6"`  | `true`  |
| `!==`    | Strict not equal (value + type)    | `5 !== "5"` | `true`  |
| `>`      | Greater than                       | `7 > 3`     | `true`  |
| `<`      | Less than                          | `2 < 10`    | `true`  |
| `>=`     | Greater than or equal              | `5 >= 5`    | `true`  |
| `<=`     | Less than or equal                 | `4 <= 3`    | `false` |

## ⚠️ **Tip:** Always prefer `===` and `!==` to avoid unexpected type coercion.

### **2. Functions**

A function is a reusable block of code that performs a specific task.

**Syntax:**

```js
function greet(name) {
  return `Hello, ${name}!`;
}

console.log(greet("Bilal")); // Output: Hello, Bilal!
```

Functions can:

- Take **parameters** (inputs)
- Return **values**
- Be **reused** in multiple places

---

### **3. Functions with Default Parameters**

Default parameters allow you to assign a default value to a parameter if no argument is provided.

**Example:**

```js
function greet(name = "Guest") {
  console.log(`Hello, ${name}!`);
}

greet(); // Hello, Guest!
greet("Bilal"); // Hello, Bilal!
```

If you don’t pass `name`, JavaScript uses the default `"Guest"`.

---

### **4. Callbacks**

A **callback** is a function passed as an argument to another function, which is then **executed later**.

**Example:**

```js
function processUserInput(callback) {
  const name = "Bilal";
  callback(name);
}

function greet(name) {
  console.log(`Hello, ${name}`);
}

processUserInput(greet); // Output: Hello, Bilal
```

Callbacks are essential for handling asynchronous operations like API calls or timers.

---

### **5. Higher-Order Functions**

A **higher-order function** either:

- Takes one or more functions as arguments, or
- Returns a function.

**Example:**

```js
function multiplier(factor) {
  return function (num) {
    return num * factor;
  };
}

const double = multiplier(2);
console.log(double(5)); // 10
```

Built-in examples include `map()`, `filter()`, and `reduce()` on arrays.

---

### **6. Arrays**

An **array** stores multiple values in a single variable.

**Example:**

```js
const fruits = ["apple", "banana", "mango"];
console.log(fruits[1]); // banana
```

**Common methods:**

- `push()` – add to end
- `pop()` – remove from end
- `shift()` – remove from start
- `unshift()` – add to start
- `map()`, `filter()`, `reduce()` – functional operations

---

### **7. Objects**

An **object** stores data as **key–value pairs**.

**Example:**

```js
const person = {
  name: "Bilal",
  age: 23,
  greet: function () {
    console.log("Hello!");
  },
};

console.log(person.name); // Bilal
person.greet(); // Hello!
```

Objects are used to represent real-world entities and structured data.

---

### **8. null vs undefined**

| Concept       | Meaning                            | Example                                 |
| ------------- | ---------------------------------- | --------------------------------------- |
| **undefined** | Variable declared but not assigned | `let x; console.log(x); // undefined`   |
| **null**      | Intentional empty value            | `let y = null; console.log(y); // null` |

**Key difference:**
`undefined` → absence of value **by default**
`null` → absence of value **intentionally set by developer**

---

### **9. truthy / falsy concept**

In JavaScript, every value is either **truthy** or **falsy** when evaluated in a boolean context.

**Falsy values (only 7):**

```
false, 0, -0, 0n, "", null, undefined, NaN
```

Everything else is **truthy**:

```
"hello", 123, [], {}, "false", function() {}
```

**Example:**

```js
if ("") console.log("Yes");
else console.log("No"); // Output: No (empty string is falsy)
```

---

---

### **Error Handling**

Error handling is about how JavaScript **detects and manages runtime errors** (when something goes wrong during execution).

If your code crashes, it can stop further execution — so you use **try...catch** blocks to handle errors gracefully.

**Example:**

```js
try {
  let result = 10 / 0;
  console.log(nonExistentVariable); // This will throw an error
} catch (error) {
  console.log("Something went wrong:", error.message);
} finally {
  console.log("This block always runs, error or not.");
}
```

**Explanation:**

- `try` → contains code that might cause an error
- `catch(error)` → handles the error if one occurs
- `finally` → runs regardless of whether an error occurred

Also, you can **manually throw errors**:

```js
throw new Error("Custom error message");
```

---

### **Hoisting in JavaScript**

Hoisting is JavaScript’s behavior of **moving declarations (not initializations)** to the top of their scope **before code execution**.

It means you can use variables or functions **before** they are declared — though this often leads to confusion.

**Example 1 (with variable):**

```js
console.log(a); // undefined
var a = 10;
```

Here, the declaration `var a` is hoisted, but its **value** (`10`) is not.

**Example 2 (with function):**

```js
greet(); // "Hello!"
function greet() {
  console.log("Hello!");
}
```

Function declarations are **fully hoisted**, so this works fine.

---

### **Variable and Function Hoisting**

Let’s separate them clearly:

#### **1. Variable Hoisting**

- **`var`** variables are **hoisted and initialized with `undefined`**.
- **`let`** and **`const`** are **hoisted but not initialized** (they stay in the _temporal dead zone_ until declared).

**Example:**

```js
console.log(x); // undefined
var x = 5;

console.log(y); // ReferenceError
let y = 10;
```

#### **2. Function Hoisting**

There are two kinds of functions in JS:

- **Function declarations** → Fully hoisted
- **Function expressions** → Not hoisted (because they behave like variables)

**Example:**

```js
// Works
sayHi();
function sayHi() {
  console.log("Hi!");
}

// Error
sayBye();
const sayBye = function () {
  console.log("Bye!");
};
```

---

### **Scope Chain and Lexical Scoping**

**Scope** defines where variables are accessible in code.
**Lexical scoping** means a variable’s scope is determined **by where it’s written in the code**, not by where it’s called from.

When you try to access a variable, JavaScript looks for it in this order (called the **scope chain**):

1. **Local scope** (inside current function)
2. **Outer (enclosing) functions**
3. **Global scope**

**Example:**

```js
let globalVar = "global";

function outer() {
  let outerVar = "outer";

  function inner() {
    let innerVar = "inner";
    console.log(innerVar); // found in inner scope
    console.log(outerVar); // found in outer scope
    console.log(globalVar); // found in global scope
  }

  inner();
}

outer();
```

If a variable isn’t found in any scope, JS throws a `ReferenceError`.

---

### **IIFE (Immediately Invoked Function Expression)**

An **IIFE** is a function that runs **immediately after it’s defined**.
It helps create a **private scope** and avoid polluting the global namespace.

**Syntax:**

```js
(function () {
  console.log("This runs instantly!");
})();
```

**Explanation:**

- The outer parentheses `()` make it an _expression_.
- The second `()` executes it immediately.

**With parameters:**

```js
(function (name) {
  console.log(`Hello, ${name}!`);
})("Bilal");
```

**Use cases:**

- Isolating variables (avoid conflicts)
- Initializing code right away
- Module pattern (before ES6 modules)

---
