# Leaderboard Replica — new-spec.md

Source-of-truth analysis derived verbatim from:

- `task-1/input/leaderboard-structure.html`
- `task-1/input/injected-leaderboard.css` (only the `_2943a085`-scoped block; offsets 162366–172773 in the minified original)
- `task-1/input/custom-styles.css` (site-chrome only; contains no `_2943a085` rules and is therefore not consumed by this component)

All declarations below are reproduced exactly as written in the minified CSS, only re-indented for readability. Nothing has been added, renamed, or normalised.

---

## 1. COMPONENT STYLES

Each block below lists the original selector, declarations exactly as written, the element it targets in `leaderboard-structure.html`, and its purpose. Rank-specific variants are explicitly flagged.

### 1.1 Container

```css
.leaderboard_2943a085 {
  background: #f8fafc;
  color: #0f172a;
  font-family: Segoe UI, -apple-system, BlinkMacSystemFont, Roboto, Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
  min-height: 100vh;
  padding: 24px;
  transition: background-color .3s, color .3s;
}
```

- Element: `<section>`. Root wrapper for the whole leaderboard component.

```css
.leaderboard_2943a085.loading_2943a085 {
  opacity: .6;
  pointer-events: none;
}
```

- State modifier added to the root `<section>` while data is loading. Trigger condition is undefined in source (see §5).

### 1.2 Header

```css
.header_2943a085 {
  align-items: flex-start;
  display: flex;
  justify-content: space-between;
  margin: 0 auto 32px;
  max-width: 1200px;
}
```

- Element: `<header>`. Top bar containing the title block and (per CSS) a theme toggle.

```css
.header_2943a085 .headerContent_2943a085 {
  flex: 1;
}
```

- Element: `<div>`. Wrapper for the `<h2>` title and `<p>` subtitle.

```css
.header_2943a085 .headerContent_2943a085 h2 {
  color: #0f172a;
  font-size: 30px;
  font-weight: 700;
  margin: 0 0 8px;
}
```

- Element: `<h2>`. Page-level leaderboard title.

```css
.header_2943a085 .headerContent_2943a085 p {
  color: #64748b;
  font-size: 14px;
  margin: 0;
}
```

- Element: `<p>`. Subtitle / description below the title.

```css
.header_2943a085 .themeToggle_2943a085 {
  background: #fff;
  border: 1px solid #e2e8f0;
  border-radius: 50%;
  box-shadow: 0 1px 2px rgba(0, 0, 0, .05);
  color: #64748b;
  cursor: pointer;
  padding: 8px;
  transition: all .2s;
}

.header_2943a085 .themeToggle_2943a085:hover {
  border-color: #0ea5e9;
  color: #0ea5e9;
}

.header_2943a085 .themeToggle_2943a085 i {
  font-size: 20px;
}
```

- Element: `<button>` (inferred — `cursor: pointer`). Light/dark theme toggle. Not present in `leaderboard-structure.html` (see §5).

### 1.3 Filter bar

```css
.filterBar_2943a085 {
  align-items: center;
  background: #fff;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, .1);
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  justify-content: space-between;
  margin: 0 auto 24px;
  max-width: 1200px;
  padding: 20px 24px;
  transition: all .2s;
}

.filterBar_2943a085:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, .05);
}
```

- Element: `<div>`. Bar holding the dropdowns and the search input.

```css
.filterBar_2943a085 .filters_2943a085 {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}
```

- Element: `<div>`. Container for the three `ms-Dropdown` widgets.

```css
.filterBar_2943a085 .search_2943a085 {
  flex: 1;
  min-width: 250px;
}
```

- Element: `<div>`. Wrapper around the `ms-SearchBox` input.

### 1.4 Podium — shell

```css
.podium_2943a085 {
  align-items: flex-end;
  display: flex;
  gap: 24px;
  justify-content: center;
  margin: 0 auto 64px;
  max-width: 900px;
  padding: 32px 8px;
}
```

- Element: `<div>`. Three-column podium, columns aligned to the bottom so block heights produce the staircase effect.

```css
.podiumColumn_2943a085 {
  align-items: center;
  display: flex;
  flex-direction: column;
  max-width: 280px;
  position: relative;
  width: 100%;
}
```

- Element: `<div>`. One podium column = user card on top + colored block below.

### 1.5 Podium — rank variants (FLAGGED)

These three classes are mutually exclusive modifiers added to `.podiumColumn_2943a085`. They control visual order, height, color theming, and font sizes throughout the podium.

#### Rank 1 (winner) — `.podiumRank1_2943a085`

```css
.podiumColumn_2943a085.podiumRank1_2943a085 {
  margin-top: -32px;
  order: 2;
}

.podiumRank1_2943a085 .podiumAvatar_2943a085 {
  background-color: #86efac;
  border: 4px solid #fbbf24;
  color: #166534;
}

.podiumRank1_2943a085 .podiumAvatar_2943a085 span {
  font-size: 32px;
}

.podiumRank1_2943a085 .podiumRankBadge_2943a085 {
  background: #eab308;
  font-size: 18px;
}

.podiumRank1_2943a085 .podiumName_2943a085 {
  font-size: 24px;
}

.podiumRank1_2943a085 .podiumScore_2943a085 {
  background: #fef9c3;
  border-color: #fde047;
  color: #ca8a04;
  font-size: 20px;
  padding: 8px 20px;
}

.podiumRank1_2943a085 .podiumScore_2943a085 i {
  font-size: 18px;
}

.podiumRank1_2943a085 .podiumBlock_2943a085 {
  background: linear-gradient(180deg, #fef3c7, #fde68a);
  border-top-color: #fde047;
  height: 160px;
}

.podiumRank1_2943a085 .podiumBlockTop_2943a085 {
  background: #fde047;
}

.podiumRank1_2943a085 .podiumRankNumber_2943a085 {
  color: rgba(234, 179, 8, .2);
  font-size: 112px;
}
```

- Visual: gold theme, raised 32px above neighbors, larger avatar/name/score text, tallest block (160px).

#### Rank 2 (silver) — `.podiumRank2_2943a085`

```css
.podiumColumn_2943a085.podiumRank2_2943a085 {
  order: 1;
}

.podiumRank2_2943a085 .podiumAvatar_2943a085 {
  background-color: #cbd5e1;
  border: 4px solid #fff;
  color: #1e293b;
}

.podiumRank2_2943a085 .podiumRankBadge_2943a085 {
  background: #94a3b8;
  font-size: 14px;
}

.podiumRank2_2943a085 .podiumScore_2943a085 {
  color: #0ea5e9;
}

.podiumRank2_2943a085 .podiumBlock_2943a085 {
  height: 128px;
}

.podiumRank2_2943a085 .podiumBlockTop_2943a085 {
  background: #cbd5e1;
}
```

- Visual: silver/slate theme, leftmost on desktop (`order: 1`), block height 128px. Inherits the default `.podiumRankNumber_2943a085` styling (no rank-2 override).

#### Rank 3 (bronze) — `.podiumRank3_2943a085`

```css
.podiumColumn_2943a085.podiumRank3_2943a085 {
  order: 3;
}

.podiumRank3_2943a085 .podiumAvatar_2943a085 {
  background-color: #5eead4;
  border: 4px solid #fff;
  color: #134e4a;
}

.podiumRank3_2943a085 .podiumRankBadge_2943a085 {
  background: #92400e;
  font-size: 14px;
}

.podiumRank3_2943a085 .podiumScore_2943a085 {
  color: #0ea5e9;
}

.podiumRank3_2943a085 .podiumBlock_2943a085 {
  height: 96px;
}

.podiumRank3_2943a085 .podiumBlockTop_2943a085 {
  background: #cbd5e1;
}

.podiumRank3_2943a085 .podiumRankNumber_2943a085 {
  top: -16px;
}
```

- Visual: teal avatar with a brown badge, rightmost on desktop (`order: 3`), shortest block (96px). The big rank number is shifted up by 16px.

> Note: `.podiumRank2_2943a085 .podiumScore_2943a085, .podiumRank3_2943a085 .podiumScore_2943a085` and the analogous `.podiumBlockTop_2943a085` rule are written as combined selectors in the source CSS. They are split per-rank above for clarity but their declarations are reproduced verbatim.

### 1.6 Podium — internals (rank-agnostic)

```css
.podiumUser_2943a085 {
  align-items: center;
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;
  position: relative;
  z-index: 10;
}
```

- Element: `<div>`. The card content stacked above the colored block (avatar + badge + name + role + score).

```css
.podiumAvatarContainer_2943a085 {
  margin-bottom: 12px;
  position: relative;
}
```

- Element: `<div>`. Positioning context for the avatar + rank badge (badge uses absolute positioning).

```css
.podiumAvatar_2943a085 {
  align-items: center;
  background-position: 50%;
  background-size: cover;
  border-radius: 50%;
  box-shadow: 0 4px 12px rgba(0, 0, 0, .15);
  color: #fff;
  display: flex;
  font-weight: 700;
  justify-content: center;
}

.podiumAvatar_2943a085 span {
  font-size: 24px;
}
```

- Element: `<div>` (image-as-background). Circular avatar; rank-1 enlarges its `<span>` to 32px.

> Important: the source CSS does NOT define a `width`/`height` on `.podiumAvatar_2943a085`. The element therefore collapses unless those dimensions are supplied (see §5).

```css
.podiumRankBadge_2943a085 {
  align-items: center;
  border: 4px solid #fff;
  border-radius: 50%;
  bottom: -8px;
  color: #fff;
  display: flex;
  font-weight: 700;
  justify-content: center;
  position: absolute;
  right: -4px;
}
```

- Element: `<div>`. Small numbered badge overlapping the bottom-right of the avatar.

> Important: no `width`/`height` is defined here either (see §5).

```css
.podiumName_2943a085 {
  color: #0f172a;
  font-size: 20px;
  font-weight: 700;
  margin: 0 0 4px;
  text-align: center;
}
```

- Element: `<h3>`. Display name on the podium.

```css
.podiumRole_2943a085 {
  color: #64748b;
  font-size: 14px;
  font-weight: 500;
  margin: 0 0 8px;
}
```

- Element: `<p>`. Role / title shown under the name.

```css
.podiumScore_2943a085 {
  align-items: center;
  background: #fff;
  border: 1px solid #e2e8f0;
  border-radius: 20px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, .05);
  display: flex;
  font-size: 18px;
  font-weight: 700;
  gap: 6px;
  padding: 6px 16px;
}

.podiumScore_2943a085 i {
  font-size: 16px;
}
```

- Element: `<div>` containing `<i data-icon-name="FavoriteStarFill">` + `<span>`. Pill-shaped score.

```css
.podiumBlock_2943a085 {
  align-items: flex-start;
  background: linear-gradient(180deg, #e2e8f0, #cbd5e1);
  border-radius: 12px 12px 0 0;
  border-top: 2px solid #cbd5e1;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, .06);
  display: flex;
  justify-content: center;
  overflow: hidden;
  padding-top: 16px;
  position: relative;
  width: 100%;
}
```

- Element: `<div>`. The colored "step" under the user card. Heights and gradient are overridden per rank.

```css
.podiumBlockTop_2943a085 {
  height: 2px;
  inset: 0 0 auto 0;
  position: absolute;
}
```

- Element: `<div>`. 2px-tall top stripe of the block; color overridden per rank.

```css
.podiumRankNumber_2943a085 {
  color: rgba(148, 163, 184, .2);
  font-size: 96px;
  font-weight: 900;
  position: relative;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
```

- Element: `<span>`. The huge faded rank digit shown inside the podium block.

### 1.7 List — row container

```css
.list_2943a085 {
  display: flex;
  flex-direction: column;
  gap: 16px;
  margin: 0 auto;
  max-width: 1200px;
}
```

- Element: `<div>`. Vertical stack of all user rows.

```css
.userRowContainer_2943a085 {
  background: #fff;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, .1);
  overflow: hidden;
  transition: all .2s;
}

.userRowContainer_2943a085:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, .1);
}

.userRowContainer_2943a085.expanded_2943a085 {
  border-color: #0ea5e9;
  box-shadow: 0 4px 12px rgba(0, 0, 0, .1);
}
```

- Element: `<div>`. One row per user. Adds `.expanded_2943a085` when the details panel is open.

```css
.row_2943a085 {
  padding: 20px 24px;
}
```

- Element: `<div>`. Inner padded wrapper inside `.userRowContainer_2943a085`.

```css
.rowMain_2943a085 {
  align-items: center;
  display: flex;
  gap: 16px;
  justify-content: space-between;
}
```

- Element: `<div>`. Flex row: `rowLeft` on the left, `rowRight` on the right.

```css
.rowLeft_2943a085 {
  align-items: center;
  display: flex;
  flex: 1;
  gap: 24px;
}
```

- Element: `<div>`. Holds rank, avatar and info.

```css
.rank_2943a085 {
  color: #94a3b8;
  font-size: 24px;
  font-weight: 700;
  min-width: 32px;
  text-align: center;
}
```

- Element: `<span>`. Numeric rank for rows 4 and below.

```css
.avatar_2943a085 {
  align-items: center;
  background-color: #fbbf24;
  background-position: 50%;
  background-size: cover;
  border-radius: 50%;
  color: #fff;
  display: flex;
  flex-shrink: 0;
  font-size: 20px;
  font-weight: 700;
  height: 56px;
  justify-content: center;
  width: 56px;
}
```

- Element: `<div>`. 56×56 circular avatar (background image OR colored circle with initials).

```css
.info_2943a085 {
  display: flex;
  flex: 1;
  flex-direction: column;
  gap: 4px;
}
```

- Element: `<div>`. Stacks the user name and role.

```css
.name_2943a085 {
  color: #0f172a;
  font-size: 18px;
  font-weight: 700;
  margin: 0;
}
```

- Element: `<h3>`. Display name in the row.

```css
.role_2943a085 {
  color: #64748b;
  font-size: 14px;
}
```

- Element: `<span>`. Role / title in the row.

```css
.rowRight_2943a085 {
  align-items: center;
  display: flex;
  gap: 24px;
}
```

- Element: `<div>`. Holds category stats, total section, and expand button.

### 1.8 Row — stats and totals

```css
.categoryStats_2943a085 {
  align-items: center;
  display: flex;
  gap: 24px;
}
```

- Element: `<div>`. Inline list of per-category stats (each wrapped in an `ms-TooltipHost`).

```css
.categoryStat_2943a085 {
  align-items: center;
  display: flex;
  flex-direction: column;
  gap: 4px;
}
```

- Element: `<div>`. One category icon + count, stacked vertically.

```css
.categoryStatIcon_2943a085 {
  color: #0ea5e9;
  font-size: 20px;
}
```

- Element: `<i>`. Icon glyph for a category (`Presentation`, `Education`, ...).

```css
.categoryStatCount_2943a085 {
  color: #475569;
  font-size: 12px;
  font-weight: 600;
}
```

- Element: `<span>`. Numeric count below the category icon.

```css
.totalSection_2943a085 {
  align-items: flex-end;
  border-left: 1px solid #e2e8f0;
  display: flex;
  flex-direction: column;
  gap: 4px;
  padding-left: 24px;
}
```

- Element: `<div>`. Right-aligned total label + total score, with a left divider line.

```css
.totalLabel_2943a085 {
  color: #94a3b8;
  font-size: 10px;
  font-weight: 600;
  letter-spacing: .05em;
}
```

- Element: `<span>`. Tiny uppercase-style label (e.g. "TOTAL").

```css
.score_2943a085 {
  align-items: center;
  color: #0ea5e9;
  display: flex;
  font-size: 24px;
  font-weight: 700;
  gap: 6px;
}

.score_2943a085 i {
  font-size: 28px;
}
```

- Element: `<div>` containing `<i data-icon-name="FavoriteStarFill">` + `<span>`. The big total score with star icon.

### 1.9 Row — expand button

```css
.expandButton_2943a085 {
  align-items: center;
  background: #f1f5f9;
  border: none;
  border-radius: 50%;
  color: #0ea5e9;
  cursor: pointer;
  display: flex;
  justify-content: center;
  padding: 8px;
  transition: background .2s;
}

.expandButton_2943a085:hover {
  background: #e2e8f0;
}

.expandButton_2943a085 i {
  font-size: 20px;
}

.userRowContainer_2943a085.expanded_2943a085 .expandButton_2943a085 {
  background: #e0f2fe;
}
```

- Element: `<button aria-label="Expand">`. Round chevron button. When the parent row has `.expanded_2943a085`, the button background switches to the lighter blue `#e0f2fe`.

> Important: no `width`/`height` is defined for the button. Sizing relies on the icon (`font-size: 20px`) plus `padding: 8px`. This may need an explicit hit-target during build (see §5).

### 1.10 Row — details panel (defined in CSS, NOT in HTML sample)

```css
.details_2943a085 {
  background: #f8fafc;
  border-top: 1px solid #e2e8f0;
  padding: 24px;
}

.detailsTitle_2943a085 {
  color: #64748b;
  font-size: 12px;
  font-weight: 600;
  letter-spacing: .05em;
  margin: 0 0 16px;
  text-transform: uppercase;
}

.tableWrapper_2943a085 {
  overflow-x: auto;
}

.activityTable_2943a085 {
  border-collapse: collapse;
  width: 100%;
}

.activityTable_2943a085 thead tr {
  border-bottom: 2px solid #e2e8f0;
}

.activityTable_2943a085 thead th {
  color: #64748b;
  font-size: 12px;
  font-weight: 600;
  letter-spacing: .05em;
  padding: 12px 8px;
  text-align: left;
  text-transform: uppercase;
}

.activityTable_2943a085 thead th:last-child {
  text-align: right;
}

.activityTable_2943a085 tbody tr {
  transition: background-color .2s;
}

.activityTable_2943a085 tbody tr:hover {
  background: #f1f5f9;
}

.activityTable_2943a085 tbody td {
  border-bottom: 1px solid #e2e8f0;
  font-size: 14px;
  padding: 16px 8px;
}

.activityTable_2943a085 tbody tr:last-child td {
  border-bottom: none;
}

.activityName_2943a085 {
  color: #1e293b;
  font-weight: 600;
}

.activityDate_2943a085 {
  color: #64748b;
}

.activityPoints_2943a085 {
  color: #0ea5e9;
  font-weight: 700;
  text-align: right;
}
```

- Elements: `<div>` panel that contains a `<h3 class="detailsTitle_2943a085">`, a `<div class="tableWrapper_2943a085">` wrapping a `<table class="activityTable_2943a085">` with `<thead>` / `<tbody>`. The structural HTML is NOT in the sample (see §5).

```css
.categoryBadge_2943a085 {
  align-items: center;
  border-radius: 12px;
  display: inline-flex;
  font-size: 12px;
  font-weight: 600;
  padding: 4px 12px;
}

.categoryBadge_2943a085.categoryTraining_2943a085 {
  background: #dbeafe;
  color: #1e40af;
}

.categoryBadge_2943a085.categoryContribution_2943a085 {
  background: #f3e8ff;
  color: #6b21a8;
}

.categoryBadge_2943a085.categoryCommunity_2943a085 {
  background: #dcfce7;
  color: #166534;
}

.categoryBadge_2943a085.categoryDefault_2943a085 {
  background: #e2e8f0;
  color: #475569;
}
```

- Element: `<span>` (inferred — `inline-flex`). Pill badge inside an activity row identifying the activity's category. Modifier classes are mutually exclusive: `categoryTraining_2943a085` (blue), `categoryContribution_2943a085` (purple), `categoryCommunity_2943a085` (green), `categoryDefault_2943a085` (gray).

```css
.categoryIcon_2943a085 {
  align-items: center;
  color: #0284c7;
  display: inline-flex;
  font-size: 16px;
  justify-content: center;
}

.categoryIcon_2943a085:hover {
  color: #0ea5e9;
}
```

- Element: `<i>` (inline icon). Used somewhere inside the details panel; not present in the sampled HTML.

```css
.diamondIcon_2943a085 {
  color: #0ea5e9;
  font-size: 24px;
}
```

- Element: `<i>`. A standalone diamond icon, location undefined in source (see §5).

### 1.11 Responsive overrides — `@media (max-width: 768px)`

All mobile overrides reproduced verbatim. They are scattered across the source CSS but are listed together below for convenience.

```css
@media (max-width: 768px) {
  .podium_2943a085 {
    align-items: center;
    flex-direction: column;
  }

  .podiumColumn_2943a085.podiumRank1_2943a085 {
    margin-top: 0;
    order: 1;
  }

  .podiumColumn_2943a085.podiumRank2_2943a085 {
    order: 2;
  }

  .podiumRank1_2943a085 .podiumBlock_2943a085 {
    height: 140px;
  }

  .podiumRank2_2943a085 .podiumBlock_2943a085 {
    height: 96px;
  }

  .podiumRank3_2943a085 .podiumBlock_2943a085 {
    height: 64px;
  }

  .row_2943a085 {
    padding: 16px;
  }

  .rowMain_2943a085 {
    flex-direction: column;
    gap: 12px;
  }

  .rowLeft_2943a085 {
    gap: 16px;
    width: 100%;
  }

  .info_2943a085 {
    flex: 1;
  }

  .rowRight_2943a085 {
    border-top: 1px solid #e2e8f0;
    justify-content: space-between;
    padding-top: 12px;
    width: 100%;
  }

  .categoryStats_2943a085 {
    gap: 16px;
  }

  .totalSection_2943a085 {
    display: none;
  }

  .details_2943a085 {
    padding: 16px;
  }

  .leaderboard_2943a085 {
    padding: 16px;
  }

  .header_2943a085 {
    margin-bottom: 24px;
  }

  .header_2943a085 .headerContent_2943a085 h2 {
    font-size: 24px;
  }

  .filterBar_2943a085 {
    align-items: stretch;
    flex-direction: column;
    padding: 16px;
  }

  .filterBar_2943a085 .filters_2943a085 {
    flex-direction: column;
    width: 100%;
  }

  .filterBar_2943a085 .search_2943a085 {
    min-width: unset;
    width: 100%;
  }

  .podium_2943a085 {
    margin-bottom: 32px;
  }
}
```

Notable mobile behaviours:

- Podium becomes a single column. Rank 1 moves to the top (`order: 1`), rank 2 to the middle (`order: 2`), rank 3 stays at the bottom.
- All three podium block heights shrink (160→140, 128→96, 96→64).
- `.totalSection_2943a085` is hidden on mobile.
- The filter bar becomes a vertical stack and the search expands to full width.

---

## 2. DESIGN TOKENS

Every literal value extracted from §1, expressed as ready-to-use CSS custom properties. Token names are descriptive, not invented styles.

### 2.1 Colors

```css
:root {
  /* Surfaces */
  --color-bg-page:                #f8fafc;
  --color-bg-surface:             #fff;
  --color-bg-surface-muted:       #f1f5f9;
  --color-border:                 #e2e8f0;

  /* Text */
  --color-text-primary:           #0f172a;
  --color-text-strong:            #1e293b;
  --color-text-secondary:         #475569;
  --color-text-muted:             #64748b;
  --color-text-faint:             #94a3b8;

  /* Accent (sky / cyan) */
  --color-accent:                 #0ea5e9;
  --color-accent-deep:            #0284c7;
  --color-accent-soft-bg:         #e0f2fe;

  /* Rank 1 — gold / yellow */
  --color-rank1-avatar-bg:        #86efac;
  --color-rank1-avatar-border:    #fbbf24;
  --color-rank1-avatar-text:      #166534;
  --color-rank1-badge-bg:         #eab308;
  --color-rank1-score-bg:         #fef9c3;
  --color-rank1-score-border:     #fde047;
  --color-rank1-score-text:       #ca8a04;
  --color-rank1-block-from:       #fef3c7;
  --color-rank1-block-to:         #fde68a;
  --color-rank1-block-top:        #fde047;
  --color-rank1-number-text:      rgba(234, 179, 8, .2);

  /* Rank 2 — silver / slate */
  --color-rank2-avatar-bg:        #cbd5e1;
  --color-rank2-avatar-text:      #1e293b;
  --color-rank2-badge-bg:         #94a3b8;

  /* Rank 3 — bronze / teal */
  --color-rank3-avatar-bg:        #5eead4;
  --color-rank3-avatar-text:      #134e4a;
  --color-rank3-badge-bg:         #92400e;

  /* Default podium block */
  --color-block-from:             #e2e8f0;
  --color-block-to:               #cbd5e1;
  --color-block-top:              #cbd5e1;
  --color-rank-number-text:       rgba(148, 163, 184, .2);

  /* Row avatar default */
  --color-row-avatar-bg:          #fbbf24;

  /* Category badges */
  --color-cat-training-bg:        #dbeafe;
  --color-cat-training-text:      #1e40af;
  --color-cat-contribution-bg:    #f3e8ff;
  --color-cat-contribution-text:  #6b21a8;
  --color-cat-community-bg:       #dcfce7;
  --color-cat-community-text:     #166534;
  --color-cat-default-bg:         #e2e8f0;
  --color-cat-default-text:       #475569;

  /* Shadows (raw rgba, see §2.5 for composed shadows) */
  --shadow-rgba-5:                rgba(0, 0, 0, .05);
  --shadow-rgba-6:                rgba(0, 0, 0, .06);
  --shadow-rgba-10:               rgba(0, 0, 0, .1);
  --shadow-rgba-15:               rgba(0, 0, 0, .15);
}
```

### 2.2 Spacing

```css
:root {
  --space-1: 4px;
  --space-2: 6px;
  --space-3: 8px;
  --space-4: 12px;
  --space-5: 16px;
  --space-6: 20px;
  --space-7: 24px;
  --space-8: 32px;
  --space-9: 64px;

  /* Composite paddings used as-is */
  --pad-row:        20px 24px;     /* .row_2943a085 */
  --pad-filter-bar: 20px 24px;     /* .filterBar_2943a085 */
  --pad-podium:     32px 8px;      /* .podium_2943a085 */
  --pad-podium-score-default: 6px 16px;
  --pad-podium-score-rank1:   8px 20px;
  --pad-cat-badge:  4px 12px;
  --pad-th:         12px 8px;
  --pad-td:         16px 8px;

  /* Container widths */
  --width-content-max: 1200px;     /* header / filterBar / list */
  --width-podium-max:  900px;      /* .podium_2943a085 */
  --width-podium-col-max: 280px;   /* .podiumColumn_2943a085 */
  --width-search-min:  250px;
  --width-rank-min:    32px;       /* .rank_2943a085 */
  --size-row-avatar:   56px;       /* .avatar_2943a085 width/height */

  /* Podium block heights */
  --height-block-rank1:        160px;
  --height-block-rank2:        128px;
  --height-block-rank3:        96px;
  --height-block-rank1-mobile: 140px;
  --height-block-rank2-mobile: 96px;
  --height-block-rank3-mobile: 64px;

  /* Other offsets */
  --offset-rank1-margin-top:   -32px;  /* raises winner column */
  --offset-rank3-number-top:   -16px;
  --offset-badge-bottom:       -8px;
  --offset-badge-right:        -4px;
  --podium-blocktop-height:    2px;
}
```

### 2.3 Typography

```css
:root {
  --font-family: "Segoe UI", -apple-system, BlinkMacSystemFont, Roboto, Oxygen,
                 Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue",
                 sans-serif;

  /* Sizes (px) */
  --fs-10:  10px;   /* .totalLabel_2943a085 */
  --fs-12:  12px;   /* counts, badges, table th/td label, detailsTitle */
  --fs-14:  14px;   /* role, header p, table td */
  --fs-16:  16px;   /* podiumScore i, categoryIcon */
  --fs-18:  18px;   /* podiumScore, name, podiumRank1 score i, podiumRank1 badge */
  --fs-20:  20px;   /* avatar, podiumName, themeToggle i, expandButton i, categoryStatIcon, podiumRank1 podiumScore */
  --fs-24:  24px;   /* score, rank, podiumAvatar span, podiumRank1 podiumName, h2 (mobile), diamondIcon */
  --fs-28:  28px;   /* score i */
  --fs-30:  30px;   /* h2 */
  --fs-32:  32px;   /* podiumRank1 podiumAvatar span */
  --fs-96:  96px;   /* podiumRankNumber */
  --fs-112: 112px;  /* podiumRank1 podiumRankNumber */

  /* Weights */
  --fw-medium:    500;
  --fw-semibold:  600;
  --fw-bold:      700;
  --fw-black:     900;

  /* Letter spacing */
  --tracking-wide: .05em;   /* totalLabel, detailsTitle, table th */
}
```

### 2.4 Border radius

```css
:root {
  --radius-pill:        20px;        /* .podiumScore_2943a085 */
  --radius-card:        12px;        /* filterBar, userRowContainer, categoryBadge */
  --radius-block-top:   12px 12px 0 0; /* .podiumBlock_2943a085 */
  --radius-circle:      50%;         /* themeToggle, podiumAvatar, podiumRankBadge, avatar, expandButton */
}
```

### 2.5 Box shadows

```css
:root {
  --shadow-xs:        0 1px 2px rgba(0, 0, 0, .05);   /* themeToggle, podiumScore */
  --shadow-sm:        0 1px 3px rgba(0, 0, 0, .1);    /* filterBar, userRowContainer */
  --shadow-md-soft:   0 4px 12px rgba(0, 0, 0, .05);  /* filterBar:hover */
  --shadow-md:        0 4px 12px rgba(0, 0, 0, .1);   /* userRowContainer:hover, .expanded */
  --shadow-md-strong: 0 4px 12px rgba(0, 0, 0, .15);  /* podiumAvatar */
  --shadow-inset:     inset 0 2px 4px rgba(0, 0, 0, .06); /* podiumBlock */
}
```

### 2.6 Transitions

```css
:root {
  --transition-theme:    background-color .3s, color .3s; /* .leaderboard_2943a085 */
  --transition-quick:    all .2s;                          /* themeToggle, filterBar, userRowContainer */
  --transition-bg:       background .2s;                   /* expandButton */
  --transition-bg-color: background-color .2s;             /* activityTable tbody tr */
}
```

### 2.7 Gradients

```css
:root {
  --gradient-block-default: linear-gradient(180deg, #e2e8f0, #cbd5e1);
  --gradient-block-rank1:   linear-gradient(180deg, #fef3c7, #fde68a);
}
```

---

## 3. HTML STRUCTURE

### 3.1 Full hierarchy

The structure file is a single line; reproduced here as an indented tree. `[DATA]` placeholders match the source. Class strings are exact.

```text
section.leaderboard_2943a085
├── header.header_2943a085
│   └── div.headerContent_2943a085
│       ├── h2 — [DATA]
│       └── p  — [DATA]
├── div.filterBar_2943a085
│   ├── div.filters_2943a085
│   │   ├── div.ms-Dropdown-container.root-241
│   │   │   └── div#Dropdown0.ms-Dropdown.dropdown-242
│   │   │       │ data-is-focusable="true" data-ktp-target="true" tabindex="0"
│   │   │       │ role="combobox" aria-haspopup="listbox" aria-expanded="false"
│   │   │       ├── span#Dropdown0-option.ms-Dropdown-title.title-273
│   │   │       │     aria-invalid="false"  — [DATA]
│   │   │       └── span.ms-Dropdown-caretDownWrapper.caretDownWrapper-244
│   │   │           └── i.ms-Dropdown-caretDown.caretDown-260
│   │   │               data-icon-name="ChevronDown" aria-hidden="true" — [DATA]
│   │   ├── div.ms-Dropdown-container.root-241   ← Dropdown1, identical inner shape
│   │   │   └── div#Dropdown1.ms-Dropdown.dropdown-242
│   │   │       └── span#Dropdown1-option.ms-Dropdown-title.title-273 …
│   │   │       └── span.ms-Dropdown-caretDownWrapper.caretDownWrapper-244 …
│   │   └── div.ms-Dropdown-container.root-261   ← Dropdown2, parent class differs (root-261 vs root-241)
│   │       └── div#Dropdown2.ms-Dropdown.dropdown-242 …
│   └── div.search_2943a085
│       └── div.ms-SearchBox.root-262
│           ├── div.ms-SearchBox-iconContainer.iconContainer-263 (aria-hidden="true")
│           │   └── i.ms-SearchBox-icon.icon-267
│           │       data-icon-name="Search" aria-hidden="true" — [DATA]
│           └── input#SearchBox3.ms-SearchBox-field.field-266
│                  placeholder="Search employee..." role="searchbox" value=""
├── div.podium_2943a085
│   ├── div.podiumColumn_2943a085.podiumRank2_2943a085      ← FIRST in DOM
│   │   ├── div.podiumUser_2943a085
│   │   │   ├── div.podiumAvatarContainer_2943a085
│   │   │   │   ├── div.podiumAvatar_2943a085
│   │   │   │   └── div.podiumRankBadge_2943a085 — [DATA]
│   │   │   ├── h3.podiumName_2943a085 — [DATA]
│   │   │   ├── p.podiumRole_2943a085  — [DATA]
│   │   │   └── div.podiumScore_2943a085
│   │   │       ├── i.root-275  data-icon-name="FavoriteStarFill" — [DATA]
│   │   │       └── span — [DATA]
│   │   └── div.podiumBlock_2943a085
│   │       ├── div.podiumBlockTop_2943a085
│   │       └── span.podiumRankNumber_2943a085 — [DATA]
│   ├── div.podiumColumn_2943a085.podiumRank1_2943a085      ← SECOND in DOM
│   │   └── (same internal shape)
│   └── div.podiumColumn_2943a085.podiumRank3_2943a085      ← THIRD in DOM
│       └── (same internal shape)
└── div.list_2943a085  data-note="SAMPLED: first 3 of N rows shown — pattern repeats"
    ├── div.userRowContainer_2943a085
    │   └── div.row_2943a085
    │       └── div.rowMain_2943a085
    │           ├── div.rowLeft_2943a085
    │           │   ├── span.rank_2943a085 — [DATA]
    │           │   ├── div.avatar_2943a085
    │           │   └── div.info_2943a085
    │           │       ├── h3.name_2943a085  — [DATA]
    │           │       └── span.role_2943a085 — [DATA]
    │           └── div.rowRight_2943a085
    │               ├── div.categoryStats_2943a085
    │               │   └── div.ms-TooltipHost.root-276 (role="none")
    │               │       ├── div.categoryStat_2943a085
    │               │       │   ├── i.categoryStatIcon_2943a085.root-275
    │               │       │   │      data-icon-name="Presentation" — [DATA]
    │               │       │   └── span.categoryStatCount_2943a085 — [DATA]
    │               │       └── div#tooltip4 (hidden) — [DATA]
    │               ├── div.totalSection_2943a085
    │               │   ├── span.totalLabel_2943a085 — [DATA]
    │               │   └── div.score_2943a085
    │               │       ├── i.root-275 data-icon-name="FavoriteStarFill" — [DATA]
    │               │       └── span — [DATA]
    │               └── button.expandButton_2943a085  aria-label="Expand"
    │                   └── i.root-275 data-icon-name="ChevronDown" — [DATA]
    ├── div.userRowContainer_2943a085   ← row 2 — same shape, single Presentation stat, tooltip5
    └── div.userRowContainer_2943a085   ← row 3 — categoryStats now contains TWO ms-TooltipHost siblings:
            ├── ms-TooltipHost ▶ Education stat        + #tooltip6
            └── ms-TooltipHost ▶ Presentation stat     + #tooltip7
```

The HTML carries this comment at the top, defining the scoping hashes:

> `CSS module hash: _2943a085 = leaderboard, _7ea1264b = breadcrumb, _cae45c08 = feedback`

Only `_2943a085` rules apply to this component.

### 3.2 `data-icon-name` values found

| Icon name           | Occurrences | Where                                                            |
| ------------------- | -----------:| ---------------------------------------------------------------- |
| `ChevronDown`       | 6           | 3× dropdown carets + 3× row expand buttons                       |
| `Search`            | 1           | Search box icon                                                  |
| `FavoriteStarFill`  | 6           | 3× podium scores + 3× row totals                                 |
| `Presentation`      | 3           | One per row (rows 1, 2, 3) inside `.categoryStats_2943a085`     |
| `Education`         | 1           | Row 3 only (additional category stat)                            |

No icon font is shipped; glyph rendering is unresolved (see §5).

### 3.3 ARIA, role and data attributes inventory

- Roles: `role="combobox"` (each dropdown), `role="searchbox"` (search input), `role="none"` (each `ms-TooltipHost`).
- ARIA: `aria-haspopup="listbox"`, `aria-expanded="false"`, `aria-invalid="false"`, `aria-hidden="true"` (icons + search-icon container), `aria-label="Expand"` (each row expand button).
- Focus / keyboarding: `data-is-focusable="true"`, `data-ktp-target="true"`, `tabindex="0"` on each dropdown.
- Tooltips: `<div hidden id="tooltipN">[DATA]</div>` is the Fluent UI pattern for tooltip content; ids found are `tooltip4`, `tooltip5`, `tooltip6`, `tooltip7`.
- Misc: `data-note` on `.list_2943a085` is informational only (not a runtime hook).
- Identifiers: `Dropdown0`, `Dropdown1`, `Dropdown2`, `Dropdown0-option`, `Dropdown1-option`, `Dropdown2-option`, `SearchBox3`, `tooltip4..7`.

### 3.4 Podium column order (left to right)

- DOM order (top to bottom in source):  `Rank2 → Rank1 → Rank3`.
- CSS `order` reorders to:               `Rank2 (1) | Rank1 (2) | Rank3 (3)` left to right on desktop.
- Vertical offset: `.podiumColumn_2943a085.podiumRank1_2943a085 { margin-top: -32px }` raises the winner column.
- Mobile (≤768px): podium becomes a column. `Rank1` is forced to `order: 1`, `Rank2` to `order: 2`, `Rank3` keeps `order: 3`. Stack top-to-bottom: `Rank1 → Rank2 → Rank3`.

### 3.5 Row sub-component structure

```text
userRowContainer_2943a085
└── row_2943a085
    └── rowMain_2943a085
        ├── rowLeft_2943a085
        │   ├── rank_2943a085           (numeric rank, e.g. "4")
        │   ├── avatar_2943a085         (56×56 circle)
        │   └── info_2943a085
        │       ├── name_2943a085       (h3)
        │       └── role_2943a085       (span)
        └── rowRight_2943a085
            ├── categoryStats_2943a085
            │   └── ms-TooltipHost.root-276  (role="none")  — repeats 1–N times
            │       ├── categoryStat_2943a085
            │       │   ├── categoryStatIcon_2943a085 (i, data-icon-name=…)
            │       │   └── categoryStatCount_2943a085 (span)
            │       └── div[hidden id=tooltipN]
            ├── totalSection_2943a085
            │   ├── totalLabel_2943a085
            │   └── score_2943a085
            │       ├── i (FavoriteStarFill)
            │       └── span (number)
            └── expandButton_2943a085 (button, aria-label="Expand")
                └── i (ChevronDown)
```

Important shape detail: `categoryStats_2943a085` can contain a variable number of `ms-TooltipHost` children — rows 1 and 2 contain one (`Presentation`); row 3 contains two (`Education` + `Presentation`).

The `.expanded_2943a085` modifier appears in the CSS but never on the sample rows. When applied to a `.userRowContainer_2943a085`, an additional `.details_2943a085` block (containing `.detailsTitle_2943a085` + `.tableWrapper_2943a085 > .activityTable_2943a085`) is expected to render below `.row_2943a085` (see §1.10 and §5).

---

## 4. INTERACTIVE COMPONENTS

| Component | Selector / id | Type | Behaviour | Filters / scope |
| --------- | ------------- | ---- | --------- | --------------- |
| Dropdown 1 | `#Dropdown0` | `role="combobox"` (custom, NOT `<select>`) | Click opens a listbox; ChevronDown caret rotates / `aria-expanded` toggles. Selecting an option updates `#Dropdown0-option` text and re-filters the list. | Purpose unspecified in source — see §5 |
| Dropdown 2 | `#Dropdown1` | same | same | Purpose unspecified — see §5 |
| Dropdown 3 | `#Dropdown2` | same | same | Purpose unspecified — see §5 |
| Search input | `#SearchBox3` | `<input role="searchbox">` placeholder `Search employee...` | On every input event, filter `.list_2943a085 > .userRowContainer_2943a085` rows by matching the user's display name (and likely role) against the input value. | Filters the row list (and presumably the podium) by name. |
| Expand button | `button.expandButton_2943a085` (one per row, `aria-label="Expand"`) | Button | Toggles `expanded_2943a085` on the closest `.userRowContainer_2943a085`. When expanded:  the container border becomes `#0ea5e9`, the box-shadow becomes `--shadow-md`, the button background becomes `#e0f2fe`, and a `.details_2943a085` panel appears beneath `.row_2943a085`. The chevron icon should also flip 180° (not encoded in CSS — see §5). `aria-expanded` should be reflected on the button. | Toggle per row only. |
| Podium | `div.podium_2943a085` | Display block | Always rendered; CSS provides no hide rule and no JS filter target. Decision: when filters reduce the dataset to <3 entries, behaviour is unspecified (see §5). Recommended: render only when ≥3 results exist. | n/a |

Theme toggle (`.themeToggle_2943a085`) is styled in CSS but absent from the HTML. If implemented, it should toggle a class on the document (or on `.leaderboard_2943a085`) to swap the color tokens. Not required by the structure file.

Loading state (`.loading_2943a085`) is styled in CSS but its activation contract is undefined. If implemented, apply it to the root `<section>` while async data is in-flight.

---

## 5. AMBIGUITIES

Decisions required before building. None of these can be answered from the three source files alone.

### 5.1 Filter dropdowns have no labels

`#Dropdown0`, `#Dropdown1`, `#Dropdown2` carry no visible label, no `aria-label`, no `aria-labelledby`, and the option list is not in the DOM. Their purpose is unspecified. The likely candidates (based on common leaderboard UIs and the fact that the data set is "employees") are: department, time period (week / month / quarter / year), and category — but the exact wording, set of options, and which dropdown does what must be confirmed.

### 5.2 Category-icon → category-badge mapping

The HTML uses two `data-icon-name` values inside `.categoryStats_2943a085`: `Presentation` and `Education`. The CSS, however, defines four category badges in the details panel:

- `.categoryTraining_2943a085`
- `.categoryContribution_2943a085`
- `.categoryCommunity_2943a085`
- `.categoryDefault_2943a085`

The mapping from icon names (e.g. `Presentation`, `Education`, plus any others present in `data.js`) to badge classes is not given. Need a definitive icon-name → category-key table.

### 5.3 Hidden tooltip contents

The `<div hidden id="tooltipN">[DATA]</div>` nodes contain `[DATA]` placeholders only. The actual tooltip text (e.g. "Presentations delivered" / "Trainings completed") is not in the source.

### 5.4 Avatar imagery

Both `.podiumAvatar_2943a085` and `.avatar_2943a085` use `background-position: 50%; background-size: cover;` but the structure file uses a blank-pixel image. The replacement strategy (initials on a colored disc? deterministic color from name? gradient backgrounds?) is undefined.

In addition, `.podiumAvatar_2943a085` has NO width/height in the source — those dimensions must be chosen (the `box-shadow`, the 4px border, and the `font-size: 24px` / `32px` of its `<span>` suggest something around 80–112 px, but this is a guess).

`.podiumRankBadge_2943a085` similarly has no width/height — sizing must be invented.

### 5.5 Expanded-row details panel

`.details_2943a085`, `.detailsTitle_2943a085`, `.tableWrapper_2943a085`, and the full `.activityTable_2943a085 thead/tbody` schema exist in the CSS, but no example DOM is in the structure file. Required decisions:

- Where in the DOM does `.details_2943a085` mount (sibling of `.row_2943a085` inside `.userRowContainer_2943a085`)?
- Exact `<thead>` columns (e.g. Activity, Category, Date, Points)?
- Whether `.activityTable_2943a085` shows ALL activities for a user or only recent ones?
- Where does `.categoryIcon_2943a085` (defined in CSS, no DOM example) go inside the table?
- The `.diamondIcon_2943a085` (color `#0ea5e9`, font-size 24px) is defined but never positioned — its location/role is unknown.

### 5.6 Theme toggle absent from HTML

`.themeToggle_2943a085` (and its `:hover`/`i` rules) is styled but not present in `leaderboard-structure.html`. Decision: include the toggle button, or omit it? If included, the dark-mode color swap is not encoded in the source CSS — would need to be authored. Per CLAUDE.md ("Do not invent styles — if it is not in the CSS files, ask"), the recommendation is to OMIT it unless explicitly approved.

### 5.7 Loading-state trigger

`.leaderboard_2943a085.loading_2943a085 { opacity: .6; pointer-events: none }` exists, but data in this build is loaded synchronously from `data.js`. Whether to expose this state at all (and if so, when) is undefined.

### 5.8 Fluent UI helper classes are unstyled

The structure file references many Fluent UI classes that do NOT appear in `injected-leaderboard.css`:

- Container helpers: `root-241`, `root-261`, `root-262`, `root-263`, `root-275`, `root-276`
- Dropdown internals: `dropdown-242`, `caretDownWrapper-244`, `caretDown-260`, `title-273`
- Search internals: `iconContainer-263`, `icon-267`, `field-266`

None of these come with their own styles in the source. Reproducing the original visual fidelity of the dropdowns and the search box requires either (a) shipping replacement CSS for these helpers, or (b) replacing `ms-Dropdown` / `ms-SearchBox` with custom equivalents that match the look. Strategy must be chosen.

### 5.9 Icon glyphs / icon font

Five Fluent icon names are referenced (`ChevronDown`, `Search`, `FavoriteStarFill`, `Presentation`, `Education`) but no font is bundled and CLAUDE.md forbids CDN/external dependencies. Replacement strategy required: inline SVGs, Unicode (e.g. ★ for `FavoriteStarFill`, ▾ for `ChevronDown`, 🔍 for `Search`), or hand-drawn SVG path data. The chosen approach must be applied consistently to all five icons.

### 5.10 Number of leaderboard rows

`leaderboard-structure.html` carries `data-note="SAMPLED: first 3 of N rows shown — pattern repeats"`, while CLAUDE.md specifies exactly 25 rows must come from `data.js`. The HTML pattern repeats, but the rendered count (and the rule for what shows in the podium when fewer than 3 entries exist) needs confirmation. Recommended default: render all 25 rows; show the podium only when ≥3 entries are present.

### 5.11 Star color for ranks 2 & 3 vs row scores

The CSS uses `#0ea5e9` (sky blue) for both `.podiumRank2_2943a085 .podiumScore_2943a085` and `.podiumRank3_2943a085 .podiumScore_2943a085`, identical to the row `.score_2943a085` color. Rank 1 uses gold (`#ca8a04`). The brown badge color on rank 3 (`#92400e`) is therefore the only differentiator from rank 2 visually for the score area. Confirm this is intentional (no separate bronze-score color is needed).

### 5.12 Chevron rotation when row is expanded

The expanded row swaps the expand button background to `#e0f2fe` but the source CSS does NOT rotate the `ChevronDown` icon. Visually this leaves the chevron pointing down even when the row is open. Decision needed: rotate via JS / inline style, or accept the original behavior.

### 5.13 Site-chrome custom CSS

`task-1/input/custom-styles.css` contains rules for SharePoint chrome (`.sp-appBar`, `div[data-sp-feature-tag^=…]`, `.ms-HubNav-nameLink`, …). None of those targets exist in the standalone `index.html` we will ship. These rules can therefore be ignored for the leaderboard build, but explicit confirmation is recommended in case any of them was intended to set fonts/colors on the page background. The only rule that touches typography globally is:

```css
div[data-sp-feature-tag^="PageHierarchyWebPart"] *:not(i) {
    font-family: var(--fontFamilyCustomFont1000, var(--fontFamilyBase)) !important;
}
```

— which depends on tokens (`--fontFamilyCustomFont1000`, `--fontFamilyBase`) that do not exist in the leaderboard CSS. Decision: drop entirely, or define these tokens? Recommended: drop.
