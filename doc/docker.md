# Docker

## Refer

[simple-docker-nodejs-api](https://github.com/alialaa/simple-docker-nodejs-api)

## Implement

``` yaml
# action.yml
name: 'Hello World'
description: 'Greet someone and record the time'
inputs:
  who-to-greet:  # id of input
    description: 'Who to greet'
    required: true
    default: 'World'
outputs:
  time: # id of output
    description: 'The time we greeted you'
runs:
  using: 'docker'
  image: 'Dockerfile'
  args:
    - ${{ inputs.who-to-greet }}
```

Docker コンテナを作ることもできる。

```yaml
name: Container

on: push

jobs:
  docker-steps:
    runs-on: ubuntu-20.04
    container: 
      image: node:19.0.0-alpine3.15
    steps:
      - name: Log node version
        run: node -v
      - name: Step with docker
        uses: docker://node:12.14.1-alpine3.10
        with:
          entrypoint: '/bin/echo' #コンテナ起動時にechoコマンドを実行
          args: 'Hello World' #echoコマンドの引数
      - name: Log node version
        uses: docker://node:12.14.1-alpine3.10
        with:
          entrypoint: '/usr/local/bin/node' #コンテナ起動時にechoコマンドを実行
          args: '-v' #echoコマンドの引数
```
