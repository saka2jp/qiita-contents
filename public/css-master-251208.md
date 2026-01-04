---
title: CSSマスターへの道「背景とグラデーション」
tags:
  - CSS
private: false
updated_at: '2026-01-05T01:37:12+09:00'
id: 17e11d68e1b9fa85d90c
organization_url_name: null
slide: false
ignorePublish: false
---

8 日目、お疲れ様です！
今日から **Phase 2: デザインの表現力を高める週** に突入します。

これまでの 1 週間で「骨組み（レイアウト）」を作る力はつきました。ここからは「**塗装（デザイン）**」の技術を磨きます。CSS は単なる配置ツールではなく、Photoshop のような「画材」にもなり得るのです。

今日はその第一歩、Web サイトの雰囲気を一瞬で変える「グラデーション」を極めましょう。

---

### はじめに：画像を使わない「色の魔法」

Web デザインにおいて、単色（ベタ塗り）の背景は安全ですが、少し退屈に見えることがあります。
CSS グラデーション（Gradients）を使えば、画像を 1 枚も読み込むことなく、奥行きのある美しい色彩や、複雑な模様を作り出すことができます。しかもデータ容量はほぼゼロ。ページの表示速度にも優しい技術です。

---

### 🎯 本日の目標

1.  **`linear-gradient`（線形）** を使いこなし、美しい夕焼けのような背景を作る。
2.  **`radial-gradient`（円形）** や **`repeating-...`（繰り返し）** を使って、CSS だけで「模様」を描く。
3.  複数のグラデーションを**重ねる**テクニックを理解する。

---

### 📝 ミッション内容

以下の 2 つのカード（長方形のボックス）を CSS で作ってください。

- **Mission 1: 「Sunset Card」**
  - 左上から右下に向かって、紫からオレンジ、そして黄色へと変化する「夕暮れの空」のような滑らかなグラデーションをかける。
- **Mission 2: 「Pattern Card」**
  - CSS の機能だけで「ストライプ（縞模様）」または「水玉模様」の背景を作る。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="gbMpjdQ" data-pen-title="CSSマスターへの道「背景とグラデーション」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/gbMpjdQ">
  CSSマスターへの道「背景とグラデーション」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. グラデーションは「画像」扱い

CSS において、グラデーションは `background-color` ではなく、`background-image` プロパティとして扱われます（短縮形の `background` でも OK）。

#### 2. `linear-gradient`（線形）の書き方

もっともよく使う形です。

```css
background: linear-gradient(方向, 色1, 色2, 色3...);
```

- **方向:** `to right`（右へ）、`to bottom`（下へ）、`45deg`（斜め）などで指定。
- **色の位置:** 色の後ろに `%` をつけると、変化する位置を細かく制御できます。
  - 例: `linear-gradient(to right, blue 50%, red 50%)` → 青と赤がくっきり分かれた 2 色旗になります。

#### 3. グラデーションは「重ねられる」

ここが中級者へのステップアップです。`background-image` はカンマ `,` 区切りで複数の値を指定できます。**「先に書いたものが手前（上）」**に表示されます。

```css
/* 例: 写真の上に、黒い半透明グラデーションを重ねる */
background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.8)),
  /* 手前の層（暗くする用） */ url("photo.jpg"); /* 奥の層（写真） */
```

これを使えば、文字が乗っても読みやすい背景画像が作れます。

---

### 💡 応用：円形グラデーションで「スポットライト」

線形だけでなく、中心から広がる `radial-gradient` もあります。これを応用すると、一部分だけ明るいスポットライトのような効果が作れます。

```css
.spotlight {
  background: radial-gradient(
    circle at center,
    #ffffff 0%,
    #dddddd 20%,
    #888888 100%
  );
}
```

- `circle`: 正円（デフォルトは楕円になることも）。
- `at center`: 中心の位置を指定（`at top left` なども可）。

---

### おわりに

今日のミッションで、のっぺりとした画面に「色気」が出たはずです。
グラデーションは色の組み合わせセンスが問われますが、「uiGradients」 などの Web サイトを参考にすると、プロっぽい配色がすぐに見つかりますよ。

明日の Day 9 は、今日のカードデザインをさらに立体的にする 「影（Box-shadow）の魔術」 です。マテリアルデザインやニューモーフィズムといったトレンド表現に挑戦しましょう！
