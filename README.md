# 41438

Reproduction for [Renovate Discussion 41438](https://github.com/renovatebot/renovate/discussions/41438).

## Current behavior

When `copier update` adds a new executable file (mode `100755` in the template),
Renovate commits it as `100644` (not executable).

Evidence: [PR #1](https://github.com/rlee4advancelocal/41438/pull/1) — `bin/deploy.sh`
is `new file mode 100644` in the diff. The git tree confirms:

```
100644 bin/deploy.sh   <-- should be 100755
```

## Expected behavior

New files added by `copier update` should preserve the executable bit from the
filesystem. `bin/deploy.sh` should be committed as `100755`.

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/41438
