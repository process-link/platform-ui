# @processlink/theme

Design tokens for Process Link apps. Plain CSS, no dependencies.

```bash
npm install @processlink/theme
```

## Usage

In `globals.css`, after Tailwind:

```css
@import "tailwindcss";
@import "tw-animate-css";

@custom-variant dark (&:where(.dark, .dark *));

@import "@processlink/theme";
```

Tailwind must come first. The `@theme` block resolves against it.

Your app keeps its own `@layer base`, keyframes and anything app-specific.

## Fonts

Utilities map to CSS variables. The app declares the faces:

| Variable | Utility |
| --- | --- |
| `--pl-font-sans` | `font-sans` |
| `--pl-font-mono` | `font-mono` |
| `--pl-font-heading` | `font-heading` |

```tsx
const geistSans = Geist({ subsets: ["latin"], variable: "--pl-font-sans" });
// put .variable on <body>
```

Skip this and the utilities fall back to the system stacks silently.

## Contents

- Brand scale `--brand-50` to `--brand-900`
- Light palette, warm neutral
- Dark palette, GitHub Dark Dimmed, elevation lightens as surfaces rise
- Shadow and radius scales
- `prefers-reduced-motion`, spinners slowed rather than stopped
- `.scrollbar-thin`

Contrast targets AA: 7.6:1 body on dark, 18.9:1 on light, form borders above
3:1 in both.

## Licence

MIT. Covers the CSS only, not the Process Link name or logo.
