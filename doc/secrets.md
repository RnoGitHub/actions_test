# Secrets

## Refer

[Automatic token authentication](https://docs.github.com/ja/actions/security-guides/automatic-token-authentication)

## How to regist Secrets

If you use token or correspond to it, it is secret things.
When you use these secrets, regist secrets to GitHub and Read to env then use it.

In GitHub your repo.

1. Vistit your repository in GitHub.
1. `settings` click in tab menu.
1. `Secrets` click in left menu bar.
1. `Actions` click in left menu bar.
1. `New repository secret` button click
1. `Name` input env name.①
1. `Secret` input secret value.  
   this is token value or something is secret

In your workflow

``` yaml
env:
  - <EnvName>: ${{ secrets.<regist to github> }}　# ①Value
```

## Default secrets value

GitHub preserves secrets value

`${{ secrets.GITHUB_TOKEN }}`

This would be used automatic authentification

for example

``` yaml
name: Pull request labeler
on: [ pull_request_target ]

permissions:
  contents: read
  pull-requests: write

jobs:
  triage:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/labeler@v4
        with:
          repo-token: ${{ secrets.GITHUB_TOKEN }}
```
