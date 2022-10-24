# GitHub Actions

## Table of Contents

- Guidance for GitHub actions
  - What is the github actions?
  - What are workflows?
  - A Runner
  - GitHub-hosted Runners
  - Self-hosted Runners
  - Pre-installed software
  - Summary GitHub Actions
- Yaml

## What is the github actions?

---
A tool that lets you automate your sofware development workflows.
You can write individual tasks, called actions, and combine them to create a custom workflow.  
ソフトウェア開発のワークフローを自動化するためのツールある。
アクションと呼ばれる個々の作業を記述し、それらを組み合わせて独自のワークフローを作成することができる。

## What are workflows?

---
Workflows are customautomated processes that you can set up in your repository to build, test, package, release, or deploy any code project on GitHub.  
ワークフローは、GitHub 上のあらゆるコードプロジェクトをビルド、テスト、パッケージ、リリース、デプロイするために、リポジトリに設定するカスタム自動化プロセスである。

`GitHub Repository` occer event  

- Event example
  - push
  - pull request(Opened merged)
  - issue(Created, Closed)
  - schedule(every 6pm)
  - external event

-------------------- ↓ `workflow` --------------------

- job1
  - `Virtual Machine instance`  
    Linux, Windows, MacOS with tools installed or Docker Container.
    - Step1(Action)
    - Step2(Action)
    - Step3(Command)
    - Step4(Command)
- job2
  - `Virtual Machine instance`  
    Linux, Windows, MacOS with tools installed or Docker Container.
    - Step1(Action)
    - Step2(Action)
    - Step3(Command)
    - Step4(Command)

It includes different OS, different timming(sequential, parallel)
違うOS、違うタイミングの物を含む

ex. Android OS and iOS build.

例．アンドロイドOSとiOSのビルド

- job1
  - `Windows Virtual Machine`  
    Building an android version of an app
- job2
  - `macOS Virtual Machine`  
    Building an iOS version of an app
- job3
  - `Linux Virtual Machine`  
    Testing the code

## A Runner

---

- Any machine with the GitHub Actions runner application installed.
- A Runner is responsible for running you jobs whenever an event happens and displays back the results.
- It can be hosted by Github or you can host your own runner.
GitHub Actions のランナーアプリケーションがインストールされているマシンであれば、どれでも構わない。
- ランナーは、イベントが発生するたびにジョブを実行し、その結果を表示する役割を担う。
- Githubがホストすることもできるし、自分でランナーをホストすることもできる。  

### GitHub-hosted Runners

---

- Linux, Windows or MacOS virtual environments with commonly-used pre-installed software.
- Maintained by GitHub.
- You cannot customize the hardware configration.
- Linux、Windows、MacOSの仮想環境で、一般的に使用されているプリインストールソフトウェアを使用することができる。
- GitHubによって管理されている。
- ハードウェア構成のカスタマイズはできない。

### Self-hosted Runners

---

- A machine you manage and maintain with the runner application installed.
- You have more control of hardware, operating system, and software tools than GitHub-hosted runners provide.
- Ideal if you need to control hardware. Ex. Add more memory for larger jobs. Or choose an operating system not offered by Github-hosted runners.  
- ランナーアプリケーションをインストールした、あなたが管理・メンテナンスするマシン。
- GitHub でホストされるランナーよりも、ハードウェア、OS、ソフトウェアツールのコントロールが可能。
- ハードウェアの制御が必要な場合に最適である。例. より大きなジョブのためにメモリを追加する。または、Githubホストランナーで提供されていないオペレーティングシステムを選択する。  

## Pre-installed software

---

- Tools like curl, git, npm, yarn and pip.
- Languages like python, ruby, nodeJS.
- Android SDK and Xcode.
- curl、git、npm、yarn、pipのようなツール。
- Python、ruby、nodeJSのような言語。
- Android SDKとXcode。

## Summary GitHub Actions

---

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
