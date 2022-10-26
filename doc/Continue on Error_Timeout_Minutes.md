# Error continue

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
