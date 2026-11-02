---
framework_version: 1.0.0
---

# Agent Guidelines: AI Job Search

This workspace is structured to manage job search activities, scraper tools, CVs, cover letters, and interview preparation.

## Thin-Pointer Design (Single Source of Truth)

To prevent duplication and configuration drift across different AI agent frameworks (Claude Code, Google Antigravity, Codex, Cursor, Gemini CLI, etc.), this workspace uses a unified thin-pointer design. All agent runtimes should load the canonical specifications and candidate profiles from the files and directories below:

1. **Personal Candidate Profile:**
   - The candidate profile, contact details, education, and target preferences are defined in [CLAUDE.md](CLAUDE.md) and the individual profile methodology files under [.claude/skills/job-application-assistant/](.claude/skills/job-application-assistant/) (specifically `01-*.md` etc.).
2. **Canonical Workflow Specifications:**
   - The step-by-step instructions and triggers for tasks (setup, scrape, rank, apply, upskill, interview) are defined in the [.claude/](.claude/) directory (specifically under `.claude/skills/` and `.claude/commands/`).
   - Do not duplicate these rules or specifications. Treat `.claude/` files as the single source of truth.
3. **Portal Search Skills:**
   - Job-portal search CLIs live under [.agents/skills/](.agents/skills/) in the portable Agent Skills format (with a `SKILL.md` per portal). Codex and Antigravity discover these automatically; the `/scrape` workflow in [.claude/skills/job-scraper/](.claude/skills/job-scraper/) orchestrates them.

## OpenAI Codex entry point

For Codex, use the repo-local skill at `.agents/skills/job-workflow/SKILL.md` and the setup guide at `CODEX.md`. Invoke the workflow as `$job-workflow setup`, `$job-workflow scrape South Africa`, or `$job-workflow apply <posting-url>`. The workflow specs in `.claude/` are shared canonical specifications, **not** a requirement to run Claude Code.

Codex does not automatically honor Claude-specific slash commands, frontmatter `allowed-tools`, named agents, or MCP connectors. The Codex adapter translates these only where equivalent capabilities are actually available. Do not claim independent agent review, fetched evidence, compiled PDFs, or verified checks unless they occurred.

**Personal-data safety:** This repository is public. The profile stored in tracked files (including `CLAUDE.md` and candidate-profile guidance) must never be committed or pushed with identifying details to this public fork. Before running setup, require a choice of a private non-fork remote or a local-only unpushed checkout. Never submit an application or send external messages without the required user approval.
