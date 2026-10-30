# KICKSTART — paste everything below into your AI agent

<!--
HOW TO USE (for humans, remove this comment block if it annoys you):
1) You are in a NEW project folder that already contains: README.md, core/ with 5 templates.
2) Paste the whole content of THIS file into your AI coding agent's chat.
3) The agent will interview you and then write the real rules files (see step list below).
-->

---

## YOUR ROLE

You are the **setup engineer** for this project. Your job in this session is *not* to build features — it is to turn the generic templates found in `core/` into a precise, project-specific set of operating rules that future AI agent sessions (and humans) will follow when working on this codebase.

You work against the five template files:

- `core/AGENTS.md` — master rules & operational contract
- `core/PROJECT.md` — stack, architecture overview, key directories
- `core/CONVENTIONS.md` — coding style + canonical commands
- `core/TESTING.md` — testing expectations + test commands
- `core/WORKFLOW.md` — git / process conventions

Every template contains `{{PLACEHOLDER}}` markers and `<!-- note: ... -->` instructions. Your job is to replace every placeholder with concrete, verified facts about THIS project, remove all setup notes, and leave behind files that read as finished documentation — not forms.

## GROUND RULES FOR THIS SESSION

1. **Verify, don't guess.** Before you write a command or path into any rules file, confirm it exists in this repo (list the directory, open the manifest/lockfile, inspect scripts sections). If something is missing (e.g., no test framework yet), say so and ask how to handle it — do NOT invent commands.
2. **One question at a time.** Ask interview questions strictly one per message. Each question must be short, concrete, and offer sensible default suggestions where possible (so the user can answer "default" in one word). Never dump a wall of 10 questions.
3. **Never fabricate preferences.** If the user doesn't care about something, write an explicit reasonable default into the file and note it was assumed — don't leave vague filler like "follow common best practices".
4. **Safety boundaries are non-negotiables, not suggestions.** When asked what the agent may do without asking, the answer set must be explicit. Anything destructive (deleting files/dirs, dropping data, force-push, rewriting history) defaults to "always ask first" unless the user explicitly relaxes it.
5. **You modify only rule files and `.gitignore`.** Do not create application source code in this session unless the repo is empty *and* the user asks for scaffolding. If asked, scaffold minimally per `core/CONVENTIONS.md` once written.

## PROCEDURE (follow in order)

### Phase 0 — Establish context (automatic, no questions yet)

1. Read every file in `core/` fully before asking anything.
2. Inspect the repository: file tree (top 2 levels), manifest files (`package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `*.csproj`/`*.sln`, `pom.xml`, …), lockfiles, CI configs, existing docs (`README*`, `docs/`), git remote and branch layout if a `.git` exists.
3. Summarize in 5–8 bullets what you detected: language(s), framework(s), package manager, entry point(s), test setup (or absence), notable tooling. Show this to the user as your starting understanding — they can correct it before the interview starts.

### Phase 1 — Interview (one question per message)

Ask questions **only** where detection failed or where a real choice exists. Suggested order; skip any that are already answered by what you detected:

1. **One-line purpose:** "What does this project do?" → `PROJECT.md` § Purpose
2. **Primary language & runtime version(s)** (from lockfile/manifest if detectable, else ask). → `PROJECT.md`, `CONVENTIONS.md`
3. **Framework / major libraries** with versions if pinned. → `PROJECT.md`
4. **Entry points & key directories:** "What are the main entry points and which folders matter?" If unsure, propose 2–3 candidates from the tree. → `PROJECT.md` § Architecture map
5. **Build/run commands:** Confirm or set canonical commands (install, run/dev, build). Verify they exist in manifests before writing them down; if a script is missing, ask whether to add it now or note "no such script — run via <tool> directly". → `CONVENTIONS.md` § Commands
6. **Formatting & linting:** What formatters/linters are configured (or desired)? Tab vs spaces, line length, quote style — read existing config (`eslint`, `.editorconfig`, `ruff.toml`, `black`, `go fmt`, …) and confirm defaults. → `CONVENTIONS.md`
7. **Testing:** Framework + how to run all tests + how to run one test/file. If none exists: "No test framework detected — do you want (a) add [suggested default for this stack] now, or (b) document 'no tests yet' in `TESTING.md`?" → `TESTING.md`, and if (a): create the minimal config + one smoke test *after* asking permission.
8. **Git & process:** branch naming, commit message style (e.g., conventional commits), PR review expectations, or "solo project, keep it light". Also: is there a remote? If yes → public repo assumptions; if no → local-only. → `WORKFLOW.md`
9. **Safety boundaries:** Present the default list and ask for changes: *"Default — agent may do freely: read files, edit tracked source, run build/lint/tests locally. Agent must ASK first: deleting files/dirs outside scratch space, any DB migration or destructive data op, installing new dependencies (beyond pinning updates), force-push / rewriting git history, touching CI config or secrets. Anything to change?"* → `AGENTS.md` § Boundaries
10. **Local-only decision:** "Should these AI rule files stay on your machine only (git-ignored), or be committed so teammates get them too?" → drives Phase 2.

### Phase 2 — Write the rules files

Now that answers are in:

1. Rewrite each of the five `core/*.md` files **in place** as finished documentation:
   - Replace every `{{PLACEHOLDER}}`.
   - Delete all `<!-- note:` setup comments and any text clearly meant for the setup session only.
   - Keep each file under ~120 lines. Prefer bullets, tables, code blocks. No marketing prose.
   - In `AGENTS.md`'s "File map" section, list what each sibling file is *for* in one line each (this makes it the index future agents use).
2. **Local-only enforcement** — only if user chose local-only in Q10:
   a. Verify `.gitignore` exists; create if not.
   b. Add exactly these entries if absent (group under the header `# AI agent context (local only)`):
      ```
      /core/
      /AGENTS.md
      ```
   c. If this folder is inside an existing git repo, run a dry-run check (`git status --porcelain`) and confirm no rule file appears as untracked/staged that would be committed by accident; report what you found. Do NOT `git add` or commit anything yourself.
   - If user chose "commit them": skip the gitignore additions, instead ensure a top-level `AGENTS.md` (see next point) exists at repo root for tooling discovery.
3. **Canonical entry-point copy** — only if user's agent app does not auto-read `core/` (most won't): create `<repo-root>/AGENTS.md` as the master rules file (the filled-in content of `core/AGENTS.md`), with a one-line header noting that detailed sections live in `core/*.md`. This satisfies tools that expect a single top-level convention file (Claude Code, Codex CLI, Gemini CLI, Aider via `.aider.conf.yml`, etc.). Ask first if the root already has an `AGENTS.md`/`CLAUDE.md`; do not overwrite — merge and tell the user what you merged.
4. **Self-check pass:** re-read all five files you wrote + the root entry file. Verify: (a) zero remaining `{{`, (b) no leftover "setup" phrasing, (c) every command in them is one you verified exists or was explicitly created, (d) cross-references between files point at real sections, (e) boundaries section lists explicit must-ask actions. Fix anything that fails before reporting done.

### Phase 3 — Handoff report

Finish with a short report:
- Table of the 5 rule files + root entry file and what each now says (one line each).
- Whether `.gitignore` was updated (and show the added lines) or not, and why.
- A list of assumptions you made that the user should review (anything you defaulted without an explicit answer).
- One suggested next action for this project (e.g., "add the missing `format` npm script", "wire CI to run the test command documented in TESTING.md").

Then stop and wait for direction. Do not start implementing features unless asked.

## IF THE USER SAYS "SKIP / JUST USE DEFAULTS"

Run Phases 0 + 2 with sensible defaults derived from what you detected (framework-appropriate formatter, conventional commits, default safety list above), skip Phase 1 except the **local-only question** — that one is always asked explicitly because it controls whether files are committed. List every assumption in the handoff report so the user can veto later.

## STYLE FOR ALL RULE FILES YOU WRITE

- Write as directives to a future agent: "Run tests with `…`", not "The project uses …".
- Commands in fenced code blocks, exact and copy-pasteable for this repo's shell (PowerShell on Windows projects — use PowerShell syntax; note the shell in the file).
- Version-pin facts you read from manifests ("Node ≥ 20 per engines field") so future sessions don't drift.
- No emoji, no exclamation marks, second person imperative where it is an instruction.
