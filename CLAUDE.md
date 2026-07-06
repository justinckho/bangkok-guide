# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# Bangkok Guide – Project Principles

## Project Philosophy

Bangkok Guide is **not** a blog or a travel diary.

It is a **personal travel knowledge base** designed for long-term maintenance and continuous expansion.

The primary goal is to organize reliable travel information into a structured, searchable, and easy-to-maintain database.

Every design and implementation decision should prioritize:

* Simplicity
* Maintainability
* Readability
* Reusability

Visual effects and technical complexity should never take priority over content quality.

---

# Development Principles

## Documentation First

Always understand and follow the project documentation before implementing new features.

If a new feature changes the project structure, data model, or navigation, update the corresponding documentation first.

Documentation is considered part of the source of truth.

---

## Simplicity First

Always choose the simplest solution that satisfies the requirements.

Avoid introducing unnecessary:

* Frameworks
* Build tools
* Dependencies
* Complex architectures

This project intentionally uses vanilla HTML, CSS, and JavaScript.

Only recommend more advanced technologies when there is a clear long-term benefit.

---

## Data First

Travel information belongs in JSON data files.

Avoid hardcoding travel content directly into HTML whenever possible.

HTML should focus on presentation.

JSON should serve as the project's database.

---

## Consistency First

Maintain consistent:

* Folder structure
* File naming
* Coding style
* Page layout
* Navigation
* UI patterns

Avoid creating multiple solutions for the same problem.

---

## Incremental Development

Develop the project in small, verifiable steps.

Each phase should produce a working website before moving to the next phase.

Avoid implementing future features prematurely.

Prefer completing one feature well before starting another.

---

# AI Collaboration Principles

Claude Code acts as the project's development assistant.

Responsibilities include:

* Maintaining project structure
* Implementing UI
* Refactoring code
* Improving documentation
* Keeping the codebase clean and consistent

The project owner is responsible for:

* Travel knowledge
* Content accuracy
* Product decisions
* User experience decisions

Claude should avoid making assumptions about travel information without confirmation.

---

# User Experience Principles

The website should always be:

* Clean
* Fast
* Easy to navigate
* Mobile-friendly
* Easy to read

Users should be able to locate useful information within a few clicks.

Avoid unnecessary animations or visual distractions.

Content is always more important than decoration.

---

# Long-Term Vision

The project will evolve gradually.

Current goal:

Static travel knowledge website

Future possibilities:

* Better navigation
* Search
* Tag filtering
* Maps
* Offline support (PWA)
* AI-assisted search
* Multi-city travel guides

All future improvements should build upon the existing architecture rather than replacing it.

---

# General Working Rules

When implementing new features:

1. Preserve the existing architecture whenever possible.
2. Prefer extending existing components over creating new ones.
3. Keep the project easy for both humans and AI to understand.
4. Write clean, readable, and maintainable code.
5. If multiple solutions exist, recommend the simplest maintainable approach.
6. Do not introduce unnecessary complexity.



## Project Overview

A static vanilla HTML/CSS/JS guide to Bangkok — covering food, shopping, hotels, transport, attractions, cafes, and massage. Data-driven: JSON → JS fetch → UI rendering. No build step, no frameworks. Deployable to GitHub Pages.

The system uses one static HTML page per category under `/pages/`, all sharing a single JS rendering pipeline (`app.js`). Adding a new category means editing `categories.json` + creating a data file + adding a page shell.

## Architecture

### Data Flow

```
DATA (JSON)  →  RENDERER (JS)  →  UI (HTML/CSS)
```

Three strictly separated layers:

| Layer | Responsibility | Files |
|---|---|---|
| **Data Layer** | All content (places, categories) | `/data/*.json` |
| **Logic Layer** | Read JSON, build DOM | `/js/*.js` |
| **Presentation Layer** | Page shells + styling only | `/*.html`, `/css/*.css` |

No layer reaches backward. HTML never contains place data. JS never contains styling. JSON never contains HTML strings.

### Pages

| Page | URL | Description |
|---|---|---|
| Home | `index.html` | Category tiles, generated from `categories.json` |
| Food | `pages/food.html` | Restaurants, street food, night markets |
| Shopping | `pages/shopping.html` | Shopping malls, markets, boutiques |
| Hotels | `pages/hotels.html` | Hotel reviews and ratings |
| Transport | `pages/transport.html` | BTS, MRT, taxis, airport transfers |
| Attractions | `pages/attractions.html` | Temples, museums, parks, viewpoints |
| Cafes | `pages/cafes.html` | Cafes for work, photos, drinks |
| Massage | `pages/massage.html` | Massage and SPA listings |

Each page is an independent HTML shell. The filename tells `app.js` which category to load — no URL params needed.

### Directory Layout

```
/
├── index.html              # Home — category tile grid
├── pages/
│   ├── food.html           # Static page per category (7 total)
│   ├── hotels.html
│   └── ...
├── css/
│   ├── layout.css          # App shell, top bar, sidebar + main layout
│   ├── sidebar.css         # Navigation list styles
│   └── card.css            # Card component + grid
├── js/
│   ├── loader.js           # Fetch JSON
│   ├── renderer.js         # Build card DOM from data items
│   ├── sidebar.js          # Render nav, hamburger menu
│   ├── filter.js           # Text search + tag filtering
│   └── app.js              # Entry point — detects page, routes logic
├── data/
│   ├── categories.json     # Category registry (id, label, icon, description)
│   ├── food.json
│   ├── shopping.json
│   ├── hotels.json
│   ├── transport.json
│   ├── attractions.json
│   ├── cafes.json
│   └── massage.json
└── assets/
    ├── icons/
    └── images/
```

### Card Rendering Rules

Each card renders one JSON item. Optional fields (`rating`, `tags`, `notes`, `links`) are conditionally rendered — if absent in JSON, that DOM element is not created.

- `links.googleMaps` present → "View on Map" button (`target="_blank"`)
- `links.phone` present → "Call" button (`tel:`)
- Neither present → action row omitted entirely

### Item JSON Format

```json
{
  "id": "unique-id",
  "name": "Place Name",
  "category": "food",
  "location": "Bangkok area",
  "tags": ["tag1", "tag2"],
  "rating": 4.5,
  "notes": "Short personal note",
  "links": {
    "googleMaps": "https://...",
    "phone": "+662..."
  }
}
```

### CSS Architecture — "Peaceful UI" Design

Per `docs/03-UI-Design.md`:
- **Palette:** warm gray bg `#f5f3f0`, dark gray text `#2c2c2c`, white cards `#ffffff`, subtle border `#e8e6e3`, muted accent `#b8a07a`
- **Typography:** system font stack, 3 sizes: title 20px / body 15px / small 13px
- **Spacing:** 8px baseline grid
- **Cards:** white bg, no shadow, 4px radius, bottom border only
- **Sidebar:** 240px (desktop), 200px (tablet), hidden with hamburger (mobile)
- **Grid:** 3 cols (≥1024px) → 2 cols (768-1023px) → 1 col (<768px)
- **No animations** beyond `transition: background 0.15s`

### Filters (client-side, on category pages)

- Text search: matches against card name as user types
- Tag chips: derived from union of tags in current category's JSON; clicking toggles on/off
- Filtering only adds/removes `.card--hidden` CSS class — no re-fetch, no re-render

## Development

### Preview Locally

```bash
python -m http.server 8000 -d src/
# or VS Code Live Server on src/index.html
```

Serve over HTTP — `file://` won't work for `fetch()` loading JSON.

### Adding a New Category

1. Add entry to `src/data/categories.json` (id, label, icon, description)
2. Create `src/data/{id}.json` with `[]` (or data)
3. No HTML or JS changes needed — sidebar and tiles auto-populate

### Adding Data Entries

Add objects to `src/data/{category}.json`. Follow the JSON format above.

### Current Data

23 entries across 7 categories (exceeds MVP minimum of 20). All Bangkok, all real places.

## Development Phases (docs/05-Roadmap.md)

- **Phase 1 ✅:** Project init — structure, templates, empty data
- **Phase 2 ✅:** Core structure — one HTML page per category in /pages/, sidebar, responsive shell, filter/search
- **Phase 3 ✅:** Content population — 23 real Bangkok entries
- **Phase 4:** Feature development — maps, sorting, more filters
- **Phase 5:** Polish & deploy — GitHub Pages, final styling

## Key Constraints

- No frameworks (vanilla HTML/CSS/JS)
- No build step
- GitHub Pages hosting
- Bangkok-only MVP
- Chinese target language (zh-CN)
