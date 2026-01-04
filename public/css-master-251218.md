---
title: CSSマスターへの道「変数 (Custom Properties)」
tags:
  - CSS
private: false
updated_at: '2026-01-05T00:16:33+09:00'
id: b644159ad0530fd9374a
organization_url_name: null
slide: false
ignorePublish: false
---

18 日目、お疲れ様です！
Phase 3 も後半戦。今日は CSS の書き方を根本から変える革命的な機能、「CSS変数」です。

これまで、色は `#007bff` のように直接コードに書いてきましたよね？
でも、もしクライアントから「テーマカラーを青から緑に変えて！」と言われたらどうしますか？
何十箇所も検索して置換して…というのはミスの元ですし、何より面倒です。

CSS 変数を使えば、**たった 1 箇所の値を書き換えるだけで、サイト全体の色やサイズを一瞬で変更**できるようになります。

---

### はじめに：もう「置換」作業はいらない

CSS 変数（カスタムプロパティ）とは、 **「値（色や大きさ）」に「名前」をつけて保存しておく機能**です。

- `#007bff` → `--main-color`
- `16px` → `--base-spacing`

このように名前をつけておけば、後から値を変えるだけで、それを参照している全ての場所に変更が適用されます。
「ダークモード」の実装も、この機能を使えば驚くほど簡単です。

---

### 🎯 本日の目標

1.  **定義と使用**: `:root` を使ってグローバル変数を定義し、`var()` 関数で呼び出す。
2.  **メンテナンス性**: 色コードを直接書かず、意味のある名前（`--primary-color`など）で管理する。
3.  **ダークモード**: CSS 変数の値を上書きするだけで、サイトの配色をガラリと変える。

---

### 📝 ミッション内容

以下の要件を満たす「テーマ切り替え可能なカードコンポーネント」を作ってください。

- **Mission 1: 変数の定義**
  - メインカラー、背景色、文字色を CSS 変数として定義する。
- **Mission 2: 変数の使用と計算**
  - 定義した変数を使い、`calc()` 関数で「余白の倍率（例: 基準の 2 倍）」を計算してレイアウトする。
- **Mission 3: ダークモード対応**
  - メディアクエリ `@media (prefers-color-scheme: dark)` を使い、OS がダークモードの時は変数の色を自動で切り替える。

---

### 💻 実装サンプル

<details><summary>正解例</summary>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="Byzjwxp" data-pen-title="CSSマスターへの道「変数 (Custom Properties)」" data-user="saka2jp" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
      <span>See the Pen <a href="https://codepen.io/saka2jp/pen/Byzjwxp">
  CSSマスターへの道「変数 (Custom Properties)」</a> by サカツ (<a href="https://codepen.io/saka2jp">@saka2jp</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
      </p>
      <script async src="https://public.codepenassets.com/embed/index.js"></script>

</details>

---

### 🧠 解説と重要ポイント

#### 1. 構文のルール

- **定義:** プロパティ名の先頭にハイフン 2 つ `2` をつけます。
  - OK: `--main-color: red;`
  - NG: `main-color: red;`
- **使用:** `var()` 関数で呼び出します。
  - `color: var(--main-color);`
- **第 2 引数（フォールバック）:** 変数が未定義だった場合の予備値を指定できます。
  - `color: var(--unknown-color, blue);` → 変数がなければ青になる。

#### 2. スコープ（有効範囲）

`:root` で定義するのが一般的ですが、特定のクラス内だけで変数を定義・上書きすることもできます。

```css
/* アラート用の変数を定義 */
.alert-box {
  --alert-color: red;
  color: var(--alert-color);
  border: 1px solid var(--alert-color);
}
/* 青色のアラートを作りたい時、変数だけ上書きできる */
.alert-blue {
  --alert-color: blue;
}
```

#### 3. JavaScript との連携

JS から CSS 変数を操作するのは非常に簡単です。これを使えば「カラーピッカーでサイトの色を自由に変える機能」などが作れます。

```javascript
// --primary-color を赤に変更する
document.documentElement.style.setProperty("--primary-color", "red");
```

---

### 💡 応用：`calc()` との最強コンボ

変数の真骨頂は、数値計算です。
例えば、「基準サイズ」を 1 つ決めておき、他はすべて計算で出すようにすると、基準を変えるだけで全てのサイズバランスを保ったまま拡大縮小できます。

```css
:root {
  --base-size: 16px;
}

.container {
  font-size: var(--base-size); /* 16px */
  padding: calc(var(--base-size) * 1.5); /* 24px */
  margin-bottom: calc(var(--base-size) / 2); /* 8px */
}
```

---

### おわりに

CSS 変数を覚えると、コードを書く時に「具体的な色コード」を意識する必要がなくなります。
「ここはプライマリーカラー」「ここは背景色」というふうに、 **「役割」で指定できる** ようになるため、デザインの一貫性が保たれやすくなります。

明日の Day 19 は、JavaScript を使わずにリッチなスライダーを作る 「**スクロールスナップ**」 です。
CSS だけで、スマホアプリのような「ピタッ」と止まるスクロール体験を作りましょう！
