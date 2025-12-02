---
title: 【Rails】redirect_toとrenderの使い分け
tags:
  - Ruby
  - Rails
private: false
updated_at: '2025-12-02T00:09:48+09:00'
id: ed10721c26963abdf121
organization_url_name: null
slide: false
ignorePublish: false
---
#renderとredirect_to
###redirect_to

指定したcontroller、actionに再度リクエストを送信
controllerのインスタンス変数は、リダイレクト先で新たに生成

###render

controllerで処理した結果の出力先Viewを指定する
controllerのインスタンス変数は、そのままViewに渡される


基本的に、
データを追加、更新、削除を行う時は「redirect_to」
データの取得を行う時は「render」

```messages_controller.rb
  def index
    @message = Message.new
  end

  def create
    @message = current_user.messages.new(message_params)
    if @message.save
      redirect_to :index
    else
      flash[:alert] = "メッセージを入力してください。"
      render action: :index
    end
  end
```

メッセージボタンを押すとフォームに入力されたメッセージが送信される時の処理。
メッセージの保存に成功すれば、redirect_toにより、indexアクションのリクエストが再度送信されるため、メッセージは正しく表示される。
例えば、ここがrenderだった場合、メッセージの保存は成功するが、正しく表示されない。



#参考記事
http://ruby-rails.hatenadiary.com/entry/20140808/1407427457
http://avosalmon.hatenablog.com/entry/2014/05/17/%E3%80%90Rails%E3%80%91render%E3%81%A8redirect_to%E3%81%AE%E9%81%95%E3%81%84
