---
title: CSSマスターへの道「スクロールスナップ」
tags:
  - CSS
private: false
updated_at: '2026-01-05T00:24:05+09:00'
id: 716351d0234f44094a50
organization_url_name: null
slide: false
ignorePublish: false
---

19 日目、おはようございます！
Phase 3 も終盤です。今日は「**スクロールスナップ（Scroll Snap）**」を学びます。

今まで、画像スライダーや「1 画面ずつ切り替わる Web サイト」を作るには、JavaScript の複雑な計算ライブラリ（Swiper.js や Slick など）が必要でした。
しかし今は違います。**CSS だけで、アプリのように「ピタッ」と止まるスクロール**が実装できるのです。

「中途半端な位置で止まって気持ち悪い…」という悩みを、たった 2 行の CSS で解決しましょう！

---

### はじめに：磁石のような吸着力

通常、Web ページのスクロールは「指を離した場所」で止まります。これを「慣性スクロール」と呼びます。
一方、**スクロールスナップ**を使うと、スクロール終了時に、指定した要素の「頭」や「真ん中」に **磁石のように吸着（スナップ）** させることができます。

- TikTok のような全画面動画切り替え
- Netflix のような横スクロールの作品リスト
- Apple の製品ページのようなプレゼンテーション

これらはすべて、この技術（または同じ挙動の JS）で作られています。

---

### 🎯 本日の目標

1.  **親要素の設定**: `scroll-snap-type` でスナップの方向と強さを決める。
2.  **子要素の設定**: `scroll-snap-align` で「どこ（端か真ん中か）」に合わせて止まるかを決める。
3.  **横スクロールギャラリー**: スマホアプリ風の横並びカードリストを作る。

---

### 📝 ミッション内容

以下の UI コンポーネントを作ってください。

- **Mission: 「App Store 風 横スクロール」**
  - カードを横一列に並べる。
  - 指でスクロールすると、中途半端な位置では止まらず、必ずカードの「中央」または「先頭」でピタッと止まるようにする。
  - （おまけ）スクロールバーを非表示にして、よりアプリっぽくする。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="vEKLeaO" data-pen-title="CSSマスターへの道「スクロールスナップ」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/vEKLeaO">
  CSSマスターへの道「スクロールスナップ」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. 親要素：`scroll-snap-type`

スクロールコンテナ（`overflow: auto` をつけている要素）に指定します。

- **方向:** `x`（横）、`y`（縦）、`both`（両方）。
- **厳格さ:**
  - **`mandatory` (推奨):** 指を離した時、必ず一番近いスナップポイントまで強制移動します。スライダーに最適。
  - **`proximity`:** 指を離した位置がスナップポイントに「近ければ」吸着し、遠ければその場で止まります。自然なスクロールの中にスナップを混ぜたい時に使います。

#### 2. 子要素：`scroll-snap-align`

中のアイテムに指定します。「要素のどこを基準に合わせるか」です。

- **`start`:** 左端（または上端）で合わせる。
- **`center`:** 中央で合わせる。
- **`end`:** 右端（または下端）で合わせる。

#### 3. 構造のルール

必ず **「スクロールする親」と「並んでいる子」** の関係で使います。
`display: flex` と組み合わせるのが鉄板パターンです。

---

### 💡 応用：全画面スクロールと「パディング」

**1. 全画面プレゼンテーション（縦）**
`height: 100vh` のセクションを縦に並べて、親に `scroll-snap-type: y mandatory` を指定すれば、Web サイト全体が PowerPoint のスライドのように「1 画面ずつ」切り替わるようになります。

**2. ヘッダーに隠れるのを防ぐ `scroll-padding`**
固定ヘッダー（`position: fixed`）がある場合、スナップした要素の上部がヘッダーの裏に隠れてしまうことがあります。
そんな時は親要素に `scroll-padding-top: 60px;`（ヘッダーの高さ分）を指定すると、スナップ位置をずらすことができます。これは非常に実用的なテクニックです！

---

### おわりに

JavaScript のスライダーライブラリは、読み込みが遅かったり、スマホでの動作が重かったりすることがあります。
CSS Scroll Snap なら、ブラウザ標準機能なので**爆速で、動きもネイティブアプリ並みに滑らか**です。

「JS を使わずにカルーセルを作る」。これもまた、モダンなフロントエンドエンジニアの嗜みです。

さて、明日の Day 20 は 「**モダン CSS (:has / :is / :where)**」 です。
これらは CSS 界の「ロジック革命」です。「親要素を選択する」という、長年不可能と言われてきたことがついに可能になります！お楽しみに！
