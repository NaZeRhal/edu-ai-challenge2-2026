# Phase 2 — Fictional Data Generation

## Your role

Generate completely fictional leaderboard data.
This data must look realistic but contain zero real information.

## Rules

- No real names, no real departments, no real scores from the original
- Names must be human-sounding (not "User 1" or "Employee A")
- Departments must be plausible but fictional
- Scores must follow a natural distribution (not all round numbers)

## Data schema

Based on the UI spec, generate a JavaScript array called LEADERBOARD_DATA.

Each entry must have:

- id: unique integer
- rank: integer (derived from score order)
- name: fictional full name (first + last)
- avatarInitials: first letter of first + last name (for avatar placeholder)
- avatarColor: a hex colour for the avatar background (varied per person)
- score: integer — use a natural distribution:
  - Rank 1: 450–600
  - Rank 2–3: 280–380
  - Rank 4–10: 150–280
  - Rank 11–25: 50–150
- categories: object with counts per activity type, e.g.:
  { lab: 3, reg: 5, uni: 2, edu: 7 }
  (values must sum logically with the total score)
- department: fictional team name

## Requirements

- Generate exactly 25 entries
- Sort by score descending (rank 1 = highest score)
- At least 4 different departments represented
- Score distribution must feel organic — avoid patterns

## Output

Return only the JavaScript data array, no explanation:
const LEADERBOARD_DATA = [ ... ];
