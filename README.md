# Improved Initiative — Custom Dark CSS

A drop-in dark theme for the **Player View** of [Improved Initiative](https://www.improved-initiative.com/),
the browser-based D&D initiative tracker. Replaces the default player view
with a dense, high-contrast, TV/laptop-friendly grid layout.

## What it looks like

- Dark translucent panel, centered on the page, with a soft inner vignette.
- A 6-column grid: **Initiative · Portrait · Name · HP · Tags · Reaction**.
- Bright green HP, gold highlight on the active turn, red gradient tag badges.
- Striped body rows for easy at-a-glance reading.

## Install

1. Open Improved Initiative and go to **Settings → Player View → Custom CSS**.
2. Paste the contents of `Additional Player View.css` into the Custom CSS box.
3. Save and reload the Player View tab.

That's it — no build step, no dependencies.

## Customizing

All commonly-tweaked values live as CSS variables at the top of the file
(`#playerview { ... }`, section 1). Change these, not the rules below them:

| Variable | What it does |
| --- | --- |
| `--panel-width` | Panel width as % of viewport (default `95%`). |
| `--col-init`, `--col-portrait`, `--col-name`, `--col-hp`, `--col-tags`, `--col-reaction` | Grid column widths. |
| `--row-height`, `--header-height`, `--row-padding-x/y`, `--column-gap` | Row spacing. |
| `--panel-bg`, `--header-bg`, `--row-bg`, `--row-alt-bg`, `--row-border` | Background and divider colors. |
| `--text-main`, `--hp-green`, `--danger-red`, `--gold`, `--gold-light` | Text and accent colors. |
| `--tag-bg-top`, `--tag-bg-bottom`, `--tag-border` | Tag badge gradient and border. |
| `font-size: 22px` | Base size; everything else scales off this via `em`/`rem`. |

The hard `max-width: 1100px` cap on the panel lives in section 2
(`#playerview .c-player-view`). Raise or lower it there if you want a wider
or narrower table on large displays.

## CSS structure

The file is organized into 11 numbered sections, top to bottom:

1. **Design Tokens / Easy Settings** — all the tunable variables (above).
2. **Main Panel** — `.c-player-view` background, vignette, width cap.
3. **Shared Grid Structure** — the 6-column `display: grid` template applied
   to both the header row and every combatant row, so cells stay aligned.
4. **Header Row** — height, background, column labels, icon normalization.
   The header's "tags" cell spans columns 5–7 because the upstream HTML
   only emits one cell for both the tag icon and the fullscreen icon.
5. **Body Rows** — striping, padding, text shadow, bottom border.
6. **Body Column Placement** — explicit `grid-column` for each cell so the
   layout doesn't depend on source order; also handles name truncation
   (`white-space: nowrap; text-overflow: ellipsis`).
7. **Portraits** — image sizing and centering inside the portrait column.
8. **Tag Badges** — red-gradient pill style for individual `.tag` elements.
9. **Active Turn** — gold inset border + warm background on the
   `.combatant.active` row, plus gold initiative number.
10. **Icon Color Overrides** — keeps the heart / tag / expand / forward
    Font Awesome icons in the header white.
11. **Footer** — `.combat-footer` styling.

If you want to change behavior, find the section by name first — the comment
banners are easy to scan.

## Tested viewports

Verified on desktop browsers at:

- **1024 px** (laptop minimum) — fits without overflow.
- **1280–1440 px** — panel hits the 1100 px cap, centered.
- **1920 px** — same layout as 1440, more empty margin.

Below 1024 px (tablet / phone) is **not supported** — see caveats.

## Known caveats / things that don't work

- **Player View only.** This file targets `#playerview` and only restyles
  the player-facing tab. The DM-side encounter view is untouched.
- **No layout below ~1024 px.** The grid has hard column minimums that add
  up to ~990 px at the default font size, so on phones / narrow tablets the
  row will overflow horizontally. Adding responsive breakpoints would
  require new media queries and is out of scope for the current file.
- **Long names get clipped, not wrapped.** Body rows use
  `text-overflow: ellipsis` to keep rows single-line. The header name does
  not truncate — if you change the name column to be very narrow, the
  header label can collide with the HP column.
- **Tags overflow silently.** The tags cell has `max-height: 2rem` and
  `overflow: hidden`. A combatant with many tags will have any tags past
  the second wrapped row clipped without a "+more" indicator.
- **Heavy use of `!important`.** Improved Initiative ships its own styles
  with high specificity, so this file relies on `!important` to override
  them. If you add your own rules, you'll likely need `!important` too —
  or put your additions *below* this file in the Custom CSS box.
- **Brittle to upstream class renames.** Selectors target Improved
  Initiative's specific class names (`.combatant`, `.combatant--header`,
  `.combatant__initiative`, `.combatant__portrait`, `.combatant__name`,
  `.combatant__hp`, `.combatant__tags`, `.reaction-tracker`,
  `.combat-footer`). If a future Improved Initiative update renames any
  of those, the affected section will silently stop applying.
- **Font size is fixed at 22 px** — it doesn't scale with viewport. On a
  4K display you may want to bump it up; on a small laptop you may want it
  down. Edit the `font-size` declaration in section 1.
- **No light-mode toggle.** This is a dark-only theme; there's no companion
  light variant.

## License

No license file. Use, copy, modify freely; attribution appreciated but not
required.
