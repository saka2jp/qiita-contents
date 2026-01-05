---
title: 'CSSマスターへの道「疑似要素 (::before / ::after)」'
tags:
  - CSS
private: false
updated_at: '2026-01-04T22:57:11+09:00'
id: 275a3f4e26f8790e4b8b
organization_url_name: null
slide: false
ignorePublish: false
---

Day 12 です。

https://qiita.com/saka2jp/items/96a16834fb4614c3d351

Phase 2 も佳境に入ってきました。今日は CSS における疑似要素（Pseudo-elements）です。

これまで、何か模様をつけたいときは HTML に `div` タグを追加していたかもしれません。
しかし、疑似要素を使えば、**HTML には何も書かずに、CSS だけで「仮想的な要素」を生み出して配置する** ことができます。

コードを汚さずにリッチな装飾を作る、実務で必須のテクニックです。

---

### はじめに：HTML に存在しない要素を作る

`::before` と `::after` はその名の通り、要素の「中身の前」と「中身の後」に、仮想的な要素を挿入する機能です。

- 見出しの横のアイコン
- おしゃれな下線
- 画像の上のフィルター
- 吹き出しの三角形

これらは実は HTML タグではなく、CSS で作られた「疑似要素」であることが多いのです。

---

### 🎯 本日の目標

1.  **`content` プロパティ**：これがないと何も始まらない、絶対ルールの理解。
2.  **`position` との合体技**：親要素を基準にして、自由自在に装飾を配置する。
3.  **HTML を汚さない美学**：装飾のためだけの無駄なタグを減らす。

---

### 📝 ミッション内容

以下の 2 つの UI コンポーネントを、HTML タグを増やさずに CSS だけで作ってください。

- **Mission 1: 「Ribbon Heading」**
  - 見出し文字の「上下」に、装飾的なボーダーラインを引く。
- **Mission 2: 「Custom List」**
  - `<ul>` `<li>` を使い、リストの先頭に「★」マークや「連番（01, 02...）」を疑似要素でつける。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="KwMVvbg" data-pen-title="CSSマスターへの道「疑似要素 (::before / ::after)」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/KwMVvbg">
  CSSマスターへの道「疑似要素 (::before / ::after)」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. `content: '';` は絶対必須

初心者が一番ハマる罠です。
疑似要素を使う時は、**必ず `content: '';`（または文字）を指定** しなければなりません。
たとえ中身が空っぽの線や図形を描きたい場合でも、これを書かないとブラウザは「存在しないもの」として無視して画面に表示してくれません。

#### 2. デフォルトは `inline` 要素

疑似要素はデフォルトで `span` タグのようなインライン要素です。
幅や高さ（width/height）を指定したい場合は、**`display: block;`** または `position: absolute;` を指定する必要があります。

#### 3. `attr()` 関数で HTML のデータを取得

CSS の中で HTML の属性値を使うテクニックです。

```html
<div data-label="New!" class="box">商品</div>
```

```css
.box::before {
  content: attr(data-label); /* "New!" と表示される */
  ...;
}
```

これを使うと、連番や補足情報を効率よく表示できます。

---

### 💡 応用：ホバーアニメーションの下線

リンクをホバーした時に、左から右へラインが伸びる動き。これも疑似要素で作ります。

```css
.link {
  text-decoration: none;
  color: #333;
  position: relative;
}

.link::after {
  content: "";
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0%; /* 最初は幅 0 */
  height: 2px;
  background: #333;
  transition: width 0.3s; /* 幅のアニメーション */
}

.link:hover::after {
  width: 100%; /* ホバーしたら幅 100% に */
}
```

---

### おわりに

HTML は「文書構造」、CSS は「見た目」。
疑似要素を使えば、この役割分担を守りつつ、デザイン性を高めることができます。
「ここにちょっと飾りが欲しいな」と思ったら、HTML をいじる前に「`::before` でいけるかも？」と考えてみてください。

次回は、写真を CSS だけで加工する **「画像加工 (object-fit / filter)」** です。Photoshop いらずの技術を身につけましょう。

https://qiita.com/saka2jp/items/020c06e566206834e64f
