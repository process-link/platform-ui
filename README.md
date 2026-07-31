# platform-ui

Shared front-end packages for Process Link apps.

| Package | Registry | Status |
| --- | --- | --- |
| [`@processlink/theme`](packages/theme) | public npm | 0.1.0 |
| `@processlink/ui-kit` | unpublished | see below |

## Release

```bash
cd packages/theme
npm version patch
npm publish
```

Consumers: `npm install @processlink/theme@latest`.

## Adopting in an app

```bash
npm install @processlink/theme
```

`globals.css`: replace the local token block with `@import "@processlink/theme";`
after the Tailwind imports. Set the three font variables in the root layout.

shift-link, dossier and files each invented their own names for tokens the
theme already has. Delete the local definitions and rename usages:

| Local | Theme |
| --- | --- |
| `--surface`, `--color-surface` | `--background` |
| `--surface-raised`, `--surface-elevated`, `--color-surface-elevated` | `--card` |
| `--surface-strong` | `--primary` |
| `--text-primary` | `--foreground` |
| `--text-secondary` | `--muted-foreground` |
| `--border-default` | `--border` |

Not covered, keep locally or drop: `--text-tertiary` and `--border-subtle`
(files only), the custom spacing scale (dossier), `--shadow-soft` /
`--shadow-outline` and the shimmer/slide keyframes (shift-link).

connect, help-desk and grafset define no competing tokens, so those are a
straight install.

Verify by diffing the compiled stylesheet before and after. It should not
change.

## ui-kit

Not packaged yet. The header components resolve app code through the `@/`
alias, so they only work inside the app they were copied into:

| Component | Aliased imports |
| --- | --- |
| `theme-toggle` | `ui/button`, `ui/dropdown-menu`, `lib/theme-cookie` |
| `org-logo` | `lib/utils` |
| `app-switcher` | + `lib/services`, `types/nav` |
| `universal-header` | 7, incl. `lib/supabase/client` |

Packaging them means injecting the auth client, service catalogue and domain as
config instead of importing them. Until that happens they stay on
`portal/scripts/sync-header-kit.mjs`.

Drift check (read-only, normalises formatting before diffing):

```bash
node portal/scripts/sync-header-kit.mjs --check ../shift-link
```

Known: grafset has no `nav/` directory and has never used the header.
