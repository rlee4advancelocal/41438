# 41438

Reproduction for [Renovate Discussion 41438](https://github.com/renovatebot/renovate/discussions/41438).

## Current behavior

When `copier update` adds a new executable file (mode `100755` in the template),
Renovate commits it as `100644` (not executable).

Evidence: [PR #1](https://github.com/rlee4advancelocal/41438/pull/1) — `bin/deploy.sh`
is committed as `100644`. Note: GitHub's PR web UI does not display file mode
changes. To verify, use the API:

```bash
# Get the PR head commit tree
gh api repos/rlee4advancelocal/41438/pulls/1 --jq '.head.sha' \
  | xargs -I{} gh api "repos/rlee4advancelocal/41438/git/trees/{}?recursive=1" \
    --jq '.tree[] | select(.path | startswith("bin/")) | "\(.mode) \(.path)"'
```

Output:
```
100644 bin/deploy.sh   <-- should be 100755
```

## Expected behavior

New files added by `copier update` should preserve the executable bit from the
filesystem. `bin/deploy.sh` should be committed as `100755`.

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/41438
