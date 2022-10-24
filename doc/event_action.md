# Events action

## Refer

[Events that trigger workflows](https://docs.github.com/ja/actions/using-workflows/events-that-trigger-workflows "Events that trigger workflows")  
[schedule](https://crontab.guru/)  
[schedule example](https://crontab.guru/examples.html)
[repository dispatch](https://docs.github.com/ja/rest/repos/repos#create-a-repository-dispatch-event)
[postman](https://identity.getpostman.com/signup)

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

repository_dispatch は GitHub の外部のイベントを検知するために用意されている機能です。GitHub API に用意されてるエンドポイントからワークフローをトリガーできる。https://docs.github.com/en/actions/reference/events-that-trigger-workflows#repository_dispatch

なお、 repository_dispatch イベントが実行されるのはワークフローが master もしくはデフォルトブランチにある時のみ。