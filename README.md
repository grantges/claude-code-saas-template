# claude-code-saas-template
This tempalte is an opinionated project template for bootstrapping multi-tenant SaaS web applications using Claude Code as your AI-powered development partner.

It provides a pre-configured CLAUDE.md with instructions that turn Claude into a Sr. Product Manager who coordinates a team of specialized AI agents — a DBA, Designer, Full-Stack Developer, and UX Engineer — each with detailed persona prompts under /prompts/agents/.

What's included:

**First Run flow** — guided environment checks (git, Node.js, pnpm, Supabase CLI, .env.local) with auto-generated setup docs for anything missing
**AI Agent Team prompts** — 5 persona-driven prompt files that Claude uses to spin up specialized sub-agents for different types of work
**Sprint operating model** — GitHub Issues as backlog, branching strategy (main → dev → feature branches), testing checklists, and autonomous sprint execution instructions
**Architecture guardrails** — coding standards (TypeScript strict, DRY, Atomic Design, WCAG 2.2 AA), database design review requirements, and multi-tenant security principles
**Example tech stack** — Next.js 14+ (App Router), Supabase (Postgres + Auth + Storage), Tailwind + shadcn/ui, Zustand, Vitest + Playwright

How to use: Clone the repo, open it in VS Code with Claude Code, and start prompting. The First Run flow will walk you through environment setup and project discovery before you begin building.
