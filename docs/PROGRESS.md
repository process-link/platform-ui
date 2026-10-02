# Progress

## Overview

platform-ui holds shared front-end packages for Process Link apps. Today it contains one published package, `@processlink/theme` (`packages/theme`): design tokens as plain CSS with no JavaScript and no dependencies. It covers the brand scale, light and dark palettes, the Tailwind v4 `@theme` mapping, shadow and radius scales, reduced-motion support and a `.scrollbar-thin` utility.

Stack: plain CSS, Tailwind v4 (consumer side), npm (public registry, MIT licence). There is no build step, no test suite and no CI in the repo.

A second package, `@processlink/ui-kit`, is named in the root README but is not packaged and has no directory.

## Current state

- `@processlink/theme` is at version 0.2.0 (`packages/theme/package.json`). It ships `theme.css`, README and LICENSE.
- Font variables are `--pl-font-sans`, `--pl-font-mono` and `--pl-font-heading`. The app declares the faces.
- The root README documents the release steps (`npm version patch`, `npm publish`) and a rename table for apps that use their own token names (shift-link, dossier, files).
- Portal consumed 0.1.0 (per git log). Whether any app has adopted 0.2.0 is not recorded in this repo.
- The header components (`theme-toggle`, `org-logo`, `app-switcher`, `universal-header`) are not packaged. They are synced from `portal/scripts/sync-header-kit.mjs`, which lives outside this repo.

## In progress

Nothing is recorded as in progress in the repo. There are no open TODOs, issues or branches beyond the working branch.

## Next up

- Package the ui-kit header components. The README says this needs the auth client, service catalogue and domain injected as config instead of imported through `@/` aliases.
- Adopt the theme in shift-link, dossier and files by deleting local tokens and renaming usages (table in the root README). Verify by diffing the compiled stylesheet before and after.
- Update the root README status table, which still lists `@processlink/theme` as 0.1.0 while the package is 0.2.0.
- Add CI or a check that the compiled stylesheet is unchanged after adoption (guess).

## Open questions

- Which apps have moved to 0.2.0 so far? (not recorded)
- Should `--text-tertiary`, `--border-subtle`, dossier's spacing scale and shift-link's shadows and keyframes move into the theme, or stay local? The README says "keep locally or drop".
- Is a versioning or changelog policy wanted for breaking token renames? (guess)
- grafset has no `nav/` directory and has never used the header. Does it need one?

## Log

### 2026-10-02

- Added `docs/PROGRESS.md` and `CLAUDE.md` from a read of the repo. No code changes.

### 2026-07-31

- `e90b913`: theme 0.2.0. Breaking rename of font variables to `--pl-font-*`. Added the adoption section and token rename table.

### 2026-07-30

- `5e9d66e`: trimmed the READMEs.
- `5c74966`: licensed `@processlink/theme` under MIT (was UNLICENSED).
- `2ccdba5`: initial commit of platform-ui with `@processlink/theme`. Compiled output verified byte-identical against Portal.
