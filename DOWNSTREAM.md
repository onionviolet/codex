# Weibao Codex downstream

This fork stays close to `openai/codex` while carrying a small set of reviewed
fixes and workflow improvements.

## Repository contract

- `upstream/main` is the current OpenAI source.
- `origin/codex/weibao-downstream` is the installable downstream branch.
- Each imported pull request or local fix stays in its own commit when practical.
- A downstream patch is removed when upstream ships an equivalent fix.
- The official Codex installation remains available as a fallback.

## Authentication contract

The downstream binary uses the normal Codex home directory. Unless
`CODEX_HOME` is explicitly set, that is `~/.codex`. Existing ChatGPT login,
configuration, sessions, skills, and plugins therefore remain available across
downstream rebuilds. Update scripts must never copy, print, or modify credential
files.

## Install or update

Run:

```sh
scripts/weibao-codex-update
```

This fast-forwards the local downstream branch to its GitHub branch, builds a
release binary, and atomically installs it as `~/.local/bin/codex-weibao`. It
does not merge upstream automatically. Upstream changes are reviewed and tested
before they enter the downstream branch.

## Absorbing upstream or community work

1. Fetch `upstream` and inspect the proposed commits or pull request.
2. Apply one bounded change to a temporary branch or worktree.
3. Run formatting and the narrowest relevant test suite.
4. Merge the verified change into `codex/weibao-downstream` and record its source.
5. Push the downstream branch, then run `scripts/weibao-codex-update` on each Mac.

