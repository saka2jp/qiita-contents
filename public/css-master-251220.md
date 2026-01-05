---
title: 'CSSマスターへの道「モダンCSS (:has / :is / :where)」'
tags:
  - CSS
private: false
updated_at: '2026-01-05T00:34:30+09:00'
id: a3ae2ce83b06f672e817
organization_url_name: null
slide: false
ignorePublish: false
---

Day 20 です。

https://qiita.com/saka2jp/items/716351d0234f44094a50

Phase 3 の最終日です。
これまでの CSS は「見た目」を作るためのものでした。
しかし、今日学ぶ **モダン CSS** は「ロジック（論理）」に近い領域です。

「親要素を選択したい」「セレクタが長すぎて読めない」
そんな長年の悩みを解決する、**CSS の歴史を変えた革命的な機能** を学びます。

---

### はじめに：CSS がついに「親」を見つけられるようになった

長年、CSS には「親要素セレクタ」が存在しませんでした。
「子供がアクティブになったら、親の色を変えたい」という単純なことさえ、JavaScript を使わないと不可能だったのです。

しかし、**`:has()`** の登場でそれが可能になりました。
さらに、**`:is()`** と **`:where()`** を使えば、重複した長いセレクタを劇的に短く書くことができます。

今日は「CSS を賢く書く」ための、現代の必須スキルです。

---

### 🎯 本日の目標

1.  **`:has()` (親セレクタ)**：子要素の状態に応じて、親要素や前の要素のスタイルを変える。
2.  **`:is()` (グループ化)**：`h1, h2, h3...` のような長い記述をまとめる。
3.  **`:where()` (詳細度ゼロ)**：ライブラリやリセット CSS で便利な「上書きしやすい」記述を知る。

---

### 📝 ミッション内容

以下の 2 つの機能を、JavaScript を一切使わずに CSS だけで実装してください。

- **Mission 1: スマートな見出し (:is)**
  - 記事（`article`）とセクション（`section`）の中にある `h1` 〜 `h3` の色とフォントを一括で指定する。
- **Mission 2: 選択されたカード (:has)**
  - カードの中にチェックボックスがある。
  - **「チェックボックスにチェックが入ったら、カード全体（親）の背景色と枠線の色が変わる」** 機能を実装する。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="PwzZJxb" data-pen-title="CSSマスターへの道「モダンCSS (:has / :is / :where)」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/PwzZJxb">
  CSSマスターへの道「モダンCSS (:has / :is / :where)」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. `:has()` は「後ろを見る」セレクタ

CSS は通常、左から右（親から子）へ読み込まれますが、`:has()` は逆です。
`Parent:has(Child)` は、**「Child を内包している Parent」** を探します。

- **`div:has(img)`**: 画像を含んでいる div だけスタイルを変える。
- **`form:has(input:invalid)`**: エラー入力があるフォーム全体の枠を赤くする。

#### 2. `:is()` と `:where()` の違い

どちらも複数のセレクタをまとめる機能ですが、「**詳細度（強さ）**」が違います。

- **`:is(.a, #b)`**: カッコ内で **一番強いセレクタの点数** が適用されます（この場合 ID の強さになる）。
- **`:where(.a, #b)`**: 何を書いても **詳細度は「0 点」** になります。
  - **使い所:** リセット CSS など、「後から簡単に上書きさせたい」スタイルには `:where()` を使います。

#### 3. ブラウザ対応

`:has()` は 2024 年現在、主要な全ブラウザ（Chrome, Edge, Safari, Firefox）でサポートされています。安心して使って大丈夫です。

---

### 💡 応用：前の要素を操作する

CSS には「次の要素（`+`）」を選ぶセレクタはありましたが、「前の要素」を選ぶことはできませんでした。
しかし、`:has()` を応用すれば擬似的に可能です。

```css
/* 「画像のすぐ後ろに figcaption がある場合の、その画像」を選択 */
img:has(+ figcaption) {
  border-bottom: 5px solid gold;
}
```

「キャプション付きの画像だけ特別なデザインにする」といった条件分岐が CSS だけで書けるようになります。

---

### おわりに

`:has()` の登場によって、「JS でクラスをつけ外しする」という作業の多くは不要になりました。
これは CSS コーディングにおけるパラダイムシフトです。

これにて **Phase 3: 動きとインタラクションの週** は終了です。
アニメーションからロジックまで、動的な Web サイトを作る力が身につきました。

次回からはラストスパート、**Phase 4: モダン CSS と総合演習** です。
初日の Day 21 は、レスポンシブデザインの最終形態 **「コンテナクエリ」** です。画面幅ではなく「自分の居場所の幅」に応じて変形する、未来のレイアウト技術を学びましょう。

https://qiita.com/saka2jp/items/0112e66fe7443c118229
