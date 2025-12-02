---
title: 【jQuery】二重送信を防止しつつ、連続送信をする方法
tags:
  - JavaScript
  - Rails
  - jQuery
private: false
updated_at: '2025-12-02T00:09:48+09:00'
id: 4c06ce27c5140e6aebae
organization_url_name: null
slide: false
ignorePublish: false
---
#はじめに
チャット機能を持つアプリケーションの実装中に、メッセージの２重送信を防ぎたいけど２重送信を防止したら連続送信できないじゃん！という現象にハマったのでその解決方法を記します。

#二重送信を防止
`= f.submit "Send", "data-disable-with": "送信中..."`
または
`= f.submit "Send", data: {disable_with: '送信...'}`
とすることで、送信中はボタンを押せなくして、"送信中..."なども文言を表示できます。
しかし、これを実装してしまうと連続投稿ができません。

<連続送信不可>
![fda2ca3c63d60385c1b754be5bd68be1.gif](https://qiita-image-store.s3.amazonaws.com/0/160547/f780f8b7-0489-21fe-8428-179820e29a35.gif)

#解決策①
data-disable-with属性を解除する。
`$('セレクタ').removeAttr('data-disable-with')`

#解決策②
submitのコールバック関数で返り値をfalseにする。
こうすることでフォームの送信を一旦止めることができます。

```js
$('セレクタ').submit(function() {
　　…
 return false;
});
```

<連続送信可能>
![63e556849385a64a7b827c54969d59c4.gif](https://qiita-image-store.s3.amazonaws.com/0/160547/131a77a2-60e0-f0ec-f13f-c5eea85bcb64.gif)

解決策①②共に連続投稿ができるようになりました。

#実際のコード
##解決策①
```js:message.js
$(function() {
  // メッセージ送信情報を追加していく関数
  function buildHTML(message) {
    var html =
    '<li class="chat-message">' +
      '<p class="chat-message__name">' +
          message.name +
      '</p>' +
      '<p class="chat-message__time">' +
          message.time +
      '</p>' +
      '<p class="chat-message__body">' +
          message.body +
      '</p>' +
      '<br>' +
      '<img class="chat-message__image" src="' + message.image + '">'
    '</li>'
    return html;
  }
  
  $('#new_message').on('submit', function(e) {
    // HTMLでの送信をキャンセル
    e.preventDefault();
    var form = $('#new_message');
    var $this = $(this);

    //追記部分
    $('#chat-footer__send-btn').removeAttr('data-disable-with');

    // フォームに入力された値を取得
    var fd = new FormData($this.get(0));

    $.ajax({
      type: form.attr('method'), // フォーム要素("post")を取得
      url: form.attr('action'), // フォーム要素("/chat_group/chat_group_id/messages")を取得
      data: fd,
      contentType : false,
      processData : false,
      dataType: 'json'
    })
    // サーバーから値が正しく返ってきた場合
    .done(function(data) {
      var html = buildHTML(data.message);
      $('.chat-messages').append(html);
      $this.get(0).reset();
      autoScroll();
    })
    // 正しく返ってこなかった場合
    .fail(function() {
      alert('メッセージを送信できません');
    });
  });
});
```
##解決策②
```js:message.js
$(function() {
  // メッセージ送信情報を追加していく関数
  function buildHTML(message) {
    var html =
    '<li class="chat-message">' +
      '<p class="chat-message__name">' +
          message.name +
      '</p>' +
      '<p class="chat-message__time">' +
          message.time +
      '</p>' +
      '<p class="chat-message__body">' +
          message.body +
      '</p>' +
      '<br>' +
      '<img class="chat-message__image" src="' + message.image + '">'
    '</li>'
    return html;
  }
  $('#new_message').submit(function(e) {//修正部分
    // HTMLでの送信をキャンセル
    e.preventDefault();
    var form = $('#new_message');
    var $this = $(this);
    // フォームに入力された値を取得
    var fd = new FormData($this.get(0));

    $.ajax({
      type: form.attr('method'), // フォーム要素("post")を取得
      url: form.attr('action'), // フォーム要素("/chat_group/chat_group_id/messages")を取得
      data: fd,
      contentType : false,
      processData : false,
      dataType: 'json'
    })
    // サーバーから値が正しく返ってきた場合
    .done(function(data) {
      var html = buildHTML(data.message);
      $('.chat-messages').append(html);
      $this.get(0).reset();
      autoScroll();
    })
    // 正しく返ってこなかった場合
    .fail(function() {
      alert('メッセージを送信できません');
    });
    //追記部分
    return false;
  });
});
```

##HTML
```ruby:message.html.haml
.chat-body
  %ul.chat-messages
  - @chat_group.messages.each do |message|
    %li.chat-message
      %p.chat-message__name
        = message.user.name
      %p.chat-message__time
        = message.created_at
      %p.chat-message__body
        = message.body
        - if message.image?
          %br
          = image_tag message.image.url
.chat-footer
  = form_for [@chat_group, @message] do |f|
    .chat-footer__body
      = f.text_area :body, placeholder: "type a message"
      .chat-footer__body__image
        = f.label :image do
          %i.fa.fa-image
            = f.file_field :image
    .chat-footer__btn
      = f.submit "Send", "data-disable-with": "送信中...", id: 'chat-footer__send-btn', class: 'chat-footer__send-btn'
```

#おわりに
rails2ヶ月目、jquery1ヶ月目の超初心者です。
改善点、問題点がありましたらご指摘よろしくお願いいたします。

#参考記事
[jQueryでフォームの送信を一旦止め、処理を挟んでから送信する方法](https://2inc.org/blog/2013/04/05/3117/)
[[Rails]submitタグにつけておきたいdisable_withオプション](http://qiita.com/sue738/items/09f569bdc3a73d26df88)

