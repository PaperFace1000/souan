# 📜 souan（草案）

紙のような落ち着いた配色と、同じ作りの部品を、複数のアプリでそろえるための**デザインシステム**です。

ここには、デザインの原則、色などの値（デザイントークン）、部品と画面の組み立ての決まり、ブラウザで開ける見本を置きます。部品のコードはパッケージとして配らず、各アプリがこの決まりと見本に合わせて作ります。

名前は「草案」から。決まりは使いながら書き直していく下書きであり、各アプリで見つけた良いやり方をここへ戻して育てます。

## 🗂️ 構成

```
README.md            このファイル
index.html           公開したページのトップ。見本の目次（samples/）へ移る
THIRD_PARTY_LICENSES.md  第三者の素材（フォント・アイコン）とライセンスの一覧
docs/
  principles.md      デザインの原則
  color.md           配色（7 テーマ、役割の色、コントラスト、その他の配色 30 色）
  typography.md      フォント、文字の大きさ・行間、日時の表記
  components.md      部品の決まり（ボタン、フォーム、入力欄、チェックボックス・ラジオボタン、セレクト、タグ、ダイアログ、トースト、アイコン、欄、一覧の行、バッジ、空の表示）
  patterns.md        画面の組み立て（タブ、サイドバー、ツリー、目次、検索、カード、ログイン）と中身の見せ方（表、本文、コード、差分、並べ替え）
  layout.md          ヘッダー、列の組み方、スマホ幅、余白の段階
  logo.md            ロゴの色・ファビコンの決まり
  accessibility.md   コントラスト、キーボード操作、aria、フォーカス
  coding.md          実装の決まり（CSS の書き方、lint、テーマの適用、localStorage）
  licenses.md        フォント・アイコンのライセンスで守ること
tokens/
  palette.json       7 テーマの色の値（正本）
  themes.css         そのまま読み込める CSS 変数
  extra-colors.json  その他の配色 30 色（分類やタグを色で見分ける）
  extra-colors.css   data-extra-color 属性で色を出す CSS
  icons.json         バッジに選べる Lucide のアイコン 86 個
samples/             ブラウザで直接開ける見本（単一の HTML、外部の読み込みなし）
  index.html         目次
  palette.html       7 テーマの色とコントラスト比
  extra-colors.html  30 色の見本（ライトと夜）
  ui-kit.html        部品の見本
  patterns.html      画面の組み立てと中身の見せ方の見本
  layout.html        ダッシュボード風の 2 列と、360px の見え方
```

## 🚀 使い方

### 🎨 色を取り込む

1. `tokens/themes.css` をアプリの `styles/themes.css` に写し、入口（`main.tsx` など）で最初に読み込む
2. 画面の CSS では `var(--color-text)` のように変数だけを使い、色を直接書かない
3. テーマの切り替えは `<html data-theme="hakushi">` のように `data-theme` を付け替える。付けなければ OS のライト・ダークに合わせる（詳しくは `docs/color.md`）
4. 分類やタグに色を付けるアプリは `tokens/extra-colors.css` も読み込み、要素に `data-extra-color="deep-002"` を付けて `var(--extra-bg)` などで塗る

色の値を変えるときは、このリポジトリの `tokens/palette.json` を先に直し、`themes.css`・`extra-colors.css`・`samples/*.html` のインラインの値を同じにしてから、各アプリへ写すこと。アプリの側だけで色を足したり変えたりしない。

### 🧩 部品と決まりを取り込む

- 新しいアプリを作るときは `docs/components.md` と `docs/coding.md` の部品（Button・Form と SubmitButton・TextField・ModalDialog・Icon）を同じ形で作る
- 見た目に迷ったら `samples/ui-kit.html` を開いて、そこに合わせる
- アプリで良い作りを見つけたら、ここの文書と見本に書き戻し、ほかのアプリにも広げる

### 👀 見本を見る

`samples/index.html` をブラウザで開く。サーバーは要らない。ページの上のボタンで 7 テーマを切り替えられる。

## 🙅 プルリクエストと Issue

このリポジトリは個人で使うために公開しています。プルリクエストと Issue は受け付けていません。

## ⚖️ ライセンス

- souan 自身のライセンスは未定
- フォント・アイコンなど第三者の素材は、それぞれのライセンスに従う。一覧と許諾文は `THIRD_PARTY_LICENSES.md`、守ることは `docs/licenses.md`
- **ライセンスは配布元が変えることがある。最新の条件は、必ず配布元の公式のページで確かめること**（Lucide: <https://lucide.dev/license>、Fraunces: <https://github.com/undercasetype/Fraunces/blob/master/OFL.txt>）

## 📅 取り込んだ時点

各アプリの値は 2026-10-23 に取り込んだ。アプリごとに違っていた点と、どれを正にしたかは `docs/color.md` と `docs/components.md` の「決めたこと」の節に書いている。
