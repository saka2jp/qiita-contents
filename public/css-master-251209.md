---
title: CSSマスターへの道「シャドウ」
tags:
  - CSS
private: false
updated_at: '2026-01-04T22:22:37+09:00'
id: fd974fe751298c8d77ca
organization_url_name: null
slide: false
ignorePublish: false
---

Day 9 です。

https://qiita.com/saka2jp/items/17e11d68e1b9fa85d90c

昨日の「グラデーション」で平面に色が着きました。
今日はそこに「**奥行き**」を与えます。

画面は 2 次元ですが、人間は「影」があるだけでそれを「物体」として認識します。
CSS の `box-shadow` は、影を落とすだけでなく、**物体を浮かせたり、へこませたり、光らせたり** できるプロパティです。

---

### はじめに：影が操る「高さ」の概念

Web デザイン（特に Google のマテリアルデザイン）では、「**要素の重要度＝高さ**」という考え方をします。

- 影が濃く、広い＝高く浮いている＝**重要**（操作してほしいボタンなど）
- 影がない＝床にくっついている＝**普通**（背景など）

この「高さ」をコントロールできると、ユーザーに「ここを押して」と視覚的に伝えられるようになります。

---

### 🎯 本日の目標

1.  **`box-shadow` の 5 つの値**（X, Y, ぼかし, 広がり, 色）を理解する。
2.  **マテリアルデザイン風**：紙が浮いているような自然な影を作る。
3.  **ニューモーフィズム風**：要素が背景から盛り上がっているような、リアルな凹凸を作る。

---

### 📝 ミッション内容

以下の 2 つのスタイルのボックスを作ってください。

- **Mission 1: 「Floating Card」**
  - ふんわりとした影をつけて、白い紙が浮いているように見せる。
- **Mission 2: 「Soft UI (Neumorphism)」**
  - 背景色と同じ色のボックスに、「明るい影」と「暗い影」の 2 つをつけて、粘土が盛り上がったような質感を作る。
  - （できれば）クリックした時に「へこむ」演出も入れる。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="ZYOQJyp" data-pen-title="CSSマスターへの道「シャドウ」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/ZYOQJyp">
  CSSマスターへの道「シャドウ」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. `box-shadow` の解剖図

```css
box-shadow: 10px 10px 20px 5px rgba(0, 0, 0, 0.5);
```

左から順に：

1.  **Offset-X (10px):** 横方向のズレ（正＝右、負＝左）。
2.  **Offset-Y (10px):** 縦方向のズレ（正＝下、負＝上）。
3.  **Blur (20px):** ぼかし具合。0 だとくっきり、数値が大きいとぼやける。
4.  **Spread (5px):** 影の拡大・縮小。省略可能。
5.  **Color:** 影の色。`rgba` を使って透明度を指定するのが基本です。真っ黒（#000）を使うと不自然に見えるので注意。

#### 2. 複数の影を操る

昨日のグラデーション同様、カンマ `,` で区切れば何個でも影をつけられます。
ニューモーフィズムはこれを利用して、「左上からの光（ハイライト）」と「右下に落ちる影（シャドウ）」を同時に描画することで、立体感を表現しています。

#### 3. `inset`（内側の影）

値の最初に `inset` と書くと、影がボックスの **内側** に落ちます。
これを使うと「穴が開いている」あるいは「ボタンが押し込まれている」状態を表現できます。

---

### 💡 応用：ボーダーや光彩として使う

`box-shadow` は影以外にも使えます。

**1. ネオンサイン（光彩）**
ぼかしを大きくし、明るい色を指定すると、発光しているように見えます。

```css
.neon-btn {
  background: #000;
  color: #fff;
  /* 青白く光る */
  box-shadow: 0 0 15px #00aaff, 0 0 30px #00aaff;
}
```

**2. レイアウトに影響しない枠線**
`border` プロパティを使うと要素のサイズが太くなりますが、`box-shadow` はサイズに影響しません。

```css
.outline-box {
  /* ぼかし 0、広がり 2px で枠線代わりになる */
  box-shadow: 0 0 0 2px red;
}
```

---

### おわりに

「影」をコントロールできると、UI デザインのクオリティが向上します。
特に **`rgba(0,0,0,0.1)` のような「薄い影」を「大きくぼかす」** のが、最近の Web サイトのトレンドです。

次回は、四角い箱から卒業します。
**「ボーダーと角丸」** を使って、有機的な「歪んだ形」や美しい円を作るテクニックです。

https://qiita.com/saka2jp/items/5549622b1d7e38e49f46
