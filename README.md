# 41438

Reproduction for [Renovate Discussion 41438](https://github.com/renovatebot/renovate/discussions/41438).

## Setup

This repo was created with [copier](https://copier.readthedocs.io/) from [rlee4advancelocal/41438-template](https://github.com/rlee4advancelocal/41438-template) at `v1.0.0`.

The template has two tags:

- **`v1.0.0`**: A minimal copier template (`copier.yml` + `.copier-answers.yml.jinja`, no other files)
- **`v1.1.0`**: Adds `bin/deploy.sh` — a shell script committed as **executable** (`100755`) in the template

You can verify the file mode in the template:

```bash
gh api repos/rlee4advancelocal/41438-template/git/trees/v1.1.0?recursive=1 \
  --jq '.tree[] | select(.path == "bin/deploy.sh") | "\(.mode) \(.type) \(.sha | .[0:7])  \(.path)"'
```

```
100755 blob 87db2b1  bin/deploy.sh
```

## Current behavior

When Renovate runs `copier update` to upgrade from `v1.0.0` → `v1.1.0`, the new file `bin/deploy.sh` is committed with mode `100644` (not executable).

See [PR #1](https://github.com/rlee4advancelocal/41438/pull/1). GitHub's PR web UI does not show file mode changes, so use the CLI to verify:

```bash
gh pr diff 1 --repo rlee4advancelocal/41438
```

```diff
diff --git a/bin/deploy.sh b/bin/deploy.sh
new file mode 100644
index 0000000..87db2b1
--- /dev/null
+++ b/bin/deploy.sh
@@ -0,0 +1,2 @@
+#!/usr/bin/env bash
+echo "Deploying project..."
```

The file is `100644` — the executable bit was dropped.

## Expected behavior

`bin/deploy.sh` should be committed as `100755`, preserving the executable permission from the template:

```diff
diff --git a/bin/deploy.sh b/bin/deploy.sh
new file mode 100755
index 0000000..87db2b1
--- /dev/null
+++ b/bin/deploy.sh
@@ -0,0 +1,2 @@
+#!/usr/bin/env bash
+echo "Deploying project..."
```

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/41438

---

This reproduction was created with AI assistance.
