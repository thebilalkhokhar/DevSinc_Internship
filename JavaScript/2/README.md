### **"use strict" mode**

`"use strict"` is a directive that tells JavaScript to **run in strict mode** — a more disciplined version of JS that helps catch errors early and prevents unsafe practices.

**How to enable it:**

```js
"use strict";
x = 10; // ❌ Error: x is not defined
```

Without strict mode, this would silently create a **global variable**, which can cause bugs.

**Key effects of strict mode:**

1. You must declare variables (`let`, `const`, or `var`).
2. You can’t delete variables or functions.
3. Duplicate parameter names are not allowed.
4. `this` inside a function (if not in an object) becomes `undefined` instead of the global object.
5. Reserved keywords are protected for future use (like `implements`, `interface`).

**Example:**

```js
"use strict";

function test() {
  console.log(this); // undefined (not window)
}
test();
```

✅ **Best practice:** Always use `"use strict"` at the top of your scripts or functions.

---

### **Closures in JavaScript**

A **closure** is created when a function “remembers” the variables from its outer scope — even after that outer function has finished executing.

**Example:**

```js
function outer() {
  let count = 0;

  function inner() {
    count++;
    console.log(count);
  }

  return inner;
}

const counter = outer();
counter(); // 1
counter(); // 2
counter(); // 3
```

Here:

- `outer()` returns `inner`.
- `inner()` still has access to `count`, even though `outer()` is done running.

**Why closures are useful:**

- Data privacy (encapsulation)
- Remembering state (like counters)
- Event handlers and callbacks

---

### **Bind() method**

The `.bind()` method lets you **manually control the value of `this`** inside a function.

**Syntax:**

```js
functionName.bind(thisArg, arg1, arg2, ...)
```

It returns a **new function** with a permanently bound `this`.

**Example:**

```js
const person = {
  name: "Bilal",
  greet: function () {
    console.log("Hello, " + this.name);
  },
};

const greetFunc = person.greet;
greetFunc(); // ❌ "Hello, undefined"

const boundGreet = person.greet.bind(person);
boundGreet(); // ✅ "Hello, Bilal"
```

**Why use it:**

- To fix `this` in callbacks or event handlers.
- Common in React class components (`this.handleClick = this.handleClick.bind(this)`).

---

### **this keyword**

`this` refers to **the object that is currently executing the function.**
Its value depends on **how** a function is called — not where it’s defined.

**Rules of `this`:**

1. **Global context**

   ```js
   console.log(this); // window (in browsers)
   ```

2. **Inside an object method**

   ```js
   const user = {
     name: "Bilal",
     greet() {
       console.log(this.name);
     },
   };
   user.greet(); // Bilal
   ```

3. **Standalone function**

   ```js
   function show() {
     console.log(this);
   }
   show(); // undefined in strict mode, window otherwise
   ```

4. **Arrow functions**
   Arrow functions **don’t have their own `this`**.
   They inherit it from their lexical (outer) scope.

   ```js
   const obj = {
     name: "Bilal",
     arrow: () => console.log(this.name),
   };
   obj.arrow(); // undefined (this = global)
   ```

5. **Constructor functions**

   ```js
   function Person(name) {
     this.name = name;
   }
   const p = new Person("Bilal");
   console.log(p.name); // Bilal
   ```

---

### **Iterators and Generators**

#### **Iterators**

An **iterator** is an object that allows you to **traverse (loop through)** a collection, one element at a time.

It has a `.next()` method that returns `{ value, done }`.

**Example:**

```js
const numbers = [1, 2, 3];
const iterator = numbers[Symbol.iterator]();

console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: 3, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

You can also use iterators **automatically** with:

```js
for (let num of numbers) {
  console.log(num);
}
```

---

#### **Generators**

A **generator** is a special function that can **pause and resume execution** using the `yield` keyword.

**Syntax:**

```js
function* generatorFunc() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = generatorFunc();
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
console.log(gen.next()); // { value: 3, done: false }
console.log(gen.next()); // { value: undefined, done: true }
```

**Why use generators:**

- For lazy evaluation (generate data on demand)
- For handling asynchronous code (pre-Promises era)
- To pause long-running computations

---

---

### **1. Classes, Objects, and Inheritance**

#### **Objects**

Objects are collections of key–value pairs that store data and behavior together.

**Example:**

```js
const person = {
  name: "Bilal",
  age: 23,
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  },
};

person.greet(); // Hello, my name is Bilal
```

---

#### **Classes**

Classes are **blueprints** for creating objects (introduced in ES6).
They make it easier to create multiple similar objects with shared behavior.

**Example:**

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hi, I'm ${this.name} and I'm ${this.age} years old.`);
  }
}

const bilal = new Person("Bilal", 23);
bilal.greet(); // Hi, I'm Bilal and I'm 23 years old.
```

---

#### **Inheritance**

Inheritance allows one class to **extend** another, reusing and customizing its behavior.

**Example:**

```js
class Employee extends Person {
  constructor(name, age, role) {
    super(name, age); // calls the parent constructor
    this.role = role;
  }

  work() {
    console.log(`${this.name} is working as a ${this.role}.`);
  }
}

const dev = new Employee("Bilal", 23, "Software Engineer");
dev.greet(); // inherited method
dev.work(); // own method
```

**Key keywords:**

- `extends` → inherit from another class
- `super()` → call parent constructor or methods

---

### **2. Callback Hell**

When many callbacks are nested inside each other (especially for async code), it becomes hard to read and maintain — this is **callback hell**.

**Example:**

```js
getUser(function (user) {
  getOrders(user.id, function (orders) {
    getOrderDetails(orders[0], function (details) {
      console.log(details);
    });
  });
});
```

➡️ This deep nesting makes code hard to follow.

**Solution:** use **Promises** or **Async/Await**.

---

### **3. Promises**

A **Promise** represents a value that may be available **now, later, or never**.
It helps handle asynchronous operations cleanly.

**States of a Promise:**

- `pending` → operation in progress
- `fulfilled` → operation succeeded
- `rejected` → operation failed

**Example:**

```js
const getData = new Promise((resolve, reject) => {
  const success = true;
  if (success) resolve("Data received!");
  else reject("Error fetching data");
});

getData
  .then((result) => console.log(result)) // runs if resolved
  .catch((error) => console.error(error)) // runs if rejected
  .finally(() => console.log("Done"));
```

**Chaining Promises:**

```js
fetchUser()
  .then((user) => fetchOrders(user.id))
  .then((orders) => console.log(orders))
  .catch((err) => console.error(err));
```

---

### **4. Async / Await**

`async` and `await` make asynchronous code **look synchronous** and more readable.

**Rules:**

- Use `async` before a function to make it return a Promise.
- Use `await` to pause execution until the Promise resolves.

**Example:**

```js
async function fetchData() {
  try {
    const user = await fetchUser();
    const orders = await fetchOrders(user.id);
    console.log(orders);
  } catch (error) {
    console.error("Error:", error);
  }
}

fetchData();
```

**Advantages:**
✅ Cleaner than `.then()` chaining
✅ Easier error handling with `try...catch`

---

### **5. Event Loop**

The **Event Loop** is how JavaScript handles **asynchronous tasks** even though it’s **single-threaded**.

#### 🧠 The idea:

1. JavaScript runs all **synchronous** code first (main thread).
2. **Async tasks** (like `setTimeout`, Promises, etc.) go to a **callback queue**.
3. Once the call stack is empty, the **event loop** picks tasks from the queue and executes them.

**Example:**

```js
console.log("1");

setTimeout(() => console.log("2"), 0);

Promise.resolve().then(() => console.log("3"));

console.log("4");
```

**Output:**

```
1
4
3
2
```

**Why this order?**

- `1` and `4` → synchronous, run immediately
- `3` → microtask (Promise), runs before macrotasks
- `2` → macrotask (`setTimeout`), runs last

---

### 🧩 Summary Table

| Concept           | Description                    | Example                       |
| ----------------- | ------------------------------ | ----------------------------- |
| **Class**         | Blueprint for creating objects | `class User {}`               |
| **Inheritance**   | Extend another class           | `class Admin extends User {}` |
| **Callback Hell** | Nested async callbacks         | Difficult to read             |
| **Promise**       | Async placeholder value        | `.then().catch()`             |
| **Async/Await**   | Simplified Promise syntax      | `await fetchData()`           |
| **Event Loop**    | Controls async execution order | Handles queue & stack         |

---
