---
title: CSSマスターへの道「Position」
tags:
  - CSS
private: false
updated_at: '2026-01-05T21:28:51+09:00'
id: 4edb5310edbf52f35abd
organization_url_name: null
slide: false
ignorePublish: false
---

Day 7 です。

https://qiita.com/saka2jp/items/fb5412cd4c1a8f69ee57

Phase 1 の最終日です。今日のテーマは **Position** です。
**「スクロールしてもついてくるヘッダーや、画像の上に重なるバッジを実装する」** ことが今日の目標です。

---

### 📝 インプット：4 つの「基準」を知る

`position` プロパティを使う時、一番大事なのは「**何（どこ）を基準に配置するか？**」です。

| 値             | 基準となるもの       | よく使う場面                                                                       |
| :------------- | :------------------- | :--------------------------------------------------------------------------------- |
| **`static`**   | なし（デフォルト）   | 何もしない普通の配置。                                                             |
| **`relative`** | **本来あるべき位置** | その場所から少しだけずらしたい時。または **`absolute` の基準点（親）にしたい時**。 |
| **`absolute`** | **親要素** ※         | 親の左上を原点として、好きな場所に配置。「画像右上の NEW アイコン」など。          |
| **`fixed`**    | **ブラウザ画面**     | スクロールしても画面の同じ場所に居続ける。「トップへ戻るボタン」「モーダル」など。 |
| **`sticky`**   | **スクロール位置**   | スクロールして画面端に来たらピタッと張り付く。「追従ヘッダー」「目次」など。       |

※ `absolute` を使う時は、親要素（または祖先）に `position: relative` が指定されている必要があります。これがないと、画面全体（body）を基準にして配置されてしまいます。「**親に relative、子に absolute**」は CSS の定石です。

---

### 🎯 本日の目標

**「Position 全部盛りの Web ページ」を作ってください。**

以下の 3 つの要件を満たすシンプルなページを作ります。

1.  **Sticky ヘッダー:** ページをスクロールしても、途中から画面上部に張り付いてついてくるヘッダー。
2.  **Absolute バッジ:** コンテンツ内のボックスの「右上」に、「SALE」や「New」というバッジを重ねて表示する。
3.  **Fixed ボタン:** 画面の「右下」に、常に表示される「トップへ戻る（↑）」ボタンを置く。

---

### 📝 ミッション内容

#### 雛形コード

今回は構造が少し複雑なので、ベースを使ってください。

```html
<!-- 1. 追従するヘッダー -->
<header class="sticky-header">My Website</header>

<div class="container">
  <p>↓ スクロールしてみてください ↓</p>

  <!-- 2. 重ね合わせのデモ -->
  <div class="box-wrapper">
    <div class="box">
      商品画像やコンテンツ
      <!-- ここに絶対配置でバッジを乗せる -->
      <span class="badge">SALE</span>
    </div>
  </div>

  <!-- スクロール発生用のダミーテキスト（長い文章） -->
  <p>
    （ここに適当な長い文章を入れて、縦スクロールが発生するようにしてください...<br /><br /><br /><br /><br />スクロール...<br /><br /><br /><br /><br />もっとスクロール...）
  </p>
</div>

<!-- 3. 画面固定ボタン -->
<a href="#" class="fab-btn">↑</a>
```

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="RNRPBKQ" data-pen-title="CSSマスターへの道「Position」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/RNRPBKQ">
  CSSマスターへの道「Position」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

1.  **`sticky` の挙動確認:**
    - `top: 0` を指定しないと機能しません。
    - 「親要素の高さの中」でしか追従しません。今回は `body` 直下に近いのでずっとついてきますが、特定のセクション内で使うと「そのセクションが終わったら消える」という挙動になります。
2.  **`relative` を外してみる:**
    - `.box` の `position: relative;` を一時的にコメントアウトしてみてください。「SALE」バッジがどこに移動するか確認しましょう（おそらくページの右上に移動します）。これが「基準点のロスト」です。
3.  **`z-index` (重なり順):**
    - 固定ヘッダーやボタンが、他の画像の下に隠れてしまわないように、`z-index` で数値を指定して手前に持ってきます。

---

### おわりに

これで **Phase 1: レイアウトの達人** は修了です。
ボックスモデル、Flexbox、Grid、レスポンシブ、そして Position。
これらを組み合わせれば、一般的な Web サイトのレイアウトを再現できる基礎力がつきました。

次回からの **Phase 2** は、「見た目」を充実させるパートです。
グラデーションや影を使って、リッチなデザインを作っていきましょう。

https://qiita.com/saka2jp/items/17e11d68e1b9fa85d90c
