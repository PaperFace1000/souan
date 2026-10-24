# 📐 レイアウト

見本は `samples/layout.html`。

## 🧢 ヘッダー

- 画面の上に固定（`position: sticky; top: 0`）。高さ 56px、余白 0 12px、背景 `surface`、下に `border` の線
- 左にロゴ（トップへのリンク、18px）、続けて主なページのリンク、右端（`margin-left: auto`）に操作（テーマ・ユーザーのメニューなど）
- リンクとボタンは高さ 40px 以上、余白 6px 10px、角 8px、14px の文字。なぞると背景を `base` に
- 今いるページのリンクは文字を `text`・太さ 600、ほかは `muted`
- **599px 以下ではアイコンだけにする**: 文言を隠し（`display: none`）、ボタンの幅を 36px に詰め、間を 0〜4px に。360px の幅に収める。文言を隠したボタンにも読み上げ用の名前を残す（`aria-label`）

## 🧱 本文の枠

- 本文は最大 76rem（1216px）で中央。余白 28px 32px 80px（下を広く取り、最後の行がボタンなどに隠れないように）
- **899px 以下**では余白を 20px 16px 64px に詰める
- サイドバーのあるアプリは、左に 280px（200〜560px でつまみで変えられる）のサイドバー、右に本文。899px 以下ではサイドバーを左から出る引き出し（幅 `min(320px, 85vw)`）にし、後ろに幕を出す
- 一覧をたくさん並べる画面だけ、最大の幅を外してよい（下の「横幅いっぱいの画面」）

## 🗂️ 2 列 → 1 列

ダッシュボードのように欄を並べる画面:

```css
.columns {
  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
  gap: 16px;
  align-items: start;
}
.column { display: grid; gap: 16px; min-width: 0; }

@media (max-width: 899px) {
  .columns { grid-template-columns: minmax(0, 1fr); }
}
```

- 列は `minmax(0, 1fr)` にする（`1fr` だけだと中身の最小幅まで広がり、狭い画面で横にはみ出す）。グリッドの子にも `min-width: 0`
- 左右の列は高さをそろえない（`align-items: start`）。それぞれ上から詰める
- 1 列にしたときの順番は、左の列 → 右の列。大事な欄を左の上に置く

## ↔️ 横幅いっぱいの画面

一覧をたくさん並べる画面（項目の一覧と、その横の要約など）だけ、本文の幅の上限（76rem）を外す。読む画面・入力の画面には使わない（行が長くなりすぎるため）。

| 項目 | 値 |
|---|---|
| 幅 | 上限なし（`max-width: none`） |
| 余白 | 上下 24px・40px、左右 24px。899px 以下は 20px 16px 32px |
| 列の比 | 項目の多い側を広く、3 : 2（`minmax(0, 3fr) minmax(0, 2fr)`） |

**1 列のときに右の列の部品を先頭に出す**

899px 以下で 1 列にするとき、右の列の先頭の部品（今日の要約など）を全体の先頭に出せる。列の枠を `display: contents` で外し、部品を 1 本に並べて `order` で並べ替える。

```css
@media (max-width: 899px) {
  .columns--wide { display: flex; flex-direction: column; align-items: stretch; }
  .columns--wide > .column { display: contents; }
  .columns--wide .column__lead { order: -1; }
}
```

- **`align-items: stretch` を忘れない**。2 列のときの `align-items: start` が残ると、縦の flex では部品が中身の幅に縮む
- 列の間（16px）は flex の `gap` で取る（列の枠が無くなるため、列の中の `gap` は効かなくなる）
- 先頭に出すのは 1 つだけにする。読み上げとキーボードの順は HTML の順のままなので、出す部品は「先に読まれても困らないもの」（要約など）に限る

## 📦 置かれた枠の幅で形を変える部品

同じ部品を広い列にも狭い列にも置くとき、画面の幅ではなく、部品の枠の幅で形を変える。

```css
.fit-card { container-type: inline-size; container-name: fit-card; }
.fit-card__body { display: grid; grid-template-columns: minmax(0, 1fr) minmax(9rem, 14rem) auto; gap: 8px 16px; }
@container fit-card (max-width: 479px) {
  .fit-card__body { grid-template-columns: minmax(0, 1fr) auto; }
  .fit-card__main { grid-column: 1 / -1; }
}
```

- 部品の外側の要素を入れ物（`container-type: inline-size`）にし、中身を `@container` で崩す。入れ物と中身を同じ要素にはできない
- 入れ物は幅を外から決めてもらう要素にする。中身の幅で広がる場所（横並びの flex の子で `flex: none` など）に置くと幅が 0 になる
- 名前（`container-name`）は部品ごとに付け、ほかの入れ物の幅で崩れないようにする
- **見本の `@container app` との違い**: `samples/*.html` の `.app` は、画面の幅の代わりに見本の枠の幅で崩すための入れ物で、アプリでは `@media` に書き直す。部品ごとの入れ物はアプリでもそのまま `@container` で書く
- 見本は `samples/layout.html` の「置かれた枠の幅で形を変える部品」。広い列では 1 段、狭い列とスマホの幅では 2 段（1 段目に名前、2 段目に進み具合とボタン）になる

## 📱 スマホ（360px）

- **360px の幅で横スクロールが出ない**こと。すべての画面で確かめ、E2E もスマホの画面サイズで実行する
- 一覧の行は 599px 以下でカードに崩す（`docs/components.md`）
- ダイアログは `min(440px, calc(100vw - 32px))` で画面の左右に 16px を残す
- 押せるものは 32px 四方以上（主な操作は 40px）
- 長い名前は省略し、URL などは `overflow-wrap: anywhere`

## 📏 余白の段階

使う値をこの中から選ぶ。中途半端な値（5px、7px、15px など）を足さない（印の 7px のような部品の大きさは別）。

| 値 | 主な使いどころ |
|---|---|
| 2px | 2 段の行の上下の間、ヘッダーのリンクの間 |
| 4px | 一覧の行の間、ラベルと入力欄の間、メニューの余白 |
| 6px | アイコンと文字の間（ボタン）、行の上下の余白 |
| 8px | 欄の中の間、ボタンの並び、入力欄の余白 |
| 10px | 行の左右の余白、メニューの項目の余白 |
| 12px | ヘッダーの左右の余白、帯の左右 |
| 16px | 欄どうしの間、列の間、ボタンの左右の余白、スマホの本文の左右 |
| 20px | ダイアログの左右、スマホの本文の上 |
| 24px | ページの中の大きな区切り |
| 28px / 32px | PC の本文の上・左右 |

## 🟫 角の丸み

| 値 | 使いどころ |
|---|---|
| 6px | 色のバッジ、メニューの項目、行の中の小さなボタン |
| 8px | ボタン、入力欄、帯 |
| 10px | 一覧の行、メニュー、お知らせの帯 |
| 12px | 欄 |
| 14px | ダイアログ |
| 999px | 状態のバッジ、件数、タグ |

## 🌫️ 影と重なり

| もの | 影 | `z-index` |
|---|---|---|
| ヘッダー | なし | 20 |
| 引き出し（サイドバー） | `4px 0 16px rgb(0 0 0 / 0.12)` | 15 |
| メニュー | `0 6px 20px rgb(0 0 0 / 0.15)` | （React Aria の重なり） |
| ダイアログ | `0 10px 40px rgb(0 0 0 / 0.25)` | 40 |
