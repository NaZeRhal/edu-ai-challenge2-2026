# Leaderboard UI Specification

> Phase 1 deliverable. Source: `leaderboard-dom.html` (Company Leaderboard 2025, SharePoint web part).
> All values below are pulled directly from the inlined computed `style` attributes. Where the DOM is silent or self-contradictory, the issue is recorded in the **Ambiguities & Open Questions** section at the end of this document.

## CSS module hash legend

The DOM uses three CSS-module hash suffixes. Treat them as namespaces — every original class name in this spec is the listed local name plus its module hash.

| Hash         | Module             | Where it lives                                                       |
| ------------ | ------------------ | -------------------------------------------------------------------- |
| `_2943a085`  | leaderboard web part | header, filter bar, podium, list rows, total section, expand button |
| `_7ea1264b`  | breadcrumb         | breadcrumb list at the top of the page                               |
| `_cae45c08`  | feedback button    | floating SharePoint feedback button bottom-right                     |

Text content: every text slot in the snapshot is sanitised to `[DATA]`. The **only** literal string preserved in the source is the search input placeholder `Search employee...`. All other strings are unknown and must be sourced separately for the replica.

---

## 1. Layout Structure

The page is a vertical stack of self-contained, horizontally centred sections rendered inside a SharePoint web-part column. The captured/measured content width is **~864 px** (web-part column); some sections cap at `max-width: 1200px` so they will widen if the host column allows.

Render order (top to bottom):

1. **Breadcrumb** — `<ul class="breadcrumbLayoutHorizontal_7ea1264b">`, `width: 914.4px; height: 40px`, transparent background, items left-aligned. (Wider than the rest because it lives in the SharePoint chrome row.)
2. **Page H1** — _absent in the snapshot_ (source comment: `❌ [PAGE H1] NOT FOUND`).
3. **Leaderboard header** — `<header class="header_2943a085">`, `width: 866.4px; max-width: 1200px; height: 65.6px; margin: 0 0 32px 0`. Holds H2 title + subtitle.
4. **Filter bar** — `<div class="filterBar_2943a085">`, `width: 816.8px; max-width: 1200px; height: 32px; padding: 20px 24px; margin: 0 0 24px 0`. White card.
5. **Top-3 podium** — `<div class="podium_2943a085">`, `width: 850.4px; max-width: 900px; height: 400px; padding: 32px 8px; margin: 0 0 64px 0`. Transparent background.
6. **List entries** — vertical stack of `<div class="userRowContainer_2943a085">`, each `width: 864.8px; height: 96px`. Per the source comment 227 such rows follow the same pattern; only 3 are sampled.
7. **Feedback button** — `position: fixed`, bottom-right, outside the document flow.

Page-level / global tokens that recur on every section:

- Body/page background — not captured (transparent on the captured nodes); the surrounding SharePoint page background sits behind the cards.
- Primary text colour: `rgb(15, 23, 42)` (slate-900-ish).
- Default font stack (everything except the breadcrumb): `"Segoe UI", -apple-system, BlinkMacSystemFont, Roboto, Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif`.

Spacing rhythm between major sections: header `margin-bottom: 32px`, filter bar `margin-bottom: 24px`, podium `margin-bottom: 64px`. List rows have no margin between them in the snapshot — the gap, if any, is supplied by the parent list (not captured).

---

## 2. Component Inventory

| # | Component                  | Tag       | Local class (suffix `_2943a085` unless noted)         | Purpose                                                        |
| - | -------------------------- | --------- | ----------------------------------------------------- | -------------------------------------------------------------- |
| 1 | Breadcrumb list            | `<ul>`    | `breadcrumbLayoutHorizontal_7ea1264b`                 | Navigation path; horizontal Fluent breadcrumb.                 |
| 2 | Breadcrumb item            | `<li>`    | `breadcrumbLayoutItem_7ea1264b`                       | One link in the breadcrumb chain.                              |
| 3 | Breadcrumb link            | `<a>`     | `breadcrumbLayoutItemButton_7ea1264b` (current item: `breadcrumbLayoutItemButtonCurrent_7ea1264b`) | Underlined link; current item is not underlined.    |
| 4 | Breadcrumb chevron         | `<span>`  | `breadcrumbLayoutHorizontalIcon_7ea1264b`             | Separator glyph between items.                                 |
| 5 | Header wrapper             | `<header>`| `header_2943a085`                                     | Holds title + subtitle.                                        |
| 6 | Header content             | `<div>`   | `headerContent_2943a085`                              | Inner block containing H2 + subtitle.                          |
| 7 | Title                      | `<h2>`    | _(no module class — inline)_                          | Page title text.                                               |
| 8 | Subtitle                   | `<p>`     | _(no module class — inline)_                          | Page subtitle / description.                                   |
| 9 | Filter bar                 | `<div>`   | `filterBar_2943a085`                                  | White card holding the filters and the search box.             |
| 10 | Filters group             | `<div>`   | `filters_2943a085`                                    | Wrapper around the 3 dropdowns.                                |
| 11 | Dropdown                  | `<div>`   | `ms-Dropdown` (Fluent UI) inside `ms-Dropdown-container` | One filter combobox.                                       |
| 12 | Dropdown title            | `<span>`  | `ms-Dropdown-title`                                   | Visible selected-value text.                                   |
| 13 | Dropdown caret            | `<i>`     | `ms-Dropdown-caretDown` (`data-icon-name="ChevronDown"`) | Down-chevron icon, Fluent MDL2.                             |
| 14 | Search wrapper            | `<div>`   | `search_2943a085`                                     | Sets flex-grow + min-width for the searchbox.                  |
| 15 | Search box                | `<div>`   | `ms-SearchBox`                                        | Fluent search field shell.                                     |
| 16 | Search icon               | `<i>`     | `ms-SearchBox-icon` (`data-icon-name="Search"`)       | Leading magnifier glyph.                                       |
| 17 | Search input              | `<input>` | `ms-SearchBox-field`                                  | Text input; `placeholder="Search employee..."`.                |
| 18 | Podium                    | `<div>`   | `podium_2943a085`                                     | Flex row holding the 3 podium columns.                         |
| 19 | Podium column             | `<div>`   | `podiumColumn_2943a085` + rank modifier `podiumRank1_2943a085` / `podiumRank2_2943a085` / `podiumRank3_2943a085` | Stacks user info on top of the pedestal block. |
| 20 | Podium user block         | `<div>`   | `podiumUser_2943a085`                                 | Avatar + name + role + score pill.                             |
| 21 | Avatar container          | `<div>`   | `podiumAvatarContainer_2943a085`                      | Holds the avatar circle + the rank badge (overlap).            |
| 22 | Avatar circle             | `<div>`   | `podiumAvatar_2943a085`                               | Round photo; rank-1 has gold border, ranks 2/3 have white.     |
| 23 | Rank badge                | `<div>`   | `podiumRankBadge_2943a085`                            | Coloured circle with the rank number, overlapping avatar.      |
| 24 | Podium name               | `<h3>`    | `podiumName_2943a085`                                 | Display name, centred.                                         |
| 25 | Podium role               | `<p>`     | `podiumRole_2943a085`                                 | Department / job title.                                        |
| 26 | Podium score pill         | `<div>`   | `podiumScore_2943a085`                                | Rounded pill with a star icon and the score.                   |
| 27 | Podium pedestal           | `<div>`   | `podiumBlock_2943a085`                                | The "step" under each user.                                    |
| 28 | Pedestal top edge         | `<div>`   | `podiumBlockTop_2943a085`                             | 2 px-tall coloured top edge of the pedestal.                   |
| 29 | Pedestal rank number      | `<span>`  | `podiumRankNumber_2943a085`                           | Huge translucent number (1/2/3) inside the pedestal.           |
| 30 | List row container        | `<div>`   | `userRowContainer_2943a085`                           | White card per user; clipped, 96 px tall when collapsed.       |
| 31 | List row inner            | `<div>`   | `row_2943a085`                                        | Padding wrapper inside the card.                               |
| 32 | Row main                  | `<div>`   | `rowMain_2943a085`                                    | Flex container splitting left/right.                           |
| 33 | Row left                  | `<div>`   | `rowLeft_2943a085`                                    | Rank + avatar + name/role.                                     |
| 34 | Rank cell                 | `<span>`  | `rank_2943a085`                                       | Numeric rank.                                                  |
| 35 | Avatar                    | `<div>`   | `avatar_2943a085`                                     | Circular 56 px photo.                                          |
| 36 | Info block                | `<div>`   | `info_2943a085`                                       | Stacked name + role.                                           |
| 37 | Name                      | `<h3>`    | `name_2943a085`                                       | Display name.                                                  |
| 38 | Role                      | `<span>`  | `role_2943a085`                                       | Department / title.                                            |
| 39 | Row right                 | `<div>`   | `rowRight_2943a085`                                   | Category icons + total + expand.                               |
| 40 | Category stats group      | `<div>`   | `categoryStats_2943a085`                              | Variable-length list of icon + count items.                    |
| 41 | Tooltip host (Fluent)     | `<div>`   | `ms-TooltipHost`                                      | Wraps each stat to provide a hover tooltip.                    |
| 42 | Single category stat      | `<div>`   | `categoryStat_2943a085`                               | One icon + count column.                                       |
| 43 | Category stat icon        | `<i>`     | `categoryStatIcon_2943a085`                           | Fluent MDL2 icon (e.g. `Presentation`, `Education`).           |
| 44 | Category stat count       | `<span>`  | `categoryStatCount_2943a085`                          | Numeric count under the icon.                                  |
| 45 | Total section             | `<div>`   | `totalSection_2943a085`                               | Right-aligned column with a left divider.                      |
| 46 | Total label               | `<span>`  | `totalLabel_2943a085`                                 | Tiny tracked-out label above the score.                        |
| 47 | Score (row)               | `<div>`   | `score_2943a085`                                      | Star icon + total score.                                       |
| 48 | Expand button             | `<button>`| `expandButton_2943a085`                               | Round button that opens the row detail; `aria-label="Expand"`. |
| 49 | Feedback controller       | `<div>`   | `FeedbackController_cae45c08`                         | SharePoint feedback wrapper.                                   |
| 50 | Feedback button           | `<div>`   | `FeedbackButton_cae45c08`                             | Floating round-corner button, `title="Share feedback"`.        |
| 51 | Feedback icon container   | `<span>`  | `FeedbackTextContainer_cae45c08`                      | Centres the icon (and its hidden label).                       |
| 52 | Feedback icon             | `<i>`     | _(no module class)_ `data-icon-name="Feedback"`        | Fluent MDL2 feedback glyph.                                    |
| 53 | Feedback text             | `<span>`  | `FeedbackText_cae45c08`                               | Empty in the snapshot; reserved for an optional label.         |

---

## 3. Design Tokens

These are the precise values pulled from `style="…"`. Variable names are suggestions for the `:root` block of the replica.

### 3.1 Colour palette

| Token                         | Value                                | Where used                                                                          |
| ----------------------------- | ------------------------------------ | ----------------------------------------------------------------------------------- |
| `--color-text-primary`        | `rgb(15, 23, 42)`                    | Header, names, podium names, score numbers (when not accent), default text colour.  |
| `--color-text-muted`          | `rgb(100, 116, 139)`                 | Subtitle, role/job-title text under names.                                          |
| `--color-text-dim`            | `rgb(148, 163, 184)`                 | List rank numbers, "TOTAL" label, silver podium badge bg.                           |
| `--color-text-stat`           | `rgb(71, 85, 105)`                   | Category-stat count number under icons.                                             |
| `--color-surface-card`        | `rgb(255, 255, 255)`                 | Filter-bar card, list-row card, score pill background.                              |
| `--color-surface-soft`        | `rgb(241, 245, 249)`                 | Expand-button background (idle state).                                              |
| `--color-surface-fluent`      | `rgb(235, 235, 237)`                 | Fluent dropdown / search input background (host control, not custom).               |
| `--color-border`              | `rgb(226, 232, 240)`                 | Filter-bar, list-row, score-pill borders; total-section left divider.               |
| `--color-fluent-border`       | `rgb(55, 55, 55)`                    | Fluent dropdown + search-box border (host control).                                 |
| `--color-accent`              | `rgb(14, 165, 233)`                  | Score numbers, score star icon, category-stat icons, expand-button icon.            |
| `--color-rank1-avatar-border` | `rgb(251, 191, 36)`                  | Gold border around rank-1 avatar; also bg of the placeholder list avatar.           |
| `--color-rank1-badge`         | `rgb(234, 179, 8)`                   | Rank-1 badge fill.                                                                  |
| `--color-rank1-pill-bg`       | `rgb(254, 249, 195)`                 | Rank-1 score pill background.                                                       |
| `--color-rank1-pill-text`     | `rgb(202, 138, 4)`                   | Rank-1 score pill text + star.                                                      |
| `--color-rank1-pill-border`   | `rgb(253, 224, 71)`                  | Rank-1 score pill border.                                                           |
| `--color-rank1-pedestal-1`   | `rgb(254, 243, 199)`                 | Rank-1 pedestal gradient start.                                                     |
| `--color-rank1-pedestal-2`   | `rgb(253, 230, 138)`                 | Rank-1 pedestal gradient end + 1.6 px top border.                                   |
| `--color-rank2-badge`         | `rgb(148, 163, 184)`                 | Rank-2 (silver) badge fill.                                                         |
| `--color-rank3-badge`         | `rgb(146, 64, 14)`                   | Rank-3 (bronze) badge fill.                                                         |
| `--color-podium-neutral-1`    | `rgb(226, 232, 240)`                 | Ranks 2 & 3 pedestal gradient start.                                                |
| `--color-podium-neutral-2`    | `rgb(203, 213, 225)`                 | Ranks 2 & 3 pedestal gradient end + their 1.6 px top edge.                          |
| `--color-rank-number-faded`   | `rgba(148, 163, 184, 0.2)`           | Huge `2`/`3` digit inside ranks 2/3 pedestals.                                      |
| `--color-rank1-number-faded`  | `rgba(234, 179, 8, 0.2)`             | Huge `1` digit inside the rank-1 pedestal.                                          |
| `--color-feedback-bg`         | `rgba(202, 202, 211, 0.62)`          | Floating feedback button background.                                                |

### 3.2 Typography

```css
:root {
  --font-app: "Segoe UI", -apple-system, BlinkMacSystemFont, Roboto, Oxygen,
              Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue",
              sans-serif;
  --font-fluent: "Segoe UI", "Segoe UI Web (West European)", "Segoe UI",
                 -apple-system, BlinkMacSystemFont, Roboto, "Helvetica Neue",
                 sans-serif;
  --font-icons: "Fluent MDL2 Hybrid Icons";
  --font-breadcrumb: "Aeonik Pro-1089496262"; /* host-page font; see Ambiguities */
}
```

| Element                                 | Size      | Weight | Line-height | Notes                                                   |
| --------------------------------------- | --------- | ------ | ----------- | ------------------------------------------------------- |
| Header H2                               | 30 px     | 700    | (default)   | Colour `--color-text-primary`.                          |
| Header subtitle                         | 14 px     | 400    | (default)   | Colour `--color-text-muted`.                            |
| Breadcrumb item label                   | 14 px     | 600    | 14 px       | Underline; current item not underlined.                 |
| Breadcrumb chevron icon                 | 14 px     | 400    | (default)   | Glyph from breadcrumb font.                             |
| Filter dropdown title                   | 14 px     | 400    | 30 px       | Fluent host control.                                    |
| Filter dropdown caret                   | 12 px     | 400    | 30 px       | Fluent MDL2 icon font.                                  |
| Search input                            | 14 px     | 400    | (default)   | Placeholder colour rendered by Fluent.                  |
| Podium 1 name                           | 24 px     | 700    | (default)   | Centred.                                                |
| Podium 2 / 3 name                       | 20 px     | 700    | (default)   | Centred.                                                |
| Podium role                             | 14 px     | 500    | (default)   | Colour `--color-text-muted`.                            |
| Podium 1 score pill                     | 20 px     | 700    | (default)   | Star icon 18 px.                                        |
| Podium 2 / 3 score pill                 | 18 px     | 700    | (default)   | Star icon 16 px.                                        |
| Podium rank number (big "2"/"3")        | 96 px     | 900    | (default)   | Colour `--color-rank-number-faded`.                     |
| Podium rank number ("1")                | 112 px    | 900    | (default)   | Colour `--color-rank1-number-faded`.                    |
| Podium rank badge text                  | 14 px (rank 2/3) / 18 px (rank 1) | 700 | (default) | White on coloured circle.                |
| List rank number                        | 24 px     | 700    | (default)   | Colour `--color-text-dim`, centred.                     |
| List name                               | 18 px     | 700    | (default)   | Colour `--color-text-primary`.                          |
| List role                               | 14 px     | 400    | (default)   | Colour `--color-text-muted`.                            |
| List total label                        | 10 px     | 600    | (default)   | `letter-spacing: 0.5px`, colour `--color-text-dim`.     |
| List score number                       | 24 px     | 700    | (default)   | Colour `--color-accent`. Star icon 28 px.               |
| Category stat icon                      | 20 px     | 400    | (default)   | Fluent MDL2.                                            |
| Category stat count                     | 12 px     | 600    | (default)   | Colour `--color-text-stat`.                             |
| Feedback icon                           | 16 px     | 400    | (default)   | Fluent MDL2 `Feedback`.                                 |

### 3.3 Spacing scale

The DOM uses a consistent 4 px-multiple scale: **4, 6, 8, 12, 16, 20, 24, 32, 64** px. Notable applications:

- Filter card padding `20px 24px`, gap `12px`.
- Podium gap between columns `24px`, padding `32px 8px`, bottom margin `64px`.
- Podium pedestal padding-top `16px`; rank-1 column `margin-top: -32px` (raises the centre column).
- List row card outer height `96px`; inner row padding `20px 24px`; `rowMain` gap `16px`; `rowLeft` gap `24px`; `rowRight` gap `24px` with `padding-left: 24px` on the total section.
- Score pills: padding `6px 16px` (rank 2/3) / `8px 20px` (rank 1); internal gap `6px`.
- Avatars sit `12px` above their name (`margin-bottom: 12px`). Name `4px` above role. Role `8px` above the score pill.
- Rank badge offset relative to its 80/80/112-px avatar: `top:56px;left:52px` for ranks 2/3, `top:80px;left:76px` for rank 1 (i.e. roughly bottom-right corner overlap).

### 3.4 Border, radius, elevation

| Token                                       | Value                                                                                          |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Card border                                 | `0.8px solid rgb(226, 232, 240)`                                                               |
| Card border-radius                          | `12px` (filter bar, list-row card)                                                             |
| Score-pill border-radius                    | `20px`                                                                                         |
| Pedestal border-radius                      | `12px 12px 0 0`                                                                                |
| Pedestal top edge                           | `border-width: 1.6px 0 0 0; border-style: solid none none none;` colour matches gradient end   |
| Avatar (list)                               | `border-radius: 50%`, no border                                                                |
| Avatar (podium)                             | `border: 4px solid rgb(255, 255, 255)` for ranks 2/3; `4px solid rgb(251, 191, 36)` for rank 1 |
| Rank badge (podium)                         | `border-radius: 50%; border: 4px solid rgb(255, 255, 255)`                                     |
| Expand button                               | `border-radius: 50%`, no border                                                                |
| Fluent dropdown / search border             | `0.8px solid rgb(55, 55, 55); border-radius: 2px`                                              |
| Total-section left divider                  | `border-left: 0.8px solid rgb(226, 232, 240)`                                                  |
| Feedback button radius                      | `5px`                                                                                          |

| Shadow token              | Value                                              | Used on                                  |
| ------------------------- | -------------------------------------------------- | ---------------------------------------- |
| `--shadow-card`           | `rgba(0, 0, 0, 0.1) 0px 1px 3px 0px`              | Filter bar, list-row card                |
| `--shadow-pill`           | `rgba(0, 0, 0, 0.05) 0px 1px 2px 0px`             | Podium score pills                       |
| `--shadow-avatar`         | `rgba(0, 0, 0, 0.15) 0px 4px 12px 0px`            | Podium avatar circles                    |
| `--shadow-pedestal-inset` | `rgba(0, 0, 0, 0.06) 0px 2px 4px 0px inset`       | All three pedestals                      |

### 3.5 Transitions

The DOM exposes very limited transition info (most elements report `transition: all`, which is the inspector's catch-all when no explicit `transition-property` is set). The few specific transitions captured are:

| Element                  | `transition`                             |
| ------------------------ | ---------------------------------------- |
| Filter bar (card)        | `0.2s` (on the `transition` shorthand)   |
| List-row card            | `0.2s`                                   |
| Expand button            | `background 0.2s`                        |
| Search-box icon container| `width 0.167s`                           |
| Search-box icon          | `opacity 0.167s`                         |
| Feedback button          | `bottom 0.4s ease-in-out`                |

---

## 4. Data Model

Inferred from the row/podium structure. All names are based on the DOM class names; only the search placeholder text is a real string, every other text node is `[DATA]`.

```ts
type Rank = 1 | 2 | 3 | number; // 1..N

interface LeaderboardEntry {
  rank: number;          // integer; 1..N
  name: string;          // displayed in <h3 class="name_2943a085"> and <h3 class="podiumName_2943a085">
  role: string;          // department / job title shown under the name
  avatarUrl: string;     // background-image of .avatar_2943a085 / .podiumAvatar_2943a085
  score: number;         // total shown next to a star (FavoriteStarFill)
  categoryStats: CategoryStat[]; // 0..N; visible in row-right and the expanded panel
}

interface CategoryStat {
  icon: 'Presentation' | 'Education' | string; // Fluent MDL2 icon name (Presentation, Education observed; more likely possible)
  count: number;                                // integer shown under the icon
  tooltipLabel: string;                         // hidden text inside ms-TooltipHost; describes the category
}
```

### Visual differentiation by rank

- **Top 3 entries** are rendered in the **podium** (section 6) with rank-specific colour, avatar size, badge and pedestal height. They do **not** appear in the list rows below the podium (the snapshot shows the list starts after the podium).
- **Rank 4..N** are rendered uniformly as `userRowContainer_2943a085` rows. The rank number stays at 24/700 in `--color-text-dim`; there is **no** alternating background, no special highlight for rank 4 etc.
- **Rank 1** is visually distinct from ranks 2 & 3: bigger avatar (112 vs 80 px), gold avatar border, gold-yellow badge fill, taller pedestal (160 px vs 128/96), warm-yellow gradient and pill, and a 112 px pedestal digit. Ranks 2 and 3 share the same neutral pedestal gradient and pill style; only the badge colour differs (silver vs bronze).

### Variable-cardinality fields

`categoryStats` is variable per entry. Sample evidence: list row 1 has 1 stat (`Presentation`), list row 3 has 2 stats (`Education`, `Presentation`). The `categoryStats_2943a085` container width grows with content (`width: 20px` → `width: 64px`).

---

## 5. Filter & Sort Controls

The filter bar is a single white card laid out as `display: flex; flex-direction: row; flex-wrap: wrap; justify-content: space-between; align-items: center; gap: 12px`.

Inside it:

- **Filters group** (`filters_2943a085`) — flex row, `gap: 12px`, holding three Fluent UI dropdowns in this order:

  | Position | DOM `id`     | Width  | Visible label                                    |
  | -------- | ------------ | ------ | ------------------------------------------------ |
  | 1        | `Dropdown0`  | 120 px | `[DATA]` (label unknown — see Ambiguities)       |
  | 2        | `Dropdown1`  | 120 px | `[DATA]`                                         |
  | 3        | `Dropdown2`  | 150 px | `[DATA]`                                         |

  Each dropdown is the standard Fluent UI shell:

  - `<div class="ms-Dropdown-container root-241">` wraps everything.
  - `<div class="ms-Dropdown" role="combobox" aria-haspopup="listbox" aria-expanded="false">` is the focusable surface, `tabindex="0"`.
  - `<span class="ms-Dropdown-title">` shows the current value.
    - Padding `0 28px 0 8px` (extra right padding clears the caret).
    - Background `rgb(235, 235, 237)`, border `0.8px solid rgb(55, 55, 55)`, radius `2px`.
    - Font 14/400, line-height 30 px, `overflow:hidden`, `cursor:pointer`.
  - `<span class="ms-Dropdown-caretDownWrapper">` is `position:absolute; right:8px; bottom:-1px;` containing an `<i data-icon-name="ChevronDown">` from `"Fluent MDL2 Hybrid Icons"`, 12 px, colour `rgb(55, 55, 55)`.
  - The dropdowns do not expose options in the snapshot (they're closed); option count is therefore unknown.

- **Search wrapper** (`search_2943a085`) — `flex: 1 1 0%; min-width: 250px; height: 32px`. Holds the Fluent search box.
  - `<div class="ms-SearchBox">` — `display: flex; align-items: stretch; padding: 1px 0 1px 4px; background: rgb(235, 235, 237); border: 0.8px solid rgb(55, 55, 55); border-radius: 2px`.
  - `<div class="ms-SearchBox-iconContainer">` — fixed 32 × 28.4 px, centred icon, `transition: width 0.167s`.
  - `<i data-icon-name="Search" class="ms-SearchBox-icon">` — 16 px, colour `rgb(41, 41, 43)`, `transition: opacity 0.167s`.
  - `<input id="SearchBox3" class="ms-SearchBox-field" placeholder="Search employee..." role="searchbox">` — `flex: 1 1 0px`, font 14/400, transparent background, no border, padding `0 0 0.5px 0`.

Layout summary: the dropdowns are pinned to the left of the bar, the search input fills the remaining width. The bar wraps to a second row only on narrow widths (`flex-wrap: wrap`).

---

## 6. Top 3 Podium

`<div class="podium_2943a085">` is a flex row with `justify-content: center; align-items: flex-end; gap: 24px` and `padding: 32px 8px`. The podium overall is `850.4 × 400 px` with `max-width: 900px`.

Three children, in DOM order **rank 2, rank 1, rank 3**, so visually rank 1 sits in the middle.

| Position (visual) | Rank | Class modifier            | Column size (W × H) | Avatar size | Avatar border               | Badge size | Badge colour            | Pedestal H | Pedestal gradient                            | Pedestal top edge          | Score pill colours                                                | Big rank number (font / colour) | Special offset       |
| ----------------- | ---- | ------------------------- | ------------------- | ----------- | --------------------------- | ---------- | ----------------------- | ---------- | -------------------------------------------- | -------------------------- | ----------------------------------------------------------------- | ------------------------------- | -------------------- |
| Left              | 2    | `podiumRank2_2943a085`    | 267.475 × 356 px    | 80 px       | 4 px solid `rgb(255,255,255)` | 32 px      | `rgb(148, 163, 184)`    | 128 px     | `linear-gradient(rgb(226,232,240), rgb(203,213,225))` | 1.6 px `rgb(203,213,225)` | bg `rgb(255,255,255)`, text/icon `rgb(14,165,233)`, border `rgb(226,232,240)` | 96/900, `rgba(148,163,184,0.2)` | none                  |
| Centre            | 1    | `podiumRank1_2943a085`    | 267.462 × 432 px    | 112 px      | 4 px solid `rgb(251,191,36)` | 40 px      | `rgb(234, 179, 8)`      | 160 px     | `linear-gradient(rgb(254,243,199), rgb(253,230,138))` | 1.6 px `rgb(253,224,71)` | bg `rgb(254,249,195)`, text/icon `rgb(202,138,4)`, border `rgb(253,224,71)` | 112/900, `rgba(234,179,8,0.2)`  | `margin-top: -32px`   |
| Right             | 3    | `podiumRank3_2943a085`    | 267.462 × 324 px    | 80 px       | 4 px solid `rgb(255,255,255)` | 32 px      | `rgb(146, 64, 14)`      | 96 px      | `linear-gradient(rgb(226,232,240), rgb(203,213,225))` | 1.6 px `rgb(203,213,225)` | bg `rgb(255,255,255)`, text/icon `rgb(14,165,233)`, border `rgb(226,232,240)` | 96/900, `rgba(148,163,184,0.2)` | rank-number block has `position: relative; top: -16px` |

Common podium details:

- Avatar circle: `border-radius: 50%; box-shadow: rgba(0, 0, 0, 0.15) 0 4px 12px 0`. Background image is the photo; fallback bg colour visible in the snapshot is the SharePoint placeholder colour for that user (`rgb(203,213,225)` for rank 2, `rgb(134,239,172)` for rank 1, `rgb(94,234,212)` for rank 3).
- Rank badge: `display: flex; justify-content: center; align-items: center; position: absolute; border: 4px solid rgb(255, 255, 255); border-radius: 50%; color: rgb(255, 255, 255)`. Positioned bottom-right of the avatar via top/left offsets (see Spacing scale).
- Name (`podiumName_2943a085`): `text-align: center`, `margin-bottom: 4px`. Rank-1 size 24/700; rank 2 & 3 size 20/700.
- Role (`podiumRole_2943a085`): 14/500, colour `rgb(100, 116, 139)`, `margin-bottom: 8px`, `text-align: left` (despite the rest of the column being centred).
- Score pill (`podiumScore_2943a085`): `display: flex; align-items: center; gap: 6px; border-radius: 20px; box-shadow: rgba(0,0,0,0.05) 0 1px 2px 0`. The pill contains an `<i data-icon-name="FavoriteStarFill">` followed by a `<span>` with the score number.
- Pedestal (`podiumBlock_2943a085`): `display: flex; justify-content: center; align-items: flex-start; padding-top: 16px; border-radius: 12px 12px 0 0; box-shadow: rgba(0,0,0,0.06) 0 2px 4px 0 inset; overflow: hidden`. Top edge is a 1.6 px-tall `border-top` only; the gradient fills the rest. Inside it sits the `podiumBlockTop_2943a085` strip (positioned `position: absolute; bottom: <pedestal-height + 14>px; height: 2px; width: 100%`) and the huge `podiumRankNumber_2943a085` digit.

The visual "elevation" of the centre column comes from `margin-top: -32px` plus the taller pedestal (160 vs 128/96 px), not from a different background colour.

---

## 7. List Entries

One row in the list (collapsed state):

```html
<div class="userRowContainer_2943a085">         <!-- 864.8 × 96 px white card -->
  <div class="row_2943a085">                    <!-- 816.8 × 56 px, padding 20 24 -->
    <div class="rowMain_2943a085">              <!-- flex row, gap 16 -->
      <div class="rowLeft_2943a085">            <!-- gap 24 -->
        <span class="rank_2943a085">…</span>
        <div class="avatar_2943a085"></div>     <!-- 56 × 56 round, with bg-image -->
        <div class="info_2943a085">             <!-- column, gap 4 -->
          <h3 class="name_2943a085">…</h3>
          <span class="role_2943a085">…</span>
        </div>
      </div>
      <div class="rowRight_2943a085">           <!-- gap 24 -->
        <div class="categoryStats_2943a085">…</div>  <!-- variable count of stats -->
        <div class="totalSection_2943a085">     <!-- left-bordered column, gap 4 -->
          <span class="totalLabel_2943a085">…</span>
          <div class="score_2943a085">          <!-- gap 6 -->
            <i data-icon-name="FavoriteStarFill"></i>
            <span>…</span>
          </div>
        </div>
        <button class="expandButton_2943a085" aria-label="Expand">
          <i data-icon-name="ChevronDown"></i>
        </button>
      </div>
    </div>
  </div>
</div>
```

Exact metrics:

- **Card** (`userRowContainer_2943a085`): `width: 864.8px; height: 96px; background: rgb(255, 255, 255); border: 0.8px solid rgb(226, 232, 240); border-radius: 12px; box-shadow: rgba(0,0,0,0.1) 0 1px 3px 0; overflow: hidden; transition: 0.2s`.
- **Inner row** (`row_2943a085`): `width: 816.8px; height: 56px; padding: 20px 24px`.
- **Row main** (`rowMain_2943a085`): `display: flex; justify-content: space-between; align-items: center; gap: 16px`.
- **Row left** (`rowLeft_2943a085`): `display: flex; align-items: center; gap: 24px; flex: 1 1 0%`.
- **Rank cell** (`rank_2943a085`): `width: 32px; min-width: 32px; height: 32px; font: 700 24px/normal var(--font-app); color: rgb(148, 163, 184); text-align: center`.
- **Avatar** (`avatar_2943a085`): `width: 56px; height: 56px; border-radius: 50%; background-color: rgb(251, 191, 36)` with the user's photo as `background-image` (`background-size: cover; background-position: 50% 50%`). No border. Centre-aligned.
- **Info** (`info_2943a085`): `display: flex; flex-direction: column; gap: 4px; flex: 1 1 0%`.
  - **Name** (`name_2943a085`): 18/700, colour `rgb(15, 23, 42)`.
  - **Role** (`role_2943a085`): 14/400, colour `rgb(100, 116, 139)`.
- **Row right** (`rowRight_2943a085`): `display: flex; align-items: center; gap: 24px; height: 48.8px`.
- **Category stats** (`categoryStats_2943a085`): `display: flex; align-items: center; gap: 24px`. Variable count of children (see section 8). When collapsed only the icon + count are visible; the tooltip host is hidden by default.
- **Total section** (`totalSection_2943a085`): `display: flex; flex-direction: column; align-items: flex-end; gap: 4px; padding-left: 24px; border-left: 0.8px solid rgb(226, 232, 240)`. Width 75.425 px in the snapshot.
  - **Label** (`totalLabel_2943a085`): 10/600 with `letter-spacing: 0.5px`, colour `rgb(148, 163, 184)`.
  - **Score** (`score_2943a085`): `display: flex; align-items: center; gap: 6px; font: 700 24px var(--font-app); color: rgb(14, 165, 233)`. Star icon (`FavoriteStarFill`) is 28 px in the same accent colour.
- **Expand button** (`expandButton_2943a085`): `<button>` with `aria-label="Expand"`. `width: 36px; height: 36px; padding: 8px; border: 0; border-radius: 50%; background: rgb(241, 245, 249); color: rgb(14, 165, 233); cursor: pointer; transition: background 0.2s`. Holds an `<i data-icon-name="ChevronDown">` 20 × 20 px, accent colour, 20 px font.

Hover / focus state: not directly observable in a static snapshot. The `transition: 0.2s` on the card and `transition: background 0.2s` on the button suggest a hover style change is intended; the design intent is left to phase 2 / inferred.

---

## 8. Expanded Entry (Category Stats)

The DOM snapshot does **not** include an actual expanded row. The "category stats" panel that section 8 references is the same `categoryStats_2943a085` block that already lives inside `rowRight_2943a085` (see section 7). Treat it as the structural reference for what each "stat" looks like.

Per-stat structure:

```html
<div class="ms-TooltipHost root-276" role="none">
  <div class="categoryStat_2943a085">
    <i data-icon-name="Presentation" class="categoryStatIcon_2943a085 root-275"></i>
    <span class="categoryStatCount_2943a085">[DATA]</span>
  </div>
  <div hidden id="tooltipN">[DATA]</div>  <!-- tooltip text, shown on hover -->
</div>
```

Layout:

- `categoryStats_2943a085`: `display: flex; align-items: center; gap: 24px; height: 40px`. Width grows with content (20 px for one stat, 64 px for two).
- `categoryStat_2943a085`: `display: flex; flex-direction: column; align-items: center; gap: 4px; width: 20px; height: 40px`. Stacks the icon over the count.
- `categoryStatIcon_2943a085`: 20 × 20 px, font `Fluent MDL2 Hybrid Icons`, colour `rgb(14, 165, 233)`. Icon names observed:
  - `Presentation` (likely "presentations given" or similar)
  - `Education` (likely "trainings completed" or similar)
  - More icons are likely possible across the 227 rows; only these two are present in the sample.
- `categoryStatCount_2943a085`: 12/600, colour `rgb(71, 85, 105)`, content is an integer.
- `ms-TooltipHost` wraps each stat; the actual tooltip text lives in a sibling `<div hidden id="tooltipN">[DATA]</div>` and is shown on hover via Fluent. The tooltip text is unknown (`[DATA]`).

What "expanded" actually means is **ambiguous** in the snapshot — see Ambiguities. Most likely behaviour: clicking the expand button reveals the same `categoryStats` (or a richer version of it) inside an expanded sub-panel, but the source does not contain that markup so it cannot be specified from the DOM alone.

---

## 9. Feedback Button

```html
<div class="FeedbackController_cae45c08">
  <div class="FeedbackButton_cae45c08" title="Share feedback">
    <span class="FeedbackTextContainer_cae45c08 css-277">
      <i data-icon-name="Feedback" class="root-275">[DATA]</i>
      <span class="FeedbackText_cae45c08"></span>  <!-- empty in snapshot -->
    </span>
  </div>
</div>
```

Properties:

- **Position**: `position: fixed; z-index: 1000`. Computed offsets in the captured viewport: `top: 599.2px; right: 30px; bottom: 60px; left: 927.6px`. Practically the button is anchored to the bottom-right of the viewport (`right: 30px; bottom: 60px`); the `top` and `left` values are computed from the viewport size at capture and should not be replicated literally.
- **Size**: `36 × 36px`.
- **Background**: `rgba(202, 202, 211, 0.62)` (translucent grey).
- **Border-radius**: `5px`.
- **No border**.
- **Cursor**: `pointer`.
- **Overflow**: `auto hidden`.
- **Transition**: `bottom 0.4s ease-in-out` (the button slides in/out from the bottom).
- **Title** (tooltip): `Share feedback` — this is the only literal accessibility/string content in the floating control.
- **Icon container** (`FeedbackTextContainer_cae45c08`): `display: flex; justify-content: center; padding: 10px; width: 16px; height: 16px`.
- **Icon**: `<i data-icon-name="Feedback">` from `Fluent MDL2 Hybrid Icons`, 16 px, colour `rgb(0, 0, 0)`.
- **Label** (`FeedbackText_cae45c08`): empty `<span>` reserved for an optional text label; in the captured state no label is rendered.

The control is **floating**, not part of any section. It belongs to SharePoint's host UI but the source instructions list it as in-scope; the replica should reproduce its visual style and behaviour.

---

## 10. Breadcrumb (extra, captured but not in instruction sections)

Although not enumerated in the analysis instructions, the breadcrumb is part of the captured DOM and should be either reproduced or explicitly skipped in the replica.

- Container: `<ul class="breadcrumbLayoutHorizontal_7ea1264b">`, `display: flex; flex-direction: row; align-items: flex-start; width: 914.4px; height: 40px`.
- Each item: `<li class="breadcrumbLayoutItem_7ea1264b">` `display: flex; align-items: center; height: 40px`.
- Each link: `<a class="ms-Button ms-Button--action ms-Button--command breadcrumbLayoutItemButton_7ea1264b">` (current item replaces the trailing class with `breadcrumbLayoutItemButtonCurrent_7ea1264b`). Padding `0 4px`, transparent border `0.8px solid rgba(0,0,0,0)`, border-radius `2px`, font 14/600, line-height 19.6 px, `text-decoration: underline` for non-current items only, `cursor: pointer`, colour `rgb(0, 0, 0)`.
- Separator: `<span class="breadcrumbLayoutHorizontalIcon_7ea1264b">` 4.9875 × 16 px, font 14/400, glyph from `"Aeonik Pro-1089496262"`. Sits between adjacent items.
- Three items captured; the third is the current page.

---

## Ambiguities & Open Questions

These are points where the snapshot is silent, contradictory, or where a design decision must be made before phase 2.

1. **Page H1 missing.** The source comment explicitly says `❌ [PAGE H1] NOT FOUND`. The replica needs either a real H1 (decide copy in phase 2) or to deliberately omit it.
2. **Text content is fully redacted.** Every text node renders as `[DATA]`. The only literal string is the search placeholder `Search employee...`. Copy for the H2 title, subtitle, breadcrumb items, dropdown labels & options, names, roles, scores, totals, "TOTAL" label, big rank digits, score numbers, category-stat tooltips, etc. is unknown and must be supplied per the user-rule that requires fictional but realistic data.
3. **Filter dropdowns are closed.** The number of options inside each dropdown, the option text, and the currently selected value are not captured. We know there are exactly **3** dropdowns at widths 120 / 120 / 150 px and that they are populated (each has a non-empty `ms-Dropdown-title`), but the labels (e.g. "Department", "Time period", "Sort by") are guesses.
4. **Section 8 "Expanded panel" is identical to the inline `categoryStats`.** The instructions imply that an expanded row reveals additional information, but the snapshot's section 8 captures only the same inline `categoryStats_2943a085` markup that already appears in section 7. There is no separate panel structure, and the only between-row variation observed is the *number* of stat children (1 in row 1, 2 in row 3). The replica's expanded-state design therefore has to be inferred or specified separately; do not attempt to derive it from this DOM alone.
5. **Bronze pedestal uses the silver gradient.** Ranks 2 and 3 share the same neutral pedestal gradient `rgb(226,232,240) → rgb(203,213,225)` and the same 2 px top-edge colour `rgb(203,213,225)`; only the badge fill differentiates them (silver `rgb(148,163,184)` vs bronze `rgb(146,64,14)`). This is unusual for a podium — possibly a SharePoint quirk vs. a design intent that all non-winners share a "neutral stone" pedestal. Replicate as-is unless told otherwise.
6. **Rank-1 elevation is structural, not visual.** The centre column's apparent height comes from `margin-top: -32px` on the column plus a 32 px taller pedestal. There is no extra shadow, no extra outer wrapper. Match this exactly.
7. **List avatar bg colour is `rgb(251, 191, 36)`.** This is the same gold used on the rank-1 podium avatar border and is applied on **every** list row's avatar as a fallback colour behind the photo. It is unlikely to be visible when the photo loads, but it is a designed fallback — keep it.
8. **`role` colour vs. text alignment on podium.** `podiumRole_2943a085` has `text-align: left` even though the rest of the user block is centred. Probably a bug in the source CSS but it is what the DOM reports; flagged here, not corrected.
9. **`transition: all` is the inspector's default**, not a real CSS rule. The only meaningful transitions are listed in 3.5; treat any other `transition: all` value as "unspecified — fall back to none".
10. **Breadcrumb font** is `"Aeonik Pro-1089496262"` (a hashed local name). This is the SharePoint host's font, not part of the leaderboard component's typography; do **not** use it in the replica's `:root`. The breadcrumb area, if reproduced, should fall back to the app font stack.
11. **`box-sizing` is reported as `content-box`** on most nodes by the inspector, but Fluent UI controls (dropdowns, search, breadcrumb buttons) are `border-box`. Width/height numbers above are taken at face value from the inspector; when implementing in CSS, prefer `box-sizing: border-box` everywhere and re-derive padding-inclusive widths if needed.
12. **`object-fit: fill`** appears on every captured node — this is a browser default for non-replaced elements and has no effect; it can be ignored when implementing.
13. **Feedback button position** is reported with both `top/right/bottom/left` offsets resolved against the viewport at capture time. Only `right: 30px; bottom: 60px` are meaningful — reproduce just those.
14. **Search input width** is reported as 353.2 px because the input is `flex: 1 1 0px` inside a 390.8 px shell. The min-width on the wrapper (`min-width: 250px`) is the meaningful constraint, not the captured pixel width.
15. **Sample list rows are presumably ranks 4, 5, 6** but the snapshot does not embed an explicit rank number in any attribute (it's a `[DATA]` text node). The source comment says "3 of 227 sampled — pattern repeats", so the spec assumes ranks 4..N are visually identical.

## Resolved Ambiguities (added post-analysis)
- Page H1: "Company Leader Board 2025" (observed in original)
- Dropdown 1 label: "All Years"
- Dropdown 2 label: "All Quarters"  
- Dropdown 3 label: "All Categories"
- H2 title: "Leaderboard"
- Subtitle: "Top performers based on contributions and activity"
- Expanded row: reveals categoryStats inline — same markup, toggle show/hide
