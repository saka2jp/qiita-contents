---
title: 【Rails】form_forの使い方
tags:
  - Ruby
  - Rails
private: false
updated_at: '2025-12-02T00:09:48+09:00'
id: ee5af466ef7959567174
organization_url_name: null
slide: false
ignorePublish: false
---
#form_forとは
モデルの新規インスタンスに値を追加して保存したい時に使用するヘルパーメソッド。
フォームが簡単に作成でき、入力されたデータをテーブルに保存できる。

#フォームの作成
レビューのフォームを想定。
###コントローラーの実装

```ruby:reviews_controller.rb
  def new
    @review = review.new
  end

  def create
    Review.create(create_params)
    render action: :new #表示したいビューを表示
  end

  private
  def create_params
    params.require(:review).permit(:text)
  end
```
###ビューの実装
```ruby:new.html.haml
%h1 Review
  = form_for @review do |f|
    = f.label :text, "レビュー"
    = f.text_field :text
    = f.submit "Send"
```

・モデルのインスタンスを引数に持つ。

・引数のインスタンスが何も情報を持っていなければcreateアクション、すでに情報を持っている場合はupdateアクションに自動的に振り分けられる。

・フォームに入力された値は、submitボタンを押した瞬間にモデルクラスの新規インスタンスにそれぞれの属性の値としてセットされ、対応するテーブルのカラムに保存される。

#ネストをした場合
groupsとmessagesが１対多関係。
ネストした場合、引数のインスタンスは二つになる。

```ruby:config/routes.rb
resources :groups do 
  resources :messages
end
```
```ruby:message/new.html.haml
= form_for [@group, @message] do |f|
...
```
