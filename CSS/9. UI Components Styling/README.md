Excellent — this section, **🧾 UI Components Styling**, is where CSS meets practical interface design.
Here we’ll explore how to style **interactive UI elements** that users click, type in, and interact with daily — all while keeping accessibility, usability, and visual consistency in mind.

Let’s go through each concept in detail 👇

---

## 🎛 **1. Buttons, Inputs, Selects, Checkboxes, Radio Styling**

### **1.1 Buttons**

Buttons are among the most reused UI elements, so consistent styling matters.

#### **Basic Button Styling:**

```css
button {
  background: #007bff;
  color: white;
  border: none;
  padding: 0.6rem 1.2rem;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 500;
  transition: background 0.3s;
}

button:hover {
  background: #0056b3;
}
```

#### **Tips:**

- Always define `cursor: pointer` for clickable elements.
- Add smooth transitions for hover/active states.
- Maintain accessible contrast (WCAG: contrast ratio ≥ 4.5:1).

#### **Common Button Variants:**

```css
.btn--primary {
  background: #007bff;
  color: white;
}
.btn--secondary {
  background: #6c757d;
  color: white;
}
.btn--outline {
  background: transparent;
  border: 1px solid #007bff;
  color: #007bff;
}
```

---

### **1.2 Inputs & Selects**

Form inputs need consistent sizing, spacing, and focus styles.

```css
input[type="text"],
select {
  padding: 0.5rem 0.75rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  outline: none;
  transition: border-color 0.2s;
}

input:focus,
select:focus {
  border-color: #007bff;
  box-shadow: 0 0 0 2px rgba(0, 123, 255, 0.25);
}
```

#### **Best Practices:**

- Never remove outline **without** providing a custom focus indicator.
- Keep height consistent across input types.
- Use `:focus-visible` for accessible focus states (only when using keyboard).

---

### **1.3 Checkboxes & Radio Buttons**

Default styles vary between browsers, so developers often use **custom check/radio designs**.

#### **Method 1: Hide Native Input + Style Label**

```html
<label class="checkbox">
  <input type="checkbox" />
  <span class="checkmark"></span> Remember Me
</label>
```

```css
.checkbox input {
  display: none;
}

.checkmark {
  width: 18px;
  height: 18px;
  border: 2px solid #007bff;
  border-radius: 3px;
  display: inline-block;
  position: relative;
}

.checkbox input:checked + .checkmark {
  background-color: #007bff;
}

.checkbox input:checked + .checkmark::after {
  content: "";
  position: absolute;
  left: 4px;
  top: 1px;
  width: 5px;
  height: 9px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
}
```

#### **Notes:**

- Works similarly for `radio` but with `border-radius: 50%`.
- Maintain sufficient spacing between the box and label for accessibility.

---

## ⚡ **2. Focus, Active, Disabled States**

### **Focus**

Triggered when an element (like input or button) is selected or navigated via keyboard.

```css
button:focus,
input:focus {
  outline: 2px solid #007bff;
  outline-offset: 2px;
}
```

✅ **Best Practice:** Don’t remove focus — instead, style it clearly.

---

### **Active**

Activated when the user is clicking or pressing down on the element.

```css
button:active {
  transform: scale(0.98);
  background-color: #0056b3;
}
```

Adds tactile feedback.

---

### **Disabled**

For elements that cannot be interacted with.

```css
button:disabled {
  background: #ccc;
  cursor: not-allowed;
  opacity: 0.6;
}
```

✅ Combine both `opacity` and `cursor` changes for clear UX.

---

## 🧭 **3. Custom Scrollbars**

Native scrollbars differ per browser and OS. You can style them in modern browsers using pseudo-elements.

### **For WebKit Browsers (Chrome, Edge, Safari):**

```css
::-webkit-scrollbar {
  width: 10px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}
```

### **For Firefox:**

```css
* {
  scrollbar-width: thin;
  scrollbar-color: #888 #f1f1f1;
}
```

✅ **Tips:**

- Keep scrollbar contrast high enough to be visible.
- Avoid too thin scrollbars; it reduces usability.

---

## 🪟 **4. Modals, Tooltips, Dropdowns (Position + z-index)**

These UI elements involve **layering and positioning** carefully using CSS.

---

### **4.1 Modals**

Pop-up overlays that sit above all content.

#### **Basic Structure:**

```html
<div class="modal">
  <div class="modal__overlay"></div>
  <div class="modal__content">Hello Modal!</div>
</div>
```

#### **CSS:**

```css
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal__overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
}

.modal__content {
  position: relative;
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  z-index: 1001;
}
```

✅ Use **`position: fixed`** for full-screen coverage.
✅ Always keep modal z-index **higher** than all page content.

---

### **4.2 Tooltips**

Appear above an element when hovered or focused.

```html
<button class="tooltip" data-tooltip="Save changes">💾 Save</button>
```

```css
.tooltip {
  position: relative;
}

.tooltip::after {
  content: attr(data-tooltip);
  position: absolute;
  bottom: 120%;
  left: 50%;
  transform: translateX(-50%);
  background: #333;
  color: white;
  padding: 4px 8px;
  font-size: 12px;
  border-radius: 4px;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.2s;
}

.tooltip:hover::after {
  opacity: 1;
}
```

✅ Use `attr(data-tooltip)` for reusable tooltips.
✅ Set `pointer-events: none` to prevent interference with hover.

---

### **4.3 Dropdowns**

Floating menus that appear below an element.

```html
<div class="dropdown">
  <button class="dropdown__toggle">Menu ▼</button>
  <ul class="dropdown__menu">
    <li>Profile</li>
    <li>Settings</li>
    <li>Logout</li>
  </ul>
</div>
```

```css
.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown__menu {
  position: absolute;
  top: 100%;
  left: 0;
  background: white;
  border: 1px solid #ddd;
  border-radius: 6px;
  padding: 0.5rem 0;
  min-width: 150px;
  display: none;
  z-index: 999;
}

.dropdown:hover .dropdown__menu {
  display: block;
}
```

✅ Use **absolute positioning** relative to the parent.
✅ Keep dropdown z-index higher than base content but below modals (e.g., `999`).

---

### **Z-Index Layering Convention (for reference):**

| Layer          | Example Component  | Recommended z-index |
| -------------- | ------------------ | ------------------- |
| Base Content   | Page elements      | 1–10                |
| Sticky Header  | Navbar             | 100                 |
| Dropdowns      | Menus              | 999                 |
| Modals         | Dialogs            | 1000+               |
| Toasts/Popups  | Notifications      | 1100+               |
| Loader/Overlay | Fullscreen spinner | 2000+               |

---

## ✅ **Summary Table**

| Category              | Key Concepts                          | Example                                  |
| --------------------- | ------------------------------------- | ---------------------------------------- |
| Buttons               | Consistent sizing, hover/focus/active | `.btn--primary { background: #007bff; }` |
| Inputs                | Accessible outlines & padding         | `input:focus { box-shadow: ... }`        |
| Checkboxes/Radios     | Hidden native input, styled label     | `.checkmark` technique                   |
| Focus/Active/Disabled | Clear visual states                   | `button:disabled { opacity: 0.6; }`      |
| Custom Scrollbars     | WebKit + Firefox styling              | `::-webkit-scrollbar-thumb`              |
| Modals                | `position: fixed`, overlay + z-index  | `.modal__overlay`                        |
| Tooltips              | `::after` with `attr()` content       | `.tooltip:hover::after`                  |
| Dropdowns             | `position: absolute` + z-index        | `.dropdown__menu`                        |

---
