# Events action

## Refer

[Events that trigger workflows](https://docs.github.com/ja/actions/using-workflows/events-that-trigger-workflows "Events that trigger workflows")  
[schedule](https://crontab.guru/)  
[schedule example](https://crontab.guru/examples.html)
[repository dispatch](https://docs.github.com/ja/rest/repos/repos#create-a-repository-dispatch-event)
[postman](https://identity.getpostman.com/signup)
[Filter pattern cheat sheet](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#filter-pattern-cheat-sheet)

## Event

`on:[events]`

events:

- push
- pull request
- etc

if you pull request to the repo, it runs.

test.yaml try to pull request and check it.

ex. pull request trigger

``` yaml
opened, synchronize, or reopened.

- assigned
- unassigned
- labeled
- unlabeled
- opened
- edited
- closed
- reopened
- synchronize
- converted_to_draft
- ready_for_review
- locked
- unlocked
- review_requested
- review_request_removed
- auto_merge_enabled
- auto_merge_disabled
```

If cancel button to reject pull request, workflow will stop.

``` yaml
on: 
  push
  pull_request
    types[closed, assigned, opend]
```

## Repository dispatch

It is something that can be triggered manually. And in order to trigger it we have to send a post request.

It means workflow control by external site or other workflow.  

repository_dispatch は GitHub の外部のイベントを検知するために用意されている機能です。GitHub API に用意されてるエンドポイントからワークフローをトリガーできる。[リンク](https://docs.github.com/en/actions/reference/events-that-trigger-workflows#repository_dispatch)

なお、 repository_dispatch イベントが実行されるのはワークフローが master もしくはデフォルトブランチにある時のみ。

workflow側

``` yaml
on:
  repository_dispatch:
    types: [build]
```

を上記のように設定し、

``` note
Post: https://api.github.com/repos/RnoGitHub/actions_test/dispatches

authentification:
  username :RnoGitHub
  password :access-token

hedder:
  key: Accept       value:application/vnd.github+json
  key: Content-Type value:application/json

body 
{
    "event_type": "build"
}

```

のように送れば、反応する。
やはり、master branchでしか反応しなかった。

## filter

filter function works at develop branch to master.
どれを有効にして、どれを無効にするかフィルターできる。

有効な設定を書いた後、フィルターの部分を記載する。

``` yaml
on:
  push:
    branches:
      - master      # default OK
      - 'feature/*' # filter/hoge
      - 'feature**' # filter feature hogehoge
      - '!feature/featC' # 例外でfeature**からfeatCだけ除外
    branches-ignore: # 無視する場合のfilter 正常系との共存はできない。
```

see detail [Patterns to match branches and tags](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#patterns-to-match-branches-and-tags)
