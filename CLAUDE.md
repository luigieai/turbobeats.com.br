# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
pnpm dev        # Start dev server at localhost:4321
pnpm build      # Build production site to ./dist/
pnpm preview    # Preview the production build locally
pnpm astro ...  # Run Astro CLI commands (e.g. astro add, astro check)
```

## Architecture

This is an **Astro 5** static site using pnpm, with TypeScript in strict mode (`astro/tsconfigs/strict`).

**Routing**: File-based routing via `src/pages/`. Each `.astro` file in this directory becomes a route.

**Component model**: Astro components use frontmatter (between `---` delimiters) for server-side logic. Components render zero client-side JS by default; use `client:*` directives to hydrate interactive islands.

**Layout pattern**: Pages wrap content in `src/layouts/Layout.astro` using `<slot />` for content injection.

**Static assets**: Files in `public/` are served as-is. Files in `src/assets/` are processed by Astro's asset pipeline (optimized images, etc.).

**Styling**: Tailwind CSS is configured via `@astrojs/tailwind`. Every `.astro` file that uses Tailwind utilities must import the global stylesheet in its frontmatter:

```ts
import '../styles/global.css';
```

Adjust the relative path based on the file's location (e.g., `../../styles/global.css` for nested components). This import is required for Tailwind classes to apply.

**Color palette**: All styling MUST use the semantic color tokens defined in `src/styles/global.css`. Never hardcode hex values or use arbitrary Tailwind colors. Always prefer semantic tokens over raw palette tokens.

| Token | Tailwind class | Usage |
|---|---|---|
| `--color-primary` | `bg-primary`, `text-primary` | Main CTAs, buttons, logo |
| `--color-primary-hover` | `bg-primary-hover` | Hover state for primary elements |
| `--color-primary-light` | `bg-primary-light`, `text-primary-light` | Tinted primary backgrounds |
| `--color-accent` | `bg-accent`, `text-accent` | Highlights, neon accents, hover indicators |
| `--color-accent-hover` | `bg-accent-hover` | Hover state for accent elements |
| `--color-accent-light` | `bg-accent-light` | Tinted accent backgrounds |
| `--color-hot` | `bg-hot`, `text-hot` | Live events, urgency, energetic badges |
| `--color-hot-hover` | `bg-hot-hover` | Hover state for hot elements |
| `--color-hot-light` | `bg-hot-light` | Tinted hot backgrounds |
| `--color-gold` | `bg-gold`, `text-gold` | Featured, VIP, premium content |
| `--color-gold-hover` | `bg-gold-hover` | Hover state for gold elements |
| `--color-gold-light` | `bg-gold-light` | Tinted gold backgrounds |
| `--color-info` | `bg-info`, `text-info` | Links, secondary actions, informational |
| `--color-info-hover` | `bg-info-hover` | Hover state for info elements |
| `--color-info-light` | `bg-info-light` | Tinted info backgrounds |
| `--color-background` | `bg-background` | Page background (blue-bell-50) |
| `--color-surface` | `bg-surface` | Cards, modals (white) |
| `--color-surface-muted` | `bg-surface-muted`, `border-surface-muted` | Subtle card backgrounds, dividers |
| `--color-text` | `text-text` | Primary body text |
| `--color-text-muted` | `text-text-muted` | Secondary/helper text |
| `--color-text-on-primary` | `text-text-on-primary` | Text placed on primary-colored backgrounds |
| `--color-text-on-accent` | `text-text-on-accent` | Text placed on accent-colored backgrounds |

Raw palette tokens (`forest-green-*`, `yellow-green-*`, etc.) are available but should only be used when no semantic token fits.
