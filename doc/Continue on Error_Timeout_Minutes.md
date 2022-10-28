# Strategy

Timeout, Error condition, Error handring they need to include strategy.
Also node.

## Refer

[actions/setup-node](https://github.com/actions/setup-node)

## Error continue and Timeout

Timeout, Error condition, Error handring they need to include strategy.
Timeout has value to judge time out.(default 360 min). this time elapsed GitHub kill workflow process automatically.

``` yaml

  dump_contexts_to_log:
    runs-on: ubuntu-latest
    if: github.event_name == 'push'
    steps:
      - name: Dump GitHub context
        id: github_context_step
        run: echo '${{ toJSON(github) }}'
        continue-on-error: true
        # if error occured, continue 
      - name: Dump job context
        if: failure()
        # if error occured, skip
        run: echo '${{ toJSON(job) }}'
      - name: Dump steps context
        if: always()
        run: echo '${{ toJSON(steps) }}'
        timeout-minutes: 360
        # Github kill over mitnute. default value is 360min
      - name: Dump runner context
        run: echo '${{ toJSON(runner) }}'
      - name: Dump strategy context
        run: echo '${{ toJSON(strategy) }}'
      - name: Dump matrix context
        run: echo '${{ toJSON(matrix) }}'
```
