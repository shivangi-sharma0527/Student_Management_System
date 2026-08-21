# Meridian Student Management System

Meridian is a responsive student administration dashboard for managing academic records, reviewing enrollment insights, and handling student CRUD workflows.

## Features

- Live dashboard metrics for enrollment, courses, years, and gender
- Student registry with search, filters, sorting, pagination, and responsive table layout
- Add, view, edit, and delete student flows with confirmation and toast feedback
- Inline form validation for Indian-style phone numbers, email, required fields, and academic options
- Loading, empty, error, and duplicate-email states
- Persistent light/dark theme and record-density preferences
- PostgreSQL-backed data with parameterized Drizzle queries

## Technologies

- Frontend: React + Vite, TypeScript, Tailwind CSS, Recharts
- Backend: Node.js, Express 5
- Database: PostgreSQL with Drizzle ORM
- Contracts: OpenAPI with generated React Query and Zod helpers

## Architecture

The frontend calls the Express REST API through `fetch`-backed generated hooks. The API validates request and response data, runs parameterized queries through Drizzle, and PostgreSQL remains the source of truth.

## API endpoints

| Method | Endpoint | Purpose |
| --- | --- | --- |
| GET | `/api/healthz` | Health check |
| GET | `/api/students` | List student records |
| POST | `/api/students` | Create a student |
| GET | `/api/students/:id` | Read one student |
| PUT | `/api/students/:id` | Update a student |
| DELETE | `/api/students/:id` | Delete a student |
| GET | `/api/dashboard/summary` | Enrollment metrics and grouped counts |

## Database structure

The `students` table stores:

`id`, `full_name`, `email`, `phone`, `course`, `year`, `gender`, `address`, and `created_at`.

Email is unique and all API input is validated before database writes.

## Installation and local development

1. Install dependencies with `pnpm install`.
2. Set `DATABASE_URL` to the provided PostgreSQL connection string.
3. Push the schema with `pnpm --filter @workspace/db run push`.
4. Start the API with `pnpm --filter @workspace/api-server run dev`.
5. Start the frontend with `pnpm --filter @workspace/student-management run dev`.

The workspace workflows provide `PORT` and `BASE_PATH` for normal Replit previews.

## Screenshots

The running dashboard preview is the source of truth for the current interface. It includes the overview dashboard, student registry, responsive navigation, forms, and settings views.

## Future enhancements

- Role-based staff access and audit history
- CSV import/export
- Attendance and fee modules
- Server-side pagination for larger institutions

## Internship task reference

This implementation follows the supplied Advanced Upgrade Prompt for a real Student Management System, including full CRUD, dashboard analytics, responsive design, validation, accessibility considerations, and database-backed behavior.