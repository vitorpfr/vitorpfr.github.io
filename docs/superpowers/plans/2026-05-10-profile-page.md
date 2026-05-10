# Personal Profile Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the existing Drifting app landing page in `index.html` with a personal profile for Vitor Freitas at vfreitas.com.

**Architecture:** Single `index.html` file with inline CSS — no build tooling, no dependencies. Adapts the dark minimal aesthetic of the Drifting landing page (CSS variables, font stack, card components) with four new sections: hero, projects (with screenshot strip), about, footer.

**Tech Stack:** HTML5, CSS3 (inline in `index.html`). No JavaScript, no frameworks, no build step.

---

## File Map

| File | Action | Responsibility |
|------|--------|---------------|
| `index.html` | Rewrite | Entire page — structure + inline CSS |
| `photo.jpg` | Create (user-provided) | Circular profile photo in hero |
| `screenshots/screenshot1.png` | Copy from `../drifting/screenshots/` | Drifting app screenshot |
| `screenshots/screenshot2.png` | Copy from `../drifting/screenshots/` | Drifting app screenshot |
| `screenshots/screenshot3.png` | Copy from `../drifting/screenshots/` | Drifting app screenshot |
| `screenshots/screenshot4.png` | Copy from `../drifting/screenshots/` | Drifting app screenshot |

---

### Task 1: Copy Drifting screenshots into profile repo

**Files:**
- Create: `screenshots/screenshot1-4.png` (copied from `../drifting/screenshots/`)

- [ ] **Step 1: Copy screenshots**

```bash
cp -r ../drifting/screenshots ./screenshots
```

- [ ] **Step 2: Verify files are present**

```bash
ls screenshots/
```

Expected output:
```
screenshot1.png
screenshot2.png
screenshot3.png
screenshot4.png
```

- [ ] **Step 3: Commit**

```bash
git add screenshots/
git commit -m "feat: add Drifting app screenshots"
```

---

### Task 2: Rewrite index.html — base structure and CSS tokens

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace the entire contents of `index.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Vitor Freitas</title>
  <meta name="description" content="Software engineer. I write code for a living. Sometimes for fun too." />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #080808;
      --surface: #111111;
      --border: #222222;
      --text: #f0f0f0;
      --muted: #888888;
      --accent: #a07af0;
    }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      line-height: 1.6;
      -webkit-font-smoothing: antialiased;
    }

    a { color: inherit; text-decoration: none; }
  </style>
</head>
<body>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify dark background**

```bash
open index.html
```

Expected: blank dark page with `#080808` background.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: initialize profile page with base structure and CSS tokens"
```

---

### Task 3: Hero section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add hero CSS inside `<style>` (before the closing `</style>` tag)**

```css
    /* Hero */
    .hero {
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
      padding: 80px 24px 64px;
    }

    .hero-photo {
      width: 96px;
      height: 96px;
      border-radius: 50%;
      margin-bottom: 24px;
      box-shadow: 0 8px 32px rgba(0,0,0,0.6);
      object-fit: cover;
      background: var(--surface);
    }

    .hero h1 {
      font-size: 48px;
      font-weight: 700;
      letter-spacing: -1px;
      margin-bottom: 8px;
    }

    .hero-tagline {
      font-size: 20px;
      color: var(--text);
      margin-bottom: 6px;
    }

    .hero-sub {
      font-size: 15px;
      color: var(--muted);
      margin-bottom: 32px;
    }

    .social-links {
      display: flex;
      gap: 16px;
      align-items: center;
    }

    .social-links a {
      color: var(--muted);
      transition: color 0.2s;
      display: flex;
    }

    .social-links a:hover { color: var(--text); }

    .social-links svg {
      width: 22px;
      height: 22px;
      fill: currentColor;
    }
```

- [ ] **Step 2: Add hero HTML inside `<body>`**

```html
  <section class="hero">
    <img class="hero-photo" src="photo.jpg" alt="Vitor Freitas" />
    <h1>Vitor Freitas</h1>
    <p class="hero-tagline">I write code for a living. Sometimes for fun too.</p>
    <p class="hero-sub">Fintech engineer — previously Nubank, now Toast.</p>
    <div class="social-links">
      <a href="https://github.com/vitorpfr" target="_blank" rel="noopener" aria-label="GitHub">
        <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M12 0C5.374 0 0 5.373 0 12c0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23A11.509 11.509 0 0112 5.803c1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576C20.566 21.797 24 17.3 24 12c0-6.627-5.373-12-12-12z"/></svg>
      </a>
      <a href="https://www.linkedin.com/in/vitorpfreitas/" target="_blank" rel="noopener" aria-label="LinkedIn">
        <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
      </a>
    </div>
  </section>
```

- [ ] **Step 3: Open in browser and verify**

```bash
open index.html
```

Expected: centered hero with a grey circle where the photo will go (broken image shows grey bg), name in large bold text, tagline, muted fintech line, GitHub and LinkedIn SVG icons below.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add hero section"
```

---

### Task 4: Projects section — Drifting card and screenshot strip

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add projects CSS inside `<style>` (before closing `</style>`)**

```css
    /* Shared section wrapper */
    .section {
      max-width: 600px;
      margin: 0 auto;
      padding: 0 24px 64px;
    }

    .section-title {
      font-size: 11px;
      font-weight: 600;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 20px;
    }

    /* Project card */
    .project-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 20px 24px;
    }

    .project-card h3 {
      font-size: 17px;
      font-weight: 600;
      margin-bottom: 6px;
    }

    .project-card p {
      font-size: 14px;
      color: var(--muted);
      line-height: 1.5;
    }

    .project-card a {
      display: inline-block;
      margin-top: 12px;
      font-size: 13px;
      color: var(--accent);
    }

    .project-card a:hover {
      text-decoration: underline;
      text-underline-offset: 3px;
    }

    /* Screenshot strip */
    .screenshots-outer {
      padding-bottom: 64px;
    }

    .screenshots {
      display: flex;
      justify-content: center;
      gap: 16px;
      padding: 24px 24px 0;
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
      scrollbar-width: none;
    }

    .screenshots::-webkit-scrollbar { display: none; }

    .screenshots img {
      height: 460px;
      width: auto;
      border-radius: 28px;
      box-shadow: 0 16px 48px rgba(0,0,0,0.7);
      flex-shrink: 0;
    }
```

- [ ] **Step 2: Add projects HTML inside `<body>`, after the hero `<section>`**

```html
  <section class="section">
    <p class="section-title">Projects</p>
    <div class="project-card">
      <h3>Drifting</h3>
      <p>An iOS radio app I built. Visualizes music as it plays.</p>
      <a href="https://github.com/vitorpfr" target="_blank" rel="noopener">GitHub →</a>
    </div>
  </section>

  <div class="screenshots-outer">
    <div class="screenshots">
      <img src="screenshots/screenshot1.png" alt="Drifting visualization" />
      <img src="screenshots/screenshot2.png" alt="Drifting Alchemy theme" />
      <img src="screenshots/screenshot3.png" alt="Drifting saved stations" />
      <img src="screenshots/screenshot4.png" alt="Drifting Plus" />
    </div>
  </div>
```

- [ ] **Step 3: Open in browser and verify**

```bash
open index.html
```

Expected: "PROJECTS" label, Drifting card with description and purple GitHub link, horizontal strip of phone screenshots below (centered on desktop, scrollable on mobile).

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add projects section with Drifting card and screenshots"
```

---

### Task 5: About section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add about CSS inside `<style>` (before closing `</style>`)**

```css
    /* About */
    .about-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 16px;
    }

    .about-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 18px 20px;
    }

    .about-card-label {
      font-size: 11px;
      font-weight: 600;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 8px;
    }

    .about-card p {
      font-size: 14px;
      color: var(--muted);
      line-height: 1.5;
    }
```

- [ ] **Step 2: Add about HTML inside `<body>`, after the `.screenshots-outer` div**

```html
  <section class="section">
    <p class="section-title">About</p>
    <div class="about-grid">
      <div class="about-card">
        <p class="about-card-label">Where</p>
        <p>Dublin, Ireland. Senior Engineer &amp; Tech Lead at Toast.</p>
      </div>
      <div class="about-card">
        <p class="about-card-label">Stack</p>
        <p>Mostly Java, Kotlin, Clojure — open to whatever gets it done</p>
      </div>
      <div class="about-card">
        <p class="about-card-label">Outside work</p>
        <p>Playing drums and bass, catching live concerts</p>
      </div>
    </div>
  </section>
```

- [ ] **Step 3: Open in browser and verify**

```bash
open index.html
```

Expected: "ABOUT" label, 3 cards side by side — Where, Stack, Outside work — each with a small purple uppercase label and muted body text.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add about section"
```

---

### Task 6: Footer

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add footer CSS inside `<style>` (before closing `</style>`)**

```css
    /* Footer */
    footer {
      border-top: 1px solid var(--border);
      padding: 32px 24px;
      text-align: center;
      font-size: 13px;
      color: var(--muted);
      display: flex;
      flex-direction: column;
      gap: 8px;
      align-items: center;
    }

    footer a {
      color: var(--muted);
      text-decoration: underline;
      text-underline-offset: 3px;
    }

    footer a:hover { color: var(--text); }
```

- [ ] **Step 2: Add footer HTML inside `<body>`, after the about `<section>`**

```html
  <footer>
    <span>© 2026 Vitor Freitas</span>
    <span>
      <a href="https://github.com/vitorpfr" target="_blank" rel="noopener">GitHub</a>
      &nbsp;·&nbsp;
      <a href="https://www.linkedin.com/in/vitorpfreitas/" target="_blank" rel="noopener">LinkedIn</a>
      &nbsp;·&nbsp;
      <a href="mailto:hello@vfreitas.com">hello@vfreitas.com</a>
    </span>
  </footer>
```

- [ ] **Step 3: Open in browser and verify**

```bash
open index.html
```

Expected: thin border line at top, copyright, three links separated by dots — GitHub, LinkedIn, hello@vfreitas.com.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add footer"
```

---

### Task 7: Responsive styles

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add responsive CSS inside `<style>` (before closing `</style>`)**

```css
    @media (max-width: 600px) {
      .hero h1 { font-size: 36px; }
      .hero-tagline { font-size: 17px; }
      .screenshots img { height: 360px; border-radius: 22px; }
      .about-grid { grid-template-columns: 1fr; }
    }
```

- [ ] **Step 2: Verify on mobile viewport**

Open DevTools in your browser (Cmd+Option+I on Mac → Cmd+Shift+M for device toolbar). Select iPhone 12 Pro (390px wide).

Expected:
- Hero `h1` is smaller (36px)
- About cards stack into a single column
- Screenshots are shorter but still horizontally scrollable

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add responsive styles"
```

---

### Task 8: Add profile photo

**Files:**
- Create: `photo.jpg`

- [ ] **Step 1: Copy your photo into the repo root, named `photo.jpg`**

Place it at the same level as `index.html`. Crop it square before copying — the CSS will apply `border-radius: 50%` and `object-fit: cover`, so a square crop ensures the face is centered.

- [ ] **Step 2: Open in browser and verify**

```bash
open index.html
```

Expected: circular photo appears in the hero section where the broken image placeholder was.

- [ ] **Step 3: Commit**

```bash
git add photo.jpg
git commit -m "feat: add profile photo"
```
