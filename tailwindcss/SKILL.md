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
- A minimal, validated config (`tailwind.config.*`) and `postcss.config.*` where needed
- A base stylesheet (`src/styles.css` or equivalent) with:
  - `@tailwind base;`
  - `@tailwind components;`
  - `@tailwind utilities;`
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
Install the Tailwind toolchain for most setups:
- `tailwindcss`
- `postcss`
- `autoprefixer`

If the framework has its own adapter, prefer the official docs.

### 3) Initialize Tailwind config
- Create Tailwind config via `tailwindcss init -p` if appropriate.
- Ensure `content` includes all template/TS/JS/HTML locations.

Example `content` targets:
- `./index.html`
- `./src/**/*.{js,ts,jsx,tsx,html}`

### 4) Add Tailwind to your CSS entry
Create/modify the global stylesheet used by the app and add:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### 5) Add sane defaults
- Prefer using CSS variables for design tokens.
- Set up default font stack.
- Add a small set of shared utilities via `@layer utilities` only if needed.

### 6) Verify integration
- Add a temporary test element using Tailwind classes.
- Run the dev server/build.
- Confirm styles are applied.

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
- Missing `content` globs results in “Tailwind not working”
- CSS file not imported in the entrypoint
- Over-aggressive CSS reset from other libraries

## Example acceptance checklist
- [ ] `tailwindcss` appears in `package.json`
- [ ] `tailwind.config.*` has correct `content` globs
- [ ] Global CSS contains `@tailwind ...` directives
- [ ] Running the dev server shows Tailwind styles in the browser
