# Agent instructions

## Security

- Never commit or push secrets: passwords, API keys, access tokens, private keys, certificates containing private keys, or credentials in connection strings.
- Never commit or push local `.env` files, credential files, database dumps, backups, private logs, or personal/customer data. Example configuration must contain clearly fake placeholders only.
- Keep sensitive local files out of version control with targeted `.gitignore` rules. Ignore rules do not protect files already tracked by Git.
- Do not expose secrets in terminal output, screenshots, documentation, issues, or PR descriptions. Redact sensitive values before sharing.
- Before committing, inspect the staged diff and file list for sensitive content and unrelated changes. Before pushing, inspect all outgoing commits, not only the latest diff. Use the repository's secret scanner if one is configured.
- If a secret is found, stop the affected commit or push and tell the user without repeating the secret. If it was already committed or shared, treat it as exposed: arrange revocation or rotation, then remove it from tracked content. Do not rewrite shared history without explicit authorization.
- Only push, publish, or deploy when authorized by the user's request. Never force-push, rewrite shared history, or bypass repository protections without explicit authorization for that action.
- Preserve authentication, authorization, input validation, and security checks. Do not disable safeguards to make a change or test pass.

## Documentation and README

- Do not create or add documentation, including README files, unless explicitly requested by the user. Do not add documentation as an unsolicited extra to a code change.
- Keep README files as short as possible while remaining informative. Include only what readers need to understand and use the project.
- Keep all documentation simple and concise. Use short sentences, brief sections, and practical examples when useful. Avoid long paragraphs, filler, and repeated information.
- Write public documentation for other people: explain what the project does and how to use it. Do not use it as a development log.
- Keep milestones, stages, progress reports, task lists, working notes, and other internal work tracking local. Do not include them in public documentation or commit or push those local records.

## Scope and workspace safety

- Make the smallest complete change that solves the requested problem. Avoid unrelated refactors, features, dependencies, or abstractions.
- Reuse existing code and conventions where practical.
- Preserve existing user changes. Do not overwrite or discard unrelated edits.
- Do not run destructive Git commands or delete user work without explicit authorization for that action.

## Tests and verification

- Keep tests minimal and focused on meaningful failures: core behavior, security boundaries, data integrity, and regressions that affect users.
- For non-trivial logic, add or update the smallest useful test that verifies observable behavior. Prefer extending an existing test over creating a new suite.
- Do not add tests for trivial edits, tests that merely mirror implementation details, redundant cases, or tests solely to increase coverage numbers.
- Do not remove useful existing tests just to reduce the test count or make checks pass.
- Run checks relevant to the change and any required repository checks. Broaden testing only when risk or failures justify it.
- Report what passed, failed, or was not run, with reasons for skipped checks. Never claim unverified success.

## Reviewing changes

Before considering a change complete, review the diff and affected callers against all eight areas:

- **Efficiency:** Avoid unnecessary work, repeated queries, excessive allocations, and avoidable latency.
- **Cost:** Check effects on API usage, compute, storage, network traffic, and paid dependencies. Avoid unnecessary recurring costs.
- **UX:** Keep flows clear and consistent. Check accessibility and loading, empty, error, and success states where applicable.
- **Correctness:** Verify intended behavior, edge cases, error handling, and compatibility with existing callers. Run checks appropriate to the change.
- **Modularisation:** Keep responsibilities focused, reuse existing code, and avoid duplication or unnecessary abstractions.
- **Folder architecture:** Follow the repository's structure. Place files with the feature or layer that owns them; avoid unrelated restructuring.
- **Naming:** Use clear, consistent names for files, modules, functions, variables, and public interfaces. Follow existing conventions.
- **Security:** Check input validation, authentication, authorization, secret handling, data exposure, and dependency risks relevant to the change.

Fix issues introduced by the change before finishing. Report unresolved findings and validation gaps clearly. Mark an area as not applicable when appropriate; do not invent work to satisfy the checklist.

## Pull request format

Use this title format:

`<type>: <short description of the change>`

Choose `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `build`, `ci`, or `perf` to match the main change. Use an imperative description, for example: `docs: add repository security rules`.

Use the following body for every PR. Replace the prompts with concrete details. Keep each section concise; write `None` or `Not applicable` where appropriate.

```markdown
## Summary

Explain the problem and the resulting behavior. Link the related issue if one exists.

## Changes

- List the changes a reviewer needs to understand.

## Validation

- List checks run and their results.
- State checks not run and why. Never claim a check passed unless it ran successfully.

## Risks

Describe breaking changes, security or data impact, or other known limitations. Write `None` if there are no known risks.
```

- Describe the final diff, not the conversation or abandoned approaches.
- Keep each PR focused on the requested change. Identify any necessary follow-up work explicitly.
- Include screenshots for visible UI changes when useful, with sensitive content removed.
