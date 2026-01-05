---
title: CSSマスターへの道「インタラクティブな仕掛け」
tags:
  - CSS
private: false
updated_at: '2026-01-05T21:28:51+09:00'
id: 4006f22abb98c51e7a32
organization_url_name: null
slide: false
ignorePublish: false
---

Day 24 です。

https://qiita.com/saka2jp/items/e04509615fe3f76e7050

この特訓もいよいよ明日でフィナーレです。

今日は「CSS だけで作るインタラクション」の総決算。
通常、クリックして何かを開いたり閉じたりするのは JavaScript (`onclick` イベント) の仕事だと思われがちです。

しかし、CSS には **「チェックボックスの ON/OFF」という「状態」を検知する機能** があります。これを応用すると、JS を 1 行も書かずに、滑らかに動くアコーディオンメニューが作れるのです。

今日はこの「CSS ロジック」を学びましょう。

---

### はじめに：「チェックボックス・ハック」

仕組みはこうです。

1.  **HTML:** 見えない「チェックボックス」と、それと紐付いた「ラベル（質問文）」を置く。
2.  **動作:** ラベルをクリックすると、見えないチェックボックスにチェックが入る（ブラウザの標準機能）。
3.  **CSS:** 「チェックが入っている時の、隣にある要素（回答）」のデザインを変える。

これを **「Checkbox Hack（チェックボックス・ハック）」** と呼びます。古くからある技術ですが、最近の CSS の進化により、アニメーションの滑らかさが向上しました。

---

### 🎯 本日の目標

1.  **ステート管理**: `input:checked` 疑似クラスを使って、開閉の状態を CSS で捉える。
2.  **兄弟セレクタ**: `+` (直後の要素) や `~` (後ろにある要素) を使い、離れた要素を操作する。
3.  **高さのアニメーション**: 長年 CSS の弱点だった「高さ（height: auto）へのアニメーション」を、Grid を使って解決する。

---

### 📝 ミッション内容

以下の機能を持つ「よくある質問（FAQ）」アコーディオンを作ってください。

- **UI:** 質問をクリックすると、回答エリアが「ヌルッ」とスライドして現れる。
- **アイコン:** 閉じている時は「＋」、開いている時は「－」（または ×）に回転するアニメーションをつける。
- **条件:** JavaScript は一切使用禁止。

---

### 💻 実装サンプル

最新のテクニックである **「Grid を使った高さアニメーション」** を採用しています。これで中身が何行あっても完璧にアニメーションします。

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="pvbgdyx" data-pen-title="CSSマスターへの道「インタラクティブな仕掛け」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/pvbgdyx">
  CSSマスターへの道「インタラクティブな仕掛け」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. CSS セレクタの連携プレー

```css
/* input がチェックされたら、その後ろにある content を操作 */
input:checked ~ .content {
  ...;
}
```

この `~`（チルダ）は「兄弟要素（同じ親を持つ要素）」の後ろにあるものを選択するセレクタです。
HTML の並び順が `input` → `label` → `content` である必要があるのはこのためです。

#### 2. 高さアニメーションの革命 `grid-template-rows`

長年、CSS では `height: 0` から `height: auto` へのアニメーション（transition）は不可能でした。
そのため、以前は `max-height: 1000px` のような適当な値を指定して無理やり動かしていました。

しかし、**Grid レイアウト** を使えば話は別です。

- 閉じる: `grid-template-rows: 0fr;`
- 開く: `grid-template-rows: 1fr;`
  これで、ブラウザが中身の高さを正確に計算してアニメーションしてくれます。これは 2023 年頃から主流になった最新テクニックです。

---

### 💡 応用：他でひとつだけ開く（ラジオボタン）

今回は「チェックボックス」を使ったので、全ての項目を同時に開くことができます。
これを `input type="radio"` に変えて、全てに同じ `name="accordion"` 属性をつけると…
**「ひとつ開くと、他が勝手に閉じる」** アコーディオンになります。
（ラジオボタンは常に 1 つしか選択できない仕様を利用するため）

この仕組みは、**「タブ切り替え UI」** にもそのまま応用できます。

---

### おわりに

「JavaScript を使わないと動かない」という固定観念、壊れましたか？
もちろん複雑なアプリを作るなら JS が必要ですが、Web サイトのちょっとした動きなら CSS だけで十分実装できますし、その方が動作も軽快です。

さあ、明日はついに **最終日 Day 25** です。
テーマは **「クリスマスカード制作」**。
これまで学んだ Flexbox、Grid、Position、Animation、そして今日のインタラクション。
全てを総動員して、最高の作品を作り上げましょう。

https://qiita.com/saka2jp/items/a7b0d22a21f76098dd6f
