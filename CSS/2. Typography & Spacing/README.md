Let’s break down **🎨 Typography & Spacing** in full detail.
Typography is one of the most visible and important aspects of web design — it defines readability, visual hierarchy, and overall feel of the UI.

---

## 🎨 **Typography & Spacing (Detailed Explanation)**

---

### 🅰️ **1. Font-family, Font-size, Font-weight, Line-height**

These four together control how text _looks and feels_ on a webpage.

---

#### 🔹 **font-family**

Defines which font(s) should be used for text.

```css
p {
  font-family: "Roboto", Arial, sans-serif;
}
```

- You can list **multiple fonts** separated by commas — browser uses the first available one.
- The **last one** should be a _generic family_:

  - `serif` → fonts like Times New Roman
  - `sans-serif` → fonts like Arial, Helvetica
  - `monospace` → fonts like Courier New
  - `cursive` → fonts like Brush Script
  - `fantasy` → decorative fonts

**Example:**

```css
body {
  font-family: "Open Sans", Helvetica, Arial, sans-serif;
}
```

---

#### 🔹 **font-size**

Sets the size of text.
Common units:

- `px` → fixed size
- `em` → relative to parent font-size
- `rem` → relative to root (`html`) font-size
- `vw` → relative to viewport width (used for fluid typography)

**Example:**

```css
h1 {
  font-size: 2rem;
} /* 2 × root font size */
p {
  font-size: 1em;
} /* same as parent font size */
small {
  font-size: 0.8em;
}
```

Default browser font size is usually **16px**.
If `html { font-size: 16px; }`, then `1rem = 16px`.

---

#### 🔹 **font-weight**

Defines how bold or light text appears.

```css
p {
  font-weight: normal;
}
h1 {
  font-weight: bold;
}
strong {
  font-weight: 700;
}
```

- Numeric range: **100 (thin)** → **900 (extra bold)**
- Keywords: `normal`, `bold`, `lighter`, `bolder`

Not all fonts support all weight values — browser approximates missing ones.

---

#### 🔹 **line-height**

Controls vertical spacing between lines of text (like leading in typography).

```css
p {
  line-height: 1.5;
}
```

- If you give a number (e.g., `1.5`), it multiplies the font-size.
- If you give units (e.g., `20px`), it’s absolute.
- Good readability range: **1.4–1.6**

---

### ⚖️ **2. Text Alignment & Decoration**

#### 🔹 **text-align**

Aligns text horizontally inside its container.

```css
p {
  text-align: left;
} /* default for LTR languages */
p {
  text-align: right;
}
p {
  text-align: center;
}
p {
  text-align: justify;
} /* stretches text to both sides */
```

- Works on block-level elements.
- `justify` adjusts spacing between words to make lines even.

---

#### 🔹 **text-decoration**

Adds underlines, overlines, or strike-throughs.

```css
a {
  text-decoration: none;
} /* remove link underline */
h2 {
  text-decoration: underline;
}
del {
  text-decoration: line-through;
}
```

You can customize style and color:

```css
a {
  text-decoration-line: underline;
  text-decoration-style: wavy;
  text-decoration-color: red;
}
```

---

#### 🔹 **text-transform**

Changes text case:

```css
h1 {
  text-transform: uppercase;
}
p {
  text-transform: capitalize;
}
```

---

#### 🔹 **text-shadow**

Adds shadow to text:

```css
h1 {
  text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
}
```

---

### 🪶 **3. Letter Spacing & Word Spacing**

These properties fine-tune horizontal rhythm and readability.

#### 🔹 **letter-spacing**

Adjusts space between _characters_:

```css
h1 {
  letter-spacing: 2px;
} /* more space between letters */
```

Can be negative too:

```css
.logo {
  letter-spacing: -1px;
}
```

#### 🔹 **word-spacing**

Adjusts space between _words_:

```css
p {
  word-spacing: 5px;
}
```

---

### 🌐 **4. Google Fonts / @font-face**

By default, browsers only support system fonts — but you can import **custom web fonts**.

---

#### 🔹 **Using Google Fonts**

Simplest method — go to [https://fonts.google.com](https://fonts.google.com) and copy the `<link>` or `@import`.

**Example (HTML link):**

```html
<link
  href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap"
  rel="stylesheet"
/>
```

Then in CSS:

```css
body {
  font-family: "Roboto", sans-serif;
}
```

**Alternative (CSS import):**

```css
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap");
```

---

#### 🔹 **Using @font-face**

Allows hosting your own custom fonts.

```css
@font-face {
  font-family: "MyFont";
  src: url("fonts/MyFont.woff2") format("woff2"), url("fonts/MyFont.woff")
      format("woff");
  font-weight: normal;
  font-style: normal;
}

body {
  font-family: "MyFont", sans-serif;
}
```

**Key points:**

- Use `.woff` or `.woff2` formats (optimized for web).
- You can define multiple weights or styles by repeating `@font-face`.

---

### 📄 **5. White-space Handling**

Controls how browsers handle spaces, tabs, and line breaks.

```css
p {
  white-space: normal;
}
```

| Value          | Description                                         |
| -------------- | --------------------------------------------------- |
| `normal`       | Default — collapses spaces, wraps lines             |
| `nowrap`       | Prevents wrapping, text continues on one line       |
| `pre`          | Preserves spaces and line breaks (like `<pre>` tag) |
| `pre-wrap`     | Preserves spaces _and_ allows wrapping              |
| `pre-line`     | Collapses spaces but keeps line breaks              |
| `break-spaces` | Like pre-wrap but breaks long words too             |

**Example:**

```css
.code-block {
  white-space: pre-wrap;
}
```

---

### ✅ **Quick Recap:**

- **font-family:** Choose multiple fallbacks, always end with a generic font.
- **font-size:** Use `rem` for scalable, consistent typography.
- **font-weight:** Numeric control (400 = normal, 700 = bold).
- **line-height:** Improves readability, keep around 1.5× font size.
- **text-align & decoration:** Controls alignment and visual emphasis.
- **letter/word-spacing:** Fine-tunes readability and style.
- **@font-face / Google Fonts:** Enables custom branding through typography.
- **white-space:** Controls wrapping and preservation of text formatting.

---
