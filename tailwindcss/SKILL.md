---
name: tailwindcss
description: Add Tailwind CSS to an existing project (web app or static pages), including config, build pipeline, styling conventions, and component patterns. Use when the user asks for Tailwind, utility-first CSS, design tokens, or shadcn-like UI styling.
metadata:
  author: spanexx
  version: "1.0.0"
  tags: ["tailwind", "css", "ui", "design-system", "frontend"]
compatibility: Works with Node.js tooling (npm/pnpm/yarn) and common bundlers (Vite/Webpack/Next). Requires filesystem access and package install permissions.
license: Proprietary
---

# Tailwind CSS Integration Skill

## When to use
Use this skill when you need to:
- Introduce Tailwind CSS into an existing codebase
- Set up Tailwind in a new frontend app
- Add Tailwind config, theming, and sane defaults
- Establish component conventions and utility patterns

## Outputs (what you must produce)
- A working Tailwind integration (build + CSS output wired into the app)
- A PostCSS configuration (Angular guide uses `.postcssrc.json`)
- A base stylesheet (`src/styles.css` or equivalent) that imports Tailwind:
  - `@import "tailwindcss";`
- A short verification section (what command to run + what to look for)

## Procedure

### 1) Detect project type and build tool
- Identify whether this is:
  - Vite
  - Next.js
  - CRA/Webpack
  - Angular
  - Static HTML
- Find where global CSS is loaded.

### 2) Install dependencies
Prefer the current official approach for your framework.

For Angular (official guide), install the Tailwind PostCSS plugin and peer deps:

```bash
npm install tailwindcss @tailwindcss/postcss postcss --force
```

### 3) Configure PostCSS (Angular)
Create `.postcssrc.json` in the project root:

```json
{ "plugins": { "@tailwindcss/postcss": {} } }
```

### 4) Add Tailwind to your CSS entry
For Angular (official guide), add this to `./src/styles.css`:

```css
@import "tailwindcss";
```

### 5) Add sane defaults
- Prefer using CSS variables for design tokens.
- Set up default font stack.
- Add a small set of shared utilities via `@layer utilities` only if needed.

### 6) Verify integration
- Add a temporary test element using Tailwind classes.
- Run the dev server/build.
- Confirm styles are applied.

Angular verification:

```bash
ng serve
```

## Recommended conventions

### Class organization
- Order classes by:
  - layout (flex/grid/position)
  - spacing
  - typography
  - colors
  - borders
  - effects
  - transitions

### Component patterns (shadcn-like)
- Use neutral surfaces:
  - `bg-white` / `bg-zinc-950`
  - `border border-zinc-200` / `border-zinc-800`
- Prefer rounded corners: `rounded-lg`
- Prefer subtle shadow: `shadow-sm`

## Common pitfalls
- CSS file not imported in the entrypoint
- Over-aggressive CSS reset from other libraries

## Example acceptance checklist
- [ ] `tailwindcss` appears in `package.json`
- [ ] `.postcssrc.json` exists (Angular guide)
- [ ] Global CSS imports Tailwind (`@import "tailwindcss";`)
- [ ] Running the dev server shows Tailwind styles in the browser
