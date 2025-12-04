---
title: CSSマスターへの道「Flexbox(基礎編)」
tags:
  - CSS
private: false
updated_at: '2025-12-03T07:37:34+09:00'
id: 3383006a106417c709f0
organization_url_name: null
slide: false
ignorePublish: false
---

2 日目、お帰りなさい！
昨日は地味な基礎でしたが、今日からは　**「目に見えてレイアウトが変わる」**　楽しいパートに入ります。

今日のテーマは **「Flexbox（基礎編）」** です。
かつて Web 制作者たちが頭を抱えていた「横並び」や「上下中央揃え」を一瞬で解決する、現代 CSS の必修科目です。

---

## Day 2: レイアウト革命「Flexbox」の基礎

### 🎯 本日の目標

1.  **`display: flex`** を使って、要素を横並びにする。
2.  **`justify-content`** と **`align-items`** を使いこなし、要素を狙った位置に配置する。
3.  Web サイトで最もよく見る**「ヘッダー（ロゴ左寄せ・メニュー右寄せ）」**を作る。

---

### 📝 ミッション内容

以下のステップで、よくある Web サイトのナビゲーションバーを作ってください。

#### 準備: HTML 構造を作る

まずは、以下の HTML を用意します（コピペ OK）。
親箱（ヘッダー）の中に、子箱（ロゴ）と子箱（ナビゲーション）が入っている構造です。

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
- **観察:** 縦に並んでいた「ロゴ」と「メニュー」がどうなりましたか？

#### Step 2: 上下中央に揃える (align-items)

- `.header` に高さを適当に（例: `height: 80px;`）つけて、背景色もつけてみてください。
- 今のままだと、中身が上端に張り付いているはずです。
- `.header` に `align-items: center;` を追加してください。
- **観察:** 中身がスッと「上下の真ん中」に来ましたか？

#### Step 3: 左右に突き放す (justify-content)

- 今はロゴとメニューが左端に固まっています。
- `.header` に `justify-content: space-between;` を追加してください。
- **観察:** ロゴは左端、メニューは右端に配置されましたか？

#### Step 4: リンク同士の間隔を空ける (gap)

- 右側のメニュー（Home, About...）がくっつきすぎています。
- `.nav-links`（リンクを囲っている親）にも `display: flex;` を指定し、新機能 **`gap: 20px;`** を追加してみてください。
- **観察:** リンクとリンクの間に隙間ができましたか？

---

### 💻 実装サンプル

うまくいきましたか？ こちらが正解のコード例です。

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

Flexbox を理解するには、以下の 2 つの軸をイメージするのがコツです。

1.  **`justify-content` = 主軸（メインの並ぶ方向）の調整**

    - 今回は「横並び」なので、**横方向**の配置を決めます。
    - `flex-start` (左詰め)
    - `center` (中央寄せ)
    - `space-between` (両端配置) ※ヘッダーで超使います

2.  **`align-items` = 交差軸（垂直方向）の調整**

    - 今回は「横並び」に対して垂直なので、**縦方向**の配置を決めます。
    - `center` (上下中央) ※これだけで文字やアイコンの高さ合わせが完了します

3.  **`gap` (ギャップ)**
    - 昔は `margin-right` などで頑張っていましたが、今は親に `gap` を指定するだけで、子要素の間にだけ余白が入ります。超便利です。

---

## なぜ Flexbox が生まれたのか？

### 1. Flexbox 登場の歴史的背景： 「CSS レイアウトの暗黒時代」

Flexbox が登場する前（2010 年頃まで）、Web 制作者たちは「要素を横に並べる」ためだけに、本来の用途とは違う機能を無理やり使っていました。

#### 😭 苦難の時代（Before Flexbox）

1.  **`float` の乱用:**
    - もともとは「画像へのテキストの回り込み（新聞のようなレイアウト）」を作るための機能です。
    - これを無理やりレイアウトに使っていたため、**「高さが消滅する（親要素が潰れる）」** という副作用があり、それを直すための `clearfix` という呪文のようなハックが必須でした。
2.  **`table` レイアウト:**
    - 昔は HTML の `<table>` タグでレイアウトを組んでいましたが、本来は表データ用なので「文書構造として間違い」とされ、廃止されました。
3.  **`inline-block`:**
    - 横並びにはできますが、改行コードが「謎の隙間」として表示されてしまう問題があり、調整が面倒でした。

#### 😱 最大の悩み：「上下中央揃え」と「高さ揃え」ができない

当時の CSS では、以下の 2 つが**絶望的に難しかった**のです。

- **上下中央揃え:** 「ボタンの中の文字」や「画面の真ん中のメッセージ」を垂直方向の真ん中に置く簡単な方法が存在しませんでした。
- **高さの不揃い:** 横並びにしたカラム（列）の中身のテキスト量が違うと、背景色の高さがガタガタになってしまいました。

**「もっとレイアウト専用の、柔軟（Flexible）な箱（Box）が必要だ！」**
という悲痛な叫びから生まれたのが、**Flexbox (Flexible Box Layout Module)** です。

### 2. Flexbox は何を解決したのか？

Flexbox は、これまでの「ハック」を一掃しました。

1.  **1 行で横並び:** `float`解除などの処理が不要。
2.  **魔法の上下中央:** `align-items: center` だけで、長年の悩みだった垂直中央揃えが解決。
3.  **高さの統一:** デフォルトで、横並びの要素は　**「一番背の高い要素」に合わせて伸びる**　ようになりました。
4.  **順序の入れ替え:** HTML を書き換えなくても、CSS だけで「右と左を入れ替える」などが可能になりました。

### 補足：CSS Grid との違いは？

Day 4 で登場する **CSS Grid** もレイアウト機能ですが、役割分担があります。

- **Flexbox:** **「1 次元（列または行）」**。要素を一列に並べたり、その中での配置を調整したりするのに向いています。「中身（コンテンツ）のサイズ」を基準に並べるのが得意です。
- **CSS Grid:** **「2 次元（面）」**。縦と横を同時に制御して、新聞やポスターのような複雑なマス目レイアウトを作るのに向いています。「外側の枠（グリッド）」を決めてから中身を入れるのが得意です。

**現代の主流:**
大枠のレイアウト（全体のマス目）は **Grid** で作り、その中の細かいパーツ（ナビゲーションやボタン配置）は **Flexbox** で作る、という使い分けが一般的です。

---

**Day 2 クリアです！**
これで「ナビゲーションバー」という Web サイトの顔が作れるようになりました。
明日は、Flexbox のもう一つの強力な機能、　**「可変サイズ（伸び縮み）」**を使って、より複雑なレイアウト（聖杯レイアウト）に挑戦します。

明日も頑張りましょう！
