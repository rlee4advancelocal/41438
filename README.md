# 41438

Reproduction for [Renovate Discussion 41438](https://github.com/renovatebot/renovate/discussions/41438).

## Setup

This repo was created with [copier](https://copier.readthedocs.io/) from [rlee4advancelocal/41438-template](https://github.com/rlee4advancelocal/41438-template) at `v1.0.0`.

The template has two tags:

- **`v1.0.0`**: A minimal copier template (`copier.yml` + `.copier-answers.yml.jinja`, no other files)
- **`v1.1.0`**: Adds `bin/deploy.sh` — a shell script committed as **executable** (`100755`) in the template

You can verify the file mode in the template:

```bash
git clone https://github.com/rlee4advancelocal/41438-template.git
git -C 41438-template ls-tree v1.1.0 bin/deploy.sh
```

```
100755 blob 87db2b16266fc0ff4c9e95f89c73ebc093f5ab03	bin/deploy.sh
```

## Current behavior

Renovate created [PR #1](https://github.com/rlee4advancelocal/41438/pull/1) to upgrade from `v1.0.0` → `v1.1.0`. The PR adds `bin/deploy.sh`, but commits it with mode `100644` (not executable) — even though the template has it as `100755`.

GitHub's PR web UI does not show file mode changes. Use `gh pr diff` to verify:

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

Note `new file mode 100644` — the executable bit from the template (`100755`) was dropped.

## Expected behavior

The file mode should match the template. `bin/deploy.sh` should be `100755`:

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
