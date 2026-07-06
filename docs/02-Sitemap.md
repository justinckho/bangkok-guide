# 02 - Sitemap

## Purpose

Define the complete site structure, page hierarchy, and navigation flow for the Bangkok Guide MVP website.

## Outline

1. Site Structure Overview
2. Page URLs
3. Data Files
4. Navigation Flow
5. Cross-linking Strategy

## Page URLs

| Page | Path | Description |
|------|------|-------------|
| Home | `/index.html` | Landing page with navigation to all categories |
| Food | `/pages/food.html` | Restaurants, street food, night markets |
| Shopping | `/pages/shopping.html` | Shopping malls, markets, boutiques |
| Hotels | `/pages/hotel.html` | Hotel reviews and ratings |
| Transport | `/pages/transport.html` | BTS, MRT, taxis, airport transfers |
| Attractions | `/pages/attractions.html` | Temples, museums, parks, viewpoints |
| Cafes | `/pages/cafe.html` | Cafes for work, photos, drinks |
| Massage & SPA | `/pages/massage.html` | Massage and SPA listings |

## Data Files

| File | Content |
|------|---------|
| `data/restaurants.json` | Restaurants, street food, night markets |
| `data/malls.json` | Shopping malls, markets, boutiques |
| `data/hotels.json` | Hotel reviews and ratings |
| `data/transport.json` | Transport overview |
| `data/bts.json` | BTS Skytrain stations and routes |
| `data/mrt.json` | MRT subway stations and routes |
| `data/attractions.json` | Temples, museums, parks, viewpoints |
| `data/cafes.json` | Cafes for work, photos, drinks |
| `data/massage.json` | Massage and SPA listings |

## Navigation Flow

```
Home (index.html)
  └── Category Pages (pages/*.html)
       └── Sidebar links to all other categories
       └── Home link in header/sidebar
```

Every category page includes a sidebar with links to all other categories for quick switching.

## TODO

- [ ] Complete site structure diagram
- [ ] Define navigation components (header, sidebar)
- [ ] Plan responsive navigation (mobile hamburger menu)
