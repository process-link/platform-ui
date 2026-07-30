# @processlink/theme

The Process Link design tokens, as plain CSS. One source of truth for colour,
typography, radius, shadow and elevation across every Process Link app.

No JavaScript, no framework, no dependencies. A Next app can use it, so can a
static page or a stylesheet for a generated document.

## Install

```bash
npm install @processlink/theme
```

## Use

Import it after Tailwind, in your `globals.css`:

```css
@import "tailwindcss";
@import "tw-animate-css";

@custom-variant dark (&:where(.dark, .dark *));

@import "@processlink/theme";
```

Order matters. Tailwind must be imported first, because the `@theme` block
inside this package resolves against it.

Your app keeps its own `@layer base`, keyframes and anything app-specific.

## Fonts

The theme maps Tailwind's font utilities onto three CSS variables. Your app
declares the actual faces, so it controls loading and subsetting:

| Variable | Used by | Portal uses |
| --- | --- | --- |
| `--font-geist-sans` | `font-sans` | Geist |
| `--font-geist-mono` | `font-mono` | Geist Mono |
| `--font-hanken` | `font-heading` | Hanken Grotesk |

```tsx
const geistSans = Geist({ subsets: ["latin"], variable: "--font-geist-sans" });
// ...then put the variables on <body>
```

Miss this step and the utilities silently fall back to the system stacks. That
is not hypothetical: Portal shipped for months downloading Inter and never
applying it, because nothing mapped it onto `--font-sans`.

## What is in here

- Brand scale, `--brand-50` through `--brand-900`, orange as an accent only
- Light palette: warm neutral, background a hair off white so white cards lift
- Dark palette: GitHub Dark Dimmed, deliberately not near-black, with elevation
  running the correct way (surfaces get lighter as they rise)
- Soft multi-stop shadow scale
- Radius scale on a multiplicative ramp
- `prefers-reduced-motion` support, with loading indicators slowed rather than
  frozen so the UI does not read as hung
- A thin, theme-aware scrollbar utility, `.scrollbar-thin`

## Accessibility

Contrast is measured, not assumed. Body text is 7.6:1 on the dark page and
18.9:1 in light. Form control borders clear the 3:1 that WCAG 1.4.11 asks of UI
component boundaries in both modes. `--muted-foreground` is lifted above
Primer's own value, which falls under AA on card surfaces.

## Licence

UNLICENSED. This is published so Process Link apps can install it from a single
place, not as an invitation to reuse. Pick a real licence before treating it as
open source.
