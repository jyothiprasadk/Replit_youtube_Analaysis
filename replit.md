# LearnScope AI

LearnScope AI compares YouTube learning sources against a student's target syllabus and explains coverage, evidence, learner feedback, and gaps.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/learnscope-ai/src/App.tsx` — local demo dashboard and routed analysis flows
- `artifacts/learnscope-ai/src/index.css` — product theme and responsive styling
- `artifacts/learnscope-ai/src/components/ui/` — reusable scaffolded UI primitives
- `artifacts/learnscope-ai/.replit-artifact/artifact.toml` — artifact workflow and preview routing

## Architecture decisions

- Phase 1 is frontend-first and uses clearly labeled fictional demo analysis data so the product is useful before the AI pipeline is connected.
- The main dashboard keeps source-level comparison and video-level evidence together; multi-video sources are not collapsed into a single video.
- New Analysis is a local, multi-step flow designed to accept transcript inputs and later hand a structured payload to an n8n webhook.
- Quantitative demo metrics are presented as evidence-backed UI values; live scoring and persistence belong in later backend phases.

## Product

- Demo dashboard with a recommendation, source comparison, topic coverage matrix, topic evidence detail, learner signals, gaps, and a learning roadmap.
- Interactive new-analysis setup for objective, topics, learning sources, videos, transcript status, and review.
- History, learning gaps, and settings surfaces ready for the next implementation phases.

## User preferences

None recorded.

## Gotchas

- Demo data is fictional and intentionally labeled in the UI; do not present it as live YouTube analysis.
- The web workflow supplies `PORT` and `BASE_PATH`; run the managed workflow rather than starting Vite manually.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
