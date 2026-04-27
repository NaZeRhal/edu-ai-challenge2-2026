# Phase 1 — UI Analysis & Specification

## Your role

You are a senior UI analyst. Analyse the provided DOM snapshot and
produce a complete developer-ready specification document.

## Input

File: leaderboard-dom.html

- All text replaced with [DATA] placeholders
- Images replaced with blank pixels
- Styles inlined from computed values
- CSS module hash \_2943a085 = leaderboard web part classes
- CSS module hash \_7ea1264b = breadcrumb classes
- CSS module hash \_cae45c08 = feedback button classes

## What to analyse and document

### 1. Layout Structure

- Overall page layout and regions
- Container widths, centering, background colours
- Spacing between major sections

### 2. Component Inventory

For each component found, document:

- Name and purpose
- HTML tag and class names
- Visual description
- Children and their roles

### 3. Design Tokens

Extract precise values from inlined styles:

- All colours (background, text, accent, border)
- Typography (font family, sizes, weights per element type)
- Spacing scale (padding, margin, gap values)
- Border radius per component
- Box shadows and elevation
- Any transition values

### 4. Data Model

From the DOM structure identify every data field:

- List fields as: fieldName: type (e.g. rank: integer)
- Note any fields with special visual treatment
- Describe how entries differ visually (rank 1 vs rank 2 vs rank 3+)

### 5. Filter & Sort Controls

Document every interactive control:

- Each dropdown: label, what it filters, how many options visible
- Search input: placeholder text style, icon position
- Layout of controls relative to each other

### 6. Top 3 Podium

Describe in detail:

- Layout of 3 positions (order: 2nd left, 1st centre, 3rd right)
- Avatar size and border treatment per rank
- Rank badge position, size, colour per rank (gold/silver/bronze)
- Score display style
- Podium/pedestal shape and colour per rank
- Any height differences between positions

### 7. List Entries

Describe one entry row in full detail:

- Height and padding
- Left side: rank number style
- Centre: name area (redacted as [DATA]) — width, style
- Right side: icons with counts, score display
- Expand button — position, style
- Border, shadow, hover state if visible

### 8. Expanded Entry (Category Stats)

Describe the expanded state:

- What additional information appears
- Icon types and their meaning
- Layout of stat items

### 9. Feedback Button

- Position on page (fixed/floating?)
- Visual style
- Any icon or label

## Output format

Return a single markdown document titled:

# Leaderboard UI Specification

Use one section per component above.
Use exact values from computed styles — not approximations.
Include short CSS snippets where they illustrate a point.
Flag anything ambiguous or unclear.

This document will be used directly to build the replica.
