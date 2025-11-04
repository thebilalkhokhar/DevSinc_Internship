Let’s dive deep into **HTML APIs**, a major part of modern web development.
You’ll get a full explanation of each topic — **HTML Web APIs**, **Geolocation**, **Drag and Drop**, **Web Storage**, **Web Workers**, and **Server-Sent Events (SSE)** — with syntax, attributes, use cases, and examples.

---

## ⚙️ **HTML APIs Overview**

An **API (Application Programming Interface)** is a set of functions that allow web applications to interact with the **browser**, **device**, or **server**.

**HTML APIs** (or **Web APIs**) are built into browsers to perform specific tasks, such as:

- Detecting location
- Storing data locally
- Handling drag-and-drop
- Running background threads
- Receiving real-time updates

These APIs are accessed using **JavaScript**.

---

## 🌐 **HTML Web APIs**

The **Web API** is not a single thing — it’s a collection of interfaces for browser features.
Some of the most used APIs include:

| API                          | Purpose                                                 |
| ---------------------------- | ------------------------------------------------------- |
| **Geolocation API**          | Get the user’s physical location                        |
| **Web Storage API**          | Store data in browser (local/session)                   |
| **Drag and Drop API**        | Drag and drop elements in the browser                   |
| **Web Workers API**          | Run background scripts without blocking the main thread |
| **Server-Sent Events (SSE)** | Receive real-time data updates from server              |
| **Canvas API**               | Draw graphics dynamically                               |
| **Fetch API**                | Request data from servers                               |
| **WebSocket API**            | Real-time bidirectional communication                   |

Let’s explore each in full depth.

---

## 📍 **HTML Geolocation API**

The **Geolocation API** allows websites to **get the user's current geographical location** (latitude and longitude).

### ✅ Syntax

```js
navigator.geolocation.getCurrentPosition(successCallback, errorCallback);
```

### 🧠 Parameters

- `successCallback` → function to run if location is found
- `errorCallback` → function to run if there’s an error (like permission denied)

---

### 📘 Example

```html
<button onclick="getLocation()">Get My Location</button>
<p id="demo"></p>

<script>
  function getLocation() {
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(showPosition, showError);
    } else {
      document.getElementById("demo").innerHTML = "Geolocation not supported.";
    }
  }

  function showPosition(position) {
    document.getElementById("demo").innerHTML =
      "Latitude: " +
      position.coords.latitude +
      "<br>Longitude: " +
      position.coords.longitude;
  }

  function showError(error) {
    switch (error.code) {
      case error.PERMISSION_DENIED:
        alert("User denied the request for Geolocation.");
        break;
      case error.POSITION_UNAVAILABLE:
        alert("Location information is unavailable.");
        break;
      case error.TIMEOUT:
        alert("The request to get user location timed out.");
        break;
      default:
        alert("An unknown error occurred.");
    }
  }
</script>
```

---

### ⚙️ Properties of `position.coords`

- `latitude` → numeric value
- `longitude` → numeric value
- `accuracy` → meters of precision
- `altitude`, `speed`, `heading` → optional

---

### ⚠️ Privacy Note

- Browser asks for **user permission** before sharing location.
- Works best with HTTPS.

---

### 📍 Use Cases

- Maps and navigation
- Weather or delivery apps
- Location-based services (ride-hailing, nearby search)

---

## 🖱️ **HTML Drag and Drop API**

This API allows you to **drag elements** (like images or text) and **drop** them into target areas — using only HTML + JavaScript.

---

### ✅ Steps to Use Drag and Drop

1. Set an element to be draggable:

   ```html
   <img draggable="true" />
   ```

2. Define drag events:

   - `ondragstart` → When dragging starts
   - `ondragover` → When dragging over a target
   - `ondrop` → When the element is dropped

---

### 📘 Example

```html
<p>Drag the logo into the box:</p>

<img
  id="drag1"
  src="logo.png"
  draggable="true"
  ondragstart="drag(event)"
  width="100"
/>

<div
  id="dropzone"
  ondrop="drop(event)"
  ondragover="allowDrop(event)"
  style="width:200px; height:200px; border:2px dashed gray;"
></div>

<script>
  function allowDrop(e) {
    e.preventDefault();
  }

  function drag(e) {
    e.dataTransfer.setData("text", e.target.id);
  }

  function drop(e) {
    e.preventDefault();
    const data = e.dataTransfer.getData("text");
    e.target.appendChild(document.getElementById(data));
  }
</script>
```

---

### 🧠 Common Events

| Event         | Description                            |
| ------------- | -------------------------------------- |
| `ondragstart` | Fired when drag begins                 |
| `ondragover`  | Fired when dragged item is over target |
| `ondrop`      | Fired when item is dropped             |
| `ondragenter` | When dragged item enters drop area     |
| `ondragleave` | When dragged item leaves drop area     |

---

### 📦 Use Cases

- File uploads
- Rearranging items (e.g., Trello boards)
- Custom UI interactions

---

## 💾 **HTML Web Storage API**

The **Web Storage API** stores data **locally** in the browser — more securely and easily than cookies.

There are two types:

| Storage Type       | Lifetime                 | Access Scope     |
| ------------------ | ------------------------ | ---------------- |
| **localStorage**   | Until manually cleared   | Same domain      |
| **sessionStorage** | Until tab/browser closed | Same tab/session |

---

### ✅ Syntax

#### ➤ localStorage

```js
localStorage.setItem("name", "Bilal");
localStorage.getItem("name"); // "Bilal"
localStorage.removeItem("name");
localStorage.clear();
```

#### ➤ sessionStorage

```js
sessionStorage.setItem("count", 1);
sessionStorage.getItem("count");
```

---

### ⚙️ Key Characteristics

- Stores **key-value pairs** (both as strings).
- Persistent and isolated per domain.
- Maximum capacity ≈ **5–10 MB** (cookies only 4 KB).
- No data sent with every HTTP request (unlike cookies).

---

### 📘 Example

```html
<button onclick="saveName()">Save Name</button>
<button onclick="showName()">Show Name</button>

<script>
  function saveName() {
    localStorage.setItem("username", "Bilal");
  }
  function showName() {
    alert(localStorage.getItem("username"));
  }
</script>
```

---

### 📱 Use Cases

- Saving user preferences
- Caching form input
- Offline mode data
- Light-weight app state storage

---

## ⚙️ **HTML Web Workers API**

Web Workers allow you to run **background JavaScript** without blocking the main UI thread.

Useful for CPU-heavy tasks like:

- Large calculations
- Data processing
- File parsing

---

### ✅ Basic Setup

#### ➤ main.js

```js
const worker = new Worker("worker.js");

worker.postMessage("Start working");

worker.onmessage = function (event) {
  console.log("Received from worker:", event.data);
};
```

#### ➤ worker.js

```js
onmessage = function (event) {
  console.log("Worker received:", event.data);
  let sum = 0;
  for (let i = 0; i < 1e7; i++) sum += i;
  postMessage("Sum is: " + sum);
};
```

---

### ⚙️ How It Works

1. The **main script** creates a worker thread.
2. Messages are exchanged using `postMessage()` and `onmessage`.
3. Workers cannot access:

   - The DOM
   - Window or document objects
   - Parent script variables directly

---

### 🧠 Types of Workers

| Type                 | Description                           |
| -------------------- | ------------------------------------- |
| **Dedicated Worker** | For one script only                   |
| **Shared Worker**    | Can be used by multiple scripts/pages |

---

### 📦 Use Cases

- Real-time data computation
- Image or video processing
- Background synchronization

---

## 🔄 **HTML SSE (Server-Sent Events)**

**SSE (Server-Sent Events)** allow a browser to **receive automatic updates** from a server over a single, long-lived HTTP connection.

Unlike WebSockets, SSE is **one-way** (server → client).

---

### ✅ Basic Setup

#### ➤ Client (HTML/JS)

```html
<h3>Live Updates:</h3>
<div id="result"></div>

<script>
  if (typeof EventSource !== "undefined") {
    const source = new EventSource("updates.php");
    source.onmessage = function (event) {
      document.getElementById("result").innerHTML += event.data + "<br>";
    };
  } else {
    document.getElementById("result").innerHTML = "SSE not supported.";
  }
</script>
```

#### ➤ Server (PHP example)

```php
<?php
header('Content-Type: text/event-stream');
header('Cache-Control: no-cache');

$time = date('H:i:s');
echo "data: The time is {$time}\n\n";
flush();
?>
```

---

### ⚙️ Key Methods and Events

| Event       | Description                   |
| ----------- | ----------------------------- |
| `onmessage` | Receives data from the server |
| `onopen`    | Connection established        |
| `onerror`   | Connection error occurred     |

---

### 🧠 Advantages

- Simple to implement (uses HTTP)
- Auto-reconnect feature
- Ideal for live notifications or dashboards

---

### 🧩 Use Cases

- Live stock or weather updates
- Real-time dashboards
- Notifications (e.g., chat or order tracking)

---

## 🧭 **Summary Table**

| API                   | Function               | Communication Direction |
| --------------------- | ---------------------- | ----------------------- |
| **Geolocation API**   | Get user’s coordinates | N/A                     |
| **Drag and Drop API** | Move elements visually | User-driven             |
| **Web Storage API**   | Store data in browser  | Local only              |
| **Web Workers API**   | Background scripts     | Internal                |
| **SSE**               | Receive live updates   | Server → Client         |

---

### ✅ Final Takeaway

- **Geolocation:** Find where the user is.
- **Drag and Drop:** Create intuitive UIs.
- **Web Storage:** Keep data persistently in browser.
- **Web Workers:** Perform background tasks smoothly.
- **SSE:** Stream real-time updates efficiently.

---
