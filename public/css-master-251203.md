---
title: CSSマスターへの道「Flexbox(応用編)」
tags:
  - CSS
private: false
updated_at: '2026-01-05T21:28:51+09:00'
id: 9e7774f3ce8baa74d8ec
organization_url_name: null
slide: false
ignorePublish: false
---

Day 3 です。

https://qiita.com/saka2jp/items/3383006a106417c709f0

昨日は「配置（左寄せ・中央寄せ）」を学びましたが、今日は **「伸縮（伸び縮み）」** をマスターします。

これを理解すると、**「画面幅が変わっても、検索バーの入力欄だけが伸び、ボタンのサイズはそのまま」** といったレスポンシブな UI が作れるようになります。

---

### 🎯 本日の目標

1.  **`flex-grow`** (伸びる) と **`flex-shrink`** (縮む) の仕組みを理解する。
2.  省略記法 **`flex: 1;`** を使いこなす。
3.  Web レイアウトの定番、 **「聖杯レイアウト（Holy Grail Layout）」** を作る。

---

### 📝 ミッション内容

今日は 2 段階構成です。まずは小さなパーツで実験し、その後にページ全体のレイアウトを作ります。

#### Step 1: 検索バーを作る（伸びる要素の実験）

検索窓を作ります。

- 親要素の中に、`<input>`（入力欄）と `<button>`（検索ボタン）を置いてください。
- 親要素に `display: flex;` をかけます。
- **課題:** 入力欄 (`input`) だけに CSS を書き足して、 **「ボタンの幅は固定のまま、入力欄だけが余ったスペース一杯に広がる」** ようにしてください。

#### Step 2: 聖杯レイアウトを作る（ページ全体の構成）

「ヘッダー」「フッター」「3 カラムのメインエリア」を持つレイアウトを作ります。

- **構造:**
  - 上：ヘッダー (Header)
  - 中：メインエリア (Container) ※ここを Flexbox にする
    - 左：メニュー (Left Sidebar) - 幅 150px 固定
    - 中：コンテンツ (Main Content) - **可変（残りの幅すべて）**
    - 右：広告枠 (Right Sidebar) - 幅 150px 固定
  - 下：フッター (Footer)
- **課題:** 画面幅を広げたり狭めたりした時、左右のサイドバーの幅は変わらず、 **真ん中のコンテンツ部分だけが伸縮する** ようにしてください。

---

### 💻 実装サンプル

まずは自分で実装してみてください。詰まったら以下のコードを参考にしてください。

<details><summary>Step 1 正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="gbrdjmb" data-pen-title="CSSマスターへの道「Flexbox(応用編)」Step.1" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/gbrdjmb">
  CSSマスターへの道「Flexbox(応用編)」Step.1</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

<details><summary>Step 2 正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="EaKeegq" data-pen-title="CSSマスターへの道「Flexbox(応用編)」Step.2" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/EaKeegq">
  CSSマスターへの道「Flexbox(応用編)」Step.2</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

Flexbox のアイテム（子要素）には、3 つの重要なプロパティがあります。これをまとめて指定できるのが **`flex`** ショートハンドです。

#### 1. `flex-grow` (成長係数)

- 「余ったスペースがあった場合、どれくらいの比率で分配するか」を指定します。
- `0` (デフォルト): 伸びない。
- `1`: 伸びる。
- 兄弟要素すべてが `1` なら等分されます。片方が `2` なら、その要素は 2 倍の余白を受け取ります。

#### 2. `flex-shrink` (収縮係数)

- 「スペースが足りなくなった時、どれくらいの比率で縮むか」を指定します。
- `1` (デフォルト): 縮む。
- `0`: **縮まない。**
- サイドバーの幅をピクセル固定(`width: 150px`)していても、画面が極端に狭くなると Flexbox は無理やり収めようとしてサイドバーを縮めます。これを防ぐために `.sidebar` に `flex-shrink: 0;` を指定します。

#### 3. 省略記法 `flex: 1;`

実務では `flex-grow: 1` と書く代わりに、以下をよく使います。

```css
.item {
  flex: 1;
}
```

これは **「幅の指定を無視して、余った場所を全部埋める（伸びる）」** という意味で、非常によく使われます。
（厳密には `flex-grow: 1; flex-shrink: 1; flex-basis: 0%;` の略です）

---

### 💡 補足：聖杯レイアウトとは

**「聖杯レイアウト (Holy Grail Layout)」** とは、2000 年代に CSS で実現が困難だったレイアウトパターンです。

「ヘッダー・フッターがあり、中央が 3 列で、左右のカラム幅固定・中央可変、かつ 3 列の高さが揃う」という要件を満たすレイアウトは、当時の技術では実装が難しく、理想郷として「聖杯」と呼ばれていました。

Flexbox の登場により、数行の `display: flex` と `flex: 1` で実現できるようになりました。

---

### おわりに

これで「並べる」「揃える」「伸縮させる」という Flexbox の 3 大機能を習得しました。
次回は、Flexbox と双璧をなすレイアウト技術、 **「CSS Grid」** に進みます。2 次元のレイアウトを扱います。

https://qiita.com/saka2jp/items/8036b99b5b8c52bde058
