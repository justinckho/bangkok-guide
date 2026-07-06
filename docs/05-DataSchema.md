# 05 - Data Schema (V1 - Minimal Stable)

## 1. Purpose

This document defines the **minimal stable data structure** for the Bangkok Guide project.

The goal is to:

* ensure consistency across all categories
* keep the system simple and maintainable
* support future expansion without redesign
* avoid over-engineering at early stage

This is a **practical MVP schema**, not a final database design.

---

## 2. Design Philosophy

This schema follows 4 principles:

* **Minimal fields only** → avoid unnecessary attributes
* **Flat structure** → no nested complexity
* **Human-editable JSON** → easy to maintain manually
* **UI-agnostic** → data should not depend on layout

---

## 3. Base Entity Schema (Core Model)

All items MUST follow this structure:

```json id="base_min"
{
  "id": "somtam-nua",
  "name": "Som Tam Nua",
  "category": "food",
  "location": "Siam Square",
  "tags": ["spicy", "local"],
  "rating": 4.5,
  "notes": "Great papaya salad",
  "links": {
    "googleMaps": "",
    "phone": ""
  }
}
```

---

## 4. Category Structure

All data is grouped by category files:

```text id="folder_structure"
/data/
  food.json
  hotels.json
  transport.json
  attractions.json
  massage.json
  shopping.json
  cafes.json
```

Each file contains an array of Base Entities.

---

## 5. Category Meaning (Important for consistency)

### Core Living Layer

* food → eating & street food
* hotels → accommodation
* transport → mobility

### Experience Layer

* attractions → sightseeing
* massage → traditional massage
* spa → wellness experience
* shopping → malls & markets

### Optional Layer

* cafe → casual lifestyle spots

---

## 6. Optional Field Rule (VERY IMPORTANT)

To avoid schema explosion:

> Only add new fields when at least 3 real entries require it.

No premature expansion.

---

## 7. Current Optional Extensions (ONLY if needed)

These are NOT mandatory fields.

### Food

```json id="food_optional"
{
  "price_level": "$ | $$ | $$$",
  "signature_dish": "string"
}
```

### Hotel

```json id="hotel_optional"
{
  "price_per_night": "string",
  "area": "string"
}
```

### Massage / Spa

```json id="massage_optional"
{
  "duration": "60 | 90 | 120 min",
  "wellness_type": "massage | spa | sauna"
}
```

👉 Note: sauna is included here, not a separate category

---

## 8. Data Usage Rules (Critical)

UI layer MUST ONLY rely on:

* name
* location
* tags
* rating
* notes

Everything else is optional enrichment.

---

## 9. Simplicity Constraints

The system MUST NOT include:

* nested objects
* relational database design
* backend-style normalization
* complex schemas per category
* over-specific attributes

Keep it flat and predictable.

---

## 10. Multi-City Future Rule

Future cities MUST reuse the same schema:

```text id="future_cities"
/data/
  bangkok/
  tokyo/
  hongkong/
```

No schema changes required for new cities.

---

## 11. Summary

This schema is designed as a **stable starting point**, not a final architecture.

It prioritizes:

* usability over completeness
* simplicity over optimization
* long-term maintainability over early perfection

It will evolve naturally through real usage, not upfront design.


