# Evidence for issue #1: repository settings and protections

Collected on 2026-11-24 (CET), after the repository was made public. Terminal output is unedited apart
from removed color codes and a redacted bypass URL; lines starting with `#` are headings added afterwards.
API output comes from read-only `gh api` calls and is formatted with `jq`. The rule suite and the alert
list are complete responses; the other JSON files hold only the relevant fields, selected and regrouped.

## Protections

| Protection | Test | Result | File |
| --- | --- | --- | --- |
| Ruleset `protect-main` on the default branch: pull request required (0 approvals, squash only), linear history, signed commits, no force pushes, no deletion, no bypass | Ruleset read after the tests | Active, empty bypass list, `current_user_can_bypass: never`; `updated_at` shows it was last changed before the tests | [ruleset-protect-main.json](ruleset-protect-main.json) |
| Direct push to `main` is rejected | An empty, signed commit pushed straight to `main` | Rejected with `GH013`: "Changes must be made through a pull request." `main` unchanged | [direct-push-rejected.txt](direct-push-rejected.txt) |
| The rejection is recorded by GitHub | Rule suite for the rejected push | `pull_request` failed; every other rule passed | [rule-suite-fail.json](rule-suite-fail.json) |
| Push protection blocks a secret | A fine-grained personal access token with no permissions, committed on a test branch | Blocked first by the local pre-push hook (gitleaks), then, with the hook skipped, by GitHub push protection (`GH013`, "Push cannot contain secrets"). The test branch was not created on GitHub and the commit cannot be retrieved from it; the token was deleted right after the test | [push-protection-blocked.txt](push-protection-blocked.txt) |
| No secret scanning alerts | Alerts read after the test | None | [secret-scanning-alerts-after.json](secret-scanning-alerts-after.json) |

Push protection is on both for the repository and for the owner's account, so the test shows that a
push with a secret is blocked, not which of the two layers blocked it. The repository setting is shown in
[security-and-analysis.json](security-and-analysis.json).

The pre-push hook is local and not part of this repository. Its last line is in Swedish and means "STOP:
gitleaks found something, or the check could not be done. The push was aborted."

## Settings

| Setting | File |
| --- | --- |
| Public; secret scanning and push protection on; Dependabot security updates on | [security-and-analysis.json](security-and-analysis.json) |
| Squash merge only, with the pull request title and description as the default commit message; head branches deleted after merge; only collaborators can create pull requests; wiki and discussions off | [repository-settings.json](repository-settings.json) |
| Actions must be pinned to a full commit SHA; the `GITHUB_TOKEN` is read-only and cannot approve pull requests; workflows from all external contributors need approval | [actions-settings.json](actions-settings.json) |

The first commit
([`5eccb10`](https://github.com/sarapersson/confidential-playtest/commit/5eccb104cdf1103d757c5595c8c3c086584beddc))
is signed and shows **Verified** on GitHub, with the noreply address as author.
