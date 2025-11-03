## **1. Object Destructuring**

Destructuring allows you to **unpack values** from arrays or objects into separate variables easily.

### **Without destructuring:**

```js
const person = { name: "Bilal", age: 23, city: "Lahore" };
const name = person.name;
const age = person.age;
```

### **With destructuring:**

```js
const { name, age } = person;
console.log(name); // Bilal
console.log(age); // 23
```

You can also rename variables:

```js
const { city: hometown } = person;
console.log(hometown); // Lahore
```

And set default values:

```js
const { country = "Pakistan" } = person;
console.log(country); // Pakistan
```

✅ **Benefits:**

- Cleaner syntax
- Easier data extraction (especially in APIs or props)

---

## **2. Object Literal (Enhanced Object Literals)**

ES6 introduced shortcuts for defining **object properties and methods** when variable names match property names.

### **Before ES6:**

```js
const name = "Bilal";
const age = 23;

const person = {
  name: name,
  age: age,
  greet: function () {
    console.log("Hello!");
  },
};
```

### **With ES6:**

```js
const name = "Bilal";
const age = 23;

const person = {
  name, // shorthand for name: name
  age,
  greet() {
    // shorthand for greet: function() { ... }
    console.log(`Hello, I'm ${this.name}`);
  },
};

person.greet(); // Hello, I'm Bilal
```

✅ **Benefits:**

- Less repetition
- Cleaner object syntax

---

## **3. Spread Operator (`...`)**

The **spread operator** expands an array or object into individual elements.

### **In arrays:**

```js
const nums = [1, 2, 3];
const newNums = [...nums, 4, 5];
console.log(newNums); // [1, 2, 3, 4, 5]
```

### **In objects:**

```js
const user = { name: "Bilal", age: 23 };
const updatedUser = { ...user, city: "Lahore" };
console.log(updatedUser); // { name: 'Bilal', age: 23, city: 'Lahore' }
```

✅ **Uses:**

- Cloning arrays/objects
- Combining arrays/objects
- Passing arguments to functions easily

---

## **4. Rest Operator (`...`)**

The **rest operator** collects remaining elements into an array.
It’s basically the _opposite_ of spread.

### **Example:**

```js
function show(a, b, ...rest) {
  console.log(a); // first argument
  console.log(b); // second argument
  console.log(rest); // remaining arguments in array
}

show(1, 2, 3, 4, 5);
// Output:
// 1
// 2
// [3, 4, 5]
```

**In object destructuring:**

```js
const { name, ...others } = { name: "Bilal", age: 23, city: "Lahore" };
console.log(others); // { age: 23, city: 'Lahore' }
```

✅ **Uses:**

- Handle dynamic arguments
- Extract subsets of data

---

## **5. Arrow Functions**

Arrow functions are a **shorter syntax** for writing functions and automatically bind `this` from their surrounding scope.

### **Before:**

```js
function add(a, b) {
  return a + b;
}
```

### **With Arrow Function:**

```js
const add = (a, b) => a + b;
console.log(add(5, 3)); // 8
```

**With multiple lines:**

```js
const greet = (name) => {
  console.log(`Hello, ${name}!`);
};
```

✅ **Key features:**

- Shorter and cleaner syntax
- Inherit `this` (no new binding)
- Great for callbacks and array methods

⚠️ **Note:** Not suitable for constructors or methods where `this` should refer to the current object.

---

## **6. Nullish Coalescing Operator (`??`)**

The `??` operator provides a **default value** only when the left side is `null` or `undefined`.

### **Example:**

```js
const name = null ?? "Guest";
console.log(name); // Guest
```

Compare with `||`:

```js
const count = 0 || 10; // 10 (because 0 is falsy)
const count2 = 0 ?? 10; // 0  (because 0 is not null/undefined)
```

✅ **Use when:**
You only want to replace **null or undefined**, not all falsy values.

---

## **7. Optional Chaining Operator (`?.`)**

The `?.` operator safely accesses deeply nested object properties **without throwing errors**.

### **Example:**

```js
const user = {
  profile: {
    name: "Bilal",
  },
};

console.log(user.profile?.name); // Bilal
console.log(user.address?.city); // undefined (no error)
```

Without optional chaining, accessing `user.address.city` would throw an error.

✅ **Use case:**
Accessing nested API data or optional properties safely.

---

## **8. var vs let vs const**

| Keyword | Scope           | Re-declaration | Re-assignment | Hoisted?                          | Typical Use                     |
| ------- | --------------- | -------------- | ------------- | --------------------------------- | ------------------------------- |
| `var`   | Function-scoped | ✅ Yes         | ✅ Yes        | ✅ Yes (initialized as undefined) | Legacy code                     |
| `let`   | Block-scoped    | ❌ No          | ✅ Yes        | ✅ Yes (TDZ applies)              | Variables that change           |
| `const` | Block-scoped    | ❌ No          | ❌ No         | ✅ Yes (TDZ applies)              | Constants, immutable references |

### **Example:**

```js
if (true) {
  var x = 10;
  let y = 20;
  const z = 30;
}
console.log(x); // 10
console.log(y); // ReferenceError
console.log(z); // ReferenceError
```

✅ **Best practice:**
Use `const` by default, `let` when you need to reassign, and avoid `var`.

---

## **9. Trailing Commas**

Trailing commas allow you to have a comma **after the last element or property** in arrays or objects.

### **Example:**

```js
const arr = [
  "apple",
  "banana",
  "mango", // <- trailing comma
];

const obj = {
  name: "Bilal",
  age: 23,
};
```

✅ **Benefits:**

- Easier to add/remove items
- Cleaner version control diffs
- No syntax error from an extra comma

---

### 🧩 **Summary Table**

| Feature                  | Purpose                         | Example                  |
| ------------------------ | ------------------------------- | ------------------------ |
| **Object Destructuring** | Extract values easily           | `const {name} = obj`     |
| **Object Literal**       | Shorter object syntax           | `{ name, greet() {} }`   |
| **Spread Operator**      | Expand arrays/objects           | `[...arr1, ...arr2]`     |
| **Rest Operator**        | Collect remaining values        | `(...args) => {}`        |
| **Arrow Functions**      | Shorter, lexical `this`         | `const sum = (a,b)=>a+b` |
| **Nullish Coalescing**   | Default only for null/undefined | `x ?? 'default'`         |
| **Optional Chaining**    | Safe deep property access       | `user?.profile?.name`    |
| **var / let / const**    | Variable declaration control    | `let count = 5`          |
| **Trailing Commas**      | Easier edits                    | `[1,2,3,]`               |

---
