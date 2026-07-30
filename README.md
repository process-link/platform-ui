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
