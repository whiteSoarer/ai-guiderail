# WORKFLOW.md — Git & Process Conventions

<!-- note (setup): Fill from `git remote -v`, existing branch/commit history style, and the local-only decision made in KICKSTART Q10. Keep < 120 lines. -->

## Repo status

- Remote: {{REMOTE_URL_OR_"none — local-only repo"}}
- Visibility assumption: {{PRIVATE_TEAM | PRIVATE_SOLO | PUBLIC}} (drives how careful we are with commit messages, branch names, and anything that could end up in history)
- AI rules files (`/core/`, root `AGENTS.md`): **{{git-ignored per .gitignore — local only | committed and shared with the team}}**

## Branching & commits

- Main branch name: {{MAIN_BRANCH}}
- New work branches: `{{BRANCH_PATTERN, e.g., "feat/<short-slug>", "fix/<issue-or-slug>"}}` off main; delete after merge.
- Commit message style: {{STYLE, e.g., "Conventional Commits (feat|fix|chore|docs): imperative summary ≤ 72 chars"}} — match the style of `git log --oneline -10`, do not invent a new one if history already has a clear pattern.
- One logical change per commit; agent-authored commits must say so in the body when useful (e.g., "Co-authored-by: <agent>").

## Pull request / review expectations

- PR title & description: {{PR_CONVENTIONS_OR_"solo project — skip PRs, push to main directly"}}
- Review gate before merge: {{GATE_OR_NONE}}
- Definition of done for a task (check all that apply): tests pass per `core/TESTING.md` · rule files updated if contracts changed per `AGENTS.md` Update rule · no secrets or ignored files staged (`git status --porcelain` check) · user-reviewed diff.

## Local-only enforcement (applies when rules are git-ignored)

Before any commit in this repo, an agent must run the ignore-check from `core/AGENTS.md`: confirm `/core/`, `AGENTS.md`, and other local-only files do not appear as staged/untracked-and-would-be-committed. If they would be picked up by `git add -A`/`-u`, stop and ask — never force them into history to "keep things simple".

## Escalation defaults

Anything touching shared state (force-push, history rewrite, deleting remote branches, changing CI or secrets) requires explicit user approval in the current session — see boundaries table in `core/AGENTS.md`.
