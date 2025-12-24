---
title: 【Rails】RSpec初心者による初心者のためのテストの書き方
tags:
  - Ruby
  - Rails
  - RSpec
private: false
updated_at: '2025-12-02T00:09:48+09:00'
id: 624e0e8635200abca619
organization_url_name: null
slide: false
ignorePublish: true
---
#はじめに
　こんにちは。RSpec5日目の超初心者です。RSpecのコントローラーのテストについて、自分が初めて行ったコントローラーのテストのコードとともにまとめる記事にしたいと思います。

　実装にあたり、たくさんの記事で勉強させていただきました。深く感謝いたします。
今回の記事はテストに関しての基本的な知識を前提としています。以下の記事が大変わかりやすいです。

　[使えるRSpec入門・その1「RSpecの基本的な構文や便利な機能を理解する」](http://qiita.com/jnchito/items/42193d066bd61c740612)

　また、FactryGirlやFakerがインストール済みの環境で行います。
　[Rails RSpecの基本 ~導入編~](http://qiita.com/shizuma/items/8221544601aa3d0770d2)


　今回テストを行ったのはメッセージを送信する処理を行うmessages_controllerです。
usersとchat_groupsが多対多関係、また、それぞれmessagesと１対多関係を持ちます。

```ruby:messages_controller.rb
class MessagesController < ApplicationController

  before_action :set_chat_group, only: %i(index create)

  def index
    @message = Message.new
  end

  def create
    @message = current_user.messages.new(message_params)
    if @message.save
      redirect_to chat_group_messages_path
    else
      flash[:alert] = "メッセージを入力してください。"
      render action: :index
    end
  end

  private
  def message_params
    params.require(:message).permit(:body, :image).merge(chat_group_id: params[:chat_group_id])
  end

  def set_chat_group
    @chat_group = ChatGroup.find(params[:chat_group_id])
  end
end

```

#テストの書き方
　コントローラーのテストの実装は

①テストケース設計
②テストデータ作成
③テストロジック作成
④リファクタリング

の順序で行います。テストの実装手順に関しては[こちら](http://qiita.com/geshi/items/a930461f36bae880657d)の記事を参考にさせていただきました。このように段階的に実装していくことでテストの構造を理解しながら進めていくことができました。

#1.テストケース設計
　コントローラーのテストでは、1つのアクションにつき2つの挙動をテストします。

①正しいビューに変遷するか。
②インスタンス変数（アクション内で@〜で定義している変数）が期待された値を持つか。

つまり、今回のコントローラーのテストでは次のように設計します。

###indexアクション
```ruby:messages_controller_spec.rb
describe 'GET #index' do
  it "正しいビューに変遷する" do
  end

  it "@messageが期待される値を持つ" do
  end

  it "@chat_groupが期待される値を持つ" do
  end
end
```
###createアクション
```ruby:messages_controller_spec.rb
describe 'Post #create' do
  context "@messageが保存できた時" do

    it "データベースに値が保存される" do
    end

    it "正しいビューに変遷する" do
    end

  end

  context "@messageが保存できなかった時" do

    it "データベースに値が保存されない" do
    end

    it "正しいビューに変遷する" do
    end

  end

 end
```
　indexアクションに関してはdescribeでのグループ化のみですが、createアクションは少し違っていますね。

　messages_controllerを見ると、createアクションでは条件分岐があります。条件分岐は、contextという機能を用いて、全ての場合についてのテストを行います。contextはdescribeと機能は変わりませんが、「条件分岐のテストである」ことを示すため（可読性を高めるため）、使用します。

#2.テストデータ作成
　テストデータの作成は以下の２つの手順で行います。

①ダミーデータの作成
②テストコントローラ内で定義

##①ダミーデータの作成

```ruby:factories/chat_groups.rb
FactoryGirl.define do

  factory :chat_group do
    name Faker::Team.name
  end
end
```
　上記のようなファイルを用意することで、テストで利用できるダミーデータを作成します。
カラムの属性によって異なるダミーデータの作成方法は[こちら](https://github.com/stympy/faker)が参考になります。

##②テストコントローラ内で定義
###indexアクション
```ruby:messages_controller_spec.rb
…
  it "@chat_groupが期待される値を持つ" do
    chat_group = create(:chat_group)
  end
…
```
　`chat_group = create(:chat_group)`

　このように定義することで作成したダミーデータを呼び出せます。今後、この作成したテストデータでテストを行っていきます。

　以上のような流れで他のexampleのテストデータも作成します。

#3.テストロジック作成
　テストロジックの作成は以下の２つの手順で行います。

①HTTPメソッドの指定
②エクスペクテーションの実装

##①HTTPメソッドの指定
###indexアクション
```ruby:messages_controller_spec.rb
…
  it "@chat_groupが期待される値を持つ" do
    chat_group = create(:chat_group)
    get :index, chat_group_id: chat_group
  end
…
```
`HTTPメソッド 　:(コントローラーのアクション)`
上記のように指定することで擬似的にコントローラーのアクションにリクエストできます。
さらに、パラメータが必要な場合は、ハッシュ形式で渡します。

![image](https://qiita-image-store.s3.amazonaws.com/0/160547/8e911b4e-6bbb-bcb3-26ca-5fc232065c1a.png)
messagesのindexアクションのパスを確認すると、chat_group_idをパラメータで持つことがわかります。
そのため、`chat_group_id: chat_group`でパラメータを渡すことで、作成したchat_groupのパスに擬似的にリクエストできるようになります。

##②エクスペクテーションの実装
###indexアクション
```ruby:messages_controller_spec.rb
…
  it "@chat_groupが期待される値を持つ" do
    chat_group = create(:chat_group)
    get :index, chat_group_id: chat_group
    expect(assigns(:chat_group)).to eq chat_group
  end
…
```
　assignsメソッドを用います。assignsメソッドはコントローラーのインスタンス変数をテストするメソッドです。引数にインスタンス変数をシンボル型で渡します。

　今回の場合、messages_controller.rbのindexアクションで@chat_groupというインスタンス変数を定義しているため、これのテストになります。

　`expect(assigns(:chat_group)).to eq chat_group`

　すなわち、この一行では、message_controller.rbのindexアクションで定義されている@chat_groupというインスタンス変数と、テスト内で作成したchat_groupというテストデータが確かに同じであることを検証しています。これが同じであれば、インスタンス変数が期待された値を持つと言えることになります。

　その他のexampleに関しても、テストしたい内容によってエクスペクテーションを実装していきます。

#4.リファクタリング

###let
```ruby:messages_controller_spec.rb
describe MessagesController do
  let(:chat_group) { create(:chat_group) }

  describe 'GET #index' do
    it "renders the :index template" do
      ~~~
    end

    it "assigns the requested messsage to @message" do
      ~~~
    end

    it "assigns the requested chat_group to @chat_group" do
      get :index, chat_group_id: chat_group
      expect(assigns(:chat_group)).to eq chat_group
    end
  end
end
```
　letでテストデータを一度定義してしまえば、それぞれexampleでわざわざテストデータを定義する必要がなくなります。コード量が減らせ、可読性も高まるためテストデータを定義する際はletを用いたいですね。

　そのほかにも様々なリファクタリングの方法があるようです。知っておけば量が少なく、可読性が高まるコードが書けるので紹介した記事などを参考にしてみてください。

#最後に
　以上のように段階的に分解して考えていくことで、少しずつテストを理解できました。間違っている点や改善点がありましたらご指摘お願いします。

#参考
- [RSpecでRailsのテストをしてみるテスト。](http://ginpen.com/2012/02/14/rspec-rails/)
- [Rails RSpecの基本 ~Controller編~](http://qiita.com/shizuma/items/84e07e558abd6593df15)
- [Rails4 rspecとFactoryGirlを用いたdeviseでサインインした状態でのコントローラのテスト](http://ayaketan.hatenablog.com/entry/2014/06/03/211110)
