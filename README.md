# 41438

Reproduction for [Renovate Discussion 41438](https://github.com/renovatebot/renovate/discussions/41438).

## Current behavior

When `copier update` adds a new executable file (mode `100755` in the template),
Renovate commits it as `100644` (not executable).

Evidence: [PR #1](https://github.com/rlee4advancelocal/41438/pull/1) — `bin/deploy.sh`
is committed as `100644`. Note: GitHub's PR web UI does not display file mode
changes. To verify:

```bash
gh pr diff 1 --repo rlee4advancelocal/41438 | grep -A2 "deploy.sh"
```

Output:
```
diff --git a/bin/deploy.sh b/bin/deploy.sh
new file mode 100644        <-- should be 100755
index 0000000..87db2b1
```

## Expected behavior

New files added by `copier update` should preserve the executable bit from the
filesystem. `bin/deploy.sh` should be committed as `100755`.

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/41438
