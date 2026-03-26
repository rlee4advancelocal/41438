# 41438

Reproduction for [Renovate Discussion 41438](https://github.com/renovatebot/renovate/discussions/41438).

## Current behavior

When `copier update` adds a new executable file (mode `100755` in the template),
Renovate commits it as `100644` (not executable).

## Expected behavior

New files added by `copier update` should preserve the executable bit from the
filesystem. `bin/deploy.sh` should be committed as `100755`.

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/41438
