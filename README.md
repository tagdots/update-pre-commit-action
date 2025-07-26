# update-pre-commit-action

[![OpenSSF Best Practices](https://www.bestpractices.dev/projects/10601/badge)](https://www.bestpractices.dev/projects/10601)
[![CI](https://github.com/tagdots/update-pre-commit/actions/workflows/ci.yaml/badge.svg)](https://github.com/tagdots/update-pre-commit/actions/workflows/ci.yaml)
[![marketplace](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/tagdots/update-pre-commit/refs/heads/badges/badges/marketplace.json)](https://github.com/marketplace/actions/update-pre-commit-action)
[![coverage](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/tagdots/update-pre-commit/refs/heads/badges/badges/coverage.json)](https://github.com/tagdots/update-pre-commit/actions/workflows/cron-tasks.yaml)


This action runs [**update-pre-commit**](https://github.com/tagdots/update-pre-commit) to keep your `pre-commit` hooks up to date and optionally creates pull request.

<br>

**update-pre-commit**:
1. reduces your supply chain risks with `openssf best practices` in our software development and operations.
1. automates your `change management operation` to optionally create `pull request` on GitHub.
1. protects you from using unreliable revs such as `alpha`, `beta`, `prerelease`, and `rc`.

<br>

## 😎 GitHub Action workflow examples

Use the example workflows below to create your own workflow inside `.github/workflows/`.

<br>

### Example 1️⃣ - summary
**update-pre-commit-action** will:

* run on a scheduled interval - every day at 5:30 pm UTC  (`- cron: '30 17 * * *'`)
* use GitHub Token with permissions: `contents: write` and `pull-requests: write`
* update `.pre-commit-config.yaml` when new revs become available (`dry-run: false`)
* open a pull request when new revs become available (`open-pr: true`)

<br>

### Example 1️⃣ - workflow
```
name: update-pre-commit-action

on:
  # on schedule: e.g. every day at 5:30 pm UTC
  schedule:
    - cron: '30 17 * * *'

  # on demand
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

jobs:
  update-pre-commit:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: write

    steps:
    - name: Run update-pre-commit
      id: update-pre-commit
      env:
        GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      uses: tagdots/update-pre-commit-action@0da91de0a91c4d24cac35b8576fba69e7abc2365 # 1.0.16
      with:
        file: .pre-commit-config.yaml
        dry-run: false
        open-pr: true
```

<br>

### Example 2️⃣ - summary
**update-pre-commit-action** will:

* run on a scheduled interval - every day at 5:30 pm UTC  (`- cron: '30 17 * * *'`)
* use GitHub Token with permissions: `contents: read` and `pull-requests: read`
* update `.pre-commit-config.yaml` when new revs become available (`dry-run: false`)
* **_NOT_** open a pull request when new revs become available (`open-pr: false`)

<br>

### Example 2️⃣ - workflow
```
name: update-pre-commit-action

on:
  # on schedule: e.g. every day at 5:30 pm UTC
  schedule:
    - cron: '30 17 * * *'

  # on demand
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

jobs:
  update-pre-commit:
    runs-on: ubuntu-latest

    steps:
    - name: Run update-pre-commit
      id: update-pre-commit
      env:
        GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      uses: tagdots/update-pre-commit-action@0da91de0a91c4d24cac35b8576fba69e7abc2365 # 1.0.16
      with:
        file: .pre-commit-config.yaml
        dry-run: false
        open-pr: false
```

<br>

## 😕  Troubleshooting

We are here to help - open an [issue](https://github.com/tagdots/update-pre-commit-action/issues)

<br>

## 📖 License

[MIT License](https://github.com/tagdots/update-pre-commit-action/blob/main/LICENSE).
