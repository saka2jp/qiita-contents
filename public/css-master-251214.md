---
title: CSSマスターへの道「クリップパス」
tags:
  - CSS
private: false
updated_at: '2026-01-04T23:44:10+09:00'
id: 652f533e4cd226fc1cb2
organization_url_name: null
slide: false
ignorePublish: false
---

14 日目、Phase 2 の最終日です！おめでとうございます！🎉
これまで、色、影、角丸、疑似要素、画像加工と、デザインの引き出しを増やしてきました。

しかし、Web サイトは依然として「四角い箱」の積み重ねに見えてしまいがちです。
最終日の今日は、その四角い箱をハサミで切り抜く「**Clip-path（クリップパス）**」です。

これで **「斜めの背景」「星型の写真」「ギザギザの境界線」** など、自由自在なレイアウトが可能になります。

---

### はじめに：Web ページを「切り絵」にする

`clip-path` は、要素の表示領域を座標で指定して「切り抜く」プロパティです。
`border-radius` では円と楕円しか作れませんでしたが、`clip-path` なら三角形、五角形、星型、複雑な多角形など、**どんな形でも作れます**。

切り抜かれた「外側」は透明になり、クリック判定も消えます。まさにデジタルな「切り絵」です。

---

### 🎯 本日の目標

1.  **`polygon()` 関数**：座標を指定して、多角形を作る仕組みを理解する。
2.  **斜めレイアウト**：最近の Web サイトでよく見る、セクションの境界線が斜めになっているデザインを作る。
3.  **複雑なシェイプ**：画像を星型などのアイコンに切り抜く。

---

### 📝 ミッション内容

以下の 2 つのデザインを作ってください。

- **Mission 1: 「Diagonal Hero」**
  - 画面上部の大きな背景エリア（ヒーローセクション）の「下辺」を斜めに切り落とす。
- **Mission 2: 「Shape Icon」**
  - 普通の四角い画像を、CSS だけで「星型（または六角形）」に切り抜く。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="gbMPxEV" data-pen-title="CSSマスターへの道「画像加工 (object-fit / filter)」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/gbMPxEV">
  CSSマスターへの道「画像加工 (object-fit / filter)」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. 座標の考え方

`clip-path: polygon(X Y, X Y, ...)` で頂点を結んでいきます。

- **X (横):** 0%が左端、100%が右端。
- **Y (縦):** 0%が上端、100%が下端。

例えば `polygon(0 0, 100% 0, 0 100%)` と書くと、左上・右上・左下を結んだ「直角三角形」になります。

#### 2. ツールを使おう！

「星型の座標なんて覚えられないよ！」と思ったあなた、正解です。プロも暗記していません。
「[Clippy](https://bennettfeely.com/clippy/)」 という有名な Web ジェネレーターを使います。
画面上で点をドラッグして好きな形を作り、CSS コードをコピペするのが基本スタイルです。

#### 3. レイアウトへの活用

サンプルコードの `.hero` のように、`100% 100%`（右下）ではなく `100% 85%` のように少し数値をずらすだけで、スタイリッシュな斜めのデザインが作れます。これは画像だけでなく、背景色を敷いた `div` にも使えます。

---

### 💡 応用：形が変わるアニメーション

`clip-path` は `transition`（アニメーション）に対応しています。
ただし条件があり、**「頂点の数が同じ」**である必要があります（例：三角形から三角形への変形）。

しかし、`circle()`（円）や `inset()`（四角）などの基本シェイプ同士、または `polygon` 同士であれば、Mission 2 のように「星型から円へ」のようなモーフィングアニメーションが可能です。
※ブラウザによって挙動が少し異なる場合があるので、複雑な変形は注意が必要です。

---

### おわりに

これで **Phase 2: デザインの表現力を高める週** はコンプリートです！お疲れ様でした！👏

- グラデーション
- 影（Box-shadow）
- 角丸とボーダー
- Web フォント
- 疑似要素
- 画像加工
- クリップパス

これらの武器があれば、もう「CSS で表現できないデザイン」はほとんどありません。

さて、明日からは **Phase 3: 動きとインタラクションの週** に突入します。
静止画だった Web サイトに「命」を吹き込みます。ボタンが心地よく動いたり、要素がふわっと現れたり。
JavaScript を使わずにどこまで動かせるか、CSS アニメーションの限界に挑戦しましょう！

明日の Day 15 は 「Transition」。心地よい動き（マイクロインタラクション）の基礎を学びます！
