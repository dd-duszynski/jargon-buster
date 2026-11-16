# Repository Guidelines

`jargon-buster` is an Astro 7 SSR web app with React 19 islands, Tailwind 4, Supabase auth, and shadcn/ui, deployed to Cloudflare Workers (`@context/foundation/prd.md`, `@context/foundation/tech-stack.md`).

## Architecture & Conventions

- **Rendering**: Full SSR (`output: "server"` in `@astro.config.mjs`); all routes render server-side by default.
- **Auth flow**: `@src/lib/supabase.ts` creates a cookie-based `@supabase/ssr` client using server-only `astro:env/server` secrets (`SUPABASE_URL`, `SUPABASE_KEY`). `@src/middleware.ts` attaches `context.locals.user` (typed in `@src/env.d.ts`) and redirects unauthenticated requests from `PROTECTED_ROUTES` (`/dashboard`). Endpoints live in `src/pages/api/auth/{signin,signup,signout}.ts`; pages in `src/pages/auth/{signin,signup,confirm-email}.astro` and `src/pages/dashboard.astro`.
- **UI & styling**: Never use Next.js directives such as `"use client"` in React islands. Merge Tailwind classes via `cn()` from `@/lib/utils`; never concatenate class strings manually.
- **shadcn/ui**: Components live in `src/components/ui/` (`new-york` style, `@components.json`); add new ones with `npx shadcn@latest add [name]`.
- **Helpers**: Place shared helpers in `src/lib/`.

## Commands

- `npm run dev` — start dev server (Cloudflare workerd runtime)
- `npm run build` / `npm run preview` — production SSR build (`@astrojs/cloudflare`) and local preview
- `npm run lint` / `npm run lint:fix` — ESLint (`@eslint.config.js`)
- `npm run format` — Prettier (`@.prettierrc.json`)
- `npx astro sync && npx astro check` — sync Astro types and run type/template checks (CI gate)
- `npm run smoke` — auth-flow smoke test (`@scripts/smoke.mjs`) against running server (`BASE_URL`, default `http://localhost:4321`)

Pre-commit hooks run `lint-staged` via `@.husky/pre-commit` (`@package.json`).

## Environment & CI

- **Runtime & secrets**: Node.js `v26.13.0` (`@.nvmrc`). Copy `@.env.example` (`SUPABASE_URL`, `SUPABASE_KEY`) to `.env` for Node and `.dev.vars` for Cloudflare local dev.
- **Local Supabase & deploy**: `npx supabase start` (Docker, config in `@supabase/config.toml`); deploy with `npx wrangler deploy` (`@wrangler.jsonc`).
- **CI**: Gates and smoke job definitions live in `@.github/workflows/ci.yml` (requires `SUPABASE_URL` and `SUPABASE_KEY` secrets).
- **Commits**: Prefix commit subjects with a Conventional Commit type (`feat:`, `fix:`, `chore:`, `docs:`, `refactor:`) or a milestone tag matching `M<n> L<n>` (per `git log`), keeping subject lines <= 72 characters.
