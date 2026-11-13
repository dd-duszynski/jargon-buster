---
bootstrapped_at: 2026-11-12T21:10:26Z
starter_id: 10x-astro-starter
starter_name: 10x Astro Starter (Astro + Supabase + Cloudflare)
project_name: jargon-buster
language_family: js
package_manager: npm
cwd_strategy: git-clone
bootstrapper_confidence: first-class
phase_3_status: ok
audit_command: npm audit --json
---

## Hand-off

```yaml
starter_id: 10x-astro-starter
package_manager: npm
project_name: jargon-buster
hints:
  language_family: js
  team_size: solo
  deployment_target: cloudflare-pages
  ci_provider: github-actions
  ci_default_flow: auto-deploy-on-merge
  bootstrapper_confidence: first-class
  path_taken: standard
  quality_override: false
  self_check_answers: null
  has_auth: true
  has_payments: false
  has_realtime: false
  has_ai: true
  has_background_jobs: false
```

### Why this stack

Projekt jargon-buster to edukacyjna aplikacja webowa realizowana w modelu jednoosobowym, wymagająca natychmiastowego serwowania treści, zintegrowanej autoryzacji oraz bezpośredniej integracji z modelami LLM. Szablon 10x-astro-starter łączy Astro 7 (architektura islands i wydajne renderowanie brzegowe) z Reactem 19, TypeScriptem i bazą Supabase (PostgreSQL z wbudowanym mechanizmem kont i RLS), co idealnie odpowiada potrzebie globalnego rejestru pojęć i izolacji danych użytkowników. Wdrożenie na Cloudflare Pages gwarantuje minimalne opóźnienia brzegowe przy znikomych kosztach infrastruktury, a pełne otypowanie TypeScriptem i zdefiniowane konwencje struktury projektu ułatwiają precyzyjną współpracę z agentami programistycznymi AI.

## Pre-scaffold verification

| Signal             | Value                              | Severity | Notes                              |
| ------------------ | ---------------------------------- | -------- | ---------------------------------- |
| npm package        | not run                            | n/a      | skipped (`cmd_template` starts with `git clone`) |
| GitHub repo        | not run via `gh api` (cloned HEAD: 2026-10-29T23:28:54+01:00) | fresh | `gh` CLI not installed at pre-scaffold step; last commit verified after clone |

## Scaffold log

**Resolved invocation**: `git clone https://github.com/przeprogramowani/10x-astro-starter .bootstrap-scaffold && cd .bootstrap-scaffold && npm install`
**Strategy**: git-clone
**Exit code**: 0
**Files moved**: 51 (plus `node_modules/`)
**Conflicts (.scaffold siblings)**: none
**.gitignore handling**: moved silently
**.bootstrap-scaffold cleanup**: deleted (after removing `.bootstrap-scaffold/.git/`)

## Post-scaffold audit

**Tool**: npm audit --json
**Summary**: 0 CRITICAL, 0 HIGH, 14 MODERATE, 0 LOW
**Direct vs transitive**: 0/0/6/0 direct of total 0/0/14/0

#### CRITICAL findings

None.

#### HIGH findings

None.

#### MODERATE findings

- **`minimatch`** (`>=7.0.0 <11.0.1`, transitive) — `GHSA-g3hv-75wg-m249`: minimatch has potential denial of service via globparts amplification (`CWE-405`). Root advisory causing the downstream ESLint / TypeScript-ESLint chain below.
- **`eslint`** (`>=10.0.0-alpha.0`, direct devDependency) — moderate severity via `@eslint/config-array` and `minimatch`. Fix available via `eslint@9.39.5` (semver major downgrade) or upstream `minimatch` bump.
- **`@eslint/js`** (`>=10.0.1`, direct dependency) — moderate severity via `eslint`. Fix available via `@eslint/js@9.39.5` (semver major).
- **`eslint-plugin-astro`** (`>=2.0.0`, direct devDependency) — moderate severity via `eslint` and `eslint-plugin-jsx-a11y`. Fix available via `eslint-plugin-astro@1.7.0` (semver major).
- **`eslint-plugin-jsx-a11y`** (`6.10.2`, direct devDependency) — moderate severity via `eslint`.
- **`eslint-plugin-react`** (`^7.37.5`, direct devDependency) — moderate severity via `eslint`.
- **`typescript-eslint`** (`<=8.72.2`, direct devDependency) — moderate severity via `@typescript-eslint/eslint-plugin`, `@typescript-eslint/parser`, `@typescript-eslint/typescript-estree`, and `@typescript-eslint/utils`.
- **`@eslint-community/eslint-utils`** (transitive) — moderate severity via `eslint`.
- **`@eslint/config-array`** (`>=0.23.0`, transitive) — moderate severity via `minimatch`.
- **`@typescript-eslint/eslint-plugin`** (`6.16.0 - 8.72.2`, transitive) — moderate severity via `@typescript-eslint/type-utils` and `@typescript-eslint/utils`.
- **`@typescript-eslint/parser`** (`6.16.0 - 8.72.2`, transitive) — moderate severity via `@typescript-eslint/typescript-estree`.
- **`@typescript-eslint/type-utils`** (`6.16.0 - 8.72.2`, transitive) — moderate severity via `@typescript-eslint/typescript-estree` and `@typescript-eslint/utils`.
- **`@typescript-eslint/typescript-estree`** (`6.16.0 - 8.72.2`, transitive) — moderate severity via `minimatch`.
- **`@typescript-eslint/utils`** (`6.16.0 - 8.72.2`, transitive) — moderate severity via `@typescript-eslint/typescript-estree`.

#### LOW / INFO findings

None.

## Hints recorded but not acted on

| Hint                       | Value                              |
| -------------------------- | ---------------------------------- |
| bootstrapper_confidence    | first-class                        |
| quality_override           | false                              |
| path_taken                 | standard                           |
| self_check_answers         | null                               |
| team_size                  | solo                               |
| deployment_target          | cloudflare-pages                   |
| ci_provider                | github-actions                     |
| ci_default_flow            | auto-deploy-on-merge               |
| has_auth                   | true                               |
| has_payments               | false                              |
| has_realtime               | false                              |
| has_ai                     | true                               |
| has_background_jobs        | false                              |

## Next steps

Next: a future skill will set up agent context (CLAUDE.md, AGENTS.md). For now, your project is scaffolded and verified — happy hacking.

Useful manual steps in the meantime:
- `git init` (if you have not already) to start your own repo history.
- Review any `.scaffold` siblings the conflict policy created and decide which version of each file to keep.
- Address audit findings per your project's risk tolerance — the full breakdown is in this log.
