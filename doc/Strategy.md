# Strategy

Timeout, Error condition, Error handring they need to include strategy.
Next, introduce matrix. it will try several combination.

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

## Matrix

---
If you use matrix, you can try combination between several os version, tool version and others.  
Matrix do the job all combination. (12=nove_v(4) * os(3) job putturn will done)

```yaml
name: Matrix

on: push

jobs:
  node-version:
    strategy:
      matrix:
        os: [macos-latest, ubuntu-20.04, windows-latest]
        node_version: [6,8,10,16]
      max-parallel: 3 # parallel jobs num. it is limit
      # fail-fast: true # default true means several jobs work. if there is an error in matrix, wf will stop.
    runs-on: ${{ matrix.os }}
    steps:
      - name: Log node node-version
        run: node -v
      - uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node_version }}
      - name: Log node node-version
        run: node -v
```
