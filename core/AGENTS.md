# AGENTS.md — Master Rules & Operating Contract

<!-- note (setup): This file is rewritten in place during the KICKSTART interview. It must end as the index and contract for every agent session on this repo. Keep < 120 lines, zero placeholders after setup. -->

## What this project is

{{ONE_LINE_PURPOSE}} — see `core/PROJECT.md` for stack & architecture.

## File map (read what you need)

| File | When to consult it |
|---|---|
| `AGENTS.md` (this file, root copy) or `core/AGENTS.md` | Always first. Contract + index. |
| `core/PROJECT.md` | Before touching architecture, adding dependencies, or asking "where does X live?" |
| `core/CONVENTIONS.md` | Before writing or editing code; for all build/lint/run commands. |
| `core/TESTING.md` | Whenever a change is testable; before reporting a task done. |
| `core/WORKFLOW.md` | Before any git operation, branch decision, or PR work. |

## Operating rules (every session)

1. Read this file first. Then the sibling file(s) for the kind of task you are doing — do not rely on memory from another session.
2. Commands: use only the canonical commands listed in `core/CONVENTIONS.md` § Commands and `core/TESTING.md`. If a needed command does not exist there, ask before improvising one.
3. Scope discipline: make the smallest change that fulfills the request. No drive-by refactors, no unasked dependency additions.
4. After any task that adds or removes: a source directory, a manifest entry, a script target, an environment variable — update the affected `core/*.md` file in the same change set (see Update rule).

## Boundaries — what needs explicit user approval

**Allowed without asking:** {{ALLOWED_ACTIONS_BULLETS}}
*(default if left to setup: reading files; editing tracked source inside this repo; running install/build/lint/test commands as documented above.)*

**Always ask first (destructive / external):** {{MUST_ASK_ACTIONS_BULLETS}}
*(defaults that survive setup unless explicitly relaxed: deleting any file or directory not created in the current session; any database migration, drop, or bulk data change; installing a new dependency or changing pinned versions materially; `git push --force`, rebasing shared history, amending pushed commits; modifying CI configuration, secrets, credentials, or `.env*` files beyond adding a documented key.)*

**Never:** fabricate command output or test results; commit files the user has git-ignored (check before `git add -A`); expose secrets to chat logs — reference them by name/path only.

## Update rule (self-maintaining docs)

These rules are living documents. When a change makes any of them stale (new dependency, renamed script, new directory, changed test command), updating the relevant file is **part of that change**, not optional follow-up. State in your final message which rule files you updated and why — or state "no rule updates needed" so the user knows you checked.
