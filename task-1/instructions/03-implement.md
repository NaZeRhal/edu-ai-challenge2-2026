# Phase 3 — Implementation

## Your role

Senior frontend developer. Build the leaderboard as a single
self-contained HTML file ready for GitHub Pages.

## Inputs

- UI Specification: [paste or reference 01-analyse.md output]
- Data: [paste or reference 02-data.md output]

## Technical requirements

- Single index.html file — HTML + CSS + JS all inline
- No frameworks, no build step, no CDN dependencies
- Must work by opening index.html directly in a browser
- Must deploy to GitHub Pages as-is

## Build in this exact order

### Step 1 — HTML skeleton

- Build semantic HTML structure for all components
- Use descriptive class names (not the original hashed ones)
- Add data-\* attributes as JS hooks where needed
- No styling yet — structure only

### Step 2 — CSS

- Implement all design tokens as CSS variables at :root
- Style every component using the spec values
- Implement top-3 podium with correct gold/silver/bronze treatment
- Implement rank badge colours per position
- Add hover states on list rows and buttons
- Match spacing, typography, colours exactly to spec

### Step 3 — Render data

- Write a renderLeaderboard() function
- Populate all entries from LEADERBOARD_DATA array
- Rank numbers derived from array order
- Avatar shows initials with background colour from data
- Score displays with star icon

### Step 4 — Filters

Wire up all three dropdowns:

- Year filter (options: All Years + list of years from data)
- Quarter filter (options: All Quarters, Q1, Q2, Q3, Q4)
- Category filter (options: All Categories + unique categories from data)
  All filters must work simultaneously with search.

### Step 5 — Search

- Real-time filtering as user types
- Searches on name field only
- Case insensitive
- Works combined with active dropdown filters

### Step 6 — Sorting

- Default: score descending
- Clicking score header or sort control toggles asc/desc
- Rank numbers update to reflect current sort order

## Output

Single complete index.html file.
After the code, list any spec details you interpreted
or decisions you made where spec was ambiguous.
