Excellent — this section covers **🎬 Animations & Effects**, which make your interfaces feel alive and polished. These are not only for visual appeal — smooth animations can also **communicate state changes and improve UX**.
Let’s go through each part carefully and completely.

---

## 🎬 Animations & Effects

---

### 1. **Transitions**

Transitions make property changes happen **gradually** instead of instantly — typically triggered by hover, focus, or JS class changes.

#### **1.1. Syntax**

```css
transition: property duration timing-function delay;
```

Example:

```css
button {
  background: #007bff;
  transition: background 0.3s ease;
}
button:hover {
  background: #0056b3;
}
```

---

#### **1.2. Sub-properties**

You can write them separately for clarity:

```css
transition-property: background, transform;
transition-duration: 0.3s, 0.5s;
transition-timing-function: ease-in-out;
transition-delay: 0.1s;
```

---

#### **1.3. Timing Functions**

| Value                          | Behavior                                    |
| ------------------------------ | ------------------------------------------- |
| `linear`                       | constant speed                              |
| `ease`                         | default (slow start, fast middle, slow end) |
| `ease-in`                      | slow start                                  |
| `ease-out`                     | slow end                                    |
| `ease-in-out`                  | smooth both ends                            |
| `cubic-bezier(x1, y1, x2, y2)` | fully custom curve                          |

Example:

```css
transition-timing-function: cubic-bezier(
  0.4,
  0,
  0.2,
  1
); /* material design curve */
```

---

#### **1.4. Multiple Transitions**

You can animate several properties:

```css
transition: background 0.3s ease, transform 0.2s ease;
```

✅ **Good candidates for transitions:** `opacity`, `transform`, `color`, `background-color`.

⚠️ Avoid heavy properties like `width`, `height`, `margin` — they trigger reflow and are less performant.

---

### 2. **Transforms**

The `transform` property changes how elements appear in 2D or 3D space — **without affecting layout**.
It’s GPU-accelerated and extremely smooth for animations.

---

#### **2.1. Translate**

Moves an element along X or Y axis (does not affect document flow).

```css
transform: translateX(50px);
transform: translateY(-20px);
transform: translate(50px, 20px);
```

Useful for sliding animations, dropdowns, modals, etc.

---

#### **2.2. Rotate**

Rotates the element by an angle.

```css
transform: rotate(45deg);
```

You can also specify a rotation point:

```css
transform-origin: center center;
```

---

#### **2.3. Scale**

Resizes an element proportionally.

```css
transform: scale(1.2); /* 20% larger */
transform: scaleX(1.5); /* stretch horizontally */
transform: scaleY(0.5); /* compress vertically */
```

Use for hover effects, zooms, or pop animations.

---

#### **2.4. Skew**

Tilts an element.

```css
transform: skewX(15deg);
transform: skewY(-10deg);
transform: skew(10deg, 5deg);
```

---

#### **2.5. Combining Multiple Transforms**

You can chain them:

```css
transform: translate(20px, 20px) rotate(10deg) scale(1.1);
```

⚠️ Order matters — they apply sequentially.

---

### 3. **Animations (@keyframes)**

While transitions animate between **two states**, keyframes allow **multi-step animations** and **continuous looping**.

---

#### **3.1. Basic Syntax**

```css
@keyframes slideIn {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0);
  }
}
```

Apply to an element:

```css
.box {
  animation-name: slideIn;
  animation-duration: 0.6s;
  animation-timing-function: ease-out;
  animation-fill-mode: forwards;
}
```

---

#### **3.2. Percentage-based Keyframes**

More control with intermediate steps:

```css
@keyframes pulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}
```

---

#### **3.3. Animation Properties**

| Property                    | Purpose                                 |
| --------------------------- | --------------------------------------- |
| `animation-name`            | name of the keyframes                   |
| `animation-duration`        | time per cycle                          |
| `animation-timing-function` | same as transitions                     |
| `animation-delay`           | delay before start                      |
| `animation-iteration-count` | number or `infinite`                    |
| `animation-direction`       | `normal`, `reverse`, `alternate`        |
| `animation-fill-mode`       | `none`, `forwards`, `backwards`, `both` |
| `animation-play-state`      | `running` or `paused`                   |

---

#### **3.4. Example: Bouncing Ball**

```css
@keyframes bounce {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-100px);
  }
}

.ball {
  animation: bounce 1s ease-in-out infinite alternate;
}
```

- `infinite` → repeats endlessly
- `alternate` → reverses direction each time

---

#### **3.5. Shorthand**

All animation sub-properties in one line:

```css
animation: bounce 1s ease-in-out 0s infinite alternate forwards;
```

Order:
`name duration timing delay iteration direction fill-mode play-state`

---

### 4. **Will-change & GPU Acceleration**

The `will-change` property hints the browser about **which properties will change**, so it can optimize rendering ahead of time.

```css
.card {
  will-change: transform, opacity;
}
```

✅ **Use Cases:**

- Elements that will animate frequently (hover transitions, sliders, modals)
- Improves performance by moving elements to GPU layers

⚠️ **Caution:**

- Don’t apply `will-change` to too many elements — it consumes extra memory.
- Only use it right before an animation (e.g., on hover or when active).

---

### 💡 **Performance Tips**

- Use **`transform` + `opacity`** for animations — both are GPU-accelerated.
- Avoid animating layout-affecting properties (`top`, `left`, `width`, `height`).
- Keep animations under **60 FPS** for smooth performance.
- Use **`requestAnimationFrame()`** for JS-based animations if needed.

---

### ✅ **Summary Table**

| Concept         | Key Properties                                 | Description                   |
| --------------- | ---------------------------------------------- | ----------------------------- |
| **Transitions** | transition-property, duration, timing-function | Smooth state changes          |
| **Transforms**  | translate, rotate, scale, skew                 | Move, resize, rotate elements |
| **Animations**  | @keyframes, animation-\*                       | Multi-step, continuous motion |
| **Will-change** | will-change: transform, opacity                | Optimize GPU rendering        |

---
