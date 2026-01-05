---
title: CSSマスターへの道「画像加工 (object-fit / filter)」
tags:
  - CSS
private: false
updated_at: '2026-01-05T21:28:51+09:00'
id: 020c06e566206834e64f
organization_url_name: null
slide: false
ignorePublish: false
---

Day 13 です。

https://qiita.com/saka2jp/items/275a3f4e26f8790e4b8b

Phase 2 も後半戦です。今日は Web サイトのビジュアルインパクトを左右する「画像」の扱い方です。

これまで、画像を配置するときに「横幅を指定したら、縦長に伸びて変になった」という経験はありませんか？
あるいは、画像をモノクロにしたり明るくしたりするために、画像編集ソフトを開いていませんか？

今日は、**画像の比率崩れを CSS 1 行で防ぎ、さらにフィルター加工まで CSS で完結させる** テクニックを学びます。

---

### はじめに：ブラウザは「画像編集ソフト」になる

現代の CSS は非常に強力です。
`object-fit` を使えば、どんなサイズの画像が来てもレイアウトに合わせて自動でトリミング（切り抜き）してくれます。
`filter` を使えば、インスタグラムのような色加工やぼかしを、コードだけで適用できます。

これにより、画像素材を加工する手間が減り、後からの変更も簡単になります。

---

### 🎯 本日の目標

1.  **`object-fit: cover`**：画像の縦横比（アスペクト比）を維持したまま、指定した枠にきれいに収める。
2.  **`filter`**：彩度を落としたり（モノクロ）、ぼかしたりして、エモーショナルな表現を作る。
3.  **ホバーエフェクト**：マウスを乗せた時に「モノクロ → カラー」になる演出を作る。

---

### 📝 ミッション内容

以下の 2 つの画像要素を作ってください。
（※お手持ちの適当な写真画像か、ネット上のフリー素材 URL を使ってください）

- **Mission 1: 「Perfect Square」**
  - 元の画像が横長でも縦長でも、**正方形（200px × 200px）** の枠の中に、歪まずに埋まるアイコン画像を作る。
- **Mission 2: 「Dramatic Card」**
  - 最初は「暗くてぼやけたモノクロ画像」だが、ホバーすると「明るく鮮明なカラー画像」に変化するカードを作る。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="gbMPxEV" data-pen-title="CSSマスターへの道「画像加工 (object-fit / filter)」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/gbMPxEV">
  CSSマスターへの道「画像加工 (object-fit / filter)」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. `object-fit` の種類

`<img>` タグに `width` と `height` を指定した時の挙動を制御します。

- **`fill` (デフォルト):** 無理やり引き伸ばして枠に合わせる（画像が歪む）。
- **`cover` (推奨):** 比率を保ったまま、枠を埋めるように拡大縮小する。はみ出た部分は切り取られる（トリミング）。
- **`contain`:** 比率を保ったまま、画像が全て入るようにする。枠との間に隙間ができる。

**「`img` タグでサイズ指定するなら、セットで `object-fit: cover;` も書く」** と覚えておくと便利です。

#### 2. `filter` でできること

Photoshop のような加工ができます。複数重ねがけも可能です。

- `blur(5px)`: ぼかし。
- `grayscale(100%)`: モノクロ化。
- `sepia(100%)`: セピア調。
- `brightness(150%)`: 明るくする（100% が基準）。
- `contrast(200%)`: コントラストを強くする。
- `hue-rotate(90deg)`: 色相を回転させる（色を変える）。

---

### 💡 応用：背景画像を暗くして文字を読ませる

ヒーローエリア（サイトのトップ画像）などで、写真の上に白い文字を載せたい時、写真が明るすぎると文字が読めませんよね？
そんな時、CSS で画像を暗くします。

```css
/* 方法 1: filter を使う場合（画像自体が暗くなる） */
.hero-image {
  filter: brightness(50%);
}

/* 方法 2: 背景色とブレンドする場合（より細かい調整が可能） */
.hero-section {
  background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    /* 黒い半透明の膜 */ url("photo.jpg");
  background-size: cover;
}
```

---

### おわりに

`object-fit` を知っているだけで、CMS（WordPress など）でクライアントがどんなサイズの画像をアップロードしても、レイアウト崩れを起こさない堅牢なサイトが作れます。これは実務で必須のスキルです。

また、`filter` を使えば、サイト全体の画像のトーンを CSS だけで統一でき、世界観を作り込むことができます。

次回は、画像を星型やハート型など、好きな形に切り抜く **「クリップパス (clip-path)」** です。Phase 2 の締めくくりとして、自由な造形を学びましょう。

https://qiita.com/saka2jp/items/652f533e4cd226fc1cb2
