---
title: PythonでCMS、どれ使えばいいの？ 〜Mezzanine vs django CMS vs Wagtail〜
tags:
  - Python
  - Django
  - Mezzanine
  - djangoCMS
  - Wagtail
private: false
updated_at: '2020-01-07T01:39:53+09:00'
id: 5ec4ef7a5615b3c2e9ac
organization_url_name: null
slide: false
ignorePublish: false
---
CMS作るならPHPでWordPress一択？いやいや、PythonだってCMS作れるんです！
この記事はPython製CMSフレームワークの比較とオススメのCMSフレームワークを紹介します。

# 記事の内容
この記事はPython製CMSフレームワークの比較とオススメのCMSフレームワークの紹介を行います。

下記のPython製CMSフレームワークを比較します。

- [Mezzanine](http://mezzanine.jupo.org/)
- [django CMS](https://www.django-cms.org/)
- [Wagtail](https://wagtail.io/)

オススメのCMSフレームワークはズバリ **「Wagtail」** です。
理由は下記の2点です。

- 管理画面のUI/UXが優れている
- アップデートもさかんで勢いがある

# 記事の目的
- Django三大CMSフレームワークのそれぞれの特徴を知る
- どのCMSフレームワークを利用するといいのかを知る

# 動機
この記事を書こうと思った動機は下記の2点です。

- どのCMSフレームワークを使えば良いか迷ったこと
- Python製CMSフレームワークの比較記事がなかったこと

私と同じようにどのCMSフレームワークを使ってみようか迷っている方の助けになればよいなと思います。

# Django三大CMSフレームワークの比較

2019年4月22日時点

|CMS|GitHub スター数|ファーストリリース|日本語ドキュメントの豊富さ（体感）|
|:-:|:-:|:-:|:-:|
|[Mezzanine](https://github.com/stephenmcd/mezzanine)|3780|2009|1st|
|[django CMS](https://github.com/divio/django-cms)|6710|2007|2nd|
|[Wagtail](https://github.com/wagtail/wagtail)|7058|2014|3rd|

**Google Trends**
<img width="440" alt="Screen Shot 2018-11-15 at 17.05.59.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/fbc313a0-1058-76c0-1412-d4204089158a.png">

## [Mezzanine](http://mezzanine.jupo.org/)

> **AN OPEN SOURCE CONTENT MANAGEMENT PLATFORM BUILT USING THE DJANGO FRAMEWORK**
Mezzanine is a powerful, consistent, and flexible content management platform.

上記はMizzanine公式HPのメインタイトルです。
今回取り上げる3つのCMSフレームワークの中でも日本語記事が多いように感じました。
WordpressライクなCMSフレームワークなのでもしかすると選択されやすいフレームワークなのかもしれません。

> In some ways, Mezzanine resembles tools such as [Wordpress](https://wordpress.org/), providing an intuitive interface for managing pages, blog posts, form data, store products, and other types of content. 

Mizzanineの特徴として、Wordpressをかなり意識したCMSフレームワークであるという点が挙げられます。
使い勝手やUIもかなりWordpressに似ているようです。

> WordPress の管理画面を触ったことのある人なら、ほとんどの機能を直感的に理解できるでしょう。

参考：[見よ！これが Python製の WordPress風フルスタックCMSフレームワーク「Mezzanine（メザニン）」だ！](http://akiyoko.hatenablog.jp/entry/2015/12/23/000100) / akiyokoさん


## [django CMS](https://www.django-cms.org/)

> **ENTERPRISE CONTENT MANAGEMENT WITH DJANGO**
The free open-source CMS used by thousands of websites since 2007

上記はdjango CMS公式HPのメインタイトルです。
DjangoのCMSフレームワークとしてのパイオニア的存在で、今回取り上げる3つのフレームワークのうち最もサービスの公開が早いです。


## [Wagtail](https://wagtail.io/)

> Wagtail, the powerful CMS for modern websites.

上記はWagtailのメインタイトルです。
今回取り上げるCMSフレームワークの中では最も後発ながらもGitHubスター数は最も多いです。

> Wagtail is a leading open source CMS. Tens of thousands of organisations worldwide, including Google, NASA, and the British NHS, are powering their digital estates with Wagtail - here’s why.

文章からかなりの自信が伺えます。
開発もさかんなようでissue、PR数共にdjango CMSの2倍くらいあります。
また、3つの中で唯一Python3.7をサポートしています。（2018年12月時点）

さらに、[The Zen of Python](https://www.python.org/dev/peps/pep-0020/) をオマージュした「[The Zen of Wagtail](https://docs.wagtail.io/en/v2.3/getting_started/the_zen_of_wagtail.html)」なるものがあり、ユニークでおもしろいなと思います。

# 管理画面UI/UXの比較
CMSの管理者がよく利用する管理画面のUI/UXに注目して比較してみました。

**Mezzanine**

<img width="944" alt="Screen Shot 2018-11-16 at 18.44.38.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/677e5075-55f8-cdfd-f9ad-b37e240a5cbf.png">

**django CMS**

<img width="833" alt="Screen Shot 2018-11-16 at 14.06.53.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/dd26e79b-7822-72f2-2561-938d27a85278.png">

**Wagtail**

<img width="778" alt="Screen Shot 2018-11-16 at 14.02.17.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/68a92dcc-6f5a-e9bd-f7fc-5d43fa1f7e24.png">

3つとも2カラムレイアウトですが、Mezzanine・Wagtailとdjango CMSで大きく特徴が異なります。

Mezzanine・Wagtailは左カラムにナビゲーションバー、右カラムにナビゲーションバーを選択したコンテンツという割と一般的なUIである一方、django CMSはDjangoデフォルト管理画面とほぼ同じUIです。

また、Wagtailに関してはFont Awesomeが適用されていたり、メールの通知設定や言語設定ができたりとかなり細かい機能までデフォルトで提供されているなという印象を持ちました。

**Wagtail アカウント設定画面**

<img width="922" alt="Screen Shot 2018-11-16 at 19.24.13.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/5982e89a-0770-a0a6-5de1-3e06ad39c683.png">


# おわりに
PHPであればWordpressに人気・認知度が一極化しているように思えますが、Pythonに関してはそうではなかったので調査するのに少し苦労しました。

Pythonは日本ではデータサイエンスのイメージが先行してしまいがちですが、Webアプリケーション開発としてのPythonも優秀な言語だと思うのでもっと盛り上げて行きたいですね。
