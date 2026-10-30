# CONVENTIONS.md — Coding Style & Canonical Commands

<!-- note (setup): Fill from the project's real configs (.editorconfig, eslint/ruff/biome/go fmt config etc.). Every command here MUST be verified to exist in the manifest/scripts before it is written down. Keep < 120 lines. -->

## Shell for this repo

**Shell:** {{SHELL}} (e.g., PowerShell on Windows projects, bash elsewhere) — all commands below use that shell's syntax and are expected to run from the repo root unless a line says otherwise.

## Canonical commands (the only ones agents may assume exist)

| Purpose | Command | Notes |
|---|---|---|
| Install deps | `{{INSTALL_CMD}}` | {{LOCKFILE_NOTE_OR_NA}} |
| Run / dev server | `{{RUN_CMD}}` | default port {{PORT_OR_NA}} if any |
| Build (if separate from run) | `{{BUILD_CMD_OR_"no build step"}}` | output goes to `{{OUT_DIR_OR_NA}}` |
| Lint | `{{LINT_CMD_OR_"none configured — ask before adding one"}}` | |
| Format | `{{FORMAT_CMD_OR_"none configured — ask before adding one"}}` | run after edits only if this row is real |
| Migrate / schema (if any) | `{{MIGRATE_CMD_OR_NA}}` | destructive variants always need approval (see `core/AGENTS.md`) |

Anything not in this table is out-of-contract: an agent that needs such a command must ask first.

## Code style

- Formatting: {{FORMATTER_AND_SETTINGS}} (line length, tabs/spaces, quote style — mirror the config file, don't restate what it already enforces)
- Naming: files `{{FILE_NAMING}}`; functions/vars `{{FN_VAR_STYLE}}`; types/classes `{{TYPE_STYLE}}`
- Imports/dependencies: import order or grouping rules if enforced; **no new dependency without explicit approval** (see boundaries in `core/AGENTS.md`)
- Comments & docs: {{COMMENT_POLICY, e.g., "comment only non-obvious intent; public API gets doc comments"}}
- Errors / logging: {{ERROR_LOGGING_CONVENTION_OR_"follow existing patterns in codebase"}}

## Commit-touching style (cross-ref)

Branch/commit/PR conventions live in `core/WORKFLOW.md` — not here. Keep this file about *code and commands only*.
