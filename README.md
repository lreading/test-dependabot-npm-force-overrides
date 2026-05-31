# test-dependabot-npm-force-overrides

End-to-end fixture for `lreading/dependabot-npm-force-overrides`.

This repo intentionally contains:

- a direct npm dependency: `npm-package-arg@12.0.2`
- a vulnerable transitive lockfile dependency: `semver@7.5.1`

Dependabot should open a security PR that updates `package-lock.json` for `semver`.
The action should then add a matching `package.json` override and commit it back to the PR branch.

Expected action result on the Dependabot PR:

```json
{
  "overrides": {
    "semver": ">=<resolved-version>"
  }
}
```

## Required Repo Settings

Enable:

- Dependabot alerts
- Dependabot security updates
- GitHub Actions

The workflow uses `pull_request_target` and `contents: write` so it can push back to the same-repo Dependabot branch.
