---
title: 知って「おっ！」てなったGitLabの知識7選
tags:
  - GitLab
private: false
updated_at: '2020-01-07T01:38:58+09:00'
id: d5a63bdd3681843866f8
organization_url_name: gitlab-jp
slide: false
ignorePublish: false
---
GitLabダイスキー！
ということで、知った時に「おっ！」と感じたGitLabに関する事項を選出してみました。

あなたに「おっ！」と思ってもらえたら幸せです。

![34473826-40b4987c-ef2c-11e7-90b9-5ff322c4966f.png](https://qiita-image-store.s3.amazonaws.com/0/160547/9fe1eb20-e5e4-4646-25bc-9c2525f30298.png)


# はじめに

[知って「おっ！」てなったGitHubの知識7選](https://qiita.com/ukiuni@github/items/56ff7dd04c1c2748fbbb) こちらの記事のパロディです。

# 知って「おっ！」てなったGitLabの知識7選

## 1. Issue Board：GitLabでカンバンが使える

<img width="996" alt="Screen Shot 2018-11-30 at 18.20.06.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/96e32551-47c3-65ea-0440-0eec61b08cff.png">

[Issue Board](https://docs.gitlab.com/ce/user/project/issue_board.html) はカンバンやスクラムボートをWebで使えちゃうタスク管理機能です。

[Trello](https://trello.com/) のような見た目や使い勝手です。

タスクの進捗状況（`Open`, `To Do`, `Doing`, `Closed` など）や追加機能の種類（`Frontend`, `Backend`, `Design`など）でイシューを分類して可視化したりドラッグ＆ドロップで変更できたりします。

GitLabのプランにもよりますが、個人でGitLab.comを利用している分にはボードは複数作成できます。

様々な分類でタスクを分別して可視化できるのでとても便利です。

**Issues** > **Boards** で確認できます。

参考：
・ [GitLabイシューボードでkanbanやスクラムを試してみる](https://qiita.com/tnir/items/a488334247f112b083f3) / @tnir さん

## 2. Time Tracking：GitLabで稼働管理ができる

<img width="761" alt="Screen Shot 2018-12-03 at 20.05.40.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/f7ddf2dd-d53a-e54a-0d15-9d74b9781d0a.png">

[Time Tracking](https://docs.gitlab.com/ce/workflow/time_tracking.html)はイシューの見積もり時間と実際にかかった工数を管理できる機能です。

使い方はいたって簡単で、 `/estimate` で見積もり時間を、 `/spend` で実際にかかった工数を入力できます。

値はイシューの右のサイドバーに表示されます。

<img width="226" alt="Screen Shot 2018-12-03 at 20.08.15.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/e4018570-ba52-d6a6-4c20-968a130534c8.png">

簡単な稼働管理ならタイムトラッキングを活用すればできてしまいます。

参考：
・ [GitLabのIssueで作業時間の記録がとても楽だった](http://takuya-1st.hatenablog.jp/entry/2018/05/16/010110) / それマグで！


## 3. Repository Graph：GitLabでGitヒストリーを確認できる

![repo_graph.png](https://qiita-image-store.s3.amazonaws.com/0/160547/df8db372-1d82-1d8d-c916-3a1e5e4d0a37.png)


[Repository Graph](https://docs.gitlab.com/ce/user/project/repository/#repository-graph) は [Sourcetree](https://ja.atlassian.com/software/sourcetree) のような見た目でGitヒストリーを確認できる機能です。

GitHubでも同様の機能があり **Insights** > **Network** から確認できますが、圧倒的にGitLabの方が使いやすいです。

**Repository** > **Graph** から確認できます。

参考：
・[GitLabのNetwork Graphが優れている4つの理由](https://hiroponz.hateblo.jp/entry/2013/05/29/195056) / プチ技術メモ

## 4. Squash and merge：コミットをまとめてからマージしてくれる

<img width="507" alt="スクリーンショット 0030-12-03 4.16.10.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/991bce2c-b825-0064-38ea-4443fe0e627c.png">


[Squash and merge](https://docs.gitlab.com/ce/user/project/merge_requests/squash_and_merge.html) はチェックボックスにチェックを入れるだけでコミットを一つにまとめてマージしてくれる機能です。

ローカルでリベースする手間が省けるのでとても便利です。

GitLab 11.0のアップデートでGitLab CEのCoreプラン（無料プラン）でも使える機能になりました。

参考：
・ [🎉GitLab11.0でSquash&Merge機能がCommunity Editionで使えるようになります！！🎉](https://qiita.com/st_1t/items/a178612dff1dc197799e) / @st_1t さん

## 5. Labコマンド：CLIでGitLabを操作する
GitLabのCLIクラアントが下記で紹介されています。
https://about.gitlab.com/partners/#cli-clients

HubコマンドライクなCLIクライアントがいくつかあるのですが、なかでも [Lab](https://github.com/zaquestion/lab) は最もスター数が多いCLIクライアントです。

CLIからパイプラインを走らせたり、

```console
lab ci create 11-add-feature
```
Issueをブラウザで表示できたりします。

```console
lab issue browse 11
```


## 6. GitLab CI/CD：標準搭載されているCI/CDツール

https://about.gitlab.com/features/gitlab-ci-cd/

> GitLab has integrated CI/CD pipelines to build, test, deploy, and monitor your code
Rated #1 in the Forrester CI Wave™

GitLab CI/CD はGitLabが提供するForresterに認められたNo.1 CIサービスです。

> GitLab supports development teams with a well-documented installation and configuration processes, an easy-to-follow UI, and a flexible per-seat pricing model that supports self service. GitLab’s vision is to serve enterprise-scale, integrated software development teams that want to spend more time writing code and less time maintaining their tool chain

Forresterのレポートによると、整備されたドキュメントや使いやすいUI、GitLabのビジョンが賞賛されています。

個人的にもGitLab CI/CDはかなり洗練された印象で、特にYAMLの構文は他のCIサービスに比べて無駄がなく書きやすいです。
また、GitLabという一つのサービスでソースコード管理とCI/CDを実現できるのがとても便利だと思います。
例えば、GitHub + CircleCIという構成をとった場合、GUIが2種類になってしまい、行ったり来たりなかなかめんどくさいです。

しかし、パイプラインの実行速度は他のCIサービスに比べると劣るかなと感じています。

参考：
・ [.gitlab-ci.yml によるジョブの設定方法(日本語訳)](https://qiita.com/ynott/items/1ff698868ef85e50f5a1) / @ynott さん
・ [gitlab.com で いますぐCI してみよう](https://qiita.com/tetsukay/items/91a03b38af8c7eec9551)　/ @tetsukay さん

## 7. ロゴはきつねじゃなくてたぬき🦊

GitLabのロゴはたぬきです。きつねではありません。

<img width="487" alt="Screen Shot 2018-11-26 at 18.54.40.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/f4a0a768-1346-e542-806e-df3ec76d1890.png">

FYI: https://twitter.com/GitLabJP/status/1024155016355962881

<img width="398" alt="Screen Shot 2018-11-26 at 18.55.50.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/569f1ff1-6ccf-e0fe-73a3-547d7ecab397.png">

FYI: https://about.gitlab.com/company/

前のロゴはかなりたぬきに似ていますが、個人的にはいまのロゴの方が好みです。（前のロゴ怖い...）

![gitlab-before.png](https://qiita-image-store.s3.amazonaws.com/0/160547/29a550f1-7ad3-fda9-6c3f-61732634a525.png)


# 番外編
7選としてあえて紹介しませんでしたが、本家の記事で紹介されているGitHubのすべての機能をGitLabでも利用できます。

- [Description Templates](https://docs.gitlab.com/ce/user/project/description_templates.html)：イシューやMRのテンプレート機能
- [Automatic issue closing](https://docs.gitlab.com/ee/user/project/issues/automatic_issue_closing.html)：自動イシュークローズ機能
- [Tags](https://docs.gitlab.com/ee/university/training/topics/tags.html)：バージョン管理で便利なタグ
- [GitLab Markdown](https://docs.gitlab.com/ce/user/markdown.html)：チェックボックスを含む基本的なマークダウン記法
- [GitLab Pages](https://docs.gitlab.com/ce/user/project/pages/)：静的サイトのホスティング

---

いかがでしたでしょうか？あなたの「おっ！」があれば幸いです。

# GitLab記事の紹介
- [GitLabの2019年を振り返る〜2億6800万ドルの資金調達・追加された新機能・世界の注目度合い〜](https://qiita.com/jumpyoshim/items/40108374823ea3188ebd)
- [GitLabに草生やしたらGitHubにも草生やしたい](https://qiita.com/jumpyoshim/items/c49bcd8b3994f3503006)
- [タスク管理専用のGitLabプロジェクトの作り方](https://qiita.com/jumpyoshim/items/f0ee99d770192c48fc7e)
