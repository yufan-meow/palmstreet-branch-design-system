# Palmstreet Branch Design System — AI Context

> This file is the single source of truth for AI tools working with the Palmstreet design system.
> Read this before generating any UI code, components, or designs.
> Token files: `tokens/global.json` (base values) · `tokens/semantic.json` (semantic layer)

---

## Stack

- **Framework:** Vue.js (scoped styles with `data-v-` attributes)
- **Styling:** CSS custom properties (semantic tokens)
- **Typeface:** Gabarito only — never use system fonts or any other typeface
- **Themes:** Light and dark mode via CSS variable swapping
- **Platforms:** Web (desktop) and Mobile (375px base width)

---

## Icons

- **Library:** Google Material Design Icons
- **Style:** Filled (not outlined)
- **Corner style:** Rounded
- Always use the filled + rounded variant. Never use outlined, sharp, or two-tone variants.
- Icon color is always set via a Content token — never hardcoded.

---

## Brand Character

Palmstreet is a live selling marketplace that bridges the digital screen with the real world — plants, handmade goods, farmers market-style products. The design reflects this.

- **Neutral and modern** — the UI steps back so the content (sellers, listings, live streams) can be the star
- **Not a typical tech aesthetic** — avoid SaaS patterns, corporate design conventions, or generic e-commerce templates
- **Trend-aware but restrained** — follows design trends without being extravagant or overly disciplined
- **The neon green (#B9EC51) is the brand's energy** — used deliberately for primary CTAs only, not decoratively
- **3D illustration** is a key visual language (see section below)

---

## 3D Illustration Style

Palmstreet uses custom 3D illustrations throughout the product. All 3D assets follow a consistent visual language.

**Style characteristics:**
- **Warm, soft lighting** — gentle shadows, no harsh or dramatic light sources
- **Saturated but natural colors** — rich yellows, oranges, reds, greens, blues. Not neon, not pastel
- **Rounded, friendly forms** — soft edges throughout, nothing sharp or angular
- **Casual 3/4 perspective** — objects sit at a slight tilt, not flat or strictly isometric
- **No background** — transparent, drops cleanly onto any surface color
- **Subtle gloss** — slight specular highlight on surfaces, like a soft clay or plastic render
- **Consistent tactile world** — all objects feel like they exist at the same scale and in the same physical environment

**Subject matter:**
Always grounded in the real-world marketplace experience — hands, storefronts, packages, coins, plants, tools, communication. Avoid abstract tech metaphors (gears, circuits, generic graphs).

**When generating new 3D illustrations**, use this prompt direction:
> 3D illustration, soft clay render style, warm lighting, rounded forms, saturated natural colors, slight 3/4 perspective tilt, transparent background, subtle specular highlight, friendly and approachable tone, marketplace/commerce subject matter

**When placing illustrations in UI:**
- Use on empty states, onboarding screens, confirmation screens, and feature callouts
- Never use as background decoration behind interactive content
- Scale proportionally — do not stretch or crop

---

## Light vs Dark Mode — Confirmed Token Values

Dark mode is handled entirely by swapping CSS variable values at the `:root` level. No component-level overrides are ever needed. The same semantic tokens are used in both modes — only the resolved values change.

| Token | CSS Alias | Light | Dark |
|---|---|---|---|
| Section-0-Basement-s0 | `--section-basement` | #FFFFFF | #1B1B1B |
| Section-1-first-floor-s1 | `--section-floor-1` | #F8F8F8 | #252525 |
| Section-2-second-floor-s2 | `--section-floor-2` | #DDDDDD | #2C2C2C |
| Line/Line | `--border` | #DDDDDD | #2C2C2C |
| Content-primary-c1 | `--content-primary` | #1B1B1B | #F8F8F8 |

**Theme-invariant tokens** — these never change between modes:
- `--section-cta` (#B9EC51) — primary CTA neon green, always the same
- `--content-always-black` (#000000) — always black
- `--content-always-white` (#FFFFFF) — always white

The only component that intentionally ignores the active theme is **Toast** — it always uses inverse tokens and always appears dark.

---

## Color Architecture — Two-Tier System

Palmstreet uses a strict two-tier color system. **Components never reference base colors directly.**

```
Tier 1 — global.json    Raw palette values (Gray, Primary, Function, Creative)
Tier 2 — semantic.json  UI role tokens that reference Tier 1 values
```

Always use Tier 2 semantic tokens in components. Never use `{Gray.800}`, `{Primary.Grass}`, or any raw hex directly in component code.

### The Three Token Groups

**Content** — text, icons, and any foreground element sitting on a surface.
Use `color`, `fill`, or `stroke` CSS properties.

**Section** — backgrounds and surfaces (pages, cards, containers, buttons).
Use `background-color` or `background` CSS properties.

**Line** — borders and dividers.
Use `border-color` or `border` CSS properties.

---

## Semantic Token Reference

### Content Tokens

| Token | CSS Alias | Use |
|---|---|---|
| Content-primary-c1 | `--content-primary` | Primary text, primary icons. Highest emphasis. |
| Content-secondary-c2 | `--content-secondary` | Supporting text, secondary labels |
| Content-tertiary-c3 | `--content-tertiary` | Muted text, placeholders, hints |
| Content-quaternary-c4 | `--content-quaternary` | Disabled states, lowest emphasis |
| Content-primary-inverse-c1i | `--content-primary-inverse` | Primary text/icons on filled or dark surfaces. Inverts with theme. |
| Content-secondary-inverse-c2i | `--content-secondary-inverse` | Secondary text on filled or dark surfaces |
| Content-tertiary-inverse-c3i | `--content-tertiary-inverse` | Tertiary text on filled or dark surfaces |
| Content-quaternary-inverse-c4i | `--content-quaternary-inverse` | Disabled text on filled or dark surfaces |
| Content-always-white | `--content-always-white` | Always white — never flips between light and dark |
| Content-always-black | `--content-always-black` | Always black — never flips between light and dark |
| Content-Interactive | `--content-interactive` | Links, active tabs, selected states |
| Content-Destructive | `--content-destructive` | Delete, remove, error state text and icons |
| Content-Success | `--content-success` | Confirmations, completed actions |
| Content-Warning | `--content-warning` | Caution messages, alerts |

**Inverse vs Always:**
- `inverse` tokens flip against the current theme (white in light mode, dark in dark mode)
- `always-white` / `always-black` never flip — use when the color must be absolute regardless of theme

### Section Tokens

| Token | CSS Alias | Use |
|---|---|---|
| Section-0-Basement-s0 | `--section-basement` | Base page and screen background. Lowest surface level. |
| Section-1-first-floor-s1 | `--section-floor-1` | Cards, panels, containers. One level above base. |
| Section-2-second-floor-s2 | `--section-floor-2` | Popovers, dropdowns, floating elements |
| Section-0-Basement-inverse-s0i | `--section-basement-inverse` | Inverted base background. Flips with theme. |
| Section-1-first-floor-inverse-s1i | `--section-floor-1-inverse` | Inverted card surface. Flips with theme. |
| Section-2-second-floor-inverse-s2i | `--section-floor-2-inverse` | Inverted elevated surface. Flips with theme. |
| Section-Interactive | `--section-interactive` | Hover and focus surface states |
| Section-Destructive | `--section-destructive` | Error banners, destructive action backgrounds |
| Section-Success | `--section-success` | Confirmation banners, success backgrounds |
| Section-Warning | `--section-warning` | Caution banners, alert backgrounds |
| Section-Neon-Green | `--section-cta` | Primary CTA button fill. Palmstreet brand green (#B9EC51). |
| Scrim-1-heavy | `--scrim-heavy` | Modals and full-screen overlays |
| Scrim-2-light | `--scrim-light` | Drawers and partial overlays |
| Section-primary-always-white | `--section-always-white` | Always white surface — never flips |
| Section-primary-always-black | `--section-always-black` | Always black surface — never flips |

### Line Tokens

| Token | CSS Alias | Use |
|---|---|---|
| Line | `--border` | Default borders and dividers |
| Line2 | `--border-strong` | Emphasized borders, focused input states |
| Line-Destructive | `--border-destructive` | Error state input borders |
| Line-Success | `--border-success` | Success state input borders |

---

## Typography

**Only typeface: Gabarito.** Weights in use: Regular (400), Medium (500), SemiBold (600).

| Token | Size | Weight | Use |
|---|---|---|---|
| Display0-70 | 70px | Medium | Hero displays |
| Display1-57 | 57px | SemiBold | Large displays |
| Display2-45 | 45px | Regular | Display text |
| Display3-36 | 36px | Regular | Display text |
| Headline1-32 | 32px | Regular | Page headlines |
| Headline2-28 | 28px | Regular | Section headlines |
| Headline30-24 | 24px | SemiBold | Sub-headlines |
| Title1-22 | 22px | Medium | Titles |
| Title2-18 | 18px | SemiBold | Page titles (mobile nav) |
| Title3-16 | 16px | Medium | Section titles, dialog headings |
| Body1-16 | 16px | Regular | Primary body text |
| Body2-14 | 14px | Regular | Secondary body text |
| Label1-12 | 12px | SemiBold | Input labels, tags |
| Label2-10 | 10px | SemiBold | Small labels |
| Button1-16 | 16px | Medium | Button text (medium size) |
| Button2-14 | 14px | Medium | Button text (small size) |

---

## Spacing Scale

Base unit: 8px grid. Available values: `0, 2, 4, 8, 12, 16, 24, 32, 40, 48`.
Use `1000` for full-radius (pill shapes).

---

## Platform Guidelines

### Desktop (Web)
- Layout: sidebar navigation + main content area
- Token usage: full semantic token set applies
- No fixed width constraint — responsive

### Mobile (375px base width)
- Layout: full-width stacked, no sidebar
- Uses **mobile-only components** not present on desktop:
  - **Docked Button** — fixed bottom action bar (375×98px)
  - **Page Title** — top navigation bar with back arrow (375×92px)
- Device layout grid: 4 columns, 16px margin, 16px gutter

---

## Component Token Patterns

### Button

**3 variants, 4 states, 2 sizes.**

| Variant | Fill | Label color | Border |
|---|---|---|---|
| Primary | `--section-cta` (#B9EC51) | `--content-always-black` | none |
| Secondary | `--section-floor-1` | `--content-primary` | `--border` |
| Destructive | `--section-destructive` | `--content-always-white` | none |

| State | Behavior |
|---|---|
| Default | Base token values above |
| Hovered | Primary: Neon Green + `Section-hover-overlay-medium` at 8% |
| Focused | `Button-color-primary` fill |
| Disabled | Base fill, reduced opacity |

| Size | Height | Typography |
|---|---|---|
| Small | 32px | Button2-14 (Gabarito Medium 14px) |
| Medium | 40px | Button1-16 (Gabarito Medium 16px) |

**Rule:** Primary button label always uses `--content-always-black`, never `--content-primary`. The neon green background is light enough that the always-black token is required for contrast in both modes.

---

### Input Field

**3 status states × error on/off.**

| State | Fill | Border | Input text | Placeholder |
|---|---|---|---|---|
| Default | `--section-floor-1` | `--border` | — | `--content-tertiary` |
| Keyboard active | `--section-floor-1` | `--border-strong` | `--content-primary` | — |
| Filled | `--section-floor-1` | `--border` | `--content-primary` | — |
| Error (any state) | `--section-floor-1` | `--border-destructive` | `--content-primary` | — |

- **Label text:** `Label1-12` SemiBold, `--content-primary`
- **Input text:** `Body1-16` Regular, `--content-primary`
- **Error message:** `Body2-14` Regular, `--content-destructive`
- **Dimensions:** 240px wide — height varies: 53px (default, no error), 75px (with error)
- Includes optional clear icon (16×16px nested instance)

---

### Toast

**Always uses inverse tokens — dark surface in both light and dark mode.**

| Element | Token | Value |
|---|---|---|
| Background | `--section-floor-1-inverse` | #252525 (always dark) |
| Message text | `--content-primary-inverse` | #F8F8F8 |
| Action label | `--content-interactive` | #2269EC |

- **Dimensions:** 343×48px
- **Typography:** text Body2-14 Medium, action Button1-16 Medium
- **Position:** aligned to top (snack bar)
- **Anatomy:** icon/check_circle_fill (24×24px) + text + label-text
- The Toast is the only component that uses inverse tokens as its default state. It intentionally appears dark regardless of the current theme.

---

### Dialog / Alert

**Light mode — basic and icon variants.**

| Element | Token |
|---|---|
| Background | `--section-basement` |
| Drop shadow | Shadow L |
| Title | `--content-primary`, Title3-16 Medium |
| Body text | `--content-secondary`, Body2-14 Regular |

- **Dimensions:** 300×300px
- **Anatomy:** icon/warning (optional) + title text + body text + 1–2 Button instances
- **Nested instances:** 1× icon/warning, 2× Button

---

### Line-Divider

All sizes and thicknesses use the same token: `--border` (Line/Line).

| Size | Thin height | Thick height |
|---|---|---|
| S | 1px | 4px |
| M | 17px | 20px |
| L | 25px | 28px |
| XL | 33px | 36px |

Width is always 375px (full-width on mobile).

---

### Docked Button — Mobile Only

Fixed bottom action bar. Not used on desktop web.

| Element | Token |
|---|---|
| Background | `--section-basement` |
| Top border | `--border` |

- **Dimensions:** 375×98px
- **Anatomy:** 1–2 Button instances + home indicator (375×34px)
- **Variants:** Default (1 button), Icon + button (2 items), 2 buttons
- Button instances inside are 168×40px each with 12px horizontal padding

---

### Page Title — Mobile Only

Top navigation bar. Not used on desktop web.

| Element | Token |
|---|---|
| Bottom border | `--border` |
| Title text color | `--content-primary` |

- **Typography:** Title2-18 SemiBold (Gabarito)
- **Dimensions:** 375×92px
- **Trailing action variants:** None, Button, 1 Icon, 2 Icons
- **Anatomy:** Page title (TEXT) + Status bar (INSTANCE) + icon/arrow (INSTANCE)

---

## Rules for AI Code Generation

1. **Never use raw hex values or base token references** (`{Gray.800}`, `#1b1b1b`) in component code. Always use CSS custom properties (`var(--content-primary)`).
2. **Never use any typeface other than Gabarito.**
3. **Always implement both light and dark mode** using the semantic token layer — do not hardcode colors for a single mode.
4. **Check if a component exists before creating a new one.** 18 components are available in the system.
5. **Spacing follows the 8px grid.** Use values from the Space scale: 0, 2, 4, 8, 12, 16, 24, 32, 40, 48.
6. **Primary button labels always use `--content-always-black`**, not `--content-primary`.
7. **Toast always uses inverse tokens** (`--section-floor-1-inverse`, `--content-primary-inverse`). Do not apply light mode tokens to toast.
8. **Docked Button and Page Title are mobile-only** (375px). Do not use them in desktop web layouts.
9. **Content tokens apply to both text and icons.** `--content-primary` is correct for `color`, `fill`, and `stroke`.
10. **Section tokens are for surfaces only.** Never apply a Section token to text color.
11. **Icons must be Google Material Design, filled style, rounded corners.** Never use outlined, sharp, or two-tone variants.
12. **Icon color is always a Content token.** Never hardcode an icon color.
13. **Do not apply generic tech or SaaS design patterns.** Palmstreet is a marketplace for real-world goods — the UI should be neutral and modern, not corporate or startup-generic.
14. **3D illustrations are placed on empty states, onboarding, and feature callouts only.** Never use as background decoration behind interactive content.

---

## Available Components (18 total)

Buttons · Docked Button · Text Inputs · Selection · Tags & Badges · Cards & Lists · Navigation · Overlays · Feedback · Dialog / Alert · Toast · Line-Divider · Page Title · and more.

Always check the component inventory before generating a new component from scratch.

---

## Token Files

- Base values: `tokens/global.json`
- Semantic layer: `tokens/semantic.json`
- Repository: `github.com/yufan-meow/palmstreet-branch-design-system`
