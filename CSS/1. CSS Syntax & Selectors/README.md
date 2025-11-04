Let’s dive deep into the **🧱 Core CSS Foundations (Must-Know)** section.
This is the true backbone of CSS — everything else builds on these concepts.
I’ll explain _every subtopic clearly and completely_, with examples and the reasoning behind how and why things behave the way they do.

---

## 🧱 **1. CSS Syntax & Selectors**

### 🔹 **CSS Syntax**

CSS (Cascading Style Sheets) uses a rule-based syntax:

```css
selector {
  property: value;
}
```

**Example:**

```css
p {
  color: blue;
  font-size: 16px;
}
```

- **selector** — targets HTML elements to style (e.g., `p`, `.class`, `#id`)
- **property** — the style attribute you want to change (like color)
- **value** — defines how the property should look (like blue)

### 🔹 **Types of Selectors**

1. **Universal Selector (`*`)**

   - Targets _every element_.

   ```css
   * {
     margin: 0;
     padding: 0;
   }
   ```

2. **Type Selector (Element)**

   - Targets HTML tags.

   ```css
   h1 {
     color: red;
   }
   ```

3. **Class Selector (`.classname`)**

   - Targets elements with a specific class.

   ```css
   .btn {
     background: blue;
   }
   ```

4. **ID Selector (`#id`)**

   - Targets an element with a specific `id` (must be unique).

   ```css
   #header {
     background: black;
   }
   ```

5. **Group Selector (`,`)**

   - Applies the same styles to multiple selectors.

   ```css
   h1,
   h2,
   h3 {
     font-family: Arial;
   }
   ```

6. **Attribute Selector**

   - Targets elements based on attributes.

   ```css
   input[type="text"] {
     border: 1px solid gray;
   }
   a[target="_blank"] {
     color: blue;
   }
   ```

---

### 🔹 **Combinator Selectors**

They define relationships between elements.

| Selector | Description             | Example   |
| -------- | ----------------------- | --------- |
| `A B`    | Descendant (B inside A) | `div p`   |
| `A > B`  | Direct child            | `div > p` |
| `A + B`  | Immediate next sibling  | `h1 + p`  |
| `A ~ B`  | All following siblings  | `h1 ~ p`  |

**Example:**

```css
ul > li {
  color: red;
} /* only direct li children */
```

---

### 🔹 **Pseudo-classes**

Used to define a special state of an element.

Examples:

```css
a:hover {
  color: red;
} /* when mouse is over */
a:visited {
  color: purple;
}
input:focus {
  border-color: blue;
}
li:first-child {
  font-weight: bold;
}
li:nth-child(2n) {
  background: #eee;
}
```

---

### 🔹 **Pseudo-elements**

Used to style _parts_ of an element.

Examples:

```css
p::first-line {
  font-weight: bold;
}
p::first-letter {
  font-size: 2em;
}
button::before {
  content: "→ ";
}
button::after {
  content: " ✓";
}
```

---

## 🧠 **2. CSS Specificity, Inheritance, and the Cascade**

### 🔹 **Specificity**

When multiple rules apply to the same element, CSS decides _which rule wins_ based on specificity.

| Selector Type                             | Specificity Value |
| ----------------------------------------- | ----------------- |
| Inline styles (`style=""`)                | 1000              |
| ID selectors                              | 100               |
| Class, Pseudo-class, Attribute selectors  | 10                |
| Element (Type) selectors, Pseudo-elements | 1                 |
| Universal selector `*`, Inherited styles  | 0                 |

**Example:**

```css
p {
  color: black;
} /* 1 */
p.text {
  color: blue;
} /* 10 + 1 = 11 */
#main p {
  color: red;
} /* 100 + 1 = 101 → wins */
```

---

### 🔹 **Inheritance**

Some CSS properties automatically inherit values from their parent elements.

**Inherited properties**:

- color
- font-family
- font-size
- line-height
- visibility

**Non-inherited properties**:

- margin, padding, border, width, height, etc.

You can force inheritance:

```css
p {
  border: inherit;
}
```

---

### 🔹 **Cascade**

CSS stands for _Cascading_ Style Sheets — meaning the browser applies styles in a specific order:

1. **User agent styles** (browser defaults)
2. **External / internal stylesheets**
3. **Inline styles** (highest priority)
4. **!important** overrides all

If two rules have the same specificity, the **later one in the stylesheet** wins.

---

## 📦 **3. Box Model (Content, Padding, Border, Margin)**

Each element in CSS is a _box_, and understanding this is critical for layout.

```
+-----------------------------+
|        Margin (outside)     |
|  +-----------------------+  |
|  |      Border           |  |
|  |  +-----------------+  |  |
|  |  |   Padding       |  |  |
|  |  |  +-----------+  |  |  |
|  |  |  |  Content  |  |  |  |
|  |  |  +-----------+  |  |  |
|  |  +-----------------+  |  |
|  +-----------------------+  |
+-----------------------------+
```

### **Content**

The actual text, image, or content inside.

### **Padding**

Space between content and border.

### **Border**

Outline surrounding padding/content.

### **Margin**

Space outside the border — separates from other elements.

---

### **Box-sizing**

Controls how width/height are calculated.

```css
box-sizing: content-box; /* default: width = content only */
box-sizing: border-box; /* includes padding + border in width */
```

---

## 🧱 **4. Display Types**

Defines how an element is rendered.

### **block**

- Starts on a new line
- Takes full width
- You can set width, height, margin, padding
  Example: `<div>, <p>, <h1>`

### **inline**

- Flows inline with text
- No width/height control
- Margin/padding only works horizontally
  Example: `<span>, <a>`

### **inline-block**

- Behaves like inline, but allows width/height control

### **none**

- Completely removes element from layout (not visible, not occupying space)

---

## 📍 **5. Positioning (relative, absolute, fixed, sticky)**

### **position: static**

- Default position; element follows normal document flow.

### **position: relative**

- Moves relative to its original position.

```css
div {
  position: relative;
  top: 10px;
  left: 20px;
}
```

### **position: absolute**

- Removed from normal flow.
- Positioned relative to the nearest positioned ancestor (not static).

```css
.child {
  position: absolute;
  top: 0;
  left: 0;
}
```

### **position: fixed**

- Positioned relative to the viewport (doesn’t move when scrolled).

### **position: sticky**

- Behaves like relative until a scroll threshold, then sticks in place.

```css
header {
  position: sticky;
  top: 0;
}
```

---

## 🧩 **6. Z-index & Stacking Context**

**z-index** controls the _stacking order_ of overlapping elements.

```css
div {
  position: absolute;
  z-index: 10;
}
```

Higher z-index = appears on top.

**Rules:**

- Works only on _positioned_ elements.
- Each positioned element creates a _stacking context_ — its children’s z-index are limited within it.

**Example:**
If parent A has z-index: 5, and child A1 has z-index: 100 —
but another parent B has z-index: 10 → B will still appear above A, regardless of A1’s large z-index.

---

## 💧 **7. Overflow & Visibility**

### **overflow**

Defines what happens when content exceeds the box size.

```css
overflow: visible; /* default */
overflow: hidden; /* cut off extra content */
overflow: scroll; /* adds scrollbars */
overflow: auto; /* adds scrollbars only when needed */
```

Separate controls:

```css
overflow-x: hidden;
overflow-y: scroll;
```

---

### **visibility**

```css
visibility: visible; /* default */
visibility: hidden; /* invisible but still occupies space */
```

Difference from `display: none` → `none` removes the element from the layout.

---

## 📏 **8. CSS Units**

| Type                   | Example            | Description                                             |
| ---------------------- | ------------------ | ------------------------------------------------------- |
| **Absolute**           | px, pt, cm         | Fixed size, not responsive                              |
| **Relative to parent** | %                  | Relative to parent’s size                               |
| **Relative to font**   | em, rem            | em = relative to parent font-size; rem = root font-size |
| **Viewport-based**     | vw, vh, vmin, vmax | % of the viewport width/height                          |

**Example:**

```css
width: 50%; /* half of parent width */
font-size: 2em; /* 2x parent font-size */
font-size: 2rem; /* 2x root font-size */
height: 100vh; /* full screen height */
```

---

## 🎨 **9. Colors**

### **Named Colors**

```css
color: red;
```

### **HEX**

```css
color: #ff0000; /* Red */
color: #f00; /* shorthand */
```

### **RGB**

```css
color: rgb(255, 0, 0);
```

### **RGBA**

Includes transparency:

```css
color: rgba(255, 0, 0, 0.5);
```

### **HSL / HSLA**

Hue (0–360), Saturation (%), Lightness (%)

```css
color: hsl(0, 100%, 50%); /* red */
color: hsla(120, 60%, 50%, 0.3);
```

---

✅ **Summary (What to Master Practically):**

- Understand how the **box model** and **positioning** combine to form layouts.
- Know how **specificity** and **cascade** decide which styles apply.
- Be confident with **Flexbox and Grid** (next section) — they rely on the above principles.
- Use **relative units** and **responsive design** for real projects.

---
