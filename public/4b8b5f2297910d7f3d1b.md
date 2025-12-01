---
title: 【Swift】TextFieldのキーボードを閉じる方法3選
tags:
  - Xcode
  - iOS
  - Swift
private: false
updated_at: '2025-12-02T00:09:48+09:00'
id: 4b8b5f2297910d7f3d1b
organization_url_name: null
slide: false
ignorePublish: false
---
TextFieldのキーボードを閉じる方法をまとめてみました。


![032d4bb4a0add2be1948bec3e048227f.gif](https://qiita-image-store.s3.amazonaws.com/0/160547/a226f72c-098f-c562-c722-63a750a64696.gif)

# 1. 「return」キーを押す
## コードベース
resignFirstResponder()メソッドを利用します。

```swift:ViewController.swift
import UIKit

class ViewController: UIViewController, UITextFieldDelegate{
    
    @IBOutlet weak var inputText: UITextField!
    @IBOutlet weak var outputText: UILabel!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        inputText.delegate = self
    }
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
    }
    
    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        // キーボードを閉じる
        textField.resignFirstResponder()
        outputText.text = textField.text
        return true
    }
}
```

## storyboardベース
Xcodeのイベントアクションを利用します。

![スクリーンショット 2017-06-26 22.56.36.png](https://qiita-image-store.s3.amazonaws.com/0/160547/555ee23d-387f-9b9f-ac2d-93393f5cb13b.png)

①TextFieldの上で右クリック（二本指でタップ）
②「Sent Events」の「Did End On Exit」を「control」キーを押しながらドラッグ
③「Name」をつけて「Connect」

![スクリーンショット 2017-06-26 22.59.41.png](https://qiita-image-store.s3.amazonaws.com/0/160547/2d8473c5-5a0c-07bd-5ee2-38a3a4a86d73.png)

コードが追加されたことを確認できます。

```swift:ViewController.swift
import UIKit

class ViewController: UIViewController {

    @IBOutlet weak var outputText: UILabel!
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
    }

    @IBAction func inputText(_ sender: UITextField) {
        outputText.text = sender.text
    }
}
```

他にも様々なイベントアクションがあるので覚えておくと簡単に実装できます。
参考記事：[ボタンによるイベント処理 – swiftによるiOSアプリ開発](https://d-suga.com/843)

# 2. ボタンを押す
endEditing()メソッドを利用します。
（resignFirstResponder()メソッドでも実装可能です。）

![005c8194729f917d5f8db590273fd42b.gif](https://qiita-image-store.s3.amazonaws.com/0/160547/66776385-0fa7-ef4c-7a2f-43e7c293601d.gif)

```swift
import UIKit

class ViewController: UIViewController {
    
    @IBOutlet weak var inputText: UITextField!
    @IBOutlet weak var outputText: UILabel!
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
    }
    
    @IBAction func button(_ sender: Any) {
        outputText.text = inputText.text
        // キーボードを閉じる
        inputText.endEditing(true)
    }
}
```

# 3. TextField以外の部分をタッチ
touchesBeganメソッドをオーバーライドします。

```swift
import UIKit

class ViewController: UIViewController {

    @IBOutlet weak var outputText: UILabel!
    
    @IBOutlet weak var inputText: UITextField!
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
    }
    
    override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        outputText.text = inputText.text
        self.view.endEditing(true)
    }
}
```

以上をうまく組み合わせることでユーザーにストレスを与えない実装になりそうです。

# 参考記事
[UITextFieldの入力後に入力用キーボードを閉じる方法](http://qiita.com/SRAUFactory/items/7314793bd51e4075a208)
