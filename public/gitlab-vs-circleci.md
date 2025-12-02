---
title: GitLab CI/CD vs CircleCI
tags:
  - GitLab
  - CircleCI
  - GitLab-CI
private: false
updated_at: '2018-12-03T19:33:52+09:00'
id: d83cd18cff7a48fb3f52
organization_url_name: gitlab-jp
slide: false
ignorePublish: false
---
# はじめに
GitLab CI/CDとCircleCIの違いを比較する記事です。

# GitLab CI/CDって何？

https://about.gitlab.com/features/gitlab-ci-cd/

> GitLab has integrated CI/CD pipelines to build, test, deploy, and monitor your code
Rated #1 in the Forrester CI Wave™

Forresterに認められたNo.1 CIサービス。

> GitLab supports development teams with a well-documented installation and configuration processes, an easy-to-follow UI, and a flexible per-seat pricing model that supports self service. GitLab’s vision is to serve enterprise-scale, integrated software development teams that want to spend more time writing code and less time maintaining their tool chain

Forresterのレポートによると、整備されたドキュメントや使いやすいUI、GitLabのビジョンが賞賛されています。

GitLabへの移行で他のCIサービス使っているというケースは考えられますが、GitLabを使っているならGitLab CI/CDを選択するのがおそらく一般的です。

# CircleCIって何？

https://circleci.com/product/

> Power, Flexibility, and Control
CircleCI gives your team more speed and configurability than ever before.

他サービスとの柔軟な連携や容易な設定が売りとしています。
ForresterにはGitLabと同じくLeaderに認定されています。

https://www2.circleci.com/circleci-forrester-wave-leader-2017.html

> Organizations striving to be lean and stay lean will appreciate the simplified, nearly zero-maintenance approach CircleCI provides. Existing customers will appreciate the new features of CircleCI 2.0 that appear to completely address all the top asks that customers are looking for.

Forresterのレポートによると、ほぼ保守が不要な点と2.0の新機能が賞賛されています。

GitHubであればTravis CIに続いて2番目のシェア率と利用者も多いようです。

![32575895-ea563032-c49a-11e7-9581-e05ec882658b.png](https://qiita-image-store.s3.amazonaws.com/0/160547/c0983151-3888-2e81-3097-faf32de88e01.png)

参考：https://blog.github.com/2017-11-07-github-welcomes-all-ci-tools/


# GitLab CI/CD vs CircleCI
それぞれサービスでGitLab CI/CDとの違い、またはCircleCIとの違いを主張するページがあります。
それぞれの主張を列挙してみます。

## GitLab CI/CDの主張

https://about.gitlab.com/comparison/gitlab-vs-circleci.html

- CLI, API, Webhookを提供しており、これらを活用することで他サービスとの連携が可能である。
- GitLab CI/CD にあってCircleCIにない機能が29個ある。
  - Application performance monitoring and alerts
  - Preview your changes with Review Apps
  - Code Quality
  - Show code coverage rate for your pipelines
  - Auto DevOps
  - Easy integration of existing Kubernetes clusters
  - Easy creation of Kubernetes clusters on GKE
  - etc...

## CircleCIの主張

https://circleci.com/gitlab-versus-circleci/

- チームの成長段階に合った最適なツールとの統合ができる。
  - GitHub, BitBucket, Slack, AWSなど、サービス切り替えが容易である。
  - GitLab CIはGitLabのユーザしか使えない。
- CI/CDにのみ焦点を当てたサービスである。
- buildersの管理が容易。
  - GitLab Runnerは独自で管理する必要がある。

まとめると、

**GitLab CI/CD**「GitLabは、DevOpsを実現するための統合ツールであり、我々はその一つのサービスである。DevOpsを実現するための機能をたくさん提供している。」

**CircleCI**「私たちは何かのツールに依存したサービスではない。CI/CDにのみ焦点を当てており、他サービスとの連携・切り替えが容易である。」

みたいなイメージかなと思います。なんとなくそれぞれのCIサービスの色が見えてきた気がします。

# YAMLファイル
Pythonスクリプトをテスト、文法チェック、コードメトリクス計測を実行するシンプルな例で実際のYAMLファイルを比較してみます。

よりスマートに書けるかもしれませんが、GitLab CI/CDもCircleCIもかなり直感的に書けることがわかります。

## GitLab CI/CD

```yml
.test_template: &test_definition
  stage: test
  image: python:3.7
  before_script:
    - pipenv install --system --dev

pytest:
  <<: *test_definition
  script:
    - py.test --tb=line --cov-report=html
  artifacts:
    paths:
      - htmlcov

flake8:
  <<: *test_definition
  script:
    - flake8

radon:
  <<: *test_definition
  script:
    - radon cc -n C .
    - radon mi -n B .

```

## CircleCI

```yml
version: 2
jobs:
  build:
    working_directory: ~/repo
    docker:
      - image: circleci/python:3.7
    steps:
      - checkout
      - run: sudo chown -R circleci:circleci /usr/local/bin
      - run: sudo chown -R circleci:circleci /usr/local/lib/python3.7/site-packages
      - restore_cache:
          key: deps1-{{ .Branch }}-{{ checksum "Pipfile.lock" }}
      - run:
          command: |
            pipenv install --system --dev
      - save_cache:
          key: deps1-{{ .Branch }}-{{ checksum "Pipfile.lock" }}
          paths:
            - ".venv"
            - "/usr/local/bin"
            - "/usr/local/lib/python3.7/site-packages"
      - run:
          command: |
            py.test --tb=line --cov-report=html
      - store_artifacts:
          path: htmlcov/
      - run:
          command: |
            flake8
      - run:
          command: |
            radon cc -n C .
            radon mi -n B .
```

# 所感
## GitLab CI/CDが優れていると感じた点
- YAMLファイルに無駄がなく洗練されている。
- GitLabという一つのサービスでソースコードの管理とCI/CDを実現できる
  - 同じGUIで利用できる

## CircleCIが優れていると感じた点
- CIの実行速度が速い（体感）
- GitHubアカウントがあればすぐに始められる

# おわりに
どちらも簡単に始めることができますし、条件はありますが基本的に無料で使えます。
さすがどちらのサービスもForresterに最高ランクであるLeaderに認定されているだけあります。

個人的にはGitLabプロジェクトではGitLab CI/CDを、GitHubプロジェクトではCircleCIを選択しています。
ちなみに、 [GitLab CI/CD for GitHub](https://about.gitlab.com/features/github/) という機能があるのでGitHubでGitLab CI/CDを使うこともできます。

よりざっくばらんな所感をまとめたブログを書いていますのでよろしければのぞいてみてください。

[コテコテのGitLabユーザがCircleCIに入門してみた](https://jumpyoshim.hatenablog.com/entry/getting-started-circleci-by-gitlab-user)
