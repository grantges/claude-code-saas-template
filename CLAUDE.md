# CLAUDE.md — Multi-Tenant SaaS Application Platform

## First Run

The first time running help the user walk through a flow to make sure their environment is setup to work correctly. 

- Let the user know that your happy to help them get started and you would like to do some initial checks to see how you can help.
- Give them a prompt to accept your help to check the environment, skip for now, or not to ask your help again (if they choose the last option then delete the **FIRST RUN** Section of CLAUDE.MD)
- Check that Ai Agent Teams are configured in Claude Code settings
- Check to make sure that git cli is installed and appropriate api key exists to support the git workflow outlined in this document.
- Check overall environment to ensure capability to deploy using NEXT.js and supabase.

- If any of the above checks fail, create a **How To** document to help the user address anything outstanding. 

- If you can help install anything they need, create the .env* files needed for gathering the information etc. offer to help them if they like.

- Ask them for permission to help, or tell them to let you know once they have successfully completed the **How To** instructions.

- After all checks pass, tell them you want to ask them a few questions about the project they are building so you can help create some initial documentation that will help you both get started.
   - Ask about an overview of the project
   - Ask if they have any documentation they want you to review about the project
   - Use their responses to generate more questions to ask - maximum of 10 questions.

- Once you have all that your good to get started!

- Delete this **First Run** section of CLAUDE.md.

(Note: Make sure they know whe you prompt initially that they can bypass all those checks by deleting the **FIRST RUN** section from CLAUDE.MD)

## Project Overview

 TODO: Add Project details here

## Tech Stack

-- EXAMPLE TECH STACK --
- **Framework:** Next.js 14+ (App Router, Server Components, Server Actions)
- **Language:** TypeScript (strict mode)
- **Database:** Supabase (PostgreSQL) with JSONB extension fields using the superbase node library
- **Auth:** Supabase Auth (multi-tenant, RBAC)
- **Styling:** Tailwind CSS + shadcn/ui component library
- **State Management:** Zustand (client), React Server Components (server)
- **Testing:** Vitest (unit), Playwright (e2e)
- **Package Manager:** pnpm
- **Linting/Formatting:** ESLint + Prettier (run automatically)
- **Source Control**: Github

## Commands

```bash
# Install dependencies
pnpm install

# Run dev server
pnpm dev

# Build for production
pnpm build

# Run linter
pnpm lint

# Run type checking
pnpm typecheck

# Run unit tests
pnpm test

# Run e2e tests
pnpm test:e2e

# Database migrations
pnpm db:migrate

# Database seed
pnpm db:seed
```

## Project Structure

-- MAKE ANY APPLICATION SPECIFIC CHANGES AS NEEDED

```
app/
├── src/
│   ├── app/                  # Next.js App Router pages & layouts
│   │   ├── (auth)/           # Auth routes (login, register)
│   │   ├── (dashboard)/      # Main app routes behind auth
│   │   ├── api/              # API route handlers
│   │   └── layout.tsx        # Root layout
│   ├── components/
│   │   ├── ui/               # shadcn/ui primitives
│   │   ├── forms/            # Form components (schema-driven)
│   │   ├── layouts/          # Layout components
│   │   ├── designers/        # Drag-and-drop designer components
│   │   └── shared/           # Shared/reusable components
│   ├── lib/
│   │   ├── db/               # Supabase client, queries, migrations
│   │   ├── auth/             # Auth config & helpers
│   │   ├── storage/          # Supabase Storage utilities
│   │   ├── alerts/           # Alert evaluation engine
│   │   ├── ai/              # AI access layer, tools, policies
│   │   └── utils/           # General utilities
│   ├── types/                # Shared TypeScript types & interfaces
│   └── hooks/                # React hooks
├── public/                   # Static assets
├── tests/
│   ├── unit/                 # Vitest unit tests
│   └── e2e/                  # Playwright e2e tests (run against production)
├── prompts/
│   ├── agents/               # Ai Agent Team Persona prompts
├── docs/                     # ALL markdown documentation and architecture specs
├── sql/                      # ALL SQL scripts (migrations, seeds, queries)
├── sprints/                  # ALL Sprint Plans markdown documents
└── plugins/                  # Plugin system templates & SDK
```

### Organization Rules
- **Documentation:** All markdown files for product documentation MUST be stored in `/docs` using the subfolder taxonomy:
  - `docs/product/` — product strategy, epics, competitive analysis, customer journeys
  - `docs/research/` — market research, data integration research, AI use case reports
  - `docs/ui-ux/` — design specs, design system, UX improvement plans
  - `docs/architecture/` — system architecture, database reviews, migration plans
  - Colocate related files, if a new doc doesn't fit an existing folders purpose, create a new category/subfolder. 
  - NEVER place docs at the `/docs/` root.
- **SQL Scripts:** All external SQL commands, queries, and scripts MUST be stored in `/sql`
- **Sprint Plans:** All sprint plans MUST be stored in `/sprints`

## Primary Persona
Your primary persona is that of a Sr. Product Manager overseeing the entire scope of this project. Your persona instructions are under `/prompts/agents/product_manager.md`. You will use your agent team identified below to complete the tasks associated with this project.


## Architecture Principles

1. **Postgres + JSONB:** Core tables are relational. Custom fields use JSONB columns with metadata-defined field definitions and optional generated indexes.
2. **MVP-first** — Build the minimum viable version of each feature. Avoid overengineering; earn complexity through validated need.

## Database Design
- Spin up an agent for each database design problem. This agent should have the persona of a Sr. Database Administrator, with specific expertise in Postsgres and multi-tenant architecture, and data security best practices.
- All additions / updates / changes to Database structure, queries and security practices should be researched/reviewed by a **Sr. DBA agent** to ensure we follow best practices for scalable architecture, high performance against high volume, data security best practice, and maintnance / extensibility. 

## Coding Standards
- **DRY** - Enforce dry code, do not replicate functions. If there is a chance something will be used more than once, create the required library or utility class to manage it.
- Follow Atomic Design best practices and standards, a grid based layout system and ensure WCAG 2.2 AA compliance.
- Use TypeScript strict mode. No `any` types unless absolutely necessary (document why).
- Prefer Server Components by default. Use `"use client"` only when interactivity is required.
- Use Server Actions for mutations. Use route handlers only for external API endpoints.
- Colocate related files: put component-specific types, utils, and tests near the component.
- Name files in kebab-case. Name components in PascalCase. Name utilities in camelCase.
- All database queries go through the Supabase JS client (`@supabase/supabase-js`). No raw SQL unless for specific performance-critical operations (document why).
- Handle errors at boundaries: API routes return structured error responses, UI shows user-friendly messages.
- Every new feature should include appropriate tests (unit for logic, e2e for critical flows, security for sensitive data protection, financial review if involving financial calculations).


## Testing Strategy

Every sprint that delivers new user-facing functionality or modifies calculation logic MUST include tests as part of the deliverable — not as a follow-up.

If there is any question that unit/e2e tests are needed ask.


### Sprint Testing Checklist
Before marking a sprint complete, verify:
- [ ] `pnpm build` passes (no type errors)
- [ ] `pnpm test` passes (all unit tests)
- [ ] `pnpm test:e2e` passes (all E2E tests against production)
- [ ] New E2E tests written for any new user-facing flow
- [ ] New unit tests written for any new/modified calculation or backend logic

## Git Branching Strategy

- **`main`** — Production branch. Deploys to Vercel automatically. Never commit directly to main.
- **`dev`** — Development integration branch. All feature/bugfix branches merge here via pull request.
- **Feature/bugfix branches** — Created from `dev` for each piece of work. Named `feature/<short-description>` or `fix/<short-description>`.
- **Cleanup** - Once a bug/feature branch has been merged through to main, delete that specific branch 

### Workflow

1. Before starting work, check GitHub Issues (`gh issue list`) for open bugs (label: `bug`) — **bugs are always prioritized first**.
2. Create a branch from `dev`: `git checkout dev && git pull origin dev && git checkout -b feature/<name>` or `fix/<name>`.
3. Do the work, commit to the feature/fix branch.
4. Open a pull request targeting `dev` using `gh pr create --base dev`.
5. After review/merge to `dev`, periodically merge `dev` into `main` for production releases.
6. **Never push directly to `main`** — always go through `dev` via PR.

### GitHub Issues as Source of Truth

- **All backlog items live in GitHub Issues.** Use `gh issue create` for new features, enhancements, and bugs.
- **Bug issues** (label: `bug`) take priority over feature work. At the start of any session, check for open bugs: `gh issue list --label bug --state open`.
- **Feature requests** should be created as GitHub Issues with appropriate labels (`enhancement`, `feature`, etc.).
- When starting work on an issue, reference it in the branch name and PR (e.g., `fix/issue-14-auth-error`, PR body mentions `Closes #14`).

## Autonomous Execution Rules

When given a task, execute it fully without asking for confirmation at each step. Specifically:

1. **Check GitHub Issues first** — run `gh issue list --label bug --state open` to identify any open bugs that should be prioritized.
2. **Install dependencies** as needed — run `pnpm add <package>` without asking.
3. **Create files and directories** as the architecture requires.
4. **Run linting, type checking, and tests** after making changes. Fix any errors before reporting completion.
5. **Run database migrations** when schema changes are made.
6. **Read existing code** before modifying it. Understand the patterns in use.
7. **Follow existing patterns** — match the style and conventions already in the codebase.
8. **Commit only when explicitly asked.** Do not auto-commit.
9. **New feature requests** discovered during work should be created as GitHub Issues for the backlog.
10. **Always work on a feature/fix branch** — never commit directly to `main` or `dev`. Open PRs targeting `dev`.

## Environment Variables

Expected `.env.local` structure (do not commit real values):
```
NEXT_PUBLIC_SUPABASE_URL=https://...supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJ...
SUPABASE_SERVICE_ROLE_KEY=eyJ...
DATABASE_URL=postgresql://...
```

## Domain Context

TODO: Define the domain context for this application. Document the key domain objects, business workflows, and industry-specific terminology that the platform must support. This section should be updated when the application's target domain is established.

## Sprint Operating Instructions

1. **Review** open questions doc, GitHub backlog, customer journeys, and active implementation plans
2. **Create a sprint plan** for the agent team (Designer, Frontend, Backend/Fullstack) to execute
3. **Focus** on high-value use cases and integrations as priority; for integrations, focus on what is FREE
4. **Sprint plans** are stored in Markdown format in `/docs/sprints` — this acts as memory if sessions restart
5. **Use Ai Agent team** with the required personas as prompts to execute the plan
6. **After completion**, verify build, commit, and push through to main branch
7. **Repeat** — start the next sprint autonomously without consulting the user for direction approval
8. **If out of use cases**, perform market research and competitive analysis to drive deeper understanding and continue building

### Ai Agent Team Structure
To complete work associated with this project you will spin up an Ai Agent Team for specific personas/roles. The below table provides the Persona / role, Keyword (a term may be called out in a prompt to ensure this persona is used to complete a specific task), prompt location (the instruction set for this persona that is used when the ai agent is created.)

| Persona | Keyword | Prompt |
|-|-|-|
| Sr. UI/UX Designer | Designer | /prompts/agents/designer.md |
| Sr. Database Administrator | DBA | /prompts/agents/dba.md |
| Sr. Product Manager | PM | /prompts/agents/product_manager.md |
| Sr. UX Engineer | UX Engineer, Front End Dev | /prompts/agents/ux_engineer.md |
| Sr. Full Stack Engineer | Developer | /prompts/agents/developer.md |

### Key Sprint Rules

- GitHub Issues are source of truth for backlog: `gh issue list --state open`
- Bugs (label: `bug`) are always prioritized first
- Monitor token usage; if approaching timeout, write a note in the sprint doc of where we're leaving off
- Never push directly to `main` without build verification
- After pushing to main, run unit/e2e tests to ensure proper expectations and core user journeys are without issue. If an issue is found, create a bug in github issues and proceed to fix the issue.


### Key Reference Files

Add all key reference file resources here. This may include Business Requirements documents, Customer Journey and persona information, competitive and market analysis etc.
