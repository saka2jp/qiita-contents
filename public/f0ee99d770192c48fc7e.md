---
title: タスク管理専用のGitLabプロジェクトの作り方
tags:
  - GitLab
  - プロジェクト管理
  - issue
  - タスク管理
private: false
updated_at: '2018-09-21T19:43:22+09:00'
id: f0ee99d770192c48fc7e
organization_url_name: gitlab-jp
slide: false
ignorePublish: false
---
# はじめに
> GitLabは、バージョン管理システムを主体としたRuby on Rails製のアプリケーション開発支援ツールです。

　[GitLab実践ガイド](https://www.amazon.co.jp/dp/4295003034/)より[^1]

　とあるように、Gitリポジトリ管理、issue管理、CI/CD、Wiki、コンテナレジストリ、GitLab Pages（静的サイトホスティング）、モニタリング、Kubernetes連携機能もあり、アプリケーション開発・運用のために統合的な機能を提供するGitLabですが、その中でもプロジェクトをissue管理専用として使いたい（ソースコードの管理はしない）という状況がありましたので、その解決策を共有させていただきます。


# Issuesのみを表示する
　何を言っているかというと、プロジェクト作成時、デフォルトではIssues、Repository、Merge Requests、CI/CD、Wiki、Snippetsが表示されていますが、Issuesのみを表示したいということです。
 
 　以下はプロジェクト作成時の初期状態のトップページですが、Repositoryが表示されます。このプロジェクトではソースコードの管理などは想定していないため、このトップページのままなのは少し気になります。（READMEを書いてもいいですが、、、）
 
<img width="1437" alt="Screen Shot 2018-03-06 at 10.03.25.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/3d2eb3fd-9049-a33d-5b74-2cd53751a415.png">


　これをIssuesのみの表示にするためには、Settings > General > Permissions から設定を行うことができます。今回はIssuesのみを利用したいので、Repository（Merge Requests、Pipelines、Container registry）、Wiki、Snippetsは無効にして保存します。
 
**変更前(プロジェクト作成時の初期状態)**
![Screen Shot 2018-03-07 at 19.00.22.png](https://qiita-image-store.s3.amazonaws.com/0/160547/eff5f6b4-c18d-28c0-349b-72da31214584.png)


**変更後**
![Screen Shot 2018-03-10 at 17.36.24.png](https://qiita-image-store.s3.amazonaws.com/0/160547/1af46b06-9806-1b70-1788-caff7b068e51.png)


　その後、プロジェクトのトップページを確認してみます。（写真はわかりやすいようにissueを作成してあります。）左側に表示されているタブバーを確認してみても、Repository、Wiki、Snippetsが表示されていないことがわかります。

 
<img width="1440" alt="Screen Shot 2018-03-06 at 10.19.07.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/64d1ac4b-9744-8c98-31ab-4645332a873e.png">

実際のGitLab Projectです。
↓↓↓↓↓↓↓↓↓↓↓↓↓↓
https://gitlab.com/jumpyoshim/only-issues

# もしうまくいかなかったら
　User Settings > Preferences > Behavior の設定がデフォルト状態ではないかもしれません。デフォルトの設定に変更してあげることで期待通りの挙動になるかもしれません。試してみてください。（User Settingsは右上のアイコンをクリックすると表示されます。）

![Screen Shot 2018-03-07 at 20.05.13.png](https://qiita-image-store.s3.amazonaws.com/0/160547/bd4e33e8-65ac-7085-1328-bba6b3e16477.png)


# おわりに
> GitLabのビジョン
誰しもがすべてのデジタルコンテンツを共同作業できるようにし、チームが効果的に協力し合いよりよい成果をより早く達成できるようにすることです。

　[GitLab実践ガイド](https://www.amazon.co.jp/dp/4295003034/)より

　注目していただきたいのは、「誰しもが」 という点です。また、以下のようにも述べられています。

> GitLabを利用すべきメリットは、誰しもが容易に利用できるWebインターフェイスを社内環境に構築できることです。コンソールを利用せずともブラウザからすべてのコンテンツ管理ができるので、エンジニアだけでなく、経営層やマーケティングといったビジネス側のメンバーとも共通の目線でコンテンツを共有することができます。 

　こういったGitLabのビジョンやメリットを考慮したとき、チーム内のいろんな職種の人の利用が想定され、かつタスク管理としてしか利用しない場合は、不要なRepositoryやSnippetは非表示にした方が良いような気がします。多機能は必ずしもユーザにとって使いやすいとは言えません。
 
 　何はともあれ、簡単に設定できるのでぜひ活用してみてください。
  
 
[^1]: GitLab実践ガイド第1章は[無料公開](https://impress.tameshiyo.me/9784295003038)されています。
