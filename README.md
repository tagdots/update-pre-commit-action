# update-pre-commit-action

[![OpenSSF Best Practices](https://www.bestpractices.dev/projects/10601/badge)](https://www.bestpractices.dev/projects/10601)
[![CI](https://github.com/tagdots/update-pre-commit/actions/workflows/ci.yaml/badge.svg)](https://github.com/tagdots/update-pre-commit/actions/workflows/ci.yaml)
[![marketplace](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/tagdots/update-pre-commit/refs/heads/badges/badges/marketplace.json)](https://github.com/marketplace/actions/update-pre-commit-action)
[![coverage](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/tagdots/update-pre-commit/refs/heads/badges/badges/coverage.json)](https://github.com/tagdots/update-pre-commit/actions/workflows/cron-tasks.yaml)


This action runs [**update-pre-commit**](https://github.com/tagdots/update-pre-commit) to keep your `pre-commit` hooks up to date and optionally creates pull request.

<br>

**update-pre-commit**:
1. reduces your supply chain risks with `openssf best practices` in our development and operations.
1. automates your `change management operation` to optionally create `pull request` on GitHub.
1. protects you against unreliable revs such as `alpha`, `beta`, `prerelease`, and `rc`.

<br>

## 😎 GitHub Action workflow examples

Use the example workflows below to create your own workflow inside `.github/workflows/`.

<br>

### Example 1️⃣ - summary
**update-pre-commit-action**:

* runs on a scheduled interval - every day at 5:30 pm UTC  (`- cron: '30 17 * * *'`)
* uses GitHub Token with permissions: `contents: write` and `pull-requests: write`
* updates `.pre-commit-config.yaml` when new revs become available (`dry-run: false`)
* opens a pull request after update to `.pre-commit-config.yaml` (`open-pr: true`)

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
      uses: tagdots/update-pre-commit-action@939e74b030e11eeb313414e9488b1b233dc32f84 # 1.0.19
      with:
        file: .pre-commit-config.yaml
        dry-run: false
        open-pr: true
```

<br>

### Example 2️⃣ - summary
**update-pre-commit-action**:

* runs on a scheduled interval - every day at 5:30 pm UTC  (`- cron: '30 17 * * *'`)
* uses GitHub Token with permissions: `contents: read` and `pull-requests: read`
* updates `.pre-commit-config.yaml` when new revs become available (`dry-run: false`)
* **_Does Not_** open a pull request (`open-pr: false`)

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
      uses: tagdots/update-pre-commit-action@939e74b030e11eeb313414e9488b1b233dc32f84 # 1.0.19
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
