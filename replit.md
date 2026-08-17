# Asteria Student Management System

A responsive registrar workspace for managing student records with a live PostgreSQL-backed directory, dashboard, and complete CRUD workflows.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm --filter @workspace/student-management run dev` — run the student management web app
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

- `artifacts/student-management/` — React + Vite application with dashboard, directory, and student forms
- `artifacts/api-server/src/routes/students.ts` — student REST handlers
- `lib/api-spec/openapi.yaml` — source of truth for student API contracts
- `lib/db/src/schema/students.ts` — PostgreSQL/Drizzle student table and types
- `lib/api-client-react/src/generated/` — generated React Query client hooks

## Architecture decisions

- The frontend uses generated React Query hooks from the OpenAPI contract rather than handwritten fetch calls.
- Student email addresses are unique at the database level to prevent duplicate records.
- Dashboard totals and grouped course/year counts come from a dedicated summary endpoint so the overview stays data-backed.
- The shared API server owns all `/api` routes; the web app is served at the root artifact path.

## Product

- Dashboard overview with total students, represented courses, year groups, recent records, and quick actions.
- Searchable and filterable student directory.
- Validated add and edit forms for full name, email, phone, course, year, gender, and address.
- Delete confirmation with success/error feedback.
- Responsive desktop and mobile navigation.

## User preferences

No additional preferences recorded.

## Gotchas

- After editing `lib/api-spec/openapi.yaml`, run `pnpm --filter @workspace/api-spec run codegen`.
- The artifact workflows provide `PORT` and `BASE_PATH`; use the managed workflows rather than starting Vite from the workspace root.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
