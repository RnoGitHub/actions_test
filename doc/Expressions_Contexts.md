# Expression and Function

## Refer

[Contexts](https://docs.github.com/en/actions/learn-github-actions/contexts)
[Functions](https://docs.github.com/en/actions/learn-github-actions/expressions#functions)

## ${{ }}

---
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

## Functions

---
Upper example toJSON  
other is
[here](https://docs.github.com/en/actions/learn-github-actions/expressions#functions).

```yaml
echo ${{ contains( 'hello','ll' ) }}
echo ${{ startsWith( 'hello','he' ) }}
echo ${{ endsWith( 'hello','lo' ) }}
echo ${{ format( 'Hello {0} {1} {2}','World', '!', '!' ) }}
```

## if

if: evaluate

```yaml
name: Contexts testing
on: [push, pull_request]

jobs:
  funtions:
   runs-on: ubuntu-20.04
   steps:
     - name: dump
       run: |
         echo ${{ contains( 'hello','ll' ) }}
         echo ${{ startsWith( 'hello','he' ) }}
         echo ${{ endsWith( 'hello','lo' ) }}
         echo ${{ format( 'Hello {0} {1} {2}','World', '!', '!' ) }}

  dump_contexts_to_log:
    runs-on: ubuntu-latest
    if: github.event_name == 'push'
    #if true
    steps:
      - name: Dump GitHub context
        id: github_context_step
        run: echo '${{ toJSON(github) }}'
      - name: Dump job context
        if: failure()
        # if true:do run  else: false skip
        run: echo '${{ toJSON(job) }}'
      - name: Dump steps context
        if: always()
        # always run
        run: echo '${{ toJSON(steps) }}'
      - name: Dump runner context
        run: echo '${{ toJSON(runner) }}'
      - name: Dump strategy context
        run: echo '${{ toJSON(strategy) }}'
      - name: Dump matrix context
        run: echo '${{ toJSON(matrix) }}'
```
