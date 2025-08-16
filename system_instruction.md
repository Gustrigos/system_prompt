System Instruction:

We will use the following stack for the backend:
- Poetry for managing environments
- Python 3.12
- FastAPI for API endpoints and main.py
- Prisma for schema set up with PostgresSQL

The structure of the backend:
- Main.py
- App
    - API
        - endpoints.py
    - Models
        - pydantic_types.py
    - Services
        - business_logic1.py
        - business_logic2.py
    - Test
        - test_for_business_logic1.py
        - test_for_business_logic2.py

Instructions:
- Use functional programming. 


We will use the following stack for the frontend:


For the frontend, please structure the code according to the following file structure:

Highlights:

* app/ → routing, layouts, pages, API routes.

* components/ui/ → shadcn-generated primitives (buttons, cards, dropdowns).

* components/ → higher-level UI (navbars, sidebars, etc.).

* components/feature1 → Components should be separated into features directly related to the app routing file structure, so for the page in `app/admin/settings` the corresponding components should be located in the `components/admin/settings` folder

* hooks/ → custom hooks folder. should not contain anything directly unless shared by multiple feartures

* hooks/fearure1 → custom hooks.

* public/ → static assets.


Here an example file structure:

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
│   │   |── banner.tsx
│   │   └── component2.tsx
│   ├── dashboard
│   │   └── settings
│   │       |── component3.tsx
│   │       └── user-setting.tsx
│   ├── navbar.tsx
│   ├── sidebar.tsx
│   └── theme-toggle.tsx
│
├── hooks
│   ├── marketing
│   │   |── hook1.tsx
│   │   └── hook2.tsx
│   └── dashboard
│      └── settings
│          └──hook1.tsx
|
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

