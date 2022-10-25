# Environment Variables Encryption

## Refer

[Environment variables](https://docs.github.com/en/actions/learn-github-actions/environment-variables#default-environment-variables)  
[GitHub Actions の if と env](https://zenn.dev/matken/articles/github-actions-if-and-env)

## Env

---
ENV define as it follows

``` yaml
env: variable

#ref
echo ${variable}
```

## env scope

---
Env scope is `Step`.

``` yaml
jobs:
  log-env:
    runs-on: ubuntu-20.04
    env:
      JPB_ENV: Available to all steps in log-env jpb
    steps:
      - name: Log ENV Variables
        env:
          STEP_ENV: Available to only this step
        run: |
          echo "WF_ENV: ${WF_ENV}"
          echo "JPB_ENV: ${JPB_ENV}"
          echo "STEP_ENV: ${STEP_ENV}"
      - name: Log Env 2
        run: |
          echo "WF_ENV: ${WF_ENV}"
          echo "JPB_ENV: ${JPB_ENV}"
          echo "STEP_ENV: ${STEP_ENV}"
          # Not effective
```

## When is ENV effective?

---
You want to separate flow by using `if` and `ENV`.  

Separate point

- Who access?
- Which Repository?
- Which WorkFlow?
- Which Event Name?

ex. When you get docker image path and use it next steps.  

``` yaml
steps:
  - name: "Output docker image url"
    # Write ENV
    run: echo 'DOCKER_IMAGE_URL=gcr.io/cloudrun/hello' >> $GITHUB_ENV

  - uses: 'google-github-actions/deploy-cloudrun@v0'
    if: startsWith(env.DOCKER_IMAGE_URL, 'gcr.io')
    with:
      service: 'hello-cloud-run'
      # Use(Read) ENV
      image: '${{ env.DOCKER_IMAGE_URL }}'
```

## Default ENV

github has default env

|default env|meaning|example|
|---|---|---|
|${HOME}|pwd|/home/runner|
|${GITHUB_WORKFLOW}|workflow name|hoge|
|${GITHUB_ACTION}|status|run|
|${GITHUB_ACTIONS}|status|true|
|${GITHUB_ACTOR}|triggered user|bar|
|${GITHUB_REPOSITORY}|repository path|repo path|
|${GITHUB_EVENT_NAME}|event type|push|
|${GITHUB_WORKSPACE}|workspace path|/home/runner/work/|
|${GITHUB_SHA}|check out id|da8eb2cac9db965e4bf3e0cd453651dc774a2595|
|${GITHUB_REF}|headder ref|refs/heads/feature_hoge|
