# Vibe Coding Challenge: Company Leaderboard Replica

## Approach and Methodology

To complete this task while strictly adhering to the requirement of **not feeding any corporate data to AI tools**, I adopted a "Sanitized Extraction & AI Assembly" approach.

Because the original application was built using React and Microsoft Fluent UI (which dynamically generates complex DOM structures and hashed CSS modules), simply taking a screenshot or copying the source code would either leak Personally Identifiable Information (PII) or result in broken, unstyled code.

---

### 1. Data Sanitization (Local Execution)

Before utilizing any AI tools, I wrote and executed a custom JavaScript DOM-scrubber directly in my local browser console. This script cloned the leaderboard's HTML structure while systematically replacing all text nodes, employee names, roles, and scores with a generic `[DATA]` placeholder. It also stripped out image sources, `href` links, and personal data attributes (`data-user-*`, `data-id`, `data-name`, `data-email`). This ensured the structural integrity of the HTML was preserved with zero data leakage.

Key sanitization operations performed locally before any AI interaction:
- All text nodes → `[DATA]`
- All `<img src>` attributes → blank 1×1 pixel GIF (data URI)
- All `href` attributes → `#`
- All `srcset` attributes → removed
- All personal `data-*` attributes → `[DATA]`
- All inline `style` attributes → removed (styles extracted separately)

The result was a clean `leaderboard-structure.html` file (~20KB) containing only the HTML skeleton with hashed Fluent UI class names and zero corporate data.

---

### 2. CSSOM Extraction

Because the styles were injected dynamically by Webpack chunks (the leaderboard component CSS is bundled inside a 1.19MB JavaScript file, not a standalone stylesheet), standard "Save Page As" would not yield usable CSS. I wrote a second local console script to traverse the browser's CSS Object Model (CSSOM). It extracted only the specific CSS rules associated with:

- The leaderboard's unique Webpack hash (`_2943a085`)
- Microsoft Fluent UI classes (`ms-Dropdown`, `ms-SearchBox`, `ms-TooltipHost`)

This produced a clean `leaderboard-styles.css` file (~7KB) containing verbatim production CSS rules with no data content.

A third script extracted computed styles for specific interactive elements (filter dropdowns, search box, breadcrumb, page title), saving them to `filter-element-styles.txt` and `top-element-styles.txt` for precision styling of elements outside the leaderboard component's own CSS module.

---

### 3. Structural Analysis (AI Phase — GitHub Copilot / Cursor + Claude Opus)

With sanitized, data-free files in hand, I used **Cursor with Claude Opus 4.7** (in Plan Mode) to perform a structured UI analysis. The AI was instructed to:

- Read `leaderboard-structure.html` as a structural source only
- Read `leaderboard-styles.css` and `custom-styles.css` as style sources
- Produce a developer-ready `ui-spec.md` specification document

The AI correctly identified all 9 component sections, documented exact CSS values, flagged 15 specific ambiguities (missing dimensions, missing expanded-panel HTML, unknown filter labels), and produced a 48KB specification covering:
- Complete CSS variable design token system
- Exact component hierarchy with class names
- Fluent UI icon name inventory (`FavoriteStarFill`, `ChevronDown`, `Presentation`, `Education`, `Search`)
- Data model schema for leaderboard entries
- Interactive behaviour specifications

No screenshots were used at any stage. The AI worked exclusively from sanitized structural and CSS data.

---

### 4. Fictional Data Generation (AI Phase — Cursor + Claude Sonnet)

To replace all original employee data, I used **Cursor with Claude Sonnet 4.6** to generate a completely fictional dataset following the schema identified in the UI spec. Generation rules enforced:

- 25 entries with human-sounding fictional names (diverse, internationally varied)
- Scores following a natural distribution (not uniform or round numbers)
- At least 6 fictional departments (e.g. "Data Engineering", "ML Research", "Security Operations")
- Activity arrays with fictional but realistic-sounding event names prefixed with `[EDU]`, `[LAB]`, `[REG]`, `[UNI]` — matching the original's category abbreviation system
- Score formula: `(lab × 4) + (reg × 6) + (uni × 8) + (edu × 3)` derived from the original's scoring logic observed in the DOM structure

No real names, scores, departments, or activity descriptions from the original were used.

---

### 5. Implementation (AI Phase — Cursor + Claude Sonnet, iterative)

The build was assembled in **Cursor Agent mode with Claude Sonnet 4.6** using a phased prompting strategy. Each phase was a separate agent session to avoid context window overflow and maintain clean, focused outputs:

**Phase structure:**
1. UI analysis → `new-spec.md`
2. Data generation → `data.js`
3. Initial build → `index.html` (HTML structure + CSS from spec + JS render engine)
4. Interaction wiring → filters, search, expand/collapse, podium visibility
5. Precision styling → iterative CSS correction using DevTools-extracted values

**Key prompting techniques used:**
- **Phased context isolation**: each agent session read only the files relevant to its phase, preventing context contamination between phases
- **CLAUDE.md**: a project-level instruction file read at the start of every agent session, containing component class name mappings, data rules, and override instructions for conflicting global Cursor rules
- **Surgical fix prompts**: rather than rewriting, each visual correction targeted specific CSS properties with exact extracted values, avoiding AI interpretation
- **DevTools loop**: for each visual discrepancy, computed styles were extracted locally and fed as exact values — eliminating AI guesswork on colours, spacing, and typography

---

### 6. Precision CSS Correction (Manual + AI-assisted)

Several elements required precision correction beyond what AI could infer from the spec alone:

**Fluent UI Dropdowns**: The original uses Microsoft Fluent UI React components with runtime-injected CSS. The dropdown title (`ms-Dropdown-title`) uses `background: rgb(235, 235, 237)` and `border: 1px solid rgb(55, 55, 55)` — a distinctly different style from standard web conventions. These were extracted from DevTools computed styles and applied verbatim.

**Typography**: The page title and breadcrumb use **Aeonik Pro**, a proprietary corporate font served from SharePoint's CDN with a runtime-hashed family name (`"Aeonik Pro-1089496262"`). The font was identified via `document.fonts` enumeration, downloaded from the internal CDN, and embedded as a base64-encoded `@font-face` declaration in `index.html` to ensure consistent rendering without external dependencies.

**Podium layout**: The rank-1 column elevation (`margin-top: -32px`) and the staircase height differential (160px / 128px / 96px) were derived from the extracted CSS. The `overflow: visible` override on the podium block was required because the large faded rank numbers (96px–112px font-size) overflow the block boundary in the original's visual design.

**Page chrome**: The SharePoint page background (`rgb(235, 235, 237)`), breadcrumb layout (flex row, 40px height, Aeonik Pro font), and white card wrapper (4px border-radius, 1px solid `rgb(226, 232, 240)`, subtle shadow) were all matched from DevTools computed style extractions rather than visual estimation.

---

### 7. Known Limitations

| Element | Status | Note |
|---|---|---|
| Employee avatars | Replaced with Pravatar.cc fictional photos | Original used real employee photos — replaced with fictional person images seeded by name |
| Comments section | Excluded | Native SharePoint social component; not part of the custom leaderboard web part |
| Aeonik Pro font | Embedded from internal CDN | Corporate font not publicly available; embedded from company SharePoint |
| Filter dropdown options | Fictional | Original filter options unknown (DOM captured closed state); options derived from fictional data |
| Activity history | Fictional | Each entry has realistic fictional activity entries matching original category structure |

---

### Tools Used

| Tool | Purpose |
|---|---|
| Chrome DevTools Console | DOM scrubbing, CSSOM extraction, computed style extraction |
| Custom JavaScript scripts | Sanitization, structure capture, style capture |
| Cursor (Agent mode) | Multi-phase AI-assisted development |
| Claude Opus 4.7 | UI analysis and specification (Phase 1, Phase 5 QA) |
| Claude Sonnet 4.6 | Data generation, implementation, iterative fixes |
| GitHub Actions | Automated deployment to GitHub Pages |
| Pravatar.cc | Fictional avatar photo generation |

---


### Responsible AI Usage Summary

> *"Screenshots were excluded entirely from the AI pipeline due to visible personally identifiable information. Instead, custom DevTools scripts were used to extract DOM structure and CSS with all personal data systematically replaced before any AI tool processed the output. The AI received only structural, stylistic, and schema information — never names, scores, photos, or any other employee data."*