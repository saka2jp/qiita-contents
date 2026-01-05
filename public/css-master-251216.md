---
title: CSSマスターへの道「Animation」
tags:
  - CSS
private: false
updated_at: '2026-01-05T00:03:05+09:00'
id: cf1e9a6b6b45a9ae6993
organization_url_name: null
slide: false
ignorePublish: false
---

Day 16 です。

https://qiita.com/saka2jp/items/7b6f93e569e451d5fa2f

昨日の `transition` は「ホバーしたら変わる」という **受動的** な動きでした。
今日の `animation` は、自動でぐるぐる回ったり、ふわふわ浮き続けたりする **能動的** な動きです。

これを使えば、JavaScript を 1 行も書かずに「ローディング画面」や「注目させたいボタンの動き」を作ることができます。
CSS で「**台本（キーフレーム）**」を書いて、要素に演技をさせましょう。

---

### はじめに：アニメーションは「パラパラ漫画」

CSS アニメーションは、2 つの要素で成り立っています。

1.  **`@keyframes`（キーフレーム）**: 「0% の時はこの場所、50% の時はあそこ、100% でここに戻る」といった **動きの台本**。
2.  **`animation` プロパティ**: 「どの台本を、何秒かけて、何回繰り返すか」という **指示出し**。

この 2 つを組み合わせることで、複雑な動きをループさせることができます。

---

### 🎯 本日の目標

1.  **`@keyframes`** を定義して、動きの「開始」と「終了」を作る。
2.  **無限ループ（infinite）**: ずっと動き続けるローディングスピナーを作る。
3.  **往復運動（alternate）**: 滑らかに行って戻ってくる、浮遊アニメーションを作る。

---

### 📝 ミッション内容

以下の 2 つの動く要素を作ってください。

- **Mission 1: 「Loading Spinner」**
  - 円形の一部が欠けた線が、その場でぐるぐると無限に回転し続ける。
  - よく見る「読み込み中」のマークです。
- **Mission 2: 「Floating Ghost」**
  - 要素がその場でふわふわと「上下」に動き続ける。
  - 「上に上がって、パッと下に戻る」のではなく、「上がって、ゆっくり下りてくる（往復）」動きにする。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="zxBrEzJ" data-pen-title="CSSマスターへの道「Animation」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/zxBrEzJ">
  CSSマスターへの道「Animation」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. `@keyframes` の書き方

```css
@keyframes 名前 {
  0% {
    スタイル...;
  }
  50% {
    スタイル...;
  }
  100% {
    スタイル...;
  }
}
```

`0%` の代わりに `from`、`100%` の代わりに `to` を使うこともできますが、細かい調整ができる `%` 表記がおすすめです。

#### 2. `animation` プロパティの解剖

ショートハンド（省略形）で書くのが一般的です。
`animation: spin 1s linear infinite;`

- **name**: 実行する `@keyframes` の名前。
- **duration**: 1 回の再生にかかる時間（例: `1s`）。
- **timing-function**: 動きの加速・減速（例: `linear` は一定、`ease` は滑らか）。**回転系は `linear` にしないと、一周ごとにガクッと止まって見えます。**
- **iteration-count**: 繰り返す回数。数字か、`infinite`（無限）。
- **direction**: 再生方向。
  - `normal`: 0% → 100% → (パッと戻る) → 0% ...
  - `alternate`: 0% → 100% → (折り返す) → 0% ... **ふわふわさせるなら必須。**

---

### 💡 応用：カチカチ動くタイプライター風

`timing-function` に `steps()` という値を使うと、滑らかではなく「コマ送り」のアニメーションが作れます。これを利用して、文字が 1 文字ずつ打たれるような演出ができます。

```css
.typing {
  width: 14ch; /* 14 文字分の幅 */
  overflow: hidden; /* はみ出た文字を隠す */
  white-space: nowrap; /* 改行させない */
  border-right: 3px solid white; /* カーソル */
  font-family: monospace; /* 等幅フォント（必須） */
  color: white;

  animation: typing 3s steps(14), /* 14 ステップで幅を広げる */ blink 0.5s
      step-end infinite alternate; /* カーソルの点滅 */
}

@keyframes typing {
  from {
    width: 0;
  }
}

@keyframes blink {
  50% {
    border-color: transparent;
  }
}
```

---

### おわりに

`transition` と `animation` の違いを整理しておきましょう。

- **Transition:** ユーザーのアクション（ホバーなど）が必要。A 地点 ⇔ B 地点。
- **Animation:** 勝手に動く。A → B → C → ... と複雑な動きが可能。ループできる。

この 2 つを使い分ければ、Web サイトの表現力は大きく広がります。

次回は、2D の世界から飛び出します。
**「Transform (2D/3D)」** を使って、カードをくるっと裏返したり、奥行きのある空間を作ったりしてみましょう。

https://qiita.com/saka2jp/items/7d19c9c352987218d21e
