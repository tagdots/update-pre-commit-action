# update-pre-commit-action

[![OpenSSF Best Practices](https://www.bestpractices.dev/projects/10601/badge)](https://www.bestpractices.dev/projects/10601)
[![CI](https://github.com/tagdots/update-pre-commit/actions/workflows/ci.yaml/badge.svg)](https://github.com/tagdots/update-pre-commit/actions/workflows/ci.yaml)
[![Code Coverage](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/tagdots/update-pre-commit/refs/heads/badge/coverage.json)](https://github.com/tagdots/update-pre-commit/actions/workflows/cron-coverage.yaml)


This action keeps your `pre-commit` hooks up to date and optionally creates pull request.

<br>

**update-pre-commit-action** uses [**update-pre-commit**](https://github.com/tagdots/update-pre-commit) with the goal to:
1. reduce your supply chain risks with `openssf best practices` in our development and operation.
1. automate your `change management operation` to optionally create `pull request` on GitHub.
1. protect you from using unreliable revs such as `alpha`, `beta`, `prerelease`, and `rc`.

<br>

## 😎 Roll out 1 2 3

1. use the example workflows below to create your own workflow inside `.github/workflows/`.
1. merge your code with the new workflow.
1. done!!

<br>

## 🔍 How to use update-pre-commit-action?

### Use Case 1️⃣ - summary descriptions
**update-pre-commit-action** in the workflow below will:

* run on a scheduled interval - every day at 5:30 pm UTC  (`- cron: '30 17 * * *'`)
* use GitHub Token with permissions: `contents: write` and `pull-requests: write`
* use pinned full commit hash from https://github.com/tagdots/update-pre-commit-action/releases
* update `.pre-commit-config.yaml` when new revs become available (`dry-run: false`)
* open a pull request when new revs become available (`open-pr: true`)

<br>

### Use Case 1️⃣ - example workflow
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
      uses: tagdots/update-pre-commit-action@2cd407af92c1c9435c6406f4e23657d3ea14dcbb # 1.0.1
      with:
        file: .pre-commit-config.yaml
        dry-run: false
        open-pr: true
```

<br>

### Use Case 2️⃣ - summary descriptions
**update-pre-commit-action** in the workflow below will:

* run on a scheduled interval - every day at 5:30 pm UTC  (`- cron: '30 17 * * *'`)
* use pinned full commit hash from https://github.com/tagdots/update-pre-commit-action/releases
* update `.pre-commit-config.yaml` when new revs become available (`dry-run: false`)
* **_NOT_** open a pull request when new revs become available (`open-pr: false`)

<br>

### Use Case 2️⃣ - example workflow
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
      uses: tagdots/update-pre-commit-action@2cd407af92c1c9435c6406f4e23657d3ea14dcbb # 1.0.1
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
