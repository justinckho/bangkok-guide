# Claude Web System Spec Prompt（Bangkok Guide）(ChatGPT版本)

You are designing a **system specification (not code)** for a personal travel knowledge base website.

## Project Name

Bangkok Guide

## Project Type

A **data-driven static website** (no backend, no frameworks) that serves as a personal travel knowledge base for Bangkok.

It is NOT a commercial travel website.

It is NOT a booking platform.

It is a structured information system.

---

# 1. Goal of the System

Design a simple, maintainable system that allows:

* browsing curated travel information about Bangkok
* navigating via categories
* viewing structured cards (places)
* optionally filtering and searching within a category
* clicking external links (Google Maps, phone, etc.)

The system must prioritize:

* simplicity
* maintainability
* clarity
* data-driven rendering

---

# 2. Core Concept

This website is built on:

> Data (JSON) → Rendered into UI (HTML cards)

There is NO backend.

There is NO database.

Everything is static files.

---

# 3. Page Structure

The site consists of:

## 3.1 Home Page

* Simple entry page
* List of categories
* Acts as navigation hub

## 3.2 Category Pages

Each category has its own page:

* Food
* Hotels
* Transport
* Attractions
* Massage / Spa
* Shopping
* Cafes (optional)

Each page:

* loads a JSON file
* renders a list of cards

---

# 4. Navigation System

## Sidebar Navigation (Primary)

* Always visible on desktop
* Contains all categories
* Clicking switches page

## Mobile Navigation

* Collapsible sidebar (hamburger menu)
* Same structure as desktop

---

# 5. Card System (Core UI Unit)

Each item is displayed as a card.

A card contains:

* Name (primary title)
* Location (secondary text)
* Rating (optional)
* Tags (optional)
* Notes (short personal comment)

## Optional Action Area

If available:

* "View on Map" (Google Maps link)
* "Call" (phone link)

These come from a `links` object.

---

# 6. Data System (IMPORTANT)

All content is stored in JSON files.

Each item follows this structure:

* id
* name
* category
* location
* tags
* rating
* notes
* links (optional)

Example:

{
"id": "example",
"name": "Place Name",
"category": "food",
"location": "Bangkok",
"tags": ["local", "cheap"],
"rating": 4.5,
"notes": "Short personal note",
"links": {
"googleMaps": "",
"phone": ""
}
}

---

# 7. Interaction Design

## 7.1 Navigation

* Clicking sidebar changes page (no SPA required)
* Simple page-based navigation

## 7.2 Filtering (optional V1.1)

* Filter within category using tags or search text

## 7.3 Search (lightweight)

* Client-side filtering only
* No backend search

## 7.4 External Actions

* Google Maps opens in new tab
* Phone uses tel: link

---

# 8. Layout System

Each page has:

* Top bar (minimal title)
* Sidebar (navigation)
* Main content area (cards list)

Main content layout:

* Desktop: 3-column card grid
* Tablet: 2-column
* Mobile: 1-column

---

# 9. Design Constraints

The system MUST follow:

* No frameworks (React, Vue, etc.)
* No backend
* No complex routing
* No heavy animations
* No external UI libraries

Only:

* HTML
* CSS
* Vanilla JavaScript

---

# 10. Data-Driven Rendering Rule

All UI must be generated from JSON.

No hardcoded content inside HTML pages (except structure shell).

---

# 11. Extensibility

The system must support:

* adding new cities in future (e.g., Tokyo, Hong Kong)
* adding new categories
* expanding JSON data without changing UI logic

---

# 12. Non-Goals

This system explicitly does NOT include:

* booking functionality
* user accounts
* backend database
* real-time data
* complex map integration

---

# 13. Final Output Required

Design and output:

* system architecture explanation
* page structure
* component design
* interaction rules
* data flow explanation

DO NOT write code.

Focus only on system design clarity.
