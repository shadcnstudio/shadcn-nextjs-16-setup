# shadcn + Next.js 16 Starter

A working Next.js 16 project with shadcn already wired up. This is the companion repo for the guide *How to Integrate shadcn into Next.js 16*, and it's the exact output of a default `shadcn init` run.

## What's inside

| | |
| --- | --- |
| Next.js | 16.2.6, App Router, Turbopack |
| React | 19.2.4 |
| shadcn CLI | 4.19.0 |
| Primitives | Base UI |
| Styling | Tailwind CSS v4 |
| Icons | Lucide |
| Preset | `b0` — Nova style, neutral base, Inter |

Dark mode is already set up through `next-themes`, and the button component ships installed so there's something on screen from the first run.

## Getting started

```bash
pnpm install
pnpm dev
```

Then open [http://localhost:3000](http://localhost:3000). Press `d` to toggle dark mode.

## Structure

```
app/
├── globals.css          theme tokens and Tailwind setup
├── layout.tsx           fonts and ThemeProvider
└── page.tsx
components/
├── ui/                  shadcn components land here
└── theme-provider.tsx   next-themes wrapper
hooks/
lib/
└── utils.ts             the cn() helper
components.json          shadcn CLI config
```

## Adding components

```bash
pnpm dlx shadcn@latest add card
```

Pass several names at once, or run `add` with no name to pick from a list. Files go wherever `components.json` says, so change the `aliases` block if you want a different layout. Preview anything first with `--dry-run`.

Import from the alias:

```tsx
import { Button } from "@/components/ui/button"
```

## Changing the theme

Colors live in `app/globals.css` as CSS variables, declared once under `:root` and again under `.dark`. Edit both or dark mode drifts out of sync.

To swap the whole palette, build one at [ui.shadcn.com/create](https://ui.shadcn.com/create) and apply it without touching your components:

```bash
pnpm dlx shadcn@latest apply --preset <code> --only theme
```

This project's preset is [`b0`](https://ui.shadcn.com/create?preset=b0). Run `pnpm dlx shadcn@latest info` to see the resolved config at any time.

## Scripts

| Command | What it does |
| --- | --- |
| `pnpm dev` | Start the dev server |
| `pnpm build` | Production build |
| `pnpm start` | Serve the production build |
| `pnpm lint` | Run ESLint |
| `pnpm format` | Format with Prettier |
| `pnpm typecheck` | Type check without emitting |

`next lint` was removed in Next.js 16, which is why `pnpm lint` calls `eslint` directly.

## A note on customizing

Components in `components/ui/` are yours to edit, and adding variants to the `cva` config is the intended way to extend them. Types come along automatically, since props are derived from the variant object.

Just remember `add --overwrite` replaces those files wholesale. Run `add <component> --diff` first to see what you'd lose.
