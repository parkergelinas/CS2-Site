# Float — Design System

The source of truth for layout and visual design. Every component references these
tokens. No one-off values. If a value isn't here, add it here first, then use it.

## Principles

1. **One screen answers one question.** Hierarchy over density. The primary action or
   number is the largest, loudest thing; everything else recedes.
2. **Every number aligns.** Numeric data uses tabular figures, right-aligned, with a
   consistent decimal count per column. A column of prices must read as a clean vertical edge.
3. **Color means something.** Green = gain, red = loss, accent = interactive. Rarity colors
   are reserved for skin rarity. Never decorative.
4. **Space is a multiple of 4.** No arbitrary margins. Layout snaps to the 4px grid.
5. **Flat, not glossy.** Surfaces are separated by 0.5px borders and subtle elevation steps,
   not drop shadows or gradients.
6. **Dark-first.** The product is a trading terminal; dark reduces eye strain and makes data
   pop. A light theme is a later port, not the baseline.

## Type scale — base 14px, ratio 1.25

| Token        | Size | Weight | Use                                  |
|--------------|------|--------|--------------------------------------|
| `text-3xl`   | 32   | 600    | Hero numbers (portfolio value)       |
| `text-2xl`   | 24   | 600    | Page titles                          |
| `text-xl`    | 20   | 500    | Section headings                     |
| `text-lg`    | 16   | 500    | Card titles                          |
| `text-base`  | 14   | 400    | Body, table cells (default)          |
| `text-sm`    | 13   | 400    | Secondary / dense table cells        |
| `text-xs`    | 12   | 500    | Labels, column heads (uppercase, +4% letter-spacing) |
| `text-2xs`   | 11   | 500    | Micro labels, hex/meta               |

Line height: `1.2` for data/headings, `1.5` for prose. Weights: **400 / 500 / 600 only.**

## Fonts

- **UI sans:** Inter. Designed for screens, ships tabular figures.
- **Numeric / mono:** JetBrains Mono (or Inter with `font-variant-numeric: tabular-nums`).
  All prices, floats, deltas, IDs, and timestamps render with tabular figures.
- Rule: any cell containing a number gets `font-variant-numeric: tabular-nums` and
  `text-align: right`.

## Spacing — 4px base unit

`4 · 8 · 12 · 16 · 24 · 32 · 48 · 64`

- Component-internal gaps: 8 / 12 / 16
- Card padding: 16 (compact) / 20 (default)
- Section rhythm: 24 / 32
- Page gutters: 24

## Color tokens — dark-first

### Surfaces
| Token            | Hex       | Use                          |
|------------------|-----------|------------------------------|
| `bg-base`        | `#0B0E14` | Deepest background           |
| `bg-surface`     | `#131722` | Cards, panels                |
| `bg-elevated`    | `#1C2230` | Hover rows, popovers, inputs |
| `border`         | `#2A3142` | Default 0.5px border         |
| `border-strong`  | `#3A4357` | Emphasis / focus outline     |

### Text
| Token            | Hex       | Use                          |
|------------------|-----------|------------------------------|
| `text-primary`   | `#E6E9EF` | Primary text, numbers        |
| `text-secondary` | `#8B93A7` | Labels, secondary data       |
| `text-tertiary`  | `#5C6373` | Hints, column heads, meta    |

### Semantic
| Token        | Hex       | Use                              |
|--------------|-----------|----------------------------------|
| `gain`       | `#16C784` | Positive delta, profit           |
| `loss`       | `#EA3943` | Negative delta, loss             |
| `accent`     | `#2E90FA` | Links, primary buttons, selection|
| `warning`    | `#F0A722` | Alerts, stale data               |

Deltas always carry an explicit sign (`+`/`−`) **and** color. Never color alone.

### CS2 rarity (canonical in-game colors — do not alter)
| Rarity        | Hex       |
|---------------|-----------|
| Consumer      | `#B0C3D9` |
| Industrial    | `#5E98D9` |
| Mil-Spec      | `#4B69FF` |
| Restricted    | `#8847FF` |
| Classified    | `#D32CE6` |
| Covert        | `#EB4B4B` |
| Rare special ★| `#E4AE39` |

Used as a 2px left border on item rows and a dot on item chips. The faded background
chip uses the same hue at ~14% alpha with a lightened text variant.

## Radius & borders

- `radius-sm` 4px · `radius-md` 6px (default) · `radius-lg` 8px (cards) · `radius-xl` 12px
- Borders are `0.5px solid border`. Single-sided accent borders (rarity) get `radius: 0`.

## Density & rows

- Table row height: 40px (default) / 32px (compact toggle)
- Hit targets (buttons, controls): min 32px height
- Tables: sticky header, zebra-free (borders separate rows), hover = `bg-elevated`

## Numeric formatting rules

- **Currency:** thousands separators, fixed 2 decimals (`8,240.00`).
- **Float (wear):** 4 decimals in tables, full precision (up to 16) in detail view.
- **Percent delta:** 2 decimals, signed (`+4.10`, `−1.12`).
- **Large counts:** thousands separators (`8,910`); abbreviate only above 1M (`1.2M`).

## Layout grid

- 12-column, 24px gutter, max content width 1440px, fluid below.
- Dashboard: KPI row (4 cards) → focus + watchlist (1.6fr / 1fr) → opportunities table.
- Progressive disclosure: summary on screen, detail one click away. Never show every market
  price at once — show the best, expand on demand.
