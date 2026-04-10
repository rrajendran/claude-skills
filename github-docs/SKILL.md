---
name: github-docs
description: Use when asked to generate, create, or update project documentation as a GitHub-style dark-themed single-page HTML doc site. Triggers on "generate docs", "create docs", "write documentation", "update docs/index.html", or "document this project".
---

# GitHub Docs Style Generator

## Overview

Generates a polished, GitHub dark-themed single-page HTML documentation site (`docs/index.html`) for any project — no build tools, no dependencies, just one self-contained file.

The output mirrors GitHub's official dark documentation aesthetic: sidebar navigation, hero section, feature cards, collapsible API endpoints, callout boxes, pipeline flow diagrams, and tree-view project structures.

## When to Use

- User asks to "generate docs" or "create documentation" for a project
- User wants to update or regenerate `docs/index.html`
- User asks for a GitHub-style doc page
- Project has no docs or only a README

## Step-by-Step Process

### 1. Gather Project Intelligence

Before writing a single line of HTML, explore the project:

```
Read in this order (skip if not present):
1. README.md / README.rst — overview, quick start, badges
2. package.json / pyproject.toml / go.mod — name, version, stack
3. .env.example / config files — all configuration variables
4. Source entry points — understand the main modules/routes
5. API route files — endpoints, methods, auth requirements
6. docker-compose.yml / Dockerfile — deployment story
7. Any existing docs/ content — merge, don't discard
```

Use `Glob` + `Read` to explore. Never invent content — only document what you find.

### 2. Plan the Sections

Map what you found to these standard sections. Only include sections where you have real content:

| Section | Required | Trigger |
|---|---|---|
| Overview / Hero | Always | Project name + description |
| Quick Start | Always | Setup steps found |
| Architecture | When backend+frontend exist | Clear stack split |
| Project Structure | When structure is non-trivial | >2 layers deep |
| Configuration | When .env.example exists | Any config vars |
| API Reference | When routes exist | Any HTTP endpoints |
| Data Models / DB | When ORM models exist | Schema definitions |
| Authentication | When auth is present | JWT, OAuth, sessions |
| Deployment | When Dockerfile/compose exists | Infra instructions |
| Dependencies | When tech stack is notable | Libraries table |
| Roadmap | When TODO / roadmap exists | Future plans |

Build the sidebar nav from the sections you decide to include.

### 3. Use the CSS Template

**Read `template.html`** (in this skill's directory) — it contains the complete CSS and all HTML component patterns.

Copy the full `<style>` block and `<body>` skeleton from `template.html` into `docs/index.html`, then fill in project-specific content.

### 4. HTML Component Reference

Use these components from the template. Compose them to match your project's content.

**Hero (always first)**
```html
<div class="hero" id="overview">
  <h1>Project Name</h1>
  <p>One-sentence description.</p>
  <div class="hero-badges">
    <span class="hero-badge"><span class="dot dot-python"></span>Python 3.11+</span>
    <span class="hero-badge">🔐 JWT Auth</span>
  </div>
</div>
```
Dot colors: `dot-python` (#3572A5), `dot-ts` (#3178c6), `dot-ml` (#3fb950), `dot-go` (#00ADD8), `dot-rust` (#CE422B)

**Feature Cards grid (use after hero)**
```html
<div class="card-grid">
  <div class="card">
    <span class="card-icon">🤖</span>
    <h4>Feature Name</h4>
    <p>One line description.</p>
  </div>
</div>
```

**Pipeline flow**
```html
<div class="pipeline">
  <div class="pipeline-step">Step<small>subtitle</small></div>
  <span class="pipeline-arrow">→</span>
  <div class="pipeline-step">Step<small>subtitle</small></div>
</div>
```

**Callout boxes**
```html
<div class="callout callout-tip">
  <div class="callout-title">💡 Tip</div>
  Content here.
</div>
```
Types: `callout-note` (blue), `callout-tip` (green), `callout-warning` (yellow), `callout-danger` (red)

**Collapsible API endpoint**
```html
<div class="endpoint open">
  <div class="endpoint-header" onclick="this.parentElement.classList.toggle('open')">
    <span class="method-badge method-post">POST</span>
    <span class="endpoint-path">/api/route</span>
    <span class="auth-badge auth-protected">Protected</span>
    <span class="endpoint-desc">Description</span>
  </div>
  <div class="endpoint-body">
    <h5>Request Body</h5>
    <pre><code>{ ... }</code></pre>
    <h5>Response <code>200</code></h5>
    <pre><code>{ ... }</code></pre>
  </div>
</div>
```
Method badges: `method-get` (green), `method-post` (blue), `method-put` (yellow), `method-delete` (red)
Auth badges: `auth-public` (green), `auth-protected` (blue), `auth-admin` (pink)

**Tree view (project structure)**
```html
<pre class="tree"><span class="dir">project/</span>
├── <span class="file">file.py</span>  <span class="comment"># comment</span>
└── <span class="dir">subdir/</span>
    └── <span class="file">file.ts</span></pre>
```

**Config table (environment variables)**
```html
<table>
  <thead><tr><th>Variable</th><th>Default</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td><code>VAR_NAME</code></td><td><code>value</code></td><td>What it does</td></tr>
  </tbody>
</table>
```

**Section wrapper (all sections use this)**
```html
<div class="section" id="section-id">
  <h2><a class="anchor" href="#section-id">#</a> Section Title</h2>
  <!-- content -->
</div>
```

**Expandable details**
```html
<details class="expandable">
  <summary>Click to expand</summary>
  Content revealed on click.
</details>
```

### 5. Sidebar Nav Template

Match the sidebar links to the sections in the main content:

```html
<nav class="sidebar" id="sidebar">
  <div class="sidebar-logo">
    <!-- SVG icon + project name -->
    Project Name
  </div>
  <div class="sidebar-section">
    <div class="sidebar-section-title">Getting Started</div>
    <a class="sidebar-link" href="#overview">Overview</a>
    <a class="sidebar-link" href="#quick-start">Quick Start</a>
  </div>
  <div class="sidebar-section">
    <div class="sidebar-section-title">Reference</div>
    <a class="sidebar-link" href="#api-reference">API Reference</a>
    <a class="sidebar-link" href="#configuration">Configuration</a>
  </div>
</nav>
```

Sidebar badges (optional, append after link text):
```html
<span class="sidebar-badge badge-new">New</span>
<span class="sidebar-badge badge-admin">Admin</span>
<span class="sidebar-badge badge-optional">Optional</span>
```

### 6. Output

Write the completed file to `docs/index.html`. Confirm it:
- Is a single self-contained file (no external CSS/JS dependencies)
- Opens correctly in a browser without a server
- Has working sidebar anchor navigation
- Includes the JS at the bottom for sidebar active state + endpoint toggles + mobile menu + back-to-top

The JS block from `template.html` handles all interactivity — copy it verbatim.

## Quality Checklist

- [ ] All sections are based on actual project content (no invented content)
- [ ] Sidebar links match section IDs exactly
- [ ] At least one pipeline diagram if project has a data/request flow
- [ ] Configuration table if `.env.example` exists
- [ ] Collapsible endpoint blocks if routes exist (first one `open` by default)
- [ ] Tree view matches actual project directory layout
- [ ] `docs/` directory created if it doesn't exist
- [ ] File is valid HTML that renders in browser

## Common Mistakes

| Mistake | Fix |
|---|---|
| Invented API endpoints or config vars | Only document what exists in the code |
| Sidebar link href doesn't match section id | Double-check every `href="#x"` against `id="x"` |
| Missing JS block | Copy the `<script>` from `template.html` verbatim |
| External CSS/font imports | Remove — keep the file self-contained |
| Section with no real content | Skip it; only include what you have evidence for |
