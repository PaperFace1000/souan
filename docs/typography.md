# 🔤 文字

## 🖋️ フォント

### 📖 本文

```css
font-family: "Hiragino Sans", "Noto Sans JP", sans-serif;
```

- Mac・iPhone はヒラギノ角ゴ、それ以外は Noto Sans JP、無ければ OS のゴシック体
- Web フォントを読み込まない（外部の CDN に頼らない。表示が速く、通信のない環境でも同じに見える）
- 等幅が要るところ（コード・キー）は OS の等幅フォント（`ui-monospace, "SF Mono", Menlo, monospace`）

### 🏷️ ロゴ

- ロゴの文字（アプリの名前）は **Fraunces**（SIL Open Font License 1.1）。太さ 500・やわらかさ（`"SOFT" 50`）・字間 `0.02em`
- アイコンと文字を横に並べ、アイコンの高さは文字の 1.3 倍、間は `0.3em`
- フォントは npm の `@fontsource-variable/fraunces` をアプリに同梱して配る（CDN から読まない）
- 見本の HTML では同梱しないので、Fraunces が無ければ OS のセリフ体で代わりに出る（`"Fraunces", Georgia, serif`）
- ロゴには OFL などロゴへの利用が認められたフォントだけを使う。OS 付属のフォント（ヒラギノ・游明朝など）はロゴに使わない
- 正式なロゴの SVG は、文字を輪郭（パス）に変換してフォントを含めない

### ⚖️ OFL 1.1 で守ること

- フォントのファイルを単体で販売しない（アプリに同梱して配るのはよい）
- フォントを改変したときも OFL のまま配る
- 同梱するときは著作権表示と OFL の全文を添える（`THIRD_PARTY_LICENSES` などに載せる）
- 作者の名前を許可なく宣伝に使わない
- 輪郭に変換したロゴの SVG や画像には、これらの義務はかからない

## 📐 大きさと行間

| 用途 | 大きさ | 太さ・ほか |
|---|---|---|
| 本文 | 15px | 行間 1.7（`body` に指定） |
| ヘッダーのロゴ | 18px | |
| 一覧の見出し（ページ内） | 18px | |
| ダイアログの見出し | 17px | 先頭にアイコン |
| 欄の見出し | 16px | |
| ボタン・メニュー・一覧の行・帯 | 14px | 小さいボタンは 13px |
| 入力欄のラベル・小見出し・帯（欄の中） | 13px | |
| 補足・日時・エラー・バッジ・件数 | 12px | 件数は太さ 600 |
| 行の中の小さなタグ | 11px | |
| 合計など目立たせる数字 | 22px | 太さ 600 |

- 見出しの太さはブラウザの既定（太字）。本文の中で太字を多用しない
- 時刻・長さ・件数など、数字が並ぶところは `font-variant-numeric: tabular-nums`
- ボタンの文言は折り返さない（`white-space: nowrap`）。長い名前や題名は 1 行で省略（`text-overflow: ellipsis`）し、`title` に全文を入れる
- URL や長い英数字が入る説明は `overflow-wrap: anywhere` で枠からはみ出さないようにする

## 🕰️ 日時の表記

画面に出す日時はすべて次の形にそろえる（24 時間表記、端末の時刻）。

| 形 | 例 | 関数（`lib/dateTime.ts`） |
|---|---|---|
| 日時 | `2026-10-01 15:23` | `formatDateTime` |
| 秒まで | `2026-10-01 15:23:08` | `formatDateTime(value, { seconds: true })` |
| 日付 | `2026-10-01` | `formatDate` |
| 時刻 | `15:23` | `formatTime` |
| 長さ | `1:05:09`（`H:MM:SS`） | `formatDuration` |
| 長さの差 | `+0:30` / `-1:15` / `±0:00` | `formatSignedDuration` |

- `toLocaleString`・`toLocaleDateString`・`toLocaleTimeString`・`Intl.DateTimeFormat` は使わない。端末の言語設定で表記が変わるため。lint の `no-restricted-properties` で禁止する（`docs/coding.md`）
- 「3 分前に更新」のような相対の表記は、更新の新しさを伝える場所（欄の右上）だけに使う
- 曜日や「今日」「昨日」を添えるときも、日付の部分は `yyyy-MM-dd` のまま
