---
title: CSSマスターへの道「ボーダーと角丸」
tags:
  - CSS
private: false
updated_at: '2026-01-05T21:28:51+09:00'
id: 5549622b1d7e38e49f46
organization_url_name: null
slide: false
ignorePublish: false
---

Day 10 です。

https://qiita.com/saka2jp/items/fd974fe751298c8d77ca

これまでの 9 日間で、四角いボックスに色を塗り、影を落として立体的にしました。
しかし、まだ「形」は四角いままです。

今日は、CSS の「角丸」を学びます。真円はもちろん、カプセル型、さらにはアメーバのような **有機的でぐにゃぐにゃした形（Blob）** まで作れるようになります。

---

### はじめに：角丸の可能性

`border-radius` は、単にボタンの角を少し丸くするためだけのプロパティではありません。
4 つの角の値をバラバラに設定したり、縦と横の比率を変えたりすることで、**CSS だけで複雑な図形を描画する** ことができます。

画像を使わずに形を作れれば、色やサイズの変更も CSS だけで完了します。

---

### 🎯 本日の目標

1.  **カプセル型（Pill Shape）**：どんな横幅になっても両端が半円になるボタンを作る。
2.  **真円（Circle）**：プロフィール画像などで使われる完璧な円を作る。
3.  **有機的な形（Blob）**：`border-radius` の「スラッシュ記法」を使い、歪んだ形を作る。

---

### 📝 ミッション内容

以下の 3 つの形状を作ってください。

- **Mission 1: 「Pill Button」**
  - 横長でも短くても、常に両端が完全に丸いボタン（角丸の値を極端に大きくするテクニック）。
- **Mission 2: 「Avatar Icon」**
  - 画像を正円（丸）で切り抜く。
- **Mission 3: 「Morphing Blob」**
  - 不規則な形のオブジェクトを作り、ホバーするとさらに形がぐにゃりと変わるアニメーションをつける。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="QwEyMrj" data-pen-title="CSSマスターへの道「ボーダーと角丸」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/QwEyMrj">
  CSSマスターへの道「ボーダーと角丸」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. 値の指定ルール（時計回り）

`border-radius` は 4 つの角を個別に指定できます。

```css
/* 左上、右上、右下、左下（時計回り） */
border-radius: 10px 20px 30px 40px;
```

#### 2. カプセル型の裏技 (`9999px`)

ボタンの高さをいちいち測って `height: 50px; border-radius: 25px;` と書くのは面倒です。
`border-radius: 9999px`（または十分大きな値）を指定すると、ブラウザが **「短い方の辺の半分」** を計算して、綺麗な半円を作ってくれます。

#### 3. Blob（歪んだ形）の正体

サンプルコードの Mission 3 にある `60% 40% ... / ...` という書き方。
これは「**水平方向の半径 / 垂直方向の半径**」を別々に指定しています。これにより、真円ではない、歪んだ曲線を作ることができます。
これと CSS アニメーションを組み合わせると、生き物のように動く背景が作れます。

**💡 ヒント:** 「[Fancy Border Radius Generator](https://9elements.github.io/fancy-border-radius/)」という Web ツールを使うと、この複雑な値を直感的に生成できます。

---

### 💡 応用：吹き出しを作る

角の 1 つだけをあえて丸くしない（`0` にする）ことで、漫画の吹き出しのような形が作れます。

```css
.speech-bubble {
  background: #eee;
  padding: 20px;
  /* 左下だけ 0 にして「しっぽ」っぽく見せる */
  border-radius: 20px 20px 20px 0;
}
```

---

### おわりに

四角形、円、そして有機的な形。これで Web 上のあらゆる「形」を操れるようになりました。
特に「Blob」は、写真の背景に薄く敷いたり、ボタンの背景に使ったりすると、今風のデザインになります。

次回は、Web デザインの要である **「テキスト装飾と Web フォント」** です。
文字をただ並べるだけでなく、美しく見せる技術を学びましょう。

https://qiita.com/saka2jp/items/96a16834fb4614c3d351
