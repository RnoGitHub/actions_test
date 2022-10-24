# Events action

## Refer

[Events that trigger workflows](https://docs.github.com/ja/actions/using-workflows/events-that-trigger-workflows "Events that trigger workflows")  
[schedule](https://crontab.guru/)  
[schedule example](https://crontab.guru/examples.html)

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
