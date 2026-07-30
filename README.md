# platform-ui

Shared front-end building blocks for the Process Link apps.

| Package | Published | Status |
| --- | --- | --- |
| [`@processlink/theme`](packages/theme) | public npm | Ready |
| `@processlink/ui-kit` | not yet | Blocked, see below |

## Why this repo exists

Nine apps shared their design by copying files between repos with
`portal/scripts/sync-header-kit.mjs`. Copying is a push with no pull, no
version, and nothing that notices when an app edits its copy.

The theme is now a versioned package instead. The header kit is not, yet, for a
concrete reason.

## Why the header kit is not here yet

Those components are not self-contained. They import from the app around them
through the `@/` path alias:

| Component | Imports from the consuming app |
| --- | --- |
| `theme-toggle.tsx` | `@/components/ui/button`, `@/components/ui/dropdown-menu`, `@/lib/theme-cookie` |
| `org-logo.tsx` | `@/lib/utils` |
| `app-switcher.tsx` | + `@/lib/services`, `@/types/nav` |
| `universal-header.tsx` | seven aliases, including `@/lib/supabase/client` |

A package cannot resolve those, because they point at whichever app the file
was copied into. Shipping the kit means inverting the dependencies first:
peer-depend or bundle the shadcn primitives, and inject the auth client,
service catalogue and domain as configuration rather than imports.

That is a refactor, not a packaging step, so the kit stays on the copy script
until it is done deliberately.

Until then `sync-header-kit.mjs --check <app>` reports real drift. It formats
both sides with Prettier before comparing, because an earlier byte comparison
reported every app as drifted when the only differences were quote style and
line wrapping.

## Releasing

```bash
cd packages/theme
npm version patch      # or minor / major
npm publish            # publishConfig.access is already "public"
```

Then in each consuming app:

```bash
npm install @processlink/theme@latest
```

and in its `globals.css`, after the Tailwind imports:

```css
@import "@processlink/theme";
```

## Verifying a change

The theme should be a no-op to adopt. Prove it rather than assume it: build the
app before and after switching to the package and compare the compiled
stylesheet. When `@processlink/theme@0.1.0` was validated against Portal, the
output was byte-identical at 103362 bytes.
