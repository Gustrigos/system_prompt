System Instruction

Project Profile

- Template
    - Project name: <name>
    - Purpose: <one sentence>
    - Base URLs: frontend <...>, backend <...> 
    - Integrations: <list>


Backend

- Stack
    - Python 3.12
    - Poetry for environment and dependency management
    - FastAPI for the ASGI application and API endpoints
    - PostgreSQL as the database
    - Prisma Client Python for schema and data access
    - Pytest for testing; Ruff + Black + isort for linting/formatting

- Project structure
    - Overview
        - `app/` → FastAPI app with core config/logging, versioned API routers, models, and services
        - `db/prisma/` → Prisma schema and generated client artifacts
        - `tests/` → pytest tests grouped by feature
    - Example

```
backend
├── app
│   ├── main.py
│   ├── core
│   │   ├── config.py
│   │   └── logging.py
│   ├── api
│   │   └── v1
│   │       ├── feature_one.py
│   │       └── health.py
│   ├── models
│   │   └── pydantic_types.py
│   └── services
│       └── feature_one.py
├── db
│   └── prisma
│       └── schema.prisma
└── tests
    ├── test_feature_one.py
    └── test_health.py
```

- Configuration
    - Environment
        - `.env` contains `DATABASE_URL=postgresql://...`
        - Centralize configuration in `app/core/config.py`
    - Database and Prisma
        - `db/prisma/schema.prisma` includes:
            - `generator client { provider = "prisma-client-py" }`
            - `datasource db { provider = "postgresql" url = env("DATABASE_URL") }`
        - Commands:
            - `poetry run prisma generate`
            - `poetry run prisma migrate dev --name init`
        - Use via `from prisma import Prisma`; initialize on startup and close on shutdown

- Commands
    - Setup
        - `poetry env use 3.12`
        - `poetry install`
    - Run
        - `poetry run uvicorn app.main:app --reload`
    - Test
        - `poetry run pytest -q`
    - Lint/format
        - `poetry run ruff check .`
        - `poetry run ruff format .`

- Conventions
    - Favor functional programming. Keep services as pure functions. Avoid classes unless strictly necessary.
    - Use snake_case for Python modules and directories. Filenames are lowercase.
    - Place request/response Pydantic models in `app/models`. Keep domain types separate from transport shapes when helpful.
    - Group API routes by feature under `app/api/v1`. Expose them under the `/api/v1` prefix.
    - Use standard `logging` configured in `app/core/logging.py`.
    - Add tests in `tests/` for each new service and route.

Frontend

- Stack
    - Next.js (App Router)
    - TypeScript
    - Tailwind CSS
    - shadcn/ui for UI primitives
    - ESLint + Prettier

- Project structure
    - Overview
        - `app/` → routing, layouts, pages, API routes
        - `components/ui/` → shadcn-generated primitives (keep filenames lowercase to match shadcn imports)
        - `components/` → higher-level UI (use PascalCase filenames, e.g., `Navbar.tsx`)
        - `hooks/` → custom hooks organized by feature
        - `public/` → static assets
        - Mirror feature paths: components and hooks follow the `app/` route structure. For `app/admin/settings/page.tsx`, use `components/admin/settings/` and `hooks/admin/settings/`.
    - Example

```
frontend
├── app
│   ├── layout.tsx
│   ├── page.tsx
│   ├── globals.css
│   ├── marketing
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── dashboard
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   └── settings
│   │       └── page.tsx
│   └── api
│       └── hello
│           └── route.ts
│
├── components
│   ├── ui
│   │   ├── button.tsx
│   │   ├── card.tsx
│   │   ├── input.tsx
│   │   └── dropdown-menu.tsx
│   ├── marketing
│   │   ├── Banner.tsx
│   │   └── ComponentTwo.tsx
│   ├── dashboard
│   │   └── settings
│   │       ├── ComponentThree.tsx
│   │       └── UserSetting.tsx
│   ├── Navbar.tsx
│   ├── Sidebar.tsx
│   └── ThemeToggle.tsx
│
├── hooks
│   ├── marketing
│   │   ├── useHookOne.ts
│   │   └── useHookTwo.ts
│   └── dashboard
│       └── settings
│           └── useHookOne.ts
│
├── public
│   └── favicon.ico
│
├── .eslintrc.json
├── .gitignore
├── next.config.js
├── postcss.config.js
├── tailwind.config.js
├── tsconfig.json
└── package.json
```

- Configuration
    - Environment
        - Access the backend via `process.env.NEXT_PUBLIC_API_BASE_URL`

- Commands
    - Setup
        - `pnpm install` (or `npm install`)
    - Run
        - `pnpm dev` (or `npm run dev`)
    - Test
        - `pnpm test` (if configured)
    - Lint/format
        - `pnpm lint`
        - `pnpm format`

- Conventions
    - Keep `components/ui` limited to shadcn primitives. Extend them in `components/` rather than modifying directly.
    - Use PascalCase for component filenames outside `components/ui`.
    - Name hooks `useXyz` and colocate by feature under `hooks/`.
    - Use server components by default; add `"use client"` only when necessary.

General Guidelines for Coding Agents

- Follow the structures and conventions above. Do not introduce new patterns without clear justification.
- Keep changes minimal and localized. Do not refactor unrelated code.
- Prefer pure functions and explicit types. Add or update tests when changing business logic.
- Store secrets in `.env`. Do not commit secrets. Use `DATABASE_URL` for the backend and `NEXT_PUBLIC_*` for frontend public variables.

