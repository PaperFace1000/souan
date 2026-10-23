# 📜 souan（草案）

紙のような落ち着いた配色と、同じ作りの部品を持つ個人アプリのための、**配色と UI のお手本**です。
色の値（トークン）、見本の HTML、決まりごとの文書をここで管理し、各アプリはここから値と決まりを取り込みます。

名前は「草案」から。決まりは使いながら書き直していく下書きであり、各アプリで見つけた良いやり方をここへ戻して育てます。

## 🗂️ 構成

```
README.md            このファイル
docs/
  principles.md      デザインの原則
  color.md           配色（7 テーマ、役割の色、コントラスト、プロジェクトの色 30 色）
  typography.md      フォント、文字の大きさ・行間、日時の表記
  components.md      部品の決まり（ボタン、フォーム、入力欄、ダイアログ、アイコン、欄、一覧の行、バッジ）
  layout.md          ヘッダー、列の組み方、スマホ幅、余白の段階
  logo.md            ロゴの色・ファビコンの決まり
  accessibility.md   コントラスト、キーボード操作、aria、フォーカス
  coding.md          実装の決まり（CSS の書き方、lint、テーマの適用、localStorage）
tokens/
  palette.json       7 テーマの色の値（正本）
  themes.css         そのまま読み込める CSS 変数
  project-colors.json  プロジェクト（分類）の色 30 色
  project-colors.css   data-project-color 属性で色を出す CSS
  project-icons.json   プロジェクトに選べる Lucide のアイコン 86 個
samples/             ブラウザで直接開ける見本（単一の HTML、外部の読み込みなし）
  index.html         目次
  palette.html       7 テーマの色とコントラスト比
  project-colors.html  30 色の見本（ライトと夜）
  ui-kit.html        部品の見本
  layout.html        ダッシュボード風の 2 列と、360px の見え方
```

## 🚀 使い方

### 🎨 色を取り込む

1. `tokens/themes.css` をアプリの `styles/themes.css` に写し、入口（`main.tsx` など）で最初に読み込む
2. 画面の CSS では `var(--color-text)` のように変数だけを使い、色を直接書かない
3. テーマの切り替えは `<html data-theme="hakushi">` のように `data-theme` を付け替える。付けなければ OS のライト・ダークに合わせる（詳しくは `docs/color.md`）
4. プロジェクトや分類に色を付けるアプリは `tokens/project-colors.css` も読み込み、要素に `data-project-color="deep-002"` を付けて `var(--project-bg)` などで塗る

色の値を変えるときは、このリポジトリの `tokens/palette.json` を先に直し、`themes.css`・`project-colors.css`・`samples/*.html` のインラインの値を同じにしてから、各アプリへ写すこと。アプリの側だけで色を足したり変えたりしない。

### 🧩 部品と決まりを取り込む

- 新しいアプリを作るときは `docs/components.md` と `docs/coding.md` の部品（Button・Form と SubmitButton・TextField・ModalDialog・Icon）を同じ形で作る
- 見た目に迷ったら `samples/ui-kit.html` を開いて、そこに合わせる
- アプリで良い作りを見つけたら、ここの文書と見本に書き戻し、ほかのアプリにも広げる

### 👀 見本を見る

`samples/index.html` をブラウザで開く。サーバーは要らない。ページの上のボタンで 7 テーマを切り替えられる。

## 📅 取り込んだ時点

各アプリの値は 2026-10-23 に取り込んだ。アプリごとに違っていた点と、どれを正にしたかは `docs/color.md` と `docs/components.md` の「決めたこと」の節に書いている。
