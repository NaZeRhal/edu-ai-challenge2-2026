# CLAUDE.md — Leaderboard Replica Project

## What we are building
A pixel-accurate replica of a company leaderboard web app.
Deployed to GitHub Pages as a single static HTML file.

## Non-negotiable technical rules
- Single index.html — HTML + CSS + JS all inline, no exceptions
- Zero external dependencies — no CDN, no npm, no frameworks
- Must work by opening index.html directly in a browser

## Non-negotiable data rules
- NEVER use real names, scores, departments or any real data
- ALL leaderboard data comes from task-1/data.js only
- data.js contains 25 fictional entries — use all of them

## Source of truth files — read these before anything else
- `task-1/leaderboard-structure.html` — exact HTML structure
- `task-1/injected-leaderboard.css`   — exact component styles
- `task-1/custom-styles.css`          — exact page styles
- `task-1/data.js`                    — fictional data
- `task-1/new-spec.md`                — analysis doc (generated)

## Style rules
- Use class names exactly as found in leaderboard-structure.html
- Extract colours/spacing from injected-leaderboard.css as CSS variables
- Do not invent styles — if it is not in the CSS files, ask

## Current phase
→ Update this line after each phase completes

## Report tracking
After each phase append a short entry to task-1/report.md:
- Phase completed
- Tools and techniques used
- Decisions made
- Problems encountered and fixes applied

## Resolved Ambiguities (from new-spec.md §5)

### Filter dropdowns
- Dropdown0 (120px): "All Years" — filters by entry.year
- Dropdown1 (120px): "All Quarters" — filters by entry.quarter  
- Dropdown2 (150px): "All Categories" — filters by activity category

### Avatar sizing (not in source CSS — must be explicit)
- podiumAvatar rank1: 112×112px, font-size 32px
- podiumAvatar rank2/3: 80×80px, font-size 24px
- podiumRankBadge rank1: 40×40px, font-size 18px
- podiumRankBadge rank2/3: 32×32px, font-size 14px

### Icon → category badge mapping
- Presentation icon → categoryDefault_2943a085 (grey)
- Education icon → categoryTraining_2943a085 (blue)
- University icon → categoryCommunity_2943a085 (green)
- Mentoring icon → categoryContribution_2943a085 (purple)

### Details panel position
- .details_2943a085 is sibling of .row_2943a085
  inside .userRowContainer_2943a085
- Columns: ACTIVITY | CATEGORY | DATE | POINTS

### Other decisions
- Theme toggle: OMIT
- Chevron on expand: rotate 180deg via JS
- Fluent helper classes: replace with custom CSS equivalents
- custom-styles.css: drop entirely
- Icon strategy: inline SVGs throughout
- Podium shows when ≥3 filtered results, hides otherwise
- Loading state: skip (data is synchronous)