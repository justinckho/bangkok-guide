# Claude Code Project Generator Prompt（最终版）(ChatGPT版本)

You are generating a complete **static website implementation** for a project called:

# Bangkok Guide

---

# 1. Project Type

This is a:

* Static website
* Data-driven (JSON → UI rendering)
* No backend
* No frameworks (NO React / Vue / Angular)

---

# 2. IMPORTANT CONSTRAINTS

You MUST strictly follow:

* Only use HTML + CSS + Vanilla JavaScript
* No build tools
* No external UI frameworks
* No backend logic
* No database
* No SPA framework

You MUST strictly follow the project design documents below:

1) Project Definition
docs/01-ProjectBrief.md
Defines the purpose and scope of the system.
2) Site Structure
docs/02-Sitemap.md
Defines pages, navigation structure, and hierarchy.
3) UI Design Rules
docs/03-UI-Design.md
Defines layout, visual system, and UI components.
4) System Behavior Spec
docs/04-System-Spec.md
Defines interaction rules, data flow, and system logic.

---

# 3. OUTPUT DIRECTORY RULES

All generated code MUST be placed in:

```
src/
```

Do NOT create files outside `src/`.

Do NOT modify `docs/`.

Do NOT create unrelated folders.

---

# 4. PROJECT STRUCTURE TO GENERATE

Create the following structure:

```
src/
  index.html
  pages/
    food.html
    hotels.html
    transport.html
    attractions.html
    massage.html
    shopping.html
    cafes.html

  css/
    style.css

  js/
    app.js

  data/
    food.json
    hotels.json
    transport.json
    attractions.json
    massage.json
    shopping.json
    cafes.json

  assets/
    icons/
    images/
```

---

# 5. CORE FUNCTIONAL REQUIREMENTS

## 5.1 Data Loading

Each page must:

* load its corresponding JSON file
* render items dynamically using JavaScript
* NOT hardcode content inside HTML

---

## 5.2 Card Rendering System

Each item should render as a card with:

* name
* location
* rating (if available)
* tags
* notes

If links exist:

* show "View on Google Maps" button
* show "Call" button (tel:)

---

## 5.3 Navigation System

* Sidebar navigation (desktop)
* Hamburger menu (mobile)
* Navigation switches between HTML pages (NOT SPA)

---

## 5.4 Layout System

Each page must include:

* Top bar (minimal title)
* Sidebar (category navigation)
* Main content area (cards grid)

---

## 5.5 Responsive Design

* Desktop: 3-column grid
* Tablet: 2-column grid
* Mobile: 1-column layout

---

# 6. DATA FORMAT (MUST FOLLOW)

All JSON files must follow this structure:

```json
{
  "id": "unique-id",
  "name": "Place Name",
  "category": "food",
  "location": "Bangkok",
  "tags": ["tag1", "tag2"],
  "rating": 4.5,
  "notes": "short description",
  "links": {
    "googleMaps": "",
    "phone": ""
  }
}
```

---

# 7. UI RULES

* Clean, minimal design
* No heavy animations
* No UI frameworks
* No decorative elements
* Focus on readability

---

# 8. DATA FLOW RULE

All pages MUST follow:

```
JSON file → JavaScript fetch → Render cards → Display UI
```

No hardcoded content inside HTML pages (except layout shell).

---

# 9. DESIGN GOAL

This is a:

> Personal travel knowledge system, not a commercial website.

It must prioritize:

* simplicity
* maintainability
* clarity
* extensibility

---

# 10. FINAL OUTPUT

Generate a fully working static website that can be:

* opened locally via http server
* deployed to GitHub Pages without modification
* extended by simply editing JSON files
