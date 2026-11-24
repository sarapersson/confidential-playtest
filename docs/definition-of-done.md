# Definition of Done

A change is done when the following are true. If an item does not apply, the pull request says why,
for example because that part of the project does not exist yet.

This is a solo project, so no second person reviews the pull requests. Instead, I review each pull
request against this list before merging and note the result under Verification.

## Functionality

- The acceptance criteria in the issue are met, including the error and access-denied cases.

## Tests

- Tests are added or updated for the change, and all checks pass.
- A bug fix or security finding gets a regression test.

## Security

- The threat model is checked for the change; new risks and new personal data are recorded.
- No secrets, personal data or private details in code, logs, screenshots or the pull request.
- New or changed dependencies, actions and images use the latest stable release, checked at the source,
  and are pinned.

## Documentation and delivery

- The README, a runbook or an ADR is updated if behavior, operations or a hard-to-reverse decision changed.
- The pull request title follows Conventional Commits, since it becomes the commit subject on `main`.
- The pull request description has Summary, Changes and Verification, and links its issue with `Closes #N`.
  The issue stays open after the merge and is closed by hand once the change is verified.
- All commits are signed.
- Evidence for the change is added to `docs/evidence/` or linked from the pull request.
