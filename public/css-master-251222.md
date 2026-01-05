---
title: CSSマスターへの道「CSSアート」
tags:
  - CSS
private: false
updated_at: '2026-01-05T01:36:00+09:00'
id: ddf4cfeda2f537a5668e
organization_url_name: null
slide: false
ignorePublish: false
---

Day 22 です。

https://qiita.com/saka2jp/items/0112e66fe7443c118229

Phase 4「モダン CSS と総合演習」の 2 日目です。
今日は少し趣向を変えて、クリエイティブな息抜き回です。

テーマは **「CSS アート」**。
画像ファイルを一切使わず、コードだけで絵を描きます。
「実務で使わないでしょ？」と思うかもしれませんが、実は CSS アート は **「Position（配置）」と「疑似要素」の特訓に最適** なのです。

たった 1 つの `<div>` タグから、無限の世界を作り出しましょう。

---

### はじめに：HTML タグは「画用紙」

CSS アートの基本ルールは、**「HTML は最小限にする」** ことです。
通常、1 つの `div` タグがあれば、CSS の疑似要素（`::before`, `::after`）を使って、合計 **3 つのパーツ**（本体、before、after）を扱うことができます。

- 本体：顔の輪郭
- before：左目
- after：右目

このようにパーツを割り当てて、積み木のように重ねていくのが CSS アートの醍醐味です。

---

### 🎯 本日の目標

1.  **シングル Div**: HTML タグを 1 つだけ使い、それ以外は CSS だけで表現する。
2.  **疑似要素の配置**: 親要素（本体）を基準に、`absolute` でパーツを自由な位置に置く。
3.  **ボーダーと円**: `border` や `box-shadow` を工夫して、図形を描く。

---

### 📝 ミッション内容

たった 1 行の HTML `<div class="camera"></div>` を、CSS の力で「カメラのアイコン」に変身させてください。

- **本体 (.camera)**: カメラのボディ（四角形）。
- **疑似要素 1 (::before)**: カメラのレンズ（大きな円）。
- **疑似要素 2 (::after)**: フラッシュやファインダー（小さな円）。

---

### 💻 実装サンプル

インスタグラムのロゴのような、シンプルでモダンなカメラを作ってみましょう。

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="ByzjwXd" data-pen-title="CSSマスターへの道「CSSアート」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/ByzjwXd">
  CSSマスターへの道「CSSアート」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. パーツの役割分担

- **`.camera`**: 土台となる画用紙です。ここに `position: relative` を指定するのが絶対条件です。
- **`::before` / `::after`**: 装飾用のパーツです。必ず `content: '';` と `position: absolute` を指定して、土台の上に配置します。

#### 2. 図形描画のテクニック

- **円を作る**: `width` と `height` を同じにして、`border-radius: 50%`。
- **ドーナツ型を作る**: 背景色（`background`）を透明にして、`border` だけに色をつける（今回のレンズ部分で使用）。
- **三角形を作る**: `width: 0; height: 0; border: ...` を使う（Day 24 のアコーディオンなどで使います）。

#### 3. 中央寄せの定番コード

CSS アートでは、パーツを親の中心に置くことが非常に多いです。

```css
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
```

この 3 行は、息をするように書けるようになりましょう。

---

### 💡 応用：`box-shadow` で分身の術

「パーツが 3 つじゃ足りない。もっと描きたい」
そんな時は、`box-shadow` を使います。実は `box-shadow` は、影だけでなく **「要素のコピー」** を好きな場所に量産できるのです。

```css
/* 例：1 つの丸い div から、3 つの団子を作る */
.dango {
  width: 20px;
  height: 20px;
  background: green;
  border-radius: 50%;

  /* 
    影を使って、本体の上に 2 つコピーを作る 
    x 方向, y 方向, ぼかし(0 にする), 広がり, 色
  */
  box-shadow: 0 -25px 0 0 white, /* 上の団子（白） */ 0 -50px 0 0 pink; /* さらに上の団子（ピンク） */
}
```

これを使えば、ドット絵のように複雑なイラストも 1 つのタグで描けてしまいます。

---

### おわりに

CSS アートを描いていると、
「あ、`absolute` の基準点はここか」「`z-index` で重ね順を変えなきゃ」
といった、**レイアウトの感覚が直感的に身につきます**。

楽しみながら、Position プロパティの完全マスターを目指しましょう。

次回は **「実践 UI トレース」** です。
お絵描きの次は模写です。有名な Web サイトのパーツを、実際にコードに落とし込む「エンジニアの写経」に挑戦しましょう。

https://qiita.com/saka2jp/items/e04509615fe3f76e7050
