# FES-DMS — Asset & Icon Library

All assets and icons used in the India Observatory Forms (FES-DMS) form-builder prototype,
exported as individual files. Open **`index.html`** in a browser for a visual gallery of everything.

## Folder structure

```
assets/
├── index.html      Visual gallery of every asset (open in a browser)
├── icons/          71 UI icons (Lucide) as individual SVGs
├── svg/            10 app-specific inline SVGs (logo avatar, stat glyphs, illustrations)
└── images/         Raster logos (PNG)
```

## icons/ — UI icons (71)

Individual SVGs for every [Lucide](https://lucide.dev) icon referenced in the app
(e.g. `search.svg`, `pin.svg`, `trash-2.svg`, `chevron-down.svg`, category icons like
`droplets.svg`/`trees.svg`/`wheat.svg`, and status icons like `check-circle-2.svg`).

- Stroke icons, `24×24` viewBox, `stroke="currentColor"` — recolor via CSS `color`.
- Source: `lucide-static` (MIT licensed).

## svg/ — app SVGs (10)

Custom/inline SVGs extracted from the prototype:

| File | Used for |
|------|----------|
| `profile-avatar.svg` | User avatar in the top bar |
| `profile-sort.svg` | Up/down chevrons next to the profile |
| `stat-total-forms.svg` | Dashboard stat card — Total Forms |
| `stat-total-responses.svg` | Dashboard stat card — Total Responses |
| `stat-active-programs.svg` | Dashboard stat card — Active Programs |
| `stat-avg-response-time.svg` | Dashboard stat card — Avg Response Time |
| `filter-funnel.svg` | Funnel glyph in filter-panel titles |
| `illustration-empty-forms.svg` | Empty-state illustration (no forms) |
| `illustration-empty-search.svg` | Empty-state illustration (no search results) |
| `illustration-preview-box.svg` | Preview/placeholder box illustration |

## images/ — raster (2)

| File | Notes |
|------|-------|
| `fes-logo.png` | FES / India Observatory logo |
| `pseudocode-logo.png` | Pseudocode logo |

> The app's header wordmark uses the 🌿 emoji as its mark (not an image asset).

## Brand tokens (for reference)

| Token | Value |
|-------|-------|
| Brand blue | `#1F4397` |
| Brand green | `#39A248` |
| Status error | `#EF4444` |
| Status pending | `#F5A623` |
