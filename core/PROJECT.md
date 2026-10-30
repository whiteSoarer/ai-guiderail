# PROJECT.md — Stack & Architecture Map

<!-- note (setup): Rewrite during the KICKSTART interview using facts verified from manifests and the tree. Keep < 120 lines. -->

## Purpose

{{ONE_LINE_PURPOSE}}

## Runtime & toolchain

| Item | Version / value | Source of truth |
|---|---|---|
| Primary language | {{LANG_AND_VERSION}} | e.g., `package.json` engines field |
| Package manager | {{PKG_MANAGER_AND_VERSION}} | lockfile name + version |
| Framework(s) | {{FRAMEWORKS_WITH_VERSIONS}} | manifest |
| Other major deps | {{MAJOR_DEPS}} (list only the ones a developer must know about) | manifest / lockfile |

## Architecture map

<!-- note: 3-6 bullets max. "Where does X live" is this file's job — be concrete with paths, not adjectives. -->

- **Entry point(s):** {{ENTRY_POINTS}} (e.g., `src/index.ts`, `cmd/server/main.go`)
- **Key directories:**
  - `{{DIR_1}}` — {{WHY_IT_MATTERS_1}}
  - `{{DIR_2}}` — {{WHY_IT_MATTERS_2}}
  - … (add up to ~5)

## Data & state

<!-- note: fill only what applies; delete the rest of this section if none. -->

- Persistence: {{DB_OR_NONE}} (engine + connection source, e.g., `DATABASE_URL` env var — never write its value here)
- Local config files: {{CONFIG_FILES}} (e.g., `.env`, `.env.local`) — which are git-ignored vs committed
- Secrets: referenced by name/path only, per `core/AGENTS.md`.

## Known constraints & gotchas

<!-- note: 0-5 bullets. The kind of thing that bites a fresh agent on day one (legacy shims, monkey-patches, platform quirks, perf hot spots). Delete section if none exist yet — do not pad it. -->

- {{GOTCHA_1}}
