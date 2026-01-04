---
title: CSSマスターへの道「実践UIトレース」
tags:
  - CSS
private: false
updated_at: '2026-01-05T01:36:03+09:00'
id: e04509615fe3f76e7050
organization_url_name: null
slide: false
ignorePublish: false
---

23 日目、いよいよ大詰めですね！
Phase 4 も中盤。今日は CSS 学習における **最強の上達法**、「UI トレース（模写）」です。

「0 からデザインを考える」のと「既存のデザインをコードで再現する」のは、使う脳の筋肉が全く違います。
プロが作った Web サイトのパーツを、まるで写経のようにそっくりそのまま再現することで、「なぜここに余白があるのか？」「なぜこの色なのか？」という意図が見えるようになります。

今日は、自分の「目」と「実装力」のズレを埋めるトレーニングです。

---

### はじめに：デベロッパーツールを見る前に

UI トレースをする時、いきなりブラウザの検証ツール（DevTools）を開いて答え（CSS）を見てはいけません。
まずは自分の目だけで、余白のサイズやフォントの大きさを推測して書いてみます。

その後に答え合わせをすることで、「自分は余白を詰めすぎる癖があるな」とか「プロの影（shadow）はもっと薄いんだな」といった発見が生まれます。

---

### 🎯 本日の目標

1.  **構造分解**: 一枚のデザインを見て、頭の中で瞬時に HTML の箱（`div`構成）を設計する。
2.  **観察眼**: ピクセル単位の余白、微妙な影、角丸のサイズを目視で盗む。
3.  **再現性**: 誰が見ても「本物そっくり」なレベルまでクオリティを高める。

---

### 📝 ミッション内容

Web サービスでよく見かける「料金プランカード」をトレースしてください。
今回は、以下の仕様のデザインを再現してみましょう。

- **デザイン要件:**
  - 3 つのプラン（Basic, Pro, Enterprise）が横並び。
  - 真ん中の「Pro プラン」だけ、少しサイズが大きく、目立つ色で、影が濃い（強調表示）。
  - 内容は「プラン名」「価格（大きく）」「機能リスト」「ボタン」。
  - 全体的に丸みを帯びたモダンなデザイン。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="JoKGOoj" data-pen-title="CSSマスターへの道「実践UIトレース」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/JoKGOoj">
  CSSマスターへの道「実践UIトレース」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. `gap` プロパティの活用

昔は `margin-bottom` でリストの間隔を空けていましたが、今は親（Flex/Grid コンテナ）に `gap` を指定するだけで均等に間隔が空きます。
`.card { display: flex; flex-direction: column; gap: 20px; }`
これだけで、「タイトル・価格・リスト・ボタン」の間がすべて 20px 空きます。修正も一瞬です。

#### 2. 強調のロジック

真ん中のカードを目立たせるために、以下の 3 点を行っています。

1.  **`transform: scale(1.1)`**: CSS でサイズを一回り大きくする。
2.  **`box-shadow`**: 影を濃く、広くすることで「浮いている（手前にある）」ように見せる。
3.  **Accent Color**: ブランドカラー（青色）をボタンや枠線に使用し、視線を誘導する。

#### 3. 影の美学

素人は `box-shadow: 5px 5px 5px black;` と書きがちですが、プロは **`rgba(0,0,0,0.05)`** のような「限りなく透明に近い黒」を使います。
「影があるかわからないけど、なんか立体的に見える」くらいが、今の Web デザインのトレンドです。

---

### 💡 応用：レスポンシブ対応

このままだとスマホで見た時に `scale(1.1)` のせいで画面からはみ出したり、重なったりする可能性があります。
コンテナクエリやメディアクエリを使って、
「画面が狭い時は `scale(1)` に戻し、縦並びにする」
という調整を加えてみてください。

```css
@media (max-width: 800px) {
  .card-popular {
    transform: scale(1); /* 拡大を解除 */
    order: -1; /* Flexboxの並び順変更機能！おすすめを一番上に持ってくる */
  }
}
```

---

### おわりに

今日のトレースで、「なんとなく」配置していた要素に、明確な意図を持てるようになったはずです。
「余白は 30px じゃなくて 40px の方が高級感が出るな」といった感覚は、このトレースを繰り返すことでしか養えません。

明日の Day 24 は、「**インタラクティブな仕掛け**」 です。
JavaScript を使わずに、CSS だけで「アコーディオンメニュー（開閉するパネル）」を作ります。
「CSS でロジックを組む」感覚を楽しみましょう！
