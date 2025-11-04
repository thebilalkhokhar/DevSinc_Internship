Let’s go through **🧮 CSS Variables & Functions** in detail — these are powerful tools that make your styles **dynamic, reusable, and adaptive** across projects.

---

### **1. CSS Custom Properties (Variables)**

CSS variables allow you to store reusable values (like colors, spacing, fonts) and reference them throughout your stylesheet.

#### **Syntax:**

```css
:root {
  --primary-color: #3498db;
  --padding-size: 1rem;
}

button {
  background: var(--primary-color);
  padding: var(--padding-size);
}
```

#### **Explanation:**

- `:root` → defines global scope (accessible everywhere).
- `--primary-color` → variable name (must start with `--`).
- `var(--primary-color)` → retrieves the value of the variable.

#### **Advantages:**

- **Reusability:** Change in one place reflects everywhere.
- **Dynamic updates:** You can change variable values via **JavaScript** or **media queries**.
- **Theming:** Great for implementing **light/dark modes** or user-selected themes.

#### **Example:**

```css
:root {
  --bg: #fff;
  --text: #000;
}

.dark-mode {
  --bg: #000;
  --text: #fff;
}

body {
  background: var(--bg);
  color: var(--text);
}
```

Switching a class toggles between light/dark modes instantly.

---

### **2. `var()` Function**

The `var()` function retrieves the value of a CSS variable and optionally provides a fallback.

#### **Syntax:**

```css
color: var(--main-color, #333);
```

- The second value (`#333`) is **fallback** — used if the variable isn’t defined.
- You can nest variables:

  ```css
  background: var(--theme-bg, var(--default-bg, white));
  ```

---

### **3. `calc()` Function**

`calc()` allows mathematical calculations directly in CSS.

#### **Syntax:**

```css
width: calc(100% - 50px);
font-size: calc(1rem + 0.5vw);
```

#### **Supported operations:**

- `+`, `-`, `*`, `/`
- Units can be **mixed** (px, %, rem, etc.)

#### **Examples:**

```css
.main {
  height: calc(100vh - 80px); /* Adjust for header height */
}
.box {
  padding: calc(var(--spacing) * 2);
}
```

#### **Usage Tips:**

- Don’t add spaces around `*` and `/` operators — browsers may misinterpret them.
- Ideal for **responsive layouts** and precise spacing.

---

### **4. `clamp()` Function**

`clamp()` defines a **value range** with a **minimum**, **preferred**, and **maximum** value.

#### **Syntax:**

```css
font-size: clamp(1rem, 2vw, 2rem);
```

- **1rem** → minimum value (never smaller than this)
- **2vw** → preferred (scales with viewport width)
- **2rem** → maximum value (never larger than this)

#### **Use Cases:**

- Perfect for **fluid typography** or **responsive padding**.
- Removes the need for multiple media queries.

---

### **5. `min()` and `max()` Functions**

Used to choose the smallest or largest value among multiple expressions.

#### **Syntax & Examples:**

```css
width: min(100%, 600px); /* Takes whichever is smaller */
height: max(50vh, 300px); /* Takes whichever is larger */
```

#### **Use Cases:**

- `min()` → Limit element width on large screens.
- `max()` → Ensure minimum visibility or tappable areas.

---

### **6. `rgba()` and `hsl()` Functions**

Color functions that include **opacity** and **hue-based control**.

#### **`rgba()`**

- `rgba(red, green, blue, alpha)`
- Example:

  ```css
  background-color: rgba(255, 99, 71, 0.7); /* tomato with 70% opacity */
  ```

#### **`hsl()`**

- `hsl(hue, saturation, lightness)`
- Example:

  ```css
  color: hsl(210, 100%, 40%);
  background-color: hsla(210, 100%, 40%, 0.5);
  ```

#### **Why use HSL:**

- Easier to tweak for themes — adjusting **lightness/saturation** feels more intuitive than RGB.

---

### **7. `cubic-bezier()` Function**

Used in **animations and transitions** to define custom easing curves.

#### **Syntax:**

```css
transition-timing-function: cubic-bezier(0.25, 0.1, 0.25, 1);
```

#### **Explanation:**

- The four numbers represent **control points** on a Bézier curve.
- Common presets:

  - `ease` → `(0.25, 0.1, 0.25, 1)`
  - `linear` → `(0, 0, 1, 1)`
  - `ease-in` → `(0.42, 0, 1, 1)`
  - `ease-out` → `(0, 0, 0.58, 1)`

#### **Visualization:**

You can test these curves at: [https://cubic-bezier.com](https://cubic-bezier.com)

---

✅ **In Summary**

| Function / Feature | Purpose                             | Example                             |
| ------------------ | ----------------------------------- | ----------------------------------- |
| `--var`            | Define reusable CSS variables       | `--primary-color: #3498db`          |
| `var()`            | Use variable with optional fallback | `color: var(--text, #333)`          |
| `calc()`           | Mathematical operations in CSS      | `width: calc(100% - 50px)`          |
| `clamp()`          | Limit a value between min–max       | `font-size: clamp(1rem, 2vw, 2rem)` |
| `min()`            | Choose smallest value               | `width: min(100%, 600px)`           |
| `max()`            | Choose largest value                | `height: max(50vh, 300px)`          |
| `rgba()`           | Color with alpha (opacity)          | `rgba(0,0,0,0.5)`                   |
| `hsl()`            | Color by hue/saturation/lightness   | `hsl(200, 80%, 50%)`                |
| `cubic-bezier()`   | Custom transition easing            | `cubic-bezier(0.4, 0, 0.2, 1)`      |

---
