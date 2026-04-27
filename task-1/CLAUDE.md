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