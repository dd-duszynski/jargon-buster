---
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
---

## Why this stack

Projekt jargon-buster to edukacyjna aplikacja webowa realizowana w modelu jednoosobowym, wymagająca natychmiastowego serwowania treści, zintegrowanej autoryzacji oraz bezpośredniej integracji z modelami LLM. Szablon 10x-astro-starter łączy Astro 7 (architektura islands i wydajne renderowanie brzegowe) z Reactem 19, TypeScriptem i bazą Supabase (PostgreSQL z wbudowanym mechanizmem kont i RLS), co idealnie odpowiada potrzebie globalnego rejestru pojęć i izolacji danych użytkowników. Wdrożenie na Cloudflare Pages gwarantuje minimalne opóźnienia brzegowe przy znikomych kosztach infrastruktury, a pełne otypowanie TypeScriptem i zdefiniowane konwencje struktury projektu ułatwiają precyzyjną współpracę z agentami programistycznymi AI.
