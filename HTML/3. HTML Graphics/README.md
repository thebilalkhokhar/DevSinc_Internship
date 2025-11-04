Let’s go through **HTML Graphics**, **Canvas**, and **SVG** in complete detail, point by point, with explanations of all key concepts, attributes, and examples.

---

## 🖼️ **HTML Graphics Overview**

HTML itself is for structuring content, but to create **visual graphics, drawings, shapes, and charts**, it relies on **Canvas** and **SVG**.

There are **three** main ways to display graphics on a webpage:

1. **HTML `<canvas>` element** – for dynamic, script-based (JavaScript) drawing.
2. **SVG (Scalable Vector Graphics)** – for vector-based graphics (resolution independent).
3. **CSS & Images** – not technically “graphics APIs” but also used for visuals (backgrounds, shapes, gradients).

---

### ✅ 1. **Canvas vs. SVG — The Core Difference**

| Feature            | Canvas                                                             | SVG                                            |
| ------------------ | ------------------------------------------------------------------ | ---------------------------------------------- |
| **Type**           | Raster (pixel-based)                                               | Vector (shape-based)                           |
| **Scalability**    | Loses quality when zoomed                                          | No loss of quality                             |
| **Performance**    | Better for lots of small objects or real-time updates (e.g. games) | Better for diagrams, charts, icons             |
| **Manipulation**   | Controlled via JavaScript drawing APIs                             | Controlled via DOM (each element is an object) |
| **Event Handling** | Manual (you calculate click regions)                               | Built-in (each shape can have event listeners) |

---

## 🎨 **HTML Canvas**

The `<canvas>` element is used to **draw graphics on the fly** via JavaScript.

### ✅ Basic Syntax

```html
<canvas id="myCanvas" width="300" height="200"></canvas>

<script>
  const c = document.getElementById("myCanvas");
  const ctx = c.getContext("2d"); // get drawing context
  ctx.fillStyle = "red"; // color
  ctx.fillRect(50, 50, 150, 100); // draw rectangle
</script>
```

---

### 🧠 Key Points About Canvas

- `<canvas>` is **just a container**. You must use JavaScript to draw inside it.
- You can draw:

  - Lines
  - Shapes
  - Text
  - Images
  - Gradients
  - Patterns
  - Animations

---

### 🧱 Common Canvas Methods

#### ➤ Drawing Rectangles

```js
ctx.fillRect(x, y, width, height); // filled rectangle
ctx.strokeRect(x, y, width, height); // rectangle outline
ctx.clearRect(x, y, width, height); // clear a region
```

#### ➤ Drawing Paths (custom shapes)

```js
ctx.beginPath();
ctx.moveTo(20, 20);
ctx.lineTo(200, 20);
ctx.lineTo(120, 100);
ctx.closePath();
ctx.stroke(); // outline
```

#### ➤ Colors & Styles

```js
ctx.fillStyle = "green";
ctx.strokeStyle = "blue";
ctx.lineWidth = 5;
```

#### ➤ Circles / Arcs

```js
ctx.beginPath();
ctx.arc(100, 75, 50, 0, 2 * Math.PI);
ctx.stroke();
```

#### ➤ Text

```js
ctx.font = "20px Arial";
ctx.fillText("Hello Canvas", 50, 50);
ctx.strokeText("Outlined", 50, 80);
```

#### ➤ Gradients

```js
const grad = ctx.createLinearGradient(0, 0, 200, 0);
grad.addColorStop(0, "red");
grad.addColorStop(1, "yellow");
ctx.fillStyle = grad;
ctx.fillRect(10, 10, 200, 100);
```

#### ➤ Images

```js
const img = new Image();
img.src = "photo.jpg";
img.onload = function () {
  ctx.drawImage(img, 10, 10, 200, 150);
};
```

#### ➤ Animations (using `requestAnimationFrame`)

```js
function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  // update position, redraw shape
  requestAnimationFrame(draw);
}
draw();
```

---

### ⚙️ Canvas Coordinate System

- Origin (0,0) is **top-left corner**.
- `x` increases → right
- `y` increases → down
- Units are **pixels**.

---

### 📱 Canvas Use Cases

- Game graphics
- Data visualization
- Particle effects
- Dynamic charts
- Photo editing

---

## 🧩 **HTML SVG (Scalable Vector Graphics)**

SVG is an **XML-based** language to define **2D vector graphics** using elements like `<rect>`, `<circle>`, `<line>`, `<path>`, and `<text>`.

---

### ✅ Basic Example

```html
<svg width="200" height="200">
  <circle
    cx="100"
    cy="100"
    r="80"
    stroke="green"
    stroke-width="4"
    fill="yellow"
  />
</svg>
```

This draws a **yellow circle** with a green border.

---

### 🧱 Common SVG Elements

| Element      | Description                       | Example                                                     |
| ------------ | --------------------------------- | ----------------------------------------------------------- |
| `<rect>`     | Rectangle                         | `<rect x="10" y="10" width="100" height="50" fill="blue"/>` |
| `<circle>`   | Circle                            | `<circle cx="60" cy="60" r="40" fill="red"/>`               |
| `<ellipse>`  | Ellipse                           | `<ellipse cx="80" cy="80" rx="60" ry="30" fill="orange"/>`  |
| `<line>`     | Straight line                     | `<line x1="10" y1="10" x2="100" y2="100" stroke="black"/>`  |
| `<polygon>`  | Closed shape with multiple points | `<polygon points="50,5 100,100 0,100" fill="lime"/>`        |
| `<polyline>` | Open series of lines              | `<polyline points="0,40 40,40 40,80 80,80" stroke="red"/>`  |
| `<path>`     | Custom shapes and curves          | `<path d="M150 0 L75 200 L225 200 Z" fill="purple"/>`       |
| `<text>`     | Add text                          | `<text x="10" y="50" fill="black">Hello SVG</text>`         |

---

### ⚙️ SVG Attributes

- `x`, `y`, `width`, `height` – position and size
- `fill` – fill color
- `stroke` – outline color
- `stroke-width` – border thickness
- `opacity` – transparency (0.0 to 1.0)

---

### 🧠 SVG Advantages

- Scales cleanly at any resolution (great for responsive design).
- Editable and readable as XML.
- CSS and JavaScript can style or animate it.
- Each shape is an element in the DOM → easy interactivity.

---

### 🎬 SVG Animations

Using `<animate>`:

```html
<circle cx="50" cy="50" r="40" fill="blue">
  <animate
    attributeName="cx"
    from="50"
    to="150"
    dur="2s"
    repeatCount="indefinite"
  />
</circle>
```

Using CSS or JS is also possible.

---

### 🧰 SVG in HTML

You can include SVG in three ways:

1. **Inline SVG** – directly in HTML.
2. **External file** – `<img src="shape.svg" />`.
3. **As background-image** in CSS.

---

### 📊 SVG Use Cases

- Logos and icons
- Charts and graphs
- Infographics
- Interactive maps
- Line art and illustrations

---

## 🧩 **Canvas vs SVG Summary Table**

| Feature       | Canvas                        | SVG                     |
| ------------- | ----------------------------- | ----------------------- |
| Rendering     | Pixel-based                   | Shape-based             |
| Animation     | Manual redraw with JS         | Built-in (CSS/SMIL)     |
| Performance   | Fast for thousands of objects | Slower for many objects |
| Interactivity | Manual                        | DOM-based               |
| Best For      | Games, animations             | Diagrams, charts, icons |

---

### ✅ Final Takeaway

- **Use Canvas** when performance and real-time rendering matter (games, visualizers).
- **Use SVG** when you need clarity, scalability, and easy manipulation (logos, charts, UI icons).

---
