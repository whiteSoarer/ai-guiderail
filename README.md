# AI Guiderail Boilerplate (Kickstart Kit)

A **portable set of rules and instructions** for AI coding agents, designed so that every new project starts with a consistent workflow from day one. No installs, no plugins, no app lock-in — just files you copy into your project root.

## The principle

For each new project you:

1. Copy everything in this folder to the **root of the new project**.
2. Paste the prompt in `KICKSTART.md` into whatever AI agent / IDE assistant you like (Claude Code, OpenAI Codex, Gemini CLI, Cursor, Windsurf, Cline, Aider, ...).
3. Answer a short interview about your stack and preferences.
4. The agent fills in the rule files from the templates in `core/`, and — if you choose to keep AI interaction **local** — makes sure they are never committed.

From then on, any agent working on that project reads those rules before acting: same conventions, same commands, same safety boundaries, regardless of which app or model does the work.

## What's in this kit

| Path | Role |
|---|---|
| `KICKSTART.md` | **The instruction prompt.** Copy its content into your AI agent to start setup. This is the only file you "use" by hand. |
| `core/AGENTS.md` | Master rules template: operating contract, safety boundaries, file map, update rule. The canonical entry point most agents read first. |
| `core/PROJECT.md` | Template: what this project *is* — stack, architecture overview, key directories. |
| `core/CONVENTIONS.md` | Template: coding style, naming, formatting, and the exact commands for build/lint/run/migrate. |
| `core/TESTING.md` | Template: how tests are written, run (full + targeted), and when they are required. |
| `core/WORKFLOW.md` | Template: git conventions, branch & commit rules, PR expectations, "definition of done". |
| `release/` | Empty by design — for you to publish/share a snapshot of this kit (e.g., zip or tag). Keep it empty while developing the boilerplate itself. |

All files in `core/` are **templates with `{{PLACEHOLDER}}` markers**. They contain instructions for both humans and agents. The setup interview (driven by `KICKSTART.md`) replaces every placeholder with your real answers, so no marker survives in a set-up project.

## Quick start (per new project)

1. `mkdir my-new-project && cd my-new-project`
2. Copy the *contents* of this folder into it:
   ```powershell
   # Windows PowerShell
   Copy-Item -Recurse "D:\ai boilerplate\*" .
   ```
   (On other shells: `cp -r /path/to/boilerplate/. /path/to/my-new-project` — note the `.` to include dotfiles if you ever add any.)
3. Initialize git and, **if this project is for public sharing or team work**, immediately run the local-only step so AI rules never leave your machine:
   ```powershell
   git init
   Add-Content .gitignore "## AI agent context (local only)"
   Add-Content .gitignore "/core/"
   Add-Content .gitignore "/AGENTS.md"
   ```
4. Open your AI app, point it at the project folder, and paste the content of `KICKSTART.md`.
5. Answer its questions; let it finish writing the rules files.
6. Commit the rest (source scaffolding, `.gitignore`, …) as normal.

> **Why ignore `core/` and `AGENTS.md`?** They encode *your* personal preferences, machine-specific paths and commands. If you don't want them shared with teammates or pushed to a remote, keep them git-ignored. The agent works fine with untracked local files — git is not required for it to read them.

## Updating the boilerplate itself (dogfooding)

This folder can bootstrap its own development: copy nothing extra, just run `KICKSTART.md` here and answer about *this* project (docs-kit / markdown, no build toolchain). The resulting filled-in rules in `core/` then describe how to maintain the kit.

## Design notes

- **App-agnostic by name.** The canonical file is `AGENTS.md` (a cross-tool convention). `KICKSTART.md` includes optional one-line adapters for tools with fixed filenames (e.g., Claude Code's `CLAUDE.md`).
- **One interview, not ten config files.** All rules live in five small markdown files. They are cheap to skim, diff, and regenerate — never a hidden schema or JSON you can't read.
- **Self-maintaining rule.** The templates carry an "Update rule": as the project evolves (new dependency, new script), the agent is expected to update these files as part of its work, not treat them as one-shot artifacts.
