---
title: CSSマスターへの道「コンテナクエリ」
tags:
  - CSS
private: false
updated_at: '2026-01-05T01:35:56+09:00'
id: 0112e66fe7443c118229
organization_url_name: null
slide: false
ignorePublish: false
---

21 日目、Phase 4「モダン CSS と総合演習」のスタートです！🎉
このフェーズでは、最新の CSS 技術と、これまで学んだスキルの総仕上げを行います。

初日の今日は、レスポンシブデザインの歴史を塗り替えた「**コンテナクエリ**」です。
これまでの「画面幅（Media Queries）」への依存を卒業し、「**自分の置き場所のサイズ**」に合わせて変形する、真のコンポーネント設計を学びましょう。

---

### はじめに：画面幅なんて関係ない

従来の `@media (min-width: ...)` には一つ弱点がありました。
「PC 画面（広い）だから横並び！」と判定しても、もしその要素が「サイドバー（狭い）」の中に置かれていたらどうなるでしょう？
PC なのに狭い場所に無理やり横並びで表示され、レイアウトが崩れてしまいます。

「コンテナクエリ」を使えば、「**画面がどれだけ広くても、私が置かれている場所（親要素）が狭ければ、スマホ用のレイアウトになる**」という、賢い挙動が可能になります。

---

### 🎯 本日の目標

1.  **`container-type`**: 親要素を「観測対象（コンテナ）」として登録する。
2.  **`@container`**: 画面幅ではなく、親要素の幅に応じてスタイルを書き換える。
3.  **コンポーネント指向**: どこに置いても勝手に最適化される「最強のカード」を作る。

---

### 📝 ミッション内容

以下の構成で、**全く同じ HTML（カード）** を 2 つの異なるエリアに配置してください。

- **エリア 1: メインエリア（広い）**
  - ここにあるカードは、横幅に余裕があるので「画像：左、テキスト：右」の**横型レイアウト**になる。
- **エリア 2: サイドバー（狭い）**
  - ここにあるカードは、幅が狭いので「画像：上、テキスト：下」の**縦型レイアウト**になる。

**※重要:** クラス名（例: `.card`）を変えてはいけません。CSS だけで自動的に判断させます。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="zxBrEQb" data-pen-title="CSSマスターへの道「コンテナクエリ」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/zxBrEQb">
  CSSマスターへの道「コンテナクエリ」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. 概念の違い

- **Media Query (`@media`)**: 「ブラウザの画面幅」を見る。ページ全体のレイアウト変更に使う。
- **Container Query (`@container`)**: 「直近の親要素の幅」を見る。パーツ（コンポーネント）ごとの最適化に使う。

#### 2. 必須プロパティ `container-type`

これがないと動きません。監視したい親要素に指定します。

- `inline-size`: 横幅（インライン軸）のみ監視。基本はこれを使います。
- `size`: 幅と高さの両方を監視（高さ指定が必須になるため、少し扱いにくいです）。

#### 3. ブラウザ対応

2025 年現在、Chrome, Edge, Safari, Firefox など、モダンブラウザの最新版ですべて対応しています。安心して実務で使える技術になりました。

---

### 💡 応用：コンテナ単位 `cqw`

`vw` (Viewport Width) という単位がありましたが、コンテナクエリ版の **`cqw` (Container Query Width)** もあります。

これを使うと、「コンテナの幅の 5%の文字サイズ」といった指定が可能になります。

```css
.card-title {
  /* 親の幅に応じて文字サイズが滑らかに変わる！ */
  font-size: clamp(1rem, 5cqw, 2rem);
}
```

コンテナが小さい時は文字も小さく、広い時は大きく。これまで JS で計算していたようなことが CSS だけで完結します。

---

### おわりに

コンテナクエリをマスターすると、「このパーツ、スマホだと崩れるんで別のクラス作りますね」という会話がなくなります。
「一度作れば、サイドバーでもメインカラムでも、どこに放り込んでも勝手に最適化される」。
これが最新のコンポーネント設計です。

さて、理論的な話が続いたので、明日は息抜きも兼ねてクリエイティブにいきましょう。
Day 22 は 「**CSS アート (初級)**」 です。
`div`タグ 1 つだけで、イラストを描く楽しさを体験してください！
