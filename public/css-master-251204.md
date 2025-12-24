---
title: CSSマスターへの道「CSS Grid (基礎編)」
tags:
  - CSS
private: false
updated_at: '2025-12-25T03:10:30+09:00'
id: 8036b99b5b8c52bde058
organization_url_name: null
slide: false
ignorePublish: false
---

4日目、お疲れ様です！
Flexbox（1次元）をマスターしたあなたなら、今日の「**CSS Grid（2次元）**」は、魔法のように感じるはずです。

Flexboxは「横一列」を制御するのに長けていましたが、Gridは「**縦と横のマス目（碁盤の目）**」を同時に支配します。今日はその第一歩、基本の「キ」です。

---

## Day 4: 2次元の支配者「CSS Grid」入門

### 🎯 本日の目標
1.  **`display: grid`** でグリッドレイアウトを開始する。
2.  新単位 **`fr` (fraction)** を理解する（これを知ると%計算がいらなくなります）。
3.  **`repeat()`** 関数を使って、効率的にマス目を作る。

---

### 📝 ミッション内容

今日は、Webサイトでよく見る「**カード型のギャラリー（3列レイアウト）**」を作ります。

#### 準備: HTML構造
親箱の中に、アイテムを6つ用意します。

```html
<div class="grid-container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <div class="item">4</div>
  <div class="item">5</div>
  <div class="item">6</div>
</div>
```

#### Step 1: グリッドの定義と「固定幅」
*   `.grid-container` に `display: grid;` を指定します。
*   続けて、**`grid-template-columns: 100px 100px 100px;`** と書いてみてください。
*   **観察:** 幅100pxの柱（カラム）が3本できましたか？アイテム4以降は自動的に次の行（2行目）に折り返されましたか？

#### Step 2: 魔法の単位「fr」を使う
*   100pxだと画面の右側が余ってしまいます。かといって `%` で `33.33%` と書くのは計算が面倒です。
*   `grid-template-columns: 1fr 1fr 1fr;` に書き換えてください。
*   **観察:** 画面幅いっぱいに、均等に3分割されましたか？
    *   `fr` は "fraction"（比率/破片）の略です。「1 : 1 : 1」の割合で分ける、という意味になります。

#### Step 3: リピート記法で楽をする
*   もし「10列」作りたい時、`1fr` を10回書くのは大変です。
*   `grid-template-columns: repeat(3, 1fr);` に書き換えてください。
*   **観察:** Step 2と同じ見た目になりますが、コードがスッキリしました。

#### Step 4: 溝（Gap）を作る
*   アイテム同士がくっついているので離したいですね。Flexboxと同じく `gap` が使えます。
*   `.grid-container` に `gap: 20px;` を追加してください。
*   **観察:** 縦横の隙間が一発で空きましたか？（昔は `margin` で苦労していた部分です！）

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="vEGVqOV" data-pen-title="CSSマスターへの道「CSS Grid (基礎)」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/vEGVqOV">
  CSSマスターへの道「CSS Grid (基礎)」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. Flexboxとの最大の違い
*   **Flexbox:** 「中身」ありき。
    *   「アイテムA、B、Cがあるから、これを横に並べよう」というアプローチ。
*   **Grid:** 「枠（グリッド）」ありき。
    *   **「ここに3列の枠を作るぞ！中身は勝手にそこに流し込まれろ！」** というアプローチ。
    *   今回の例でも、HTML側のアイテム（`.item`）には一切CSSを書いていません（幅指定などしていません）。親要素（Container）だけでレイアウトを完全に支配できるのがGridの強みです。

#### 2. `fr` (フラクション) とは？
Grid専用の単位で、「残りの空間の配分比率」です。
*   `1fr 1fr` → 1:1 で2等分。
*   `2fr 1fr` → 2:1 で分割（左側が2倍の広さになる）。
*   `200px 1fr` → 左は200px固定、 **残りのスペース全部** を右側にする。

#### 3. `grid-template-columns`
文字通り「グリッドのテンプレート（ひな形）の柱（カラム）」を定義します。
ここに書いた値の数だけ、横に列ができます。

---

### 💡 応用：田の字レイアウト（2x2）にするには？

3列ではなく2列（2x2）にしたい場合は、CSSをどう書き換えれば良いでしょうか？

答え：
```css
grid-template-columns: repeat(2, 1fr); /* 2回繰り返す */
```
これだけで、アイテムは自動的に2列ごとに改行され、田の字（アイテムが4つの場合）や2列のリストになります。

---

**Day 4 クリアです！**
「親要素に設定を書くだけで、子要素が勝手に整列する」というGridの支配力を体感できましたか？
明日は、このGridを使って、雑誌のような「**複雑なエリア分けレイアウト**」に挑戦します。ここからがGridの真骨頂です！
