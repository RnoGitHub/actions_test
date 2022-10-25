# Secrets

## Refer

[Automatic token authentication](https://docs.github.com/ja/actions/security-guides/automatic-token-authentication)
[Assigning permissions to jobs](https://docs.github.com/ja/actions/using-jobs/assigning-permissions-to-jobs)

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

``` yaml
name: Create issue on commit

on: [ push ]

jobs:
  create_issue:
    runs-on: ubuntu-latest
    permissions:
      issues: write 
    steps:
      - name: Create issue using REST API
        run: |
          curl --request POST \
          --url https://api.github.com/repos/${{ github.repository }}/issues \
          --header 'authorization: Bearer ${{ secrets.GITHUB_TOKEN }}' \
          --header 'content-type: application/json' \
          --data '{
            "title": "Automated issue for commit: ${{ github.sha }}",
            "body": "This issue was automatically created by the GitHub Action workflow **${{ github.workflow }}**. \n\n The commit hash was: _${{ github.sha }}_."
            }' \
          --fail
```

Permission is different from before.
see [Assigning permissions to jobs](https://docs.github.com/ja/actions/using-jobs/assigning-permissions-to-jobs)

``` yaml
name: Create issue on commit

on: [ push ]

jobs:
  create_issue:
    runs-on: ubuntu-latest
    # this is point read -> write
    permissions:
      issues: write
      actions: write
      checks: write
      contents: write
      deployments: write
      packages: write
      pull-requests: write
      repository-projects: write
      security-events: write
      statuses: write
    steps:
      - name: Push a randome file
        run: |
          pwd
          ls -a
          git init
          git remote add origin "https://$GITHUB_ACTOR:${{ secrets.GITHUB_TOKEN}}@github.com/$GITHUB_REPOSITORY.git"
          git config --global user.email "my-bot@bot.com"
          git config --global user.name "my-bot"
          git fetch
          git checkout main
          git branch --set-upstream-to=origin/main
          git pull
          ls -a
          echo $RANDUM >> random.text
          ls -a
          git add -A
          git commit -m"Random file"
          git push

      - name: Create issue using REST API
        run: |
          curl --request POST \
          --url https://api.github.com/repos/${{ github.repository }}/issues \
          --header 'authorization: Bearer ${{ secrets.GITHUB_TOKEN }}' \
          --header 'content-type: application/json' \
          --data '{
            "title": "Automated issue for commit: ${{ github.sha }}",
            "body": "This issue was automatically created by the GitHub Action workflow **${{ github.workflow }}**. \n\n The commit hash was: _${{ github.sha }}_."
            }' \
          --fail
```

[this method](https://dev.classmethod.jp/articles/getting-an-access-token-with-only-the-necessary-permissions-on-github-appsgithub-actions/) also OK but 30days is effective.
