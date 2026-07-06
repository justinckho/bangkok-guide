# Prompt: Add Location

## Purpose

Template prompt for adding a new location entry to the data JSON files.

## Usage

Use this prompt when adding a new restaurant, shop, hotel, or other location to the dataset.

## Template

```
Add a new location entry to src/data/[CATEGORY].json.

Location details:
- Name: [NAME]
- Name (Thai): [NAME_TH]
- Address: [ADDRESS]
- Area: [NEIGHBORHOOD]
- Category: [CATEGORY]
- Coordinates: [LAT, LNG]
- Rating: [RATING]
- Price Level: [$ / $$ / $$$]
- Description: [DESCRIPTION]
- Website: [URL]
- Tags: [TAG1, TAG2, ...]
- Personal Notes: [NOTES]

Follow the existing schema in the data file.
```

## TODO

- [ ] Add sample data entry format
- [ ] Document all supported fields per category
