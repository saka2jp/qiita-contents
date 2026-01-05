---
title: CSSマスターへの道「Transform (2D/3D)」
tags:
  - CSS
private: false
updated_at: '2026-01-05T21:28:51+09:00'
id: 7d19c9c352987218d21e
organization_url_name: null
slide: false
ignorePublish: false
---

Day 17 です。

https://qiita.com/saka2jp/items/cf1e9a6b6b45a9ae6993

Phase 3 も中盤です。ここまでのアニメーション（`transition`, `animation`）は、主に「色」や「位置」の変化でした。

今日は、要素そのものを「**変形**」させます。
CSS の `transform` プロパティを使えば、要素を回転させたり、拡大縮小したり、斜めに歪ませたりできます。

さらに、実は Web ブラウザの中には「**3D 空間**」が存在します。
今日はその扉を開けて、カードをくるっと裏返す立体的な表現に挑戦しましょう。

---

### はじめに：ブラウザは 2 次元だけじゃない

通常、Web ページは平面（2 次元）ですが、CSS には Z 軸（奥行き）の概念があります。
`transform` を使うと、まるで手に持った紙を操るように、要素を自由な角度に配置したり、手前に引き寄せたりすることができます。

特に「フリップカード（裏返るカード）」は、限られたスペースで 2 倍の情報を伝えられるため、実務でも非常によく使われるテクニックです。

---

### 🎯 本日の目標

1.  **基本の 3 変形**: `translate`（移動）、`scale`（拡大）、`rotate`（回転）をマスターする。
2.  **3D の呪文**: 3 次元表現に必須の `perspective`（遠近感）と `preserve-3d` の意味を理解する。
3.  **フリップアニメーション**: ホバーするとパタンと裏返るカードを作る。

---

### 📝 ミッション内容

以下の 2 つの要素を作ってください。

- **Mission 1: 「2D Transform」**
  - ホバーすると、「少し拡大」しながら「少し傾く」画像を作る。
- **Mission 2: 「3D Flip Card」**
  - 表面には「Question?」、裏面には「Answer!」と書かれたカードを作る。
  - マウスを乗せると、Y 軸（縦軸）を中心にくるっと回転して裏面が現れる。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="XJKXezP" data-pen-title="CSSマスターへの道「Transform (2D/3D)」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/XJKXezP">
  CSSマスターへの道「Transform (2D/3D)」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. `transform` プロパティ

位置や形を変えるプロパティです。レイアウト（`top` や `left`）を変えるよりも描画負荷が軽く、アニメーション向きです。

- `translate(x, y)`: 移動。`translateY(-10px)` で浮く表現によく使います。
- `scale(倍率)`: 拡大縮小。`1` が基準。
- `rotate(角度)`: 回転。`deg`（度）を使います。
- `skew(角度)`: 斜めに歪ませる。

#### 2. 3D 表現の「三種の神器」

3D 回転を成功させるには、以下の 3 つがセットで必要です。

1.  **`perspective: 1000px;`** (大枠の親要素)
    - 視点の距離。これがないと回転しても「幅が縮むだけ」に見えます。
2.  **`transform-style: preserve-3d;`** (回転する要素)
    - これを指定しないと、子要素（表・裏）が平面に押しつぶされてしまいます。
3.  **`backface-visibility: hidden;`** (表・裏の要素)
    - 「裏側になった時に非表示にする」設定。これと「裏面をあらかじめ 180 度回しておく」ことで、リバーシブルなカードが成立します。

---

### 💡 応用：マウスの方向に傾くカード

JavaScript を少し組み合わせる必要がありますが、3D Transform を使うと、マウスの位置に合わせてカードをぐりぐり傾ける「3D Tilt エフェクト」も作れます（Apple TV のアイコンのような動き）。
CSS だけでも、`:active`（クリック時）に `scale(0.95)` を入れるだけで、「押し込んだ感」のある気持ちいいボタンが作れます。

---

### おわりに

3D Transform を使えば、画面の中に奥行きが生まれ、表現の幅が広がります。
最初は「どの要素に `perspective` だっけ？」と混乱するかもしれませんが、「カメラ(親) → 回転体(子) → 面(孫)」という構造を覚えておけば大丈夫です。

ここまでは「見た目」と「動き」を作ってきました。
次回は、少しプログラミング寄りな話です。
CSS を効率よく管理し、一瞬でダークモードに変えたりできる **「変数 (Custom Properties)」** について学びます。

https://qiita.com/saka2jp/items/b644159ad0530fd9374a
