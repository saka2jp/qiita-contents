---
title: CSSマスターへの道「レスポンシブデザイン」
tags:
  - CSS
private: false
updated_at: '2025-12-28T15:59:03+09:00'
id: fb5412cd4c1a8f69ee57
organization_url_name: null
slide: false
ignorePublish: false
---

6日目、お疲れ様です！もうすぐ1週間達成ですね。
今日は現代のWeb制作において**避けては通れない最重要項目**、「レスポンシブデザイン」です。

スマホ、タブレット、PC、どのデバイスで見ても崩れないレイアウトを作る力を手に入れましょう。

---

# Day 6: レスポンシブデザインとMedia Queries

今日のゴール：**「画面幅に応じて、レイアウト（列数）が切り替わるカードリストを作る」**

## 📚 今日のインプット：仕組みを理解する

レスポンシブデザインの主役は **Media Queries（メディアクエリ）** です。
CSSの中で「条件分岐（もし画面幅が〇〇px以上なら…）」を書くことができます。

### 1. おまじない（Viewport）
HTMLの`<head>`にこれがないと、スマホで見た時にサイトが勝手に縮小されてしまいます。必ず入れましょう。
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### 2. モバイルファーストという考え方
「PC用のCSSを書いてから、スマホ用に上書きする」のではなく、「**スマホ用のCSS（ベース）を書いて、画面が広がったらPC用のレイアウトを追加する**」という書き方（モバイルファースト）が現在の主流です。

コードは以下のように書きます。

```css
/* ① 基本のスタイル（スマホ用・全デバイス共通） */
.container {
  display: grid;
  grid-template-columns: 1fr; /* 1列 */
  gap: 16px;
}

/* ② タブレット以上の時（画面幅 600px以上）に追加・上書きするスタイル */
@media (min-width: 600px) {
  .container {
    grid-template-columns: 1fr 1fr; /* 2列になる */
  }
}

/* ③ PC以上の時（画面幅 1024px以上）に追加・上書きするスタイル */
@media (min-width: 1024px) {
  .container {
    grid-template-columns: 1fr 1fr 1fr; /* 3列になる */
    gap: 32px; /* 余白も広げてみる */
  }
}
```

*   `min-width: 〇〇px` は「**最低でも**幅が〇〇pxあれば」＝「〇〇px**以上**なら」という意味です。
*   小さい順に書いていくのがコツです。

---

## 🛠️ 今日のアウトプット（お題）

**「ニュース記事一覧」のようなカードレイアウトを作ってください。**

### 仕様
1.  **HTML:** 親要素の中に、記事カード（画像＋タイトル＋少しの文章）を6個ほど配置する。
2.  **CSS:**
    *   **スマホ（初期状態）:** カードは縦に1列に並ぶ。
    *   **タブレット（600px以上）:** カードは2列になる。
    *   **PC（960px以上）:** カードは3列になる。
3.  **Day 4の復習:** レイアウトには `display: grid` を使うのが一番簡単です。

### 雛形コード（ヒント）

HTML構造の例です。CSSを記述して完成させてください！

```html
<div class="card-list">
  <!-- これを6個くらいコピペしてください -->
  <div class="card">
    <div class="card-image"></div>
    <div class="card-content">
      <h3>タイトル</h3>
      <p>ここに記事の抜粋テキストが入ります。</p>
    </div>
  </div>
</div>
```

```css
/* ベースの装飾（ここは自由にいじってください） */
body {
  margin: 0;
  padding: 20px;
  background-color: #f0f2f5;
  font-family: sans-serif;
}

.card {
  background: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.card-image {
  height: 150px;
  background-color: #ddd; /* 画像の代わりにグレーの背景 */
  /* 余裕があれば Day 13 の予習で background-image を使ってもOK */
}

.card-content {
  padding: 16px;
}

/* ▼ ここから下にレイアウトとメディアクエリを書いてください ▼ */

.card-list {
  display: grid;
  gap: 20px;
  /* スマホ用（デフォルト）の列指定 */
  
}

/* タブレット用ブレイクポイント */
@media (min-width: 600px) {
  .card-list {
    /* ここで2列にする */
    
  }
}

/* PC用ブレイクポイント */
@media (min-width: 960px) {
  .card-list {
    /* ここで3列にする */
    
  }
}
```

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="azZzMBJ" data-pen-title="CSSマスターへの道「レスポンシブデザイン」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/azZzMBJ">
  CSSマスターへの道「レスポンシブデザイン」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

### ✅ チャレンジのポイント
*   ブラウザの幅をマウスでグイーッと縮めたり広げたりして、**パッ、パッ**とレイアウトが切り替わる瞬間を確認してください。これがレスポンシブの醍醐味です！
*   Gridを使えば `grid-template-columns` を書き換えるだけで列数が変えられるので、Flexboxよりも簡単に実装できます（Flexboxの場合は `width` を `50%` や `33.33%` に変える必要があります）。

### 余裕がある人向け（プラスα）
*   PCの時だけ、カードの画像の高さを高くしてみる。
*   PCの時だけ、タイトル文字のサイズ（`font-size`）を少し大きくしてみる。
*   CSS変数（Day 18の予習）を使ってみる。

明日はPhase 1の最終日、「**Position（絶対配置・固定配置）**」です。お楽しみに！
