### **1. Execution Context**

Every time JS runs code, it creates an **Execution Context (EC)** — a kind of _environment_ that defines how variables, functions, and `this` behave.

Two main types:

- **Global Execution Context (GEC):** Created when JS first runs the file.

  - `this` → refers to the `window` (in browsers)
  - Creates global memory for variables/functions.

- **Function Execution Context (FEC):** Created when a function is called.

  - Each function gets its own local variables, arguments, and scope chain.

Each EC has two phases:

1. **Creation Phase**

   - Memory space allocated for variables and functions.
   - Variables are set to `undefined`.
   - Functions are stored as references.

2. **Execution Phase**

   - Code runs line by line and values are assigned.

👉 JS maintains a **Call Stack** — last function called is the first to finish (LIFO).

---

### **2. `undefined` vs `not defined`**

| Term            | Meaning                                             | Example                                               |
| --------------- | --------------------------------------------------- | ----------------------------------------------------- |
| **undefined**   | Variable exists in memory but no value is assigned. | `let x; console.log(x); // undefined`                 |
| **not defined** | Variable doesn’t exist at all.                      | `console.log(y); // ReferenceError: y is not defined` |

---

### **3. Temporal Dead Zone (TDZ)**

For `let` and `const`, variables are hoisted **but not initialized**.
From the start of the scope until the line of declaration, they are in the **TDZ**.

```js
console.log(a); // ❌ ReferenceError
let a = 5;
```

The variable is known to JS but not usable yet.

---

### **4. Hoisting**

JS moves variable and function declarations **to the top of their scope** during compilation.

- **var** → hoisted and initialized as `undefined`
- **let/const** → hoisted but in TDZ
- **function declaration** → fully hoisted
- **function expression / arrow function** → behaves like variable (not usable before definition)

```js
sayHi(); // ✅ Works
function sayHi() {
  console.log("Hi");
}

console.log(a); // undefined
var a = 10;
```

---

### **5. How `this` works (normal vs arrow function)**

- **In regular functions:**

  - `this` is **dynamic** — depends on _how_ the function is called.
  - If called as a method: `this = object`
  - If called alone: `this = window` (or `undefined` in strict mode)

- **In arrow functions:**

  - `this` is **lexically bound** — takes `this` from its outer scope.
  - Arrow functions **don’t create their own this**.

```js
const obj = {
  name: "Bilal",
  normal() {
    console.log(this.name);
  },
  arrow: () => console.log(this.name),
};
obj.normal(); // Bilal
obj.arrow(); // undefined (this = window)
```

---

### **6. Generator Functions**

Generators can **pause** and **resume** execution using `yield`.

```js
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

const g = gen();
console.log(g.next()); // {value:1, done:false}
console.log(g.next()); // {value:2, done:false}
```

Use case: controlling async flow, infinite sequences, etc.

---

### **7. Array Prototyping**

You can add custom methods to all arrays via `Array.prototype`:

```js
Array.prototype.sum = function () {
  return this.reduce((acc, val) => acc + val, 0);
};
console.log([1, 2, 3].sum()); // 6
```

⚠️ Not recommended for production — can cause conflicts if built-in methods are added later.

---

### **8. Prototypal Inheritance**

Every object in JS inherits from another object called its **prototype**.

```js
const parent = {
  greet() {
    console.log("Hello");
  },
};
const child = Object.create(parent);
child.greet(); // Hello
```

The **prototype chain** continues up to `Object.prototype`.

---

### **9. Window keyword vs This keyword**

| Keyword    | Meaning                                                     |
| ---------- | ----------------------------------------------------------- |
| **window** | Global object in browsers (holds `alert`, `document`, etc.) |
| **this**   | Context-dependent (changes based on how/where it’s used)    |

```js
console.log(window === this); // true (in global scope)
```

But inside an object or arrow function, results differ.

---

### **10. Changing properties of a `const` object**

`const` only locks the _reference_, not the _contents_.

```js
const user = { name: "Bilal" };
user.name = "Ahmad"; // ✅ allowed
user = {}; // ❌ TypeError
```

So you can modify properties, not reassign the variable.

---

### **11. Event Bubbling vs Capturing (Trickling)**

- **Bubbling:** Event starts from the innermost element → bubbles **up** to ancestors.
- **Capturing:** Event moves from outermost element → **down** to target.

```js
element.addEventListener("click", handler, true); // capturing
element.addEventListener("click", handler, false); // bubbling (default)
```

---

### **12. Problem with Event Bubbling**

If multiple nested elements have click listeners, **all** get triggered.
For example:

```js
<div onclick="console.log('div')">
  <button onclick="console.log('button')">Click</button>
</div>
```

Clicking the button logs both `'button'` and `'div'`.

---

### **13. Stop Propagation**

To prevent bubbling:

```js
button.addEventListener("click", (e) => {
  e.stopPropagation();
  console.log("Button only");
});
```

---

### **14. Prevent Default**

Stops the browser’s **default behavior** (like navigating, form submission, etc.)

```js
form.addEventListener("submit", (e) => {
  e.preventDefault(); // stops page reload
});
```

---

### **15. Throttling vs Debouncing**

Both control how often a function runs (especially in scroll/resize events).

| Technique    | Description                                                 | Example                  |
| ------------ | ----------------------------------------------------------- | ------------------------ |
| **Debounce** | Waits for user to stop triggering for X ms before running.  | Search input suggestions |
| **Throttle** | Runs at most once every X ms, even if triggered repeatedly. | Scroll position listener |

---

### **16. IIFE (Immediately Invoked Function Expression)**

Runs **immediately** after it’s defined.

```js
(function () {
  console.log("Runs instantly!");
})();
```

Useful for creating a **private scope**.

---

### **17. Closures, Lexical Scoping, Scope Chaining**

**Lexical Scoping:** A function can access variables from where it was _defined_, not where it’s _called_.

**Closure:** When a function “remembers” its outer scope even after the outer function is done.

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
```

**Scope Chain:** JS looks for variables from inner → outer → global scope.

---

### **18. Syntax Error vs Type Error vs Reference Error**

| Error Type         | When it Happens                            | Example           |
| ------------------ | ------------------------------------------ | ----------------- |
| **SyntaxError**    | Invalid JS syntax (caught at compile time) | `if (true {}`     |
| **TypeError**      | Operation on wrong data type               | `null.toString()` |
| **ReferenceError** | Accessing variable that doesn’t exist      | `console.log(x)`  |

---

### **19. Debouncing and Throttling Explained**

---

## 🧭 **Problem samjho pehle**

Jab hum kuch events (like `scroll`, `resize`, `input`, `mousemove`, etc.) par functions lagate hain,
to browser **har millisecond** us function ko trigger karta rehta hai — even hundreds of times per second!

👉 Example:

```js
window.addEventListener("scroll", () => {
  console.log("User scrolled!");
});
```

Ab agar user 1 second scroll karta hai, ye line **hundreds of times** chalegi 😬
→ performance slow
→ laggy UI
→ unnecessary re-rendering

Is problem ko control karne ke liye hum use karte hain:

> 🔹 **Debouncing**
> 🔹 **Throttling**

---

## ⚡ **Debouncing**

**Concept:**
👉 “Wait until the user stops doing something for a specific time.”

Matlab function tabhi chalega jab user ne event trigger karna **band kar diya** ho — aur uske baad X ms beet gaye ho.

---

### **Example 1: Search Input**

Tum search box me likh rahe ho aur har keypress par API call ho rahi hai.
Without debounce: har character par API call! ❌

With debounce: jab user likhna **band kar de** (e.g. 500 ms tak koi keypress na ho)
→ tab API call hoti hai ✅

```js
let timer;
function searchHandler(e) {
  clearTimeout(timer); // purana timer cancel
  timer = setTimeout(() => {
    console.log("API call for:", e.target.value);
  }, 500);
}

input.addEventListener("keyup", searchHandler);
```

🧠 **Logic:**

- Har keypress par timer reset hota hai
- Jab user rukta hai (500ms tak koi aur keypress nahi hoti), function chal jata hai.

---

### 📊 Visualize Debounce

```
User typing:  H - E - L - L - O
Time (ms):    0   100 200 300 400 900
Action:                        ^ (function runs at 900ms)
```

---

## 🕓 **Throttling**

**Concept:**
👉 “Allow the function to run only once every X milliseconds, no matter how often event triggers.”

Matlab agar event bar bar fire ho raha hai, to hum us function ko **limit** kar dete hain ke wo har X ms me sirf ek dafa chale.

---

### **Example 2: Scroll Event**

Tum scroll par position update kar rahe ho:

Without throttle → function 100+ times per second chalega ❌
With throttle → function sirf e.g. har 200ms me ek dafa chalega ✅

```js
let lastTime = 0;

function throttle(fn, limit) {
  return function (...args) {
    const now = Date.now();
    if (now - lastTime >= limit) {
      fn.apply(this, args);
      lastTime = now;
    }
  };
}

function logScroll() {
  console.log("Scroll position:", window.scrollY);
}

window.addEventListener("scroll", throttle(logScroll, 200));
```

🧠 **Logic:**

- Function chalega → next 200ms tak ignore karega events.
- 200ms ke baad agla call allowed hai.

---

### 📊 Visualize Throttle

```
User scrolling continuously:
|----|----|----|----|----|----|----|----|
Function runs:   ^    ^    ^    ^    ^

(only every fixed interval)
```

---

## ⚔️ **Debounce vs Throttle Summary**

| Feature       | Debounce                              | Throttle                                 |
| ------------- | ------------------------------------- | ---------------------------------------- |
| **When runs** | After user stops triggering           | At regular intervals while user triggers |
| **Use case**  | Text input, search box, resize events | Scroll, window resize, mouse move        |
| **Behavior**  | Waits for silence (pauses)            | Runs periodically                        |
| **Goal**      | Run _after_ activity                  | Run _during_ activity but in control     |

---

### ✅ **Easy way to remember**

- **Debounce:** “Run _after_ the user stops.”
- **Throttle:** “Run _every_ X ms _while_ user is active.”

---
