## MM :: Merge branc

Runs a git merge in your CI.

Examples:

### Sync branches

```yaml
name: Sync multiple branches
on:
  push:
    branches:
      - '*'
jobs:
  sync-branch:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master

      - name: Merge development -> staging
        uses: michelmelo/merge-branch@master
        with:
          type: now
          from_branch: development
          target_branch: staging
          github_token: ${{ secrets.GITHUB_TOKEN }}

      - name: Merge staging -> uat
        uses: michelmelo/merge-branch@master
        with:
          type: now
          from_branch: staging
          target_branch: uat
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

### Merge current branch

```yaml
name: Merge any release branch to uat
on:
  push:
    branches:
      - 'release/*'
jobs:
  merge-branch:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master

      - name: Merge staging -> uat
        uses: michelmelo/merge-branch@master
        with:
          type: now
          target_branch: uat
          github_token: ${{ secrets.GITHUB_TOKEN }}
```
