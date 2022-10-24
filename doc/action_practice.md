# Intro

outline introduce in summary.

- GitHub actions flow
  - Event
  - Workflow run(Schejule)
  - Job
  - Step
  - Action
- Virtual Environment
- Runners
  - Github-hosted Runner
  - Self-hosted Runners

## First Workflow

---
Make folder .github and workflows.
Then, make file simple.yaml in workflows folder.

``` bash
.github
│   └── workflows
│       └── simple.yaml
```

## Event {on :}

---
`on:` measn event.  
There are several events. Please reffer [Events that trigger workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#branch_protection_rule "Events that trigger workflows")

example  

``` yaml
on: [push, pull_request]
```

`[]` means array.

``` yaml
name: Shell Commands

on: [push]

```

## Event {jobs : simple bash}

---
`jobs:` measn job.  
There are several steps. `bash`, `python` and `pwd`,etc.  
Please reffer [Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions "Workflow syntax for GitHub Actions")

example  

``` yaml
jobs:
  name_tag:
    # Virtual Environment
    runs-on: ubuntu-20.04
    # tasks = steps
    steps:
      - name: echo a string
        run: echo "Hello Github Actions"
```

## Event {multi jobs: parallel }

---
multi event expresses as it follows.

``` yaml
name: Shell Commands

on: [push]

jobs:
  run-shell-command:
    runs-on: ubuntu-20.04
    steps:
      - name: echo a string
        run: echo "Hello Github Actions"
      - name: multiline script
        run: |
          node -v
          npm -v
      - name: python Command
        run: |
          import platform
          print(platform.processor())
        shell: python
  run-windows-command:
    runs-on: windows-latest
    steps:
      - name: Directory Powershell
        run: Get-Location
      - name: Directory Bash
        run: pwd
        shell: bash
```

## Event {multi jobs: sequential }

---
multi event expresses as it follows.  
needs: [`relay on process`]

``` yaml
name: Shell Commands

on: [push]

jobs:
  run-shell-command:
    runs-on: ubuntu-20.04
    steps:
      - name: echo a string
        run: echo "Hello Github Actions"
      - name: multiline script
        run: |
          node -v
          npm -v
      - name: python Command
        run: |
          import platform
          print(platform.processor())
        shell: python
  run-windows-command:
    runs-on: windows-latest
    needs: ["run-shell-command"]
    steps:
      - name: Directory Powershell
        run: Get-Location
      - name: Directory Bash
        run: pwd
        shell: bash
```
