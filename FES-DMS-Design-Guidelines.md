# FES DMS — Design System & Style Guidelines

> Reusable design language for the **FES DMS** product family (VI / Village‑Information Data Management System).
> Use this document whenever you add a **new product, module, or screen** so everything stays visually consistent.
>
> Source of truth: Figma — `FES-DMS` (`umwQkHdjwcrIkE1YQZMM05`). Values below are extracted directly from the file's variables and components.

---

## 1. Product at a glance

FES DMS is a **role‑based, data‑heavy admin platform** for managing field records ("VIs" — Village Information submissions), the organizations and users that create them, and the approval workflow around them.

**Roles** (each gets its own scoped module set):
- **Super Admin** — all orgs, all users, global approvals, downloads, help.
- **Org Admin** — own organization's workspace, users, approvals, downloads.
- **Field User** — workspace (table/map), creates submissions, onboarding, works **offline + sync queue**.

**Core modules** (the IA every role shares some subset of):
| Module | Purpose | Primary views |
|---|---|---|
| **Workspace** | Browse/manage VI records | Table view ⇄ Map view, fullscreen, filters, VI detail, edit VI |
| **Approvals / Submissions** | Review & action submissions | List + detail, Approve / Reject / Request Changes |
| **Orgs & Users** | Manage organizations and accounts | Card grid + add/edit modals |
| **Downloads** | Export jobs | List, search, status |
| **Help & Documentation** | Guides | Article pages |
| **Onboarding** (Field User) | First‑run setup | 4‑step flow |

**Design signature in one line:** a *floating glassmorphic top nav* over a soft blue‑gray canvas, white rounded cards, a blue + green brand pair, and a Table⇄Map duality on every data module.

---

## 2. Brand foundations

| Token | Value | Use |
|---|---|---|
| **Brand Blue** | `#1F4397` | Primary buttons, nav labels (inactive), links, logo "V", outlines, profile name, headings emphasis |
| **Brand Green** | `#39A248` | Active nav item, "create/add" emphasis, positive metrics (`+12%`), Approved/Active status, logo "I" |

**Logo:** wordmark `VI` — `V` in Brand Blue, `I` in Brand Green, Helvetica Bold 24px. Keep the two‑color split in any lockup.

**Two‑primary rule:** Blue is the *default* primary (confirm, submit, brand). Green is the *generative/positive* primary (Add VI, Add New, Active/Approved). Never use green for destructive or neutral actions.

---

## 3. Design tokens

### 3.1 Color — full swatch list

Every color in the system, grouped by role. **✓** = extracted directly from Figma components/variables; **≈** = visually matched (lock the exact value when first coded).

**Brand**
| Swatch | Hex | Src | Use |
|---|---|---|---|
| Brand Blue | `#1F4397` | ✓ | Primary buttons, nav (inactive), links, logo "V", outlines, profile name |
| Brand Green | `#39A248` | ✓ | Active nav, create/add buttons, positive delta, Approved/Active, logo "I" |

**Text & on‑surface**
| Swatch | Hex | Src | Use |
|---|---|---|---|
| Heading | `#101828` | ✓ `text-heading` | Page & section titles |
| Strong / on‑light | `#292929` | ✓ | Modal titles, chip text, field labels, input values, helper text |
| Placeholder / disabled | `rgba(41,41,41,.37)` | ✓ | Input placeholder text **and** default input border |
| Body muted | `#667085` | ≈ | Secondary labels, table meta |

**Dashboard metric palette** (stat cards only — Horizon‑style)
| Swatch | Hex | Src | Use |
|---|---|---|---|
| Metric value | `#2B3674` | ✓ | Stat big numbers |
| Metric label | `rgba(43,54,116,.72)` | ✓ | Stat card label |
| Metric muted | `#A3AED0` | ✓ | Stat sub‑caption |

**Surfaces, lines & glass**
| Swatch | Value | Src | Use |
|---|---|---|---|
| Surface | `#FFFFFF` | ✓ | Cards, tables, modals |
| Input surface | `#F9FAFB` | ✓ | Input / select / search field background |
| Canvas | `#EEF2F9` | ≈ | Page background (soft blue‑gray gradient) |
| Divider | `#C4C4C4` | ✓ | Hairline separators |
| Input border | `rgba(41,41,41,.37)` | ✓ | Input / select / search border |
| Border subtle | `#E2E8F0` | ≈ | Card / table borders |
| Glass bg | `linear-gradient(90deg, rgba(255,255,255,.82), rgba(255,255,255,.80))` | ✓ | Header |
| Glass border | `#FFFFFF` (1.5px) | ✓ | Header edge |

**Semantic / status** — always a **colored dot or icon + label** (never color alone):
| Role | Hex | Src | Applies to |
|---|---|---|---|
| Success / Approved / Active | `#39A248` | ✓ | Approved submissions, Active org/user |
| Pending / In‑review | `#F5A623` | ≈ | Pending submission, Inactive org (amber) |
| Error / Rejected | `#EF4444` | ≈ | Rejected submission |
| Info / Request Changes | `#4318FF` | ≈ | "Request Changes" state |

> Pending/Rejected/Request‑Changes are inferred from screenshot dots/icons (raster in Figma). Lock exact hexes when the badge component is coded, then mark them ✓ here.

### 3.2 Typography

**Three font families — each has a fixed job. Do not mix roles.**

| Family | Role | Where |
|---|---|---|
| **Helvetica** | Bold UI chrome | Nav, **buttons**, headings, modal titles, field labels, input text, chips, logo, profile |
| **Inter** | Base / body / data | Table cells & long‑form body (`typography/font-family/font-base`) |
| **DM Sans** | Dashboard metrics only | Stat card value (Bold), label (Medium), delta (Regular) |

> If Helvetica isn't licensed for the web build, substitute a close neutral grotesque (Arial, Inter Tight, or Helvetica Neue) and record the swap in §8 notes. Keep weights identical.

**Font size scale** (token → px / line‑height):
| Token | Size | Line‑height | Use |
|---|---|---|---|
| `text-2xl` | **24** | 24–28 | Page titles, stat values |
| (modal) | **20** | 28 | Modal / dialog titles |
| `text-lg` | **18** | 24 | Section & card titles |
| `text-sm` | **14** | 20 | **Default UI size** — body, buttons, nav, modal subtitle, input text, chips, table cells |
| (caption) | **12** | 12–16 | Field labels, helper text, stat delta, captions |
| (micro) | **10** | 15 | Profile role line |

Weights: `Light (300)` · `Regular (400)` · `Medium (500)` · `Semi Bold (600, logo)` · `Bold (700)`.

**Element‑by‑element type map** (exact, from Figma):
| Element | Family | Weight | Size / LH | Color | Case |
|---|---|---|---|---|---|
| Logo `VI` | Helvetica | Bold | 24 / 24 | Blue + Green | — |
| Nav item | Helvetica | Bold | 14 / 21 (1.5) | Blue · **Green when active** | UPPERCASE |
| Profile name | Helvetica | Bold | 14 / 18 | `#1F4397` | — |
| Profile role | Helvetica | Light | 10 / 15 | `#1F4397` | — |
| Page title | Helvetica | Bold | 24 / 24 | `#101828` | Title Case |
| Section / card title | Helvetica | Bold | 18 / 24 | `#101828` | Title Case |
| Modal title | Helvetica | Bold | 20 / 28 | `#292929` | Title Case |
| Modal subtitle | Helvetica | Regular | 14 / 22 | `#292929` | Sentence |
| Button label | Helvetica | Bold | 14 / 20 | White (filled) / Blue (outline) | — |
| Filter / status chip | Helvetica | Bold | 14 / 20 | `#292929` | — |
| **Field label** | Helvetica | Regular | 12 / 12 | `#292929` | — |
| **Input text / value** | Helvetica | Regular | 14 / 20 | `#292929` | — |
| **Input placeholder** | Helvetica | Regular | 14 / 20 | `rgba(41,41,41,.37)` | — |
| **Field helper text** | Helvetica | Regular | 12 / 12 | `#292929` | Sentence |
| Table cell / body | Inter | Regular | 14 / 20 | `#101828` / muted | — |
| Stat label | DM Sans | Medium | 14 / 18 | `rgba(43,54,116,.72)` | — |
| Stat value | DM Sans | Bold | 24 / 28 | `#2B3674` | — |
| Stat delta | DM Sans | Regular | 12 / 16 | Green (+) / `#A3AED0` | — |

### 3.3 Spacing — 4px base scale

| Token | px | Token | px |
|---|---|---|---|
| `spacing/0` | 0 | `spacing/4` | 16 |
| `spacing/1.5` | 6 | `spacing/9` | 36 |
| `spacing/2` | 8 | (header py) | 18 |
| `spacing/3` | 12 | (header px / gutter) | 32 |

Most‑used rhythm: **6 / 8 / 12 / 16**. Nav item gap = 30. Page gutter = 32.

### 3.4 Radius

| Token | px | Use |
|---|---|---|
| `rounded-0` | 0 | square dividers |
| chip | 8 | status filter chips, small badges |
| **`rounded-base`** | **12** | **buttons, inputs, dropdowns** |
| container | 16 | header, modals |
| card | 20 | stat cards, large surface cards |
| pill | full | segmented toggles, some action pills |

### 3.5 Borders & elevation

```
--border:        1px      /* default */
--border-glass:  1.5px    /* header */

shadow-xs:       0 1px .5px rgba(29,41,61,.02)        /* buttons, resting */
shadow-card:     0 6px 24px rgba(0,0,0,.06)           /* header & cards */
shadow-float:    0 3px 9px rgba(31,67,151,.16)        /* overlays, slide-overs, map cards (token "Floating Shadow") */
```

### 3.6 Field & control sizes (dimensions)

Exact heights, padding and radius for every interactive control — extracted from the Figma components. **Use these heights verbatim** so forms and toolbars line up across modules.

| Control | Height | Padding (v · h) | Radius | Other |
|---|---|---|---|---|
| **Button** (primary / secondary / green) | **44px** | 12 · 12 | 12 | gap 6; min‑width by label, can be full‑width (e.g. 646) |
| **Icon‑only button** | **40 × 40** | — | 12 | square; glyph 16–24px |
| **Header icon** (search/bell/help) | 24 × 24 glyph | — | — | hit‑area ≥ 40 |
| **Text input** | **36px** | 8 · 12 | 12 | `bg #F9FAFB`, `1px rgba(41,41,41,.37)`, `shadow-xs`, gap 6 |
| **Select / dropdown** (closed) | **36px** | 8 · 12 | 12 | same as input + trailing 16px chevron |
| **Search bar** | **36px** | 8 · 12 | 12 | leading 16px magnifier; default width 240 |
| **Filter / status chip** | ~32px | 6 · 12 | 8 | `1px #1F4397` border, gap 5, text `#292929` |
| **Status pill / badge** | ~28–32px | 6 · 12 | 8 | dot/icon + label |
| **Table row** | **54px** | cell v‑pad ~16 | — | hairline `--divider` separators |
| **Stat card** | auto | 16 | 20 | 56px circular icon; row of 4 |
| **Modal / dialog** | auto | ~24 | 16 | `shadow-float` |
| **App header** | ~60px | 18 · 32 | 16 | glass; sticky |

**Field‑group rhythm (forms):**
- Label → input gap: **6px**
- Between fields: **20px**
- Optional helper text sits 6px under the input.
- Field group order: `Label (12)` → `Input/Select (36px box)` → `Helper (12, optional)`.

**Input states to design** (all keep 36px height & 12 radius):
| State | Border | Background | Text |
|---|---|---|---|
| Default / empty | `1px rgba(41,41,41,.37)` | `#F9FAFB` | placeholder `rgba(41,41,41,.37)` |
| Filled | `1px rgba(41,41,41,.37)` | `#F9FAFB` | `#292929` |
| Focus | `1px #1F4397` (recommended) | `#FFFFFF` | `#292929` |
| Error | `1px #EF4444` | `#FFFFFF` | `#292929` + 12px error helper in red |
| Disabled | `1px` @ 37% | `#F9FAFB` @ 60% | muted |

> Focus / error / disabled visuals aren't all in the Figma source yet — the above keeps the same box metrics and is the recommended default. Confirm against the design before shipping.

---

## 4. Layout & page templates

**App shell is a *floating top nav*, not a sidebar.**

```
┌─────────────────────────────────────────────────────────┐
│  ▓ Floating glass header (rounded-16, 32px gutter)       │  ← sticky
├─────────────────────────────────────────────────────────┤
│  Page Title            [ Map | Table ]  [⛶ Fullscreen]   │
│                                                          │
│  [Stat][Stat][Stat][Stat]        ← optional metric row   │
│                                                          │
│  Toolbar:  [view toggle] [+ Primary]  [Filters][Export]  │
│                                                          │
│  ┌── Content ───────────────────────────────────────┐   │
│  │  Table  ⇄  Map  ⇄  Card grid                      │   │
│  └──────────────────────────────────────────────────┘   │
│  Showing 1–20 of 300                  ‹ 1 2 3 … 10 ›      │
└─────────────────────────────────────────────────────────┘
```

- **Canvas:** 1440px desktop reference; content band ≈ 1376px with **32px** left/right gutters.
- **Background:** soft blue‑gray (`--canvas`), subtle vertical gradient.
- **Every data module supports Table ⇄ Map**, plus a **Fullscreen** mode of each.
- **Detail pattern:** keep the map/list and open a **right slide‑over panel** (`shadow-float`) instead of navigating away.

---

## 5. Component specifications

> Exact specs pulled from the Figma components. Reuse these — don't invent new variants.

### 5.1 App Header (glass nav)
- Container: `bg: --glass-bg`, `border: 1.5px #FFFFFF`, `backdrop-blur: 10.5px`, `radius: 16`, `shadow: 0 6px 24px rgba(0,0,0,.06)`, padding `18px 32px`, space‑between.
- Left: `VI` logo. Center: nav items (icon + label, Helvetica **Bold 14**, **UPPERCASE**, `gap 6` icon↔label, `gap 30` between items). **Active = Brand Green**, inactive = Brand Blue.
- Right (`gap 16`): Search, Notifications (bell), Help (?) — each 24px icon — then **Profile** (avatar + name `Bold 14` + role `Light 10` + sort chevron).

### 5.2 Buttons
All buttons are **44px tall**, `radius 12`, padding `12 · 12`, `gap 6`, label Helvetica **Bold 14/20**, `shadow-xs`.

| Variant | Spec |
|---|---|
| **Primary (blue)** | `bg #1F4397`, white text |
| **Secondary / outline** | `bg white`, `1px #1F4397` border, text `#1F4397` |
| **Create (green)** | `bg #39A248`, white text — for Add VI / Add New / generative actions |
| **Icon + label** | leading icon (16–20px) + label, `gap 6` |
| **Icon‑only** | **40 × 40**, `radius 12`; header glyphs 24px, row actions (edit ✎ / delete 🗑) |

Width is content‑driven (min‑width by label) and can stretch full‑width (e.g. modal footer). Optional pill (`radius full`) form is used for segmented toggles and some top‑right actions; the **default button radius is 12**.

### 5.3 Stat / metric card
- `bg white`, `radius 20`, padding 16, soft‑shadow circular icon (56px) on the left.
- Label: **DM Sans Medium 14**, `--metric-label`.
- Value: **DM Sans Bold 24/28**, `--metric-value (#2B3674)`.
- Delta: **DM Sans 12**, e.g. `+12%` in **green** + ` from last month` in `--metric-muted`.
- Used in a **row of 4** at the top of overview pages.

### 5.4 Segmented toggle (view switch)
- Two+ pills (e.g. `Map View | Table View`, `Organizations | Users`). Active pill = filled **green**, inactive = ghost. Pill radius, Helvetica Bold 14.

### 5.5 Filter / status chip
- `bg white`, `1px #1F4397` border, `radius 8`, padding `6px 12px`, `gap 5`, Helvetica Bold 14, text `#292929`. Used for `All / Pending / Request Change / Rejected` filter rows (selected state filled).

### 5.6 Status badge
- Colored **dot or icon + label**. Map role → color via §3.1 semantic tokens. Keep label text; never rely on color alone (accessibility).

### 5.7 Data table
- Columns lead with a **checkbox** select column; headers sortable; right‑most **Actions** column (icon buttons).
- Row height comfortable, hairline `--divider` row separators, white surface, `radius 16` outer container.
- Footer: left `Showing 1–20 of 300`, right numbered **pagination** with ‹ › arrows.
- Inline tag/badge cells (e.g. source `FES`) use the chip style.

### 5.8 Inputs & selects
- **Field group:** label → input gap **6px**; fields stacked with **20px** gap; optional helper 6px below.
- **Label:** Helvetica Regular **12/12**, `#292929`, **required** marked with `*`.
- **Input box (36px tall):** `bg #F9FAFB`, `1px solid rgba(41,41,41,.37)`, `radius 12`, padding `8 · 12`, `gap 6`, `shadow-xs`.
  - Text: Helvetica Regular **14/20**, value `#292929`, **placeholder `rgba(41,41,41,.37)`**.
- **Select / dropdown:** same box + trailing **16px chevron‑down**; "Select …" placeholder.
- **Search:** same box + leading 16px magnifier; default width 240.
- **Helper text:** Helvetica Regular 12/12, `#292929` (red on error).
- States: see the input‑states table in §3.6.

### 5.9 Modal / dialog
- Centered white card, `radius 16`, `shadow-float`, dim backdrop.
- Header: **title** (Bold, `--text-heading`) + subtitle (muted) + **✕ close** top‑right.
- Body: stacked form fields (2‑up grid where logical, e.g. State / District).
- Footer (right‑aligned): **Cancel** (outline) + **Primary** (filled). Buttons per §5.2.

### 5.10 Entity card (card grid)
- Used in Orgs & Users. Contains: ID (`ORG-001`), **status pill** (top‑right) + edit/delete icons, **name** (Bold), meta rows with leading icons (📍 location, ✉ email, ☎ phone), and **sub‑stat tiles** (e.g. `12 Users`). 3‑column responsive grid.

### 5.11 Slide‑over detail panel
- Right‑docked panel over map/list, `shadow-float`. Header with title + status; body in labelled sections (Submission Info, VI Details, VI Location w/ mini‑map, Supporting Documents); primary action (e.g. **Edit VI**) pinned.

### 5.12 Map view
- Full‑bleed map, pin markers, floating overlay cards (`shadow-float`), and "Add VI on Map" placement flow for Field Users. Always paired with a Table toggle.

### Component inventory checklist
Header · Stat card · Button (primary/secondary/green/icon) · Segmented toggle · Filter chip · Status badge · Data table + pagination · Search · Input · Select · Modal · Entity card · Slide‑over panel · Map overlay · Tabs · Onboarding step · Offline/Sync‑queue state · Empty state.

---

## 6. Interaction & content patterns

- **Table ⇄ Map duality:** any list of geo‑records ships both views + a fullscreen mode.
- **Filter row** of status chips above tables/lists; selected chip filled.
- **Detail without navigation:** prefer slide‑over panels and modals over full page changes.
- **Approval workflow** states: `Pending → Approved / Rejected / Request Changes`. Provide Reject and Request‑Changes confirmation modals.
- **Field User resilience:** design **Offline** and **Sync Queue** states for every create/edit flow; show priority‑area and onboarding affordances.
- **Metrics framing:** overview pages open with a 4‑stat row + month‑over‑month delta in green/red.
- **Microcopy:** nav UPPERCASE; titles Title Case; supportive subtitles under modal/section titles.

---

## 7. Adding a NEW product / module — checklist

Follow this to keep a new addition on‑style:

1. **Shell** — Reuse the floating glass header; add the module as an UPPERCASE nav item with an icon. Active state = green. Respect role scoping (Super Admin / Org Admin / Field User).
2. **Page template** — Title row → (optional) 4 stat cards → toolbar (view toggle + green primary action + Filters + Export) → content → pagination. 32px gutters, `--canvas` background.
3. **Tokens only** — Pull every color/size from §3. No new hexes, radii, or font families. Blue = confirm, Green = create/positive, status colors for status only.
4. **Type** — Inter for content, Helvetica Bold for chrome/buttons/labels, DM Sans *only* for stat cards. Default size 14.
5. **Components** — Compose from §5 inventory. If a new component is unavoidable, match radius (12 controls / 16 containers / 20 cards), `shadow-xs`/`shadow-card`/`shadow-float`, and 6/8/12/16 spacing.
6. **Data views** — If it lists geo/records: provide Table + Map + Fullscreen, a status filter‑chip row, row checkboxes, and a slide‑over detail.
7. **Forms** — Labelled fields with `*`, 12‑radius inputs, modal with Cancel(outline) + Primary(filled) footer.
8. **States** — Design empty, loading, error, **offline**, and **sync‑queue** states (Field‑User contexts especially).
9. **Status semantics** — Reuse the badge component + semantic colors; always pair color with a label.
10. **A11y** — 14px min body, never color‑only signals, visible focus, AA contrast on text (note: white‑on‑green `#39A248` is borderline — prefer it for fills with bold text, not small captions).

---

## 8. Copy‑paste token reference

```css
:root {
  /* Brand */
  --brand-blue:#1F4397; --brand-green:#39A248;

  /* Metric (stat cards) */
  --metric-value:#2B3674; --metric-label:rgba(43,54,116,.72); --metric-muted:#A3AED0;

  /* Text */
  --text-heading:#101828; --text-strong:#292929;
  --text-muted:#667085; --text-placeholder:rgba(41,41,41,.37);

  /* Surface */
  --surface:#FFFFFF; --input-surface:#F9FAFB; --canvas:#EEF2F9;
  --divider:#C4C4C4; --border-subtle:#E2E8F0; --input-border:rgba(41,41,41,.37);

  /* Status */
  --status-success:#39A248; --status-pending:#F5A623;
  --status-error:#EF4444;  --status-info:#4318FF;

  /* Type — families */
  --font-bold:'Helvetica',Arial,sans-serif;    /* nav, buttons, labels, inputs */
  --font-base:'Inter',sans-serif;              /* body, table data */
  --font-metric:'DM Sans',sans-serif;          /* stat cards */
  /* Type — sizes */
  --fs-2xl:24px; --fs-xl:20px; --fs-lg:18px; --fs-sm:14px; --fs-xs:12px; --fs-2xs:10px;
  /* Type — line heights */
  --lh-2xl:28px; --lh-lg:24px; --lh-sm:20px; --lh-xs:12px;
  /* Type — weights */
  --fw-light:300; --fw-regular:400; --fw-medium:500; --fw-semibold:600; --fw-bold:700;

  /* Spacing (4px base) */
  --sp-1:6px; --sp-2:8px; --sp-3:12px; --sp-4:16px;
  --sp-field-gap:20px; --sp-gutter:32px; --nav-gap:30px;

  /* Control sizes */
  --h-button:44px; --h-input:36px; --h-search:36px; --h-icon-btn:40px;
  --h-row:54px; --h-header:60px; --chip-pad:6px 12px; --input-pad:8px 12px; --button-pad:12px;

  /* Radius */
  --r-chip:8px; --r-control:12px; --r-container:16px; --r-card:20px; --r-pill:9999px;

  /* Elevation */
  --border:1px solid var(--border-subtle);
  --shadow-xs:0 1px .5px rgba(29,41,61,.02);
  --shadow-card:0 6px 24px rgba(0,0,0,.06);
  --shadow-float:0 3px 9px rgba(31,67,151,.16);
  --glass-bg:linear-gradient(90deg,rgba(255,255,255,.82),rgba(255,255,255,.80));
  --glass-blur:10.5px;
}
```

---

### Notes / to confirm against Figma when implementing
- Exact **status** hexes (pending/rejected/request‑changes) — icons are raster in Figma; lock when the badge component is coded.
- `--text-muted`, `--canvas`, `--border-subtle` are visually matched approximations; replace with the exact variable values if/when they're published as Figma variables.
- Header nav and buttons render in **Helvetica** in the file; if Helvetica isn't licensed for the web build, substitute a close grotesque (e.g. Arial / Inter Tight) and record the swap here.

_Last updated from Figma `FES-DMS` — keep this file versioned alongside the design library._
