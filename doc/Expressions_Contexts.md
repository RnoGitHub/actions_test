# Expression

## Refer

[Contexts](https://docs.github.com/en/actions/learn-github-actions/contexts)

## ${{ }}

$env

${{ }} means evaluated value in GitHub

${{ a == b}}等と書ける

## Contexts

hoge.fuga  
ex secrets.ENV  

hoge = Contexts  

```yaml
name: Contexts testing
on: push

jobs:
  dump_contexts_to_log:
    runs-on: ubuntu-latest
    steps:
      - name: Dump GitHub context
        id: github_context_step
        run: echo '${{ toJSON(github) }}'
      - name: Dump job context
        run: echo '${{ toJSON(job) }}'
      - name: Dump steps context
        run: echo '${{ toJSON(steps) }}'
      - name: Dump runner context
        run: echo '${{ toJSON(runner) }}'
      - name: Dump strategy context
        run: echo '${{ toJSON(strategy) }}'
      - name: Dump matrix context
        run: echo '${{ toJSON(matrix) }}'
```
