---
title: CSSマスターへの道「Flexbox(基礎編)」
tags:
  - CSS
private: false
updated_at: '2025-12-25T03:10:27+09:00'
id: 3383006a106417c709f0
organization_url_name: null
slide: false
ignorePublish: false
---

Day 2 です。

https://qiita.com/saka2jp/items/825fd04510e709355f0c

今日のテーマは **Flexbox（基礎編）** です。
Web 制作で頻出の「横並び」や「上下中央揃え」を簡潔に実現できる、現代 CSS の必修科目です。

---

### 🎯 本日の目標

1.  **`display: flex`** を使って、要素を横並びにする。
2.  **`justify-content`** と **`align-items`** を使いこなし、要素を狙った位置に配置する。
3.  Web サイトで頻出の **「ヘッダー（ロゴ左寄せ・メニュー右寄せ）」** を作る。

---

### 📝 ミッション内容

以下のステップで、ナビゲーションバーを作ってください。

#### 準備: HTML 構造を作る

以下の HTML を用意します。
親要素（ヘッダー）の中に、子要素（ロゴ）と子要素（ナビゲーション）が入っている構造です。

```html
<header class="header">
  <div class="logo">My Website</div>
  <nav class="nav-links">
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Contact</a>
  </nav>
</header>
```

#### Step 1: Flexbox を起動する

- `.header` クラスに `display: flex;` を指定してください。
- **確認:** 縦に並んでいた「ロゴ」と「メニュー」がどうなりましたか？

#### Step 2: 上下中央に揃える (align-items)

- `.header` に高さを適当に（例: `height: 80px;`）つけて、背景色もつけてみてください。
- 今のままだと、中身が上端に張り付いているはずです。
- `.header` に `align-items: center;` を追加してください。
- **確認:** 中身が「上下の真ん中」に来ましたか？

#### Step 3: 左右に配置する (justify-content)

- 今はロゴとメニューが左端に固まっています。
- `.header` に `justify-content: space-between;` を追加してください。
- **確認:** ロゴは左端、メニューは右端に配置されましたか？

#### Step 4: リンク同士の間隔を空ける (gap)

- 右側のメニュー（Home, About...）がくっつきすぎています。
- `.nav-links`（リンクを囲っている親）にも `display: flex;` を指定し、**`gap: 20px;`** を追加してみてください。
- **確認:** リンクとリンクの間に隙間ができましたか？

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="RNaYxEj" data-pen-title="Untitled" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/RNaYxEj">
  Untitled</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

Flexbox を理解するには、以下の 2 つの軸をイメージすることが重要です。

1.  **`justify-content` = 主軸（メインの並ぶ方向）の調整**

    - 今回は「横並び」なので、 **横方向** の配置を決めます。
    - `flex-start` (左詰め)
    - `center` (中央寄せ)
    - `space-between` (両端配置) ※ヘッダーでよく使います

2.  **`align-items` = 交差軸（垂直方向）の調整**

    - 今回は「横並び」に対して垂直なので、 **縦方向** の配置を決めます。
    - `center` (上下中央) ※これだけで文字やアイコンの高さ合わせが完了します

3.  **`gap` (ギャップ)**
    - 以前は `margin-right` などで調整していましたが、今は親に `gap` を指定するだけで、子要素の間に余白が入ります。

---

### 💡 補足：Flexbox が生まれた背景

Flexbox が登場する前（2010 年頃まで）、Web 制作者は「要素を横に並べる」ために、本来の用途とは異なる機能を使っていました。

#### Flexbox 以前の手法

1.  **`float` の使用:**
    - もともとは「画像へのテキストの回り込み」を作るための機能です。
    - レイアウトに使うと **「高さが消滅する（親要素が潰れる）」** という副作用があり、`clearfix` というハックが必須でした。
2.  **`table` レイアウト:**
    - HTML の `<table>` タグでレイアウトを組んでいましたが、本来は表データ用なので「文書構造として不適切」とされました。
3.  **`inline-block`:**
    - 横並びにはできますが、改行コードが「隙間」として表示される問題があり、調整が必要でした。

#### 当時の課題

- **上下中央揃え:** 垂直方向の真ん中に要素を置く簡単な方法が存在しませんでした。
- **高さの不揃い:** 横並びにしたカラムの中身のテキスト量が違うと、背景色の高さがばらばらになっていました。

Flexbox は、これらの課題を解決するために設計されました。

### CSS Grid との違い

Day 4 で学ぶ **CSS Grid** もレイアウト機能ですが、役割が異なります。

- **Flexbox:** **「1 次元（列または行）」** 向き。要素を一列に並べて配置を調整するのに適しています。
- **CSS Grid:** **「2 次元（面）」** 向き。縦と横を同時に制御して、複雑なマス目レイアウトを作るのに適しています。

実務では、大枠のレイアウトは **Grid** で作り、その中の細かいパーツは **Flexbox** で作る、という使い分けが一般的です。

---

### おわりに

これで「ナビゲーションバー」という Web サイトの基本パーツが作れるようになりました。
次回は、Flexbox の **「可変サイズ（伸び縮み）」** を使って、より複雑なレイアウト（聖杯レイアウト）に挑戦します。

https://qiita.com/saka2jp/items/9e7774f3ce8baa74d8ec
