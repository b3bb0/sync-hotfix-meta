# 🔁 sync-hotfix-meta

This GitHub Action automatically updates a structured `<details>` JSON block in your pull request description based on:

- Selected checkboxes (e.g. "use fast-forward")
- Text like `apply tag: v1.2.3`
- Promotion targets: `promote to branches: staging,qa`

## ✅ What It Does

1. Parses PR description for user choices
2. Detects and generates a structured metadata block:
    ```json
    {
      "merge_mode": "ff",
      "tag": "v1.2.3",
      "branches": ["staging", "qa"]
    }
    ```
3. Updates PR body with latest values

## 🚀 Usage

```yaml
- uses: b3bb0/sync-hotfix-meta@v1
  with:
    github_token: ${{ secrets.GITHUB_TOKEN }}
```

## 🧠 Use it before calling your hotfix handler:

```yaml
jobs:
  sync-meta:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: b3bb0/sync-hotfix-meta@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

Then parse that JSON block in your downstream workflows.
