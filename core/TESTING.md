# TESTING.md — Testing Rules & Commands

<!-- note (setup): If the project has no test framework, this file becomes a short statement of that fact plus the agreed plan (see KICKSTART Q7). Never invent a command for a tool that is not in the manifest. Keep < 120 lines. -->

## Test stack

- Framework: {{FRAMEWORK_AND_VERSION}} (per manifest)
- Location pattern: {{TEST_LOCATION, e.g., "co-located `*.test.ts`" or "`tests/` mirroring source"}}
- Fixtures / test data: {{FIXTURE_POLICY_OR_NONE}}

## Canonical commands

| Purpose | Command |
|---|---|
| Run all tests | `{{RUN_ALL_TESTS}}` |
| Single file | `{{RUN_ONE_FILE, e.g., "pnpm vitest run src/foo.test.ts"}}` |
| Watch mode (dev only) | `{{WATCH_CMD_OR_NA}}` |

## Rules for agent work in this repo

1. **Test-or-explain.** Any code change that is testable under the stack above must either include a new/updated test or state explicitly why it cannot be tested — silence on tests is not an acceptable default.
2. **Run before reporting done.** Execute the relevant command from the table (at minimum: affected file(s) + full suite if cheap). Paste real output, never paraphrase results you did not run.
3. **No test weakening.** Never change a failing test to make it pass unless the user asked for the behavior change; flag the mismatch instead.
4. **Flaky handling:** if a test fails intermittently, re-run once and report both outcomes with timestamps — do not silently drop it from your "tests pass" claim.

## Coverage & gates (fill only what is actually enforced)

- Coverage requirement: {{COVERAGE_OR_NONE}} (enforced by {{MECHANISM_OR_"nothing"}})
- CI gate: {{CI_CHECK_NAME_OR_"no CI configured"}}
