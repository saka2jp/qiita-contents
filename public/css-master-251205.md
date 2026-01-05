---
title: CSSマスターへの道「CSS Grid (応用編)」
tags:
  - CSS
private: false
updated_at: '2026-01-05T21:28:51+09:00'
id: 3614aa0732dcaa5a7807
organization_url_name: null
slide: false
ignorePublish: false
---

Day 5 です。

https://qiita.com/saka2jp/items/8036b99b5b8c52bde058

昨日の「マス目を作る（行と列の定義）」に続き、今日は CSS Grid の強力な機能 **「エリア（Areas）」** を学びます。
座標（何行目の何列目）を数字で指定するのではなく、「ここにヘッダー」「ここにサイドバー」と名前で場所を指定する、直感的な書き方をマスターしましょう。

---

### 🎯 本日の目標

1.  **`grid-area`** で要素に「名前」をつける。
2.  **`grid-template-areas`** で、コード上に「レイアウトの地図」を描く。
3.  典型的な「ヘッダー・2 カラム・フッター」のレイアウトを作る。

---

### 📝 ミッション内容

今日は、ブログや Web サイトで最もよく使われる **「聖杯レイアウト（ヘッダー、メイン記事、サイドバー、フッター）」** を作ります。

#### 準備: HTML 構造

親要素の中に、役割の違う 4 つのブロックを用意します。

```html
<div class="layout-container">
  <header class="box-header">Header</header>
  <main class="box-main">Main Content</main>
  <aside class="box-sidebar">Sidebar</aside>
  <footer class="box-footer">Footer</footer>
</div>
```

#### Step 1: 子要素に「名前」をつける

- 配置したいアイテム（子要素）に、ニックネームを付けます。
- CSS で各クラスに **`grid-area: 名前;`** を指定してください。
  - 例: `.box-header { grid-area: hd; }`
  - 名前は `h` や `head` など、自分で決めて OK です（クォーテーション `""` は不要）。

#### Step 2: グリッドの分割（列と行）

- 親要素 `.layout-container` に `display: grid;` を指定します。
- レイアウトの土台を作ります。
  - **横（列）:** メインとサイドバーの比率を決めます。 `grid-template-columns: 2fr 1fr;`（左を広く、右を狭く）。
  - **縦（行）:** ヘッダー、中身、フッターの 3 行です。 `grid-template-rows: auto 1fr auto;`（中身だけ伸びるように）。

#### Step 3: 地図を描く

ここが今日のポイントです。親要素に **`grid-template-areas`** を記述します。
定義した「2 列」に合わせて、以下のように書きます。

```css
grid-template-areas:
  "hd   hd"
  "main side"
  "ft   ft";
```

- 1 行目は両方 `hd` → ヘッダーが横いっぱいに広がる。
- 2 行目は `main` と `side` → 左右に分かれる。
- 3 行目は両方 `ft` → フッターが横いっぱいに広がる。

コードの見た目が、そのまま画面のレイアウトに対応しています。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="vEGQbEg" data-pen-title="Untitled" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/vEGQbEg">
  Untitled</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. 「結合」の概念が不要になる

HTML の `<table>` タグや Excel で「セル結合」をした経験はありますか？
Grid Areas なら、「同じ名前を並べて書く」だけで結合になります。

- `"hd hd"` と書けば、その 2 マスは繋がって 1 つのヘッダーエリアになります。
- `colspan` のような数値計算をしなくて良いので、ミスが減ります。

#### 2. HTML の順番を気にしなくていい

これが大きなメリットです。
HTML 上では `<main>` の下に `<aside>`（サイドバー）があっても、CSS の地図（areas）で `"side main"` と書き換えれば、 **画面上ではサイドバーを左、メインを右に入れ替えることができます。**
HTML 構造（文書の正しさ）を保ったまま、見た目だけを自由に変えられます。

#### 3. 空白を作りたい時

何も置かないマスを作りたい時は、名前の代わりにドット **`.`** を書きます。
例：フッターの右側を空けたい場合

```css
grid-template-areas:
  "hd   hd"
  "main side"
  "ft   ."; /* 右下は空白になる */
```

---

### 💡 応用：スマホ対応（レスポンシブ）

スマホ（画面幅が狭い時）は、サイドバーをメインの下に落として「縦積み」にしたい場合があります。
Grid Areas なら、 **「地図」を書き換えるだけ** で対応できます。

```css
@media (max-width: 600px) {
  .layout-container {
    grid-template-columns: 1fr; /* 1 列にする */
    /* 地図を縦並びに書き換え */
    grid-template-areas:
      "hd"
      "main"
      "side"
      "ft";
  }
}
```

---

### おわりに

CSS の中に「アスキーアートのような地図」を書くこの手法は、コードを見ただけでレイアウト構造がわかるため、チーム開発でも理解しやすくなります。

次回は、ここまでの知識を使って **「レスポンシブデザイン（Media Queries）」** を深掘りし、どんなデバイスでも適切に見えるレイアウトを完成させましょう。

https://qiita.com/saka2jp/items/fb5412cd4c1a8f69ee57
