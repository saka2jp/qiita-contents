---
title: 【Swift】hogehoge.delegate = self は何をしているのか。
tags:
  - Xcode
  - iOS
  - Swift
private: false
updated_at: '2025-12-02T00:09:48+09:00'
id: 7667e0cc81ad91016f03
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
プログラミング経験：Ruby3ヶ月。Python3ヶ月
Swift始めて9日目の人間が書きます。至らない点があると思うのでぜひご指摘お願いします。
前回：[【Swift】俺はデリゲートなんか使わない。](http://qiita.com/JumpeiYoshimura/items/de0905a8e415e8d9c0e6)

デリゲートがよくわかりません。

特に、

`hogehoge.delegate = self`　←　コイツ

コイツを理解するために徹底的に調べてみました。


# デリゲートについて
デリゲートの概念についてはわかりやすいサイトや記事があるのでそれを参考にしてみてください。

[Swift言語を学ぶ](http://tea-leaves.jp/swift/content/%E3%83%97%E3%83%AD%E3%83%88%E3%82%B3%E3%83%AB)
[プロトコルとデリゲートのとても簡単なサンプルについて](http://qiita.com/mochizukikotaro/items/a5bc60d92aa2d6fe52ca)

簡単にまとめると、

**デリゲートは他のクラスに処理を委譲したり、通知したりする仕組み**

です。

①処理を依頼するクラス
②処理を依頼するクラスと処理を依頼されるクラスを取り持つプロトコル
③処理を依頼されるクラス

の3つの動きを理解するとわかりやすいです。

# とりあえず実装してみる
仕組みはわかったけど実装できないと意味がありません。
デリゲートを用いて実装してみます。

「TextField(inputText)に文字列を入力後、**returnを押したら** Label(outputText)に入力された文字列が表示される」という実装内容です。

![032d4bb4a0add2be1948bec3e048227f.gif](https://qiita-image-store.s3.amazonaws.com/0/160547/a226f72c-098f-c562-c722-63a750a64696.gif)

```swift:ViewController.swift
import UIKit

class ViewController: UIViewController, UITextFieldDelegate { // 追加記述①

  @IBOutlet weak var inputText: UITextField!
  @IBOutlet weak var outputText: UILabel!

  override func viewDidLoad() {
    super.viewDidLoad()
    // 追加記述②
    inputText.delegate = self
  }

  override func didReceiveMemoryWarning() {
    super.didReceiveMemoryWarning()
  }
  
  // 追加記述③
  func textFieldShouldReturn(_ textField: UITextField) -> Bool {
    textField.resignFirstResponder()
    let text = textField.text
    outputText.text = text
    return true
  }
}
```

どうやら3つの記述を追加することでデリゲートを用いた実装ができるってことがわかります。

それぞれ何をしているのかみていきます。


## ①ViewControllerクラスがUITextFieldDelegateプロトコルに準拠することを宣言する

クラスがプロトコルに準拠しているとは、**クラスがプロトコル（クラスの挙動を決めた設計図）を参照している**といったイメージだと思います。

では、なぜクラスをプロトコルに準拠させるんでしょう。

**UITextFieldDelegateプロトコルの定義を確認してみましょう。**

![スクリーンショット 2017-06-20 17.33.24.png](https://qiita-image-store.s3.amazonaws.com/0/160547/9b47fff6-ff7e-614b-ae6e-43d2fb1a869f.png)

・UITextFieldDelegateを選択して右クリック（二本指でタップ）
・Jump to Definitionをクリック
（この操作でクラスやプロトコルの定義を確認できます。）

![スクリーンショット 2017-06-20 17.33.56.png](https://qiita-image-store.s3.amazonaws.com/0/160547/931dcfd8-f236-9502-aff0-e987246bc184.png)

UITextDelegateプロトコルにtextFieldShouldReturnメソッドが定義されています！
他にも様々なメソッドが定義されていることがわかります。

UITextFieldDelegateに定義されているtextFieldShouldReturnを使うためにこの実装が必要だったんですね。

まとめると、この実装で

**依頼するクラス(ViewController)にこのプロトコル(UITextFieldDelegate)を使いますよと教えてあげていた**ということになるかと思います。


## ②inputTextのdelegateの通知先を自分自身に設定する

私はこの

```swift
inputText.delegate = self
```

に最も苦戦しました。日本語訳してみると、

**UITextFieldクラスのインスタンスであるinputTextのdelegateプロパティにViewControllerのインスタンスを渡している**

です。これがどういったことを意味しているのか理解するのが難しかったです。

※ プロパティについての参考サイト：[Swift言語を学ぶ](http://tea-leaves.jp/swift/content/%E3%83%97%E3%83%AD%E3%83%91%E3%83%86%E3%82%A3)

一旦、

```swift
inputText.delegate = self
```

からは離れて

```swift
outputText.text = text
```

を考えてみましょう。(上記実装内容のtextFieldShouldReturnメソッドの4行目です）

あれ？なんか形似てますね。。。
これは何をしてるのか初心者の私でも直感的にわかりました。

**UILabelクラスのインスタンスのtextプロパティにUITextFieldクラスのインスタンスのtextプロパティを渡しています。**

UILabelとUITextFieldの定義を確認してみましょう。
![スクリーンショット 2017-06-21 11.08.51.png](https://qiita-image-store.s3.amazonaws.com/0/160547/1c7053f5-3f45-3202-699d-b0b97c52fea5.png)

![スクリーンショット 2017-06-21 11.08.25.png](https://qiita-image-store.s3.amazonaws.com/0/160547/075938b4-6705-92db-70dd-31e83f7a5d20.png)

2つとも１行目にtextプロパティが定義されていることが確認できます！

```swift
outputText.text = text
```

outputTextはUITextFieldクラスのインスタンスなので、これは、**outputTextのtextプロパティにtextを代入することを意味します。**


なるほど、だからこう実装することでUITextField(inputText)に入力された文字列をUILabel(outputText)に渡せるんですね。


それでは、

```swift
inputText.delegate = self
```

に戻ってみましょう。

これは、**UITextFieldクラスのインスタンスであるinputTextのdelegateプロパティにViewControllerのインスタンスを渡している**んでしたね。

ふむふむ、なんだかさっきより飲み込めてきた気がします。

inputTextは　UITextFieldクラスのインスタンスです。
**UITextFieldクラス確認してみます。**

![スクリーンショット 2017-06-20 17.06.10.png](https://qiita-image-store.s3.amazonaws.com/0/160547/86da929e-ab57-6a44-a18d-71b4f10bdf80.png)


textプロパティと同じようにdelegateというプロパティが定義されているのが確認できます。

通常、変数の定義の時は型宣言をします。

```swift
open var text: String?
```
textプロパティであればString型が宣言されています。

これは、**String型の値を代入できる変数textを定義しています。**

※ 変数の型についての参考サイト：[「分かりそう」で「分からない」でも「分かった」気になれるIT用語辞典](http://wa3.i-3-i.info/word11026.html)

```swift
weak open var delegate: UITextFieldDelegate?
```

同じように、delegateプロパティはUITextFieldDelegateを型宣言しています。
UITextFieldDelegateとはプロトコルです。

プロトコルを型宣言すると、**変数にはそのプロトコルに準拠している値（オブジェクト）を格納できるようになります。**

つまりこれは、**UITextFieldDelegateプロトコルに準拠しているオブジェクトを代入できる変数delegateを定義しています。**

※ プロトコルの型宣言についての参考サイト：[Swift プログラミング](https://ez-net.jp/article/79/kblLTu9C/EbTamNAA9jw_/)
※ オブジェクトについての参考サイト：[クラスとオブジェクトとインスタンスの関係
](http://qiita.com/N-qiita/items/de972c176f50c22414a6)


```swift
inputText.delegate = self
```

inputTextはUITextFieldクラスのインスタンスなので、これは**inputTextのdelegateプロパティにselfを代入している**という意味になります。

selfはViewControllerクラスのインスタンスですが、ViewControllerクラスは①でUITextFieldDelegateプロトコルに準拠する宣言をしています。

すなわち、**そのインスタンスであるselfもまたUITextFieldDelegateに準拠しています。**

つまり、何を意味するかというと、
**inputTextがreturnを押されたらViewController（私）に教えてね！**
といったことかと思います。

**returnが押されたら**という処理は③で実装するので、
②単体の意味は、

**inputTextでUITextFieldDelegateプロトコルで定義されているメソッドが実行されたらViewController（私）に教えてね！**

ということになります。

**inputTextのdelegateの通知先を自分自身に設定する**
という表現をサイトでよく見かけましたが、ここまで細かく噛み砕いてようやく理解できました。

## ③delegateから通知してほしい内容を指定する

ここまで理解できてしまえば、③の実装は問題ないかと思います。
依頼したい処理のメソッドとその後の処理を実装します。

delegateから通知してほしいのは**returnが押されたら**というタイミングなので、その処理をしてくれるメソッドであるtextFieldShouldReturnを指定します。

#まとめ
##一般的な説明
①**クラスがプロトコルに準拠することを宣言する**
②**delegateの通知先を自分自身に設定する**
③**delegateから通知してほしい内容を指定する**
##自分なりの解釈
依頼するクラス：ViewController
依頼されるクラス：UITextField
プロトコル：UITexgFieldDelegate

①**処理を依頼するクラスにこのプロトコルを使いますよと教えてあげる**
②**依頼されるクラスのインスタンスでプロトコルで定義されているメソッドが実行されたら私（ViewController）に教えてね！**
③**プロトコルで定義されているメソッドのうちなんのメソッドの処理を依頼するか指定する**

①、②、③の情報を整理された図が[こちらのサイト](https://teratail.com/questions/30716)でわかりやすくまとめられています。
文字ばかりで説明してしまったので思考の整理ができると思います。ぜひ見てみてください。

[猿がもがきまくって理解したSwiftのデリゲート（Delegate）という仕組み](http://qiita.com/ika_tarou/items/8208153f30fdb4144c18)
こちらの記事もわかりやすかったです。

最終的には一般的な説明で理解しています。
一般的な説明の補助になれば幸いです。




