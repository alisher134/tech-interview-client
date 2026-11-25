# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some Oxlint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Oxc](https://oxc.rs)
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/)

## Tooling

- **oxlint** — linting (`.oxlintrc.json`), including Tailwind class checks via
  `eslint-plugin-better-tailwindcss`
- **oxfmt** — formatting (`.oxfmtrc.json`): formats code, sorts imports and
  Tailwind classes
- **lefthook** — git hooks (`lefthook.yml`)

oxlint uses the default plugins (`unicorn`, `typescript`, `oxc`) plus `react`.
Since specifying `plugins` replaces the defaults, they are listed explicitly.
Only rules that are off by default are configured: `react/rules-of-hooks`,
`react/only-export-components` and the Tailwind rules. Class ordering and line
wrapping are left to oxfmt, so the linter does not duplicate the formatter.

Tailwind linting rules: `no-conflicting-classes`, `no-concatenated-classes`,
`no-unknown-classes` (errors), `no-duplicate-classes`, `no-deprecated-classes`,
`enforce-canonical-classes`, `enforce-shorthand-classes` (warnings).
The demo classes from the Vite template are ignored by `no-unknown-classes` via
a regex in `.oxlintrc.json`.

```sh
pnpm lint          # check for lint errors
pnpm lint:fix      # auto-fix lint errors
pnpm format        # format the project
pnpm format:check  # verify formatting
```

Git hooks are installed automatically on `pnpm install` (via the `prepare` script).
On commit, staged files are linted and formatted; on push, the whole project is
checked. To install them manually, run `pnpm exec lefthook install`.

## Styling

- **Tailwind CSS v4** via `@tailwindcss/vite`, imported in `src/index.css`
- **shadcn/ui** (Radix + Nova preset), configured in `components.json`
- Path alias: `@/*` → `src/*` (in `vite.config.ts` and `tsconfig.app.json`)

Add UI components with:

```sh
pnpm dlx shadcn@latest add button
```

Components land in `src/components/ui`, helpers in `src/lib`.

Dark mode is class-based (`.dark` on `<html>`) and follows the OS preference on
first load via a small inline script in `index.html`.

## React Compiler

The React Compiler is not enabled on this template because of its impact on dev & build performances. To add it, see [this documentation](https://react.dev/learn/react-compiler/installation).

## Expanding the Oxlint configuration

If you are developing a production application, we recommend enabling type-aware lint rules by installing `oxlint-tsgolint` and editing `.oxlintrc.json`:

```json
{
  "$schema": "./node_modules/oxlint/configuration_schema.json",
  "plugins": ["react", "typescript", "oxc"],
  "options": {
    "typeAware": true
  },
  "rules": {
    "react/rules-of-hooks": "error",
    "react/only-export-components": ["warn", { "allowConstantExport": true }]
  }
}
```

See the [Oxlint rules documentation](https://oxc.rs/docs/guide/usage/linter/rules) for the full list of rules and categories.
