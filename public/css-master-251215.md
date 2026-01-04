---
title: CSSマスターへの道「Transition」
tags:
  - CSS
private: false
updated_at: '2026-01-04T23:50:46+09:00'
id: 7b6f93e569e451d5fa2f
organization_url_name: null
slide: false
ignorePublish: false
---

15 日目、おめでとうございます！🎉
今日から **Phase 3: 動きとインタラクションの週** に突入します。

これまでの 2 週間で作ったデザインは、まだ「静止画」です。
今日からは、そこに「時間」の概念を取り入れ、命を吹き込みます。

最初のステップは **`transition`（トランジション／遷移）**。
「A の状態から B の状態へ、時間をかけて滑らかに変化させる」技術です。これがあるだけで、Web サイトの使い心地（UX）は何倍も良くなります。

---

### はじめに：0 か 1 か、ではなく「余韻」を作る

CSS でホバー効果（`:hover`）をつけた時、初期状態では色が「パッ」と一瞬で切り替わりますよね？
これは機械的で、少し安っぽい印象を与えてしまいます。

`transition` を使うと、色が「じわっ」と変わったり、ボタンが「ふわり」と浮き上がったりします。
この **「変化の過程」を補間する** のが今日のテーマです。

---

### 🎯 本日の目標

1.  **書き方の基本**：`transition` プロパティの省略形（プロパティ、時間、イージング）をマスターする。
2.  **置く場所のルール**：`:hover` の中ではなく、**元のクラス**に書く理由を理解する。
3.  **イージング（緩急）**：`ease`、`linear`、`ease-in-out` の違いを知り、気持ちいい動きを作る。

---

### 📝 ミッション内容

以下の 2 つのインタラクティブな要素を作ってください。

- **Mission 1: 「Smooth Button」**
  - ホバーすると、背景色が変わり、同時にサイズが少し大きくなるボタン。
  - 変化にかかる時間は「0.3 秒」。
- **Mission 2: 「Elastic Card」**
  - ホバーすると、上に浮き上がりながら影が濃くなるカード。
  - 「行き（ホバー時）」と「帰り（マウスを離した時）」で変化のスピードを変えてみる（応用）。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="qENbPqL" data-pen-title="CSSマスターへの道「Transition」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/qENbPqL">
  CSSマスターへの道「Transition」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. 書き方の解剖図

```css
/* ショートハンド（省略形） */
transition: <プロパティ> <時間> <イージング> <遅延(省略可) >;

/* 例 */
transition: background-color 0.5s ease-in-out;
```

- **プロパティ**: `all` にすると全部まとめて変化します。個別に `color` や `transform` と書くとパフォーマンスが良いです。
- **時間**: `0.3s` (0.3 秒) や `300ms` (300 ミリ秒) と書きます。Web の UI では **0.2s 〜 0.4s** が最も心地よいとされています。
- **イージング (Easing)**: 動きの「加減速」です。
  - `linear`: 一定速度（機械的な動き）。
  - `ease`: 開始と終了が滑らか（デフォルト）。
  - `ease-out`: 素早く始まって、ゆっくり止まる（ふわりと停まる感じ）。

#### 2. なぜ `:hover` に書かないの？

`.btn:hover { transition: ... }` と書いてしまうと、**「マウスを乗せた時」しかアニメーションしません**。
マウスを離した瞬間、アニメーションなしで「バチッ」と元の位置に戻ってしまいます。
**「元のクラス（.btn）」** に書くことで、行きも帰りもスムーズになります。

---

### 💡 応用：プロパティごとに時間をずらす

`transition-delay` を使うと、複数の変化に時間差をつけることができます。
例えば、「まず背景が変わってから、そのあと文字色が変わり、最後に枠線が広がる」といった凝った演出です。

```css
.complex-box {
  background: white;
  color: black;
  border: 2px solid transparent;

  /* 
     1. backgroundは すぐ(0s) 始まる
     2. colorは 0.2s 待ってから始まる
  */
  transition: background-color 0.3s ease 0s, color 0.3s ease 0.2s;
}

.complex-box:hover {
  background: black;
  color: white;
}
```

これを使うと、非常に洗練された印象を与えられます。

---

### おわりに

`transition: all 0.3s ease;`
この 1 行をお守りのように覚えておいてください。
ボタン、リンク、カードなど、クリックできる要素にはとりあえずこれを入れておくだけで、サイトのクオリティが保証されます。

さて、`transition` は「A 地点から B 地点へ」の単純な往復でした。
明日の Day 16 は、**「Animation (キーフレーム)」** です。
「A → B → C → A」のように、もっと複雑で自由な動きを作り出します。CSS だけでローディングアニメーションを作ってみましょう！
