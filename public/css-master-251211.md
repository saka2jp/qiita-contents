---
title: CSSマスターへの道「テキスト装飾とWebフォント」
tags:
  - CSS
private: false
updated_at: '2026-01-05T21:28:51+09:00'
id: 96a16834fb4614c3d351
organization_url_name: null
slide: false
ignorePublish: false
---

Day 11 です。

https://qiita.com/saka2jp/items/5549622b1d7e38e49f46

Phase 2 も中盤です。今日は Web デザインの多くを占める「文字（タイポグラフィ）」です。
「ただ文字を表示する」のと「読ませる・魅せる」のは別物です。
フォント選びとちょっとした CSS の調整だけで、サイトのデザインが変わります。

---

### はじめに：文字は「声色」を変える

Web サイトにおけるフォントは、話し言葉でいう「声のトーン」です。
明朝体なら「真面目で上品な声」、ゴシック体なら「親しみやすく元気な声」。
さらに CSS を使えば、グラデーションのドレスを着せたり、ネオンのように光らせたりすることも可能です。

---

### 🎯 本日の目標

1.  **Google Fonts** を導入して、脱・デフォルトフォントをする。
2.  **`line-height`（行間）** と **`letter-spacing`（字間）** で、「読みやすさ」を向上させる。
3.  **グラデーション文字**：文字の中だけを虹色やグラデーションにするモダンなテクニックを習得する。

---

### 📝 ミッション内容

以下の要素を含む「タイポグラフィ・ポスター」のような画面を作ってください。

- **Mission 1: Google Fonts の導入**
  - 英語フォント（例: 'Poppins' や 'Montserrat'）と日本語フォント（例: 'Noto Sans JP'）を読み込んで適用する。
- **Mission 2: グラデーション見出し**
  - 背景ではなく、「文字の色」自体がグラデーションになっている大きな見出しを作る。
- **Mission 3: 美しい本文**
  - 行間と文字間隔を調整して、雑誌のように読みやすいパラグラフを作る。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="PwzZKBr" data-pen-title="CSSマスターへの道「テキスト装飾とWebフォント」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/PwzZKBr">
  CSSマスターへの道「テキスト装飾とWebフォント」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. Google Fonts の使い方

基本は 3 ステップです。

1.  [Google Fonts](https://fonts.google.com/) にアクセス。
2.  好きなフォントを選び、太さ（Weights）を選択してカートに入れる。
3.  発行されたコードを HTML の `<head>` または CSS の `@import` に貼り付ける。

#### 2. 読みやすさの基本数値

- **`line-height` (行の高さ):**
  - デフォルトは狭すぎます。
  - 本文なら **`1.6` 〜 `1.8`** くらいに設定すると、読みやすくなります。単位（px や%）をつけずに数字だけで指定するのがベストプラクティスです。
- **`letter-spacing` (文字の間隔):**
  - 見出しや英語は、広め（`0.05em` 〜 `0.1em`）に取ると高級感が出ます。
  - 長文の本文は、広すぎると散漫になるので `0` 〜 `0.05em` 程度に抑えます。

#### 3. グラデーション文字の仕組み

`background-clip: text` は、「背景画像を文字の形で切り抜く」プロパティです。
これを使う時、元の文字色（`color`）があると背景が見えないので、**`color: transparent` で文字を透明にする** のが最大のポイントです。

---

### 💡 応用：袋文字（アウトライン）

`text-shadow` を使うと影を落とせますが、モダンな Web デザインでは「中抜き文字（ストローク）」も使われます。

```css
.outline-text {
  font-size: 4rem;
  font-weight: bold;
  color: transparent; /* 中身は透明 */
  /* 文字の縁取り（幅 色） */
  -webkit-text-stroke: 2px white;
}
```

背景画像の上にこれを配置すると、背景が文字の中を透けて見えます。

---

### おわりに

「フォントを変える」「行間を空ける」。この 2 つを意識するだけで、サイトのクオリティは向上します。
特にポートフォリオなどでは、文字の美しさがそのまま「几帳面さ」として評価されることがあります。

次回は **「疑似要素 (::before / ::after)」** です。
HTML には何も書かずに、CSS だけでアイコンや装飾を出現させるテクニックを学びます。

https://qiita.com/saka2jp/items/275a3f4e26f8790e4b8b
