# Codex Quick Start — AI Job Search

This fork supports **OpenAI Codex** as an agent entry point. Claude Code is **not required** for the Codex route. The original Claude commands remain available for upstream compatibility.

## 1. Open the repository in Codex

Clone `https://github.com/tdollar15/ai-job-search` locally, open its root folder in Codex Desktop / IDE, or run `codex` from the repository root in a terminal.

Codex reads `AGENTS.md` for project instructions and discovers the `job-search` skill under `.agents/skills/job-workflow/SKILL.md`. Mention it using `$job-workflow` in a prompt (or choose it from the skills selector). If it does not appear, restart Codex after updating the checkout.

## 2. Start with these requests

| What you want | Prompt in Codex |
|---|---|
| Build a candidate profile | `$job-workflow setup` |
| Find roles matching your profile | `$job-workflow scrape South Africa` |
| Rank the latest results | `$job-workflow rank` |
| Evaluate a posting and tailor application drafts | `$job-workflow apply <job-posting-url>` |
| Prepare for an interview | `$job-workflow interview` |
| Record an outcome or follow-up | `$job-workflow outcome` |
| Identify competency gaps | `$job-workflow upskill` |
| Create an offline tracker dashboard | `$job-workflow html-report` |
| Add a job-board integration for your market | `$job-workflow add-portal <job-board-url>` |

Other supported actions: `expand`, `gmail-sync`, `notion-sync`, `add-template`, and `reset`.

The adapter reads the existing step-by-step instructions in `.claude/commands/` and `.claude/skills/`. It substitutes Codex tools for Claude-specific tool names; it does **not** require installing Claude Code or running commands like `/setup` in Codex.

## 3. Prerequisites

- **Codex** — Desktop, IDE extension, or CLI.
- **Python 3.10+** — runs safety, deduplication, ranking, and verification scripts.
- **Bun** — runs portal CLI implementations under `.agents/skills/*/cli/`.
- **LaTeX** — for the stock CV and cover-letter PDF templates: `lualatex` for CVs, `xelatex` for cover letters.
- **pypdf** (optional) — PDF text-layer/ATS checks.

To install the portal CLI dependencies after cloning:

```bash
python3 tools/install_portal_clis.py
```

On Windows use `python` instead of `python3` when needed. See `SETUP.md` for platform-specific Bun/LaTeX guidance. Do not install Claude Code just because it appears in the original setup guide.

## 4. Protect your personal details **before setup**

**This is a public GitHub fork.** The original `setup` workflow writes real names, contact details, work history, preferences, and salary expectations to **tracked** files. `.gitignore` cannot protect content written to an already tracked file. Never commit and push a populated candidate profile to this public fork.

Use a **private, non-fork repository** for personal job-search data, or keep a local checkout unpushed. When Codex runs `setup`, it must check the origin and ask before writing sensitive profile information. Avoid adding personal CV documents to a public GitHub repository.

## 5. Market setup: South Africa

The repository ships LinkedIn and Freehire integrations that can search across markets. Its four Denmark-specific portal integrations are disabled by default. To add South African boards, use:

```text
$job-workflow add-portal <South-African-job-board-URL>
```

Review a new portal's terms, `robots.txt`, and generated CLI before using it. Do not assume bulk automated access to LinkedIn or any third-party board is permitted. The adapter does not install South African portal integrations automatically.

## 6. Important limitations

- Codex does **not** execute Claude slash commands, read Claude-only `allowed-tools` grants, or automatically provide Claude's named agents. The `$job-workflow` skill maps those steps to capabilities actually available in Codex.
- A distinct reviewer/fetcher agent is used only when the active Codex session supports delegation; otherwise review is a single-agent check and is labelled accordingly.
- Gmail and Notion require the corresponding connector configured **in Codex**. They are not included by installing this repository.
- The application flow drafts documents and tracks outcomes. It does **not** silently submit applications.
- Actual end-to-end job searching depends on network access, portal availability, external tools, LaTeX installation, and having a completed, private candidate profile.

## 7. Canonical sources

- `AGENTS.md` — project-wide agent instructions
- `.agents/skills/job-workflow/SKILL.md` — Codex orchestration adapter
- `.claude/commands/` and `.claude/skills/` — established workflow specifications
- `.agents/skills/*-search/` — portal search CLIs
- `CLAUDE.md` — historical name for candidate profile (not a requirement to use Claude Code)
