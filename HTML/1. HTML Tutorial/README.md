# HTML — Complete detailed guide

Below is a thorough, practical explanation of every topic you listed. I’ll cover definitions, syntax, examples, common pitfalls, accessibility/SEO notes, and best practices for each subtopic. Because you asked not to skip anything, I’ll be exhaustive but kept readable with examples.

---

# HTML HOME (Overview)

**What it is:** HTML (HyperText Markup Language) is the standard language for structuring content on the web. It uses elements (tags) to describe headings, paragraphs, lists, links, images, and more. Browsers parse HTML and render a web page.

**Role in the web:** Structure (HTML) + Presentation (CSS) + Behavior (JavaScript). HTML is semantic markup — it should describe _what_ content is, not _how_ it looks.

**File extension & MIME:** `.html` or `.htm`. MIME type `text/html`.

---

# HTML Introduction

- **Document model:** An HTML document is a tree of nodes (DOM — Document Object Model). Elements nest inside each other.
- **Basic flow:** Browser requests `.html`, parses tags, builds DOM, applies CSS, runs JS, paints page.
- **Doctype:** `<!doctype html>` — tells browser to use modern HTML (HTML5) mode.

Example minimal page:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example</title>
  </head>
  <body>
    <h1>Hello</h1>
    <p>Welcome.</p>
  </body>
</html>
```

---

# HTML Editors

Options range from simple to advanced:

- **Text editors:** Notepad, TextEdit (basic).
- **Code editors:** VS Code (recommended), Sublime Text, Atom, WebStorm.
- **WYSIWYG:** Dreamweaver, online site-builders (for non-developers).
- **Browser devtools:** Edit HTML live (Chrome DevTools, Firefox DevTools).
  **Tips:** Use an editor with syntax highlighting, Emmet, linters (HTMLHint), and live server extension.

---

# HTML Basic (Core concepts)

- **Elements** are `<tagname>content</tagname>` or self-closing: `<img ... />` (HTML permits without trailing slash).
- **Nesting rules:** Proper nesting (open/close order). E.g. `<b><i>text</i></b>` OK; `<b><i>text</b></i>` wrong.
- **Case-insensitive (HTML):** Tags are usually lowercase by convention.
- **Whitespace:** Browsers collapse consecutive spaces into one (use `<pre>` to preserve).
- **Document metadata:** inside `<head>` (charset, title, links, meta).

---

# HTML Elements

- **Definition:** Building blocks: `<p>`, `<a>`, `<div>`, etc.
- **Structure:** Start tag, content, end tag. Some void elements have no closing tag: `<img>`, `<br>`, `<hr>`, `<input>`, `<meta>`, `<link>`.
- **Custom elements:** Web Components `<my-component>` possible; requires JS to define behavior.
- **ARIA roles & semantic tags:** Enhance accessibility when semantics are unclear.

---

# HTML Attributes

- **Syntax:** `<tag attr="value">`. Some attributes boolean: `<input disabled>`.
- **Global attributes:** `id`, `class`, `style`, `title`, `data-*`, `lang`, `dir`, `hidden`, `tabindex`, `draggable`.
- **ARIA attributes:** `role`, `aria-label`, `aria-hidden`, `aria-expanded` for accessibility.
- **Event attributes:** `onclick`, `oninput` (inline JS — generally avoid).
- **Data attributes:** `data-user-id="123"` — accessible via `element.dataset.userId` in JS.
- **Security:** Never place secrets in attributes (e.g., API keys).

---

# HTML Headings

- Tags: `<h1>` through `<h6>`. `<h1>` is top-level.
- **Semantic use:** Headings define document outline and help SEO and screen readers.
- **Best practice:** One `<h1>` per page (often), then hierarchical `<h2>` → `<h3>` etc.
- **Styling:** Do not use headings purely for size — use CSS for visual control.

Example:

```html
<h1>Site Title</h1>
<h2>Section</h2>
<h3>Subsection</h3>
```

---

# HTML Paragraphs

- Tag: `<p>Paragraph text</p>`.
- Paragraphs cannot contain block-level elements like `<div>` (in HTML5 some blocks can be nested differently, but keep semantic rules).
- Use `<br>` for forced line break, but avoid excessive `<br>` for spacing — use CSS margin/padding.

---

# HTML Styles

- **Inline styles:** `<p style="color: red;">` — quick but bad for maintainability.
- **Internal styles:** `<style> /* CSS */ </style>` inside `<head>` — useful for page-specific CSS.
- **External stylesheet:** `<link rel="stylesheet" href="styles.css">` — best practice for caching and separation of concerns.
- **Cascading & specificity:** Order matters (later rules override earlier). Specificity: inline > id > class > element.
- **Best practices:** Keep styles in external files, minimize inline styles, use classes for reusable rules.

---

# HTML Formatting (text-level semantic tags)

- **Bold/strong:** `<b>` (presentational) vs `<strong>` (semantic importance).
- **Italic/emphasis:** `<i>` vs `<em>` (semantic emphasis).
- **Underline:** `<u>` (usually avoid — can be confused with links).
- **Small:** `<small>` for fine print.
- **Marked text:** `<mark>highlight</mark>`.
- **Deleted/inserted:** `<del>`, `<ins>`.
- **Superscript/subscript:** `<sup>`, `<sub>`.
- **Code vs preformatted:** `<code>` for code fragments, `<pre>` to preserve whitespace.

Always prefer semantic tags (`<strong>`,`<em>`) over purely presentational ones.

---

# HTML Quotations

- **Inline quote:** `<q>Quoted text</q>` — browser may insert quotation marks.
- **Block quote:** `<blockquote cite="source-url">Long quoted block</blockquote>` — for longer quotes or excerpts.
- **Cite:** `<cite>Source title</cite>` — for works; don't confuse with `cite` attribute.
- **Accessibility:** Provide attribution if needed; use `cite` attribute for source URL.

---

# HTML Comments

- Syntax: `<!-- This is a comment -->`
- Use for developer notes; not visible to users. Avoid leaving sensitive info in comments.
- Conditional comments (old IE) are obsolete.

---

# HTML Colors

- **Hex:** `#RRGGBB` (e.g. `#ff0000`), `#RGB` shorthand.
- **RGB:** `rgb(255,0,0)`, **RGBA:** `rgba(255,0,0,0.5)` (alpha transparency).
- **HSL:** `hsl(120, 100%, 50%)`, **HSLA** with alpha.
- **Named colors:** `red`, `blue` (limited list).
- **Best practice:** Use variables (`--primary-color`) in CSS for maintainability.

---

# HTML CSS (how to use CSS with HTML)

- **Link external:** `<link rel="stylesheet" href="styles.css">`
- **Embedded:** `<style>` in `<head>`.
- **Inline:** `style="..."` on an element.
- **Preprocessors:** SASS/LESS compile to CSS; use build tools in larger projects.
- **Responsive:** Use media queries, flexbox, grid, relative units (%, em, rem).

---

# HTML Links

- Tag: `<a href="url">link text</a>`
- **Absolute vs relative URLs:** `https://example.com/page` vs `./page.html` or `/folder/page.html`.
- **Open in new tab:** `target="_blank"` **must** include `rel="noopener noreferrer"` for security/performance.
- **Mailto/tel:** `href="mailto:me@example.com"`, `href="tel:+123456789"`.
- **Anchor links:** `href="#section-id"` jumps to element with `id="section-id"`.
- **Accessibility:** Link text should be descriptive ("Read about accessibility", not "click here").

---

# HTML Images

- Tag: `<img src="image.jpg" alt="Description" width="..." height="...">`
- **Required:** `alt` attribute — essential for accessibility and SEO. If purely decorative, `alt=""`.
- **Responsive images:** `srcset` and `sizes` let browser pick best image:

```html
<img
  src="small.jpg"
  srcset="small.jpg 480w, medium.jpg 800w, large.jpg 1600w"
  sizes="(max-width:600px) 480px, 800px"
  alt="..."
/>
```

- **Lazy loading:** `loading="lazy"` delays offscreen images.
- **Formats:** JPEG (photos), PNG (transparency), SVG (vector), WebP/AVIF (modern compressed).
- **Security:** Don't load untrusted SVG inline without sanitizing.

---

# HTML Favicon

- Small icon shown in tab/bookmarks.
- Add in `<head>`:

```html
<link rel="icon" href="/favicon.ico" sizes="any" />
<link rel="icon" type="image/png" href="/favicon-32x32.png" />
```

- Provide multiple sizes and formats for different devices; include `apple-touch-icon` for iOS.

---

# HTML Page Title

- `<title>Page title</title>` inside `<head>`. Shows in browser tab and search engine results.
- **Best practice:** Keep concise and descriptive; include brand and page topic.

---

# HTML Tables

- Structure:

```html
<table>
  <caption>
    Table title
  </caption>
  <thead>
    <tr>
      <th>Heading</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Data</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Footer</td>
    </tr>
  </tfoot>
</table>
```

- **Cells:** `<th>` for header cells (scope can be `row` or `col`), `<td>` for data.
- **Span:** `colspan="2"`, `rowspan="3"`.
- **Accessibility:** Use `<caption>`, `scope` on `<th>`, and avoid using tables for layout.
- **Styling:** Use CSS to control table layout; `table-layout: fixed` helps predictability.

---

# HTML Lists

- **Unordered:** `<ul><li>Item</li></ul>`
- **Ordered:** `<ol><li>Item</li></ol>`
- **Description list:** `<dl><dt>Term</dt><dd>Definition</dd></dl>`
- **Nested lists:** Allowed; mind semantic structure and visual indentation with CSS.
- **Accessibility:** Proper markup helps screen readers enumerate list items.

---

# HTML Block & Inline

- **Block-level elements** generate a block box that spans width: `<div>`, `<p>`, `<h1>`, `<ul>`, `<section>`.
- **Inline elements** flow inside line: `<span>`, `<a>`, `<img>`, `<strong>`.
- **CSS display:** Use `display: block`, `inline`, `inline-block`, `flex`, `grid` to change behavior.
- **Best practice:** Use semantic block elements for structure; inline elements for small text-level adjustments.

---

# HTML Div

- `<div>` is a generic block container with no semantic meaning — used for grouping.
- **When to use:** When no semantic element fits. Prefer semantic elements (`section`, `article`, etc.) when possible.
- **Styling and layout:** Often used as flex/grid containers.

---

# HTML Classes

- `class="btn primary large"`
- Used for styling and JS selection: `document.querySelectorAll('.btn')`.
- Multiple elements can share the same class (reusable).
- **Naming conventions:** BEM (Block**Element--Modifier) improves maintainability: `.card**title--large`.
- **Selectors:** `.class`, `.parent .child`, `.class:hover`.

---

# HTML Id

- `id="main-header"` — must be unique within a document.
- Used for anchors (`#main-header`), JS select (`#id`), and high-specificity CSS (`#id`).
- **Best practice:** Use IDs sparingly; prefer classes for styling. IDs are useful for fragments and accessibility references.

---

# HTML Iframes

- `<iframe src="..."></iframe>` — embeds another HTML page.
- **Use cases:** Embedding external content (maps, videos), sandboxed widgets.
- **Attributes:** `width`, `height`, `loading="lazy"`, `title` (required for accessibility).
- **Security:** Use `sandbox` attribute to restrict capabilities (e.g. `sandbox="allow-scripts"`). Prevent clickjacking with `X-Frame-Options` on server.
- **Performance:** Iframes can be expensive; prefer direct inclusion when possible.

---

# HTML JavaScript

- **Embedding JS:** `<script src="script.js"></script>` or inline `<script>/* code */</script>`.
- **Placement:**

  - In `<head>` with `defer` (`<script src="app.js" defer></script>`) — file downloads early but executes after parsing.
  - Or before `</body>` to avoid blocking.

- **Async vs Defer:**

  - `async`: download + execute as soon as ready (not guaranteed order).
  - `defer`: executes in order after parsing.

- **Event handlers:** Prefer `addEventListener` in JS over inline `onclick`.
- **Modules:** `<script type="module" src="module.js"></script>` uses ES modules, supports `import`/`export`.
- **Security:** Avoid inline JS where possible; Content Security Policy (CSP) can mitigate XSS.

---

# HTML File Paths

- **Relative paths:** `images/pic.jpg`, `../assets/style.css`.
- **Root-relative:** `/assets/script.js` (starts from domain root).
- **Absolute:** `https://domain.com/path`.
- **Data URLs:** `src="data:image/png;base64,...."` embed small resources inline (use sparingly).
- **Best practice:** For portability keep relative paths coherent; use consistent structure (e.g., `/assets`, `/images`, `/css`).

---

# HTML Head

- Contains metadata and resources:

  - `<meta charset="utf-8">` — character encoding (use UTF-8).
  - `<meta name="viewport" content="width=device-width, initial-scale=1">` — responsive.
  - `<title>` — page title.
  - `<link rel="stylesheet" href="...">` — CSS.
  - `<meta name="description" content="...">` — SEO snippet.
  - Open Graph tags (`og:title`, `og:image`) for social previews.
  - `<script defer src="...">` is also allowed.

- **Order:** Put `meta charset` first; `viewport` early.

---

# HTML Layout (basic techniques)

- **Traditional:** floats + clearfix (legacy).
- **Modern:** Flexbox (`display: flex`) for 1D layouts; CSS Grid (`display: grid`) for 2D layouts.
- **Containers:** `.container { max-width: 1200px; margin: 0 auto; padding: ... }`.
- **Positioning:** `static`, `relative`, `absolute`, `fixed`, `sticky`.
- **Best practices:** Use semantic containers (`header`, `main`, `footer`, `nav`) + flex/grid for layout.

---

# HTML Responsive

- **Viewport meta:** required for mobile-friendly pages.
- **Fluid units:** `%`, `vw`, `vh`, `em`, `rem` rather than fixed `px`.
- **Media queries:** `@media (max-width: 768px) { ... }`.
- **Responsive images:** `srcset`, `sizes`.
- **Mobile-first CSS:** write base styles for small screens, add media queries for larger screens.
- **Testing:** Resize browser devtools, test on multiple devices and orientations.

---

# HTML Computercode (code presentation)

- `<code>` for inline code, `<pre>` for preformatted blocks, `<samp>` for sample output, `<kbd>` for keyboard input.
  Example:

```html
<pre><code>function add(a, b) { return a + b; }</code></pre>
```

- For syntax highlighting, use JS libraries (Prism, highlight.js).

---

# HTML Semantics

- **Why semantics matter:** Improves accessibility, SEO, maintainability.
- **Common semantic elements:**

  - `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`, `<figure>`, `<figcaption>`.

- **When to use:** Use `article` for independent content, `section` for thematic grouping; `div` only when no semantic tag fits.
- **Screen readers & SEO** leverage semantics to understand page structure.

---

# HTML Style Guide (best practices)

- **Structure:** Consistent file layout and indentation.
- **Naming:** Meaningful class names; follow BEM or similar conventions.
- **Accessibility (a11y):** Alt text, semantic tags, keyboard focus states, ARIA where necessary.
- **Performance:** Minimize DOM size, defer non-critical resources, compress images, use caching.
- **Security:** Sanitize user input, use CSP, avoid inline JS/CSS for stricter CSP.
- **Validation:** Use validators (W3C HTML validator) and linters.
- **Comments & documentation:** Clear comments for complex sections.

---

# HTML Entities

- Represent reserved characters or special symbols: `&amp;` (`&`), `&lt;` (`<`), `&gt;` (`>`), `&quot;` (`"`), `&apos;` (`'` — not standard in older HTML versions but supported).
- Example: Show `<` literally: `&lt;div&gt;`.
- Named entities (many), numeric entities `&#8211;` (en dash) or hex `&#x2013;`.

---

# HTML Symbols

- Many common symbols available via entities: `&copy;`, `&reg;`, `&euro;`, `&mdash;`, etc.
- Use Unicode directly (`—`) when file encoding is UTF-8 and meta charset is set, but entities ensure compatibility.

---

# HTML Emojis

- Emojis are Unicode characters (e.g., 😊). Use them directly in UTF-8 pages.
- Accessibility: Provide context; screen readers read emoji names or may read them awkwardly — avoid crucial content relying only on emoji.
- Fallbacks: Not all devices render identical emoji styles.

---

# HTML Charsets

- **UTF-8** recommended: `<meta charset="utf-8">`.
- Charset must be declared early in `<head>`.
- Ensures consistent display of characters, emojis, non-Latin scripts.

---

# HTML URL Encode

- URL encoding (percent-encoding) replaces unsafe characters: space → `%20`, `?` → `%3F`.
- Use when building query strings or encoding form data.
- Example: `https://example.com/search?q=hello%20world`
- In forms with `enctype="application/x-www-form-urlencoded"` browsers encode values automatically.

---

# HTML vs. XHTML

- **HTML (HTML5):** More forgiving parser, void elements need no `/`, attribute quoting is recommended but flexible.
- **XHTML:** XML-based, stricter — tags must be well-formed, lower-case, attributes quoted, XML prolog required. Follows XML rules; served as `application/xhtml+xml`.
- **Practical:** Modern web uses HTML5. XHTML is rare for general websites.

---

# Extra: Accessibility & SEO (cross-cutting)

- **Accessibility:** Keyboard navigation, correct heading order, `alt` text, labels for inputs (`<label for="id">`), form validation helpful text, `aria-*` only when necessary, `role` if semantic elements absent.
- **SEO basics:** Title and meta description, semantic headings, proper use of `<h1>`, structured data (JSON-LD), fast load time, mobile-friendly layout.
- **Internationalization:** Set `lang` attribute on `<html lang="en">` for correct screen reader pronunciation.

---

# Extra: Common pitfalls & debugging

- **Missing charset** → garbled characters.
- **Forgetting `alt`** → accessibility issues and SEO penalties.
- **Inline JS/CSS overuse** → hard to maintain and problematic for CSP.
- **Using tables for layout** → harms accessibility and mobile responsiveness.
- **Broken relative paths** → 404 for assets; check base URL and folder structure.
- **Overusing `<div>`** — prefer semantics.

---

# Quick reference: Example full page with many concepts

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <title>Demo: HTML Concepts</title>
    <meta name="description" content="Demo page showing HTML best practices" />
    <link rel="stylesheet" href="/css/styles.css" />
  </head>
  <body>
    <header>
      <h1 id="site-title">Site Title</h1>
      <nav aria-label="Main navigation">
        <ul>
          <li><a href="#home">Home</a></li>
        </ul>
      </nav>
    </header>

    <main>
      <article>
        <h2>Article heading</h2>
        <p>
          This is a <strong>semantic</strong> paragraph with
          <code>inline code</code>.
        </p>
        <figure>
          <img src="/images/photo.jpg" alt="A descriptive alt" loading="lazy" />
          <figcaption>Photo caption</figcaption>
        </figure>
      </article>

      <section>
        <h2>Form</h2>
        <form action="/submit" method="post">
          <label for="email">Email</label>
          <input id="email" name="email" type="email" required />
          <button type="submit">Send</button>
        </form>
      </section>
    </main>

    <footer>
      <p>&copy; 2025 Example</p>
    </footer>

    <script src="/js/main.js" defer></script>
  </body>
</html>
```

---
