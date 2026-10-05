# CLAUDE.md

@docs/PROGRESS.md

Update `docs/PROGRESS.md` at the end of every task: current state, in progress, next up, open questions, and a dated Log entry (newest first).

## What this is

Shared front-end packages for Process Link apps. Currently one package: `@processlink/theme` (`packages/theme`), design tokens as plain CSS for Tailwind v4 apps. Published to public npm under MIT.

## Stack

Plain CSS, Tailwind v4 (consumer side), npm. No JavaScript, no dependencies, no build step.

## Run, test, lint

There is no test suite, linter or CI in this repo. Check a change by building a consuming app (for example Portal) against the packed tarball and diffing the compiled stylesheet.

Release:

```bash
cd packages/theme
npm version patch   # or minor / major
npm publish
```

## Layout

```
README.md              release steps, adoption guide, ui-kit notes
docs/PROGRESS.md       progress log (imported above)
packages/theme/        @processlink/theme
  theme.css            tokens, @theme mapping, utilities
  package.json         exports, files, version
```

## Conventions

- Tokens follow the shadcn vocabulary (`--background`, `--card`, `--primary`, `--foreground`, `--muted-foreground`, `--border`). Do not add parallel names such as `--surface`.
- Brand scale is `--brand-50` to `--brand-900`.
- Font variables are `--pl-font-sans`, `--pl-font-mono`, `--pl-font-heading`. Names must not contain a typeface.
- Light palette in `:root`, dark palette in `.dark`, Tailwind mapping in `@theme inline`.
- Keep contrast at AA or better. Respect `prefers-reduced-motion`.
- Renaming a public variable is a breaking change: bump the version and say so in the commit.
- Commits use conventional style (`feat(theme)!:`, `docs:`, `chore:`) with a body that explains why.
- Keep READMEs short: install, usage and constraints that bite.
- The header kit is not packaged here. Do not copy app code into this repo.

## Writing style

- Australian English (organisation, colour, licence, behaviour).
- No em-dashes. Use a comma, colon, parentheses or a hyphen.
- Never push to `main` or `staging`. Use a feature branch and a pull request.
