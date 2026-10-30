# 🛠️ 実装の決まり

各アプリは React + TypeScript + Vite、CSS Modules + CSS 変数、React Aria Components、Lucide で作っている。新しいアプリも同じ組み合わせにする。

## 🎨 CSS

- **CSS Modules + CSS 変数**。部品ごとに `Button.module.css` のようなファイルを置き、色は `var(--color-*)` だけを使う。色の値（`#fff` や `rgb()`）を直接書かない（例外は影と幕の黒の透明度だけ）
- テーマの色は `tokens/themes.css` から写した `styles/themes.css`、全体の土台は `styles/base.css`。入口でこの順に読み込む
- カスタムの CSS は最小限にする。同じ見た目は共通の部品（Button・TextField・ModalDialog など）を使い、画面ごとに作り直さない
- CSS のフレームワーク（Bootstrap・Tailwind など）は使わない。独自の配色と部品の見本があるため
- 大きさ・余白・角の値は `docs/layout.md` の段階から選ぶ
- スクロールバーは `base.css` でテーマの色にそろえる。部品ごとに上書きしない
- 外部の CDN・Web フォントを読み込まない。フォントは npm から同梱する

### 🧱 base.css

```css
*, *::before, *::after { box-sizing: border-box; }
html { -webkit-text-size-adjust: 100%; }
body {
  margin: 0;
  background: var(--color-base);
  color: var(--color-text);
  font-family: "Hiragino Sans", "Noto Sans JP", sans-serif;
  font-size: 15px;
  line-height: 1.7;
}
:focus-visible { outline: 2px solid var(--color-accent); outline-offset: 2px; }
a { color: var(--color-accent-strong); }

/* スクロールバーをテーマの色に。細くし、つまみは薄い文字の色を透かしたもの */
:root { --scrollbar-thumb: color-mix(in srgb, var(--color-muted) 45%, transparent); }
* { scrollbar-width: thin; scrollbar-color: var(--scrollbar-thumb) transparent; }
::-webkit-scrollbar { width: 10px; height: 10px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb {
  background: var(--scrollbar-thumb);
  border: 2px solid transparent;
  border-radius: 999px;
  background-clip: padding-box;
}
::-webkit-scrollbar-thumb:hover { background: var(--color-muted); background-clip: padding-box; }
::-webkit-scrollbar-corner { background: transparent; }
```

## 🚫 lint で禁止すること

`eslint.config.js` の画面（`apps/web/src/**/*.tsx`）向けの設定に入れる。

| 禁止するもの | 代わり | 理由 |
|---|---|---|
| `<form>` の直接の使用 | `components/Form.tsx` の `Form` | 二重送信を防ぐ |
| `type="submit"` | `SubmitButton` | 二重送信を防ぐ |
| `react-aria-components` の `Form` | `components/Form.tsx` の `Form` | 二重送信を防ぐ |
| `dangerouslySetInnerHTML` | React の要素で組み立てる | XSS を防ぐ |
| `toLocaleString` など、`Intl.DateTimeFormat` | `lib/dateTime.ts` の `formatDateTime` | 日時の表記をそろえる |
| JSX の文字列の中の絵文字 | `Icon`（Lucide） | 見た目をそろえる |

```js
{
  files: ["apps/web/src/**/*.tsx"],
  ignores: ["apps/web/src/components/Form.tsx"],
  rules: {
    "no-restricted-syntax": ["error",
      { selector: "JSXOpeningElement[name.name='form']",
        message: "<form> を直接書かず、components/Form.tsx の Form を使うこと（二重送信を防ぐため）" },
      { selector: "JSXAttribute[name.name='type'][value.value='submit']",
        message: "送信ボタンは components/Form.tsx の SubmitButton を使うこと（二重送信を防ぐため）" },
      { selector: "JSXAttribute[name.name='dangerouslySetInnerHTML']",
        message: "dangerouslySetInnerHTML を使わず、React の要素で組み立てること（XSS を防ぐため）" },
    ],
    "no-restricted-imports": ["error", { paths: [
      { name: "react-aria-components", importNames: ["Form"],
        message: "components/Form.tsx の Form を使うこと（二重送信を防ぐため）" },
    ] }],
  },
}
```

- **絵文字**: 画面に絵文字を出さない（アイコンは Lucide だけ）。JSX の文字列に `\p{Extended_Pictographic}` が入ったら止める。例外は利用者が書いた本文や Markdown の中身（データとして描くものなので lint の対象外）

```js
// no-restricted-syntax に足す。入れたら、絵文字を書いた行で lint が落ちることを一度確かめること
...["JSXText", "JSXAttribute > Literal", "JSXExpressionContainer > Literal", "JSXExpressionContainer > TemplateLiteral > TemplateElement"].map((node) => ({
  selector: `${node}[value${node.endsWith("TemplateElement") ? ".raw" : ""}=/\\p{Extended_Pictographic}/u]`,
  message: "画面に絵文字を使わないこと。アイコンは components/Icon.tsx（Lucide）を使う",
})),
```

- `toLocaleString` などは `no-restricted-properties` で止める（`apps/web/**/*.{ts,tsx}` すべて）
- `dangerouslySetInnerHTML` がどうしても要るとき（サーバーで許可リストを通して消毒した Markdown の HTML を出すなど）は、**それ専用の部品 1 つに閉じる**。その部品だけ `eslint-disable-next-line` に理由を書いて許し、受け取る HTML がどこから来たものか（消毒済みのものだけ）をコメントに書く。ほかの場所では使わない
- 比較は `===`、`var` は使わない（`eqeqeq`・`no-var`）

## 🌗 テーマの適用

```ts
// main.tsx の先頭、画面を描く前に
import "./styles/themes.css";
import "./styles/base.css";
import { applyTheme, loadTheme } from "./features/theme/theme.ts";

// 画面を描く前にテーマを反映して、色がちらつかないようにする
applyTheme(loadTheme());
```

- `features/theme/theme.ts` にテーマの一覧（キーと名前）、`loadTheme`・`saveTheme`・`applyTheme` を置く。キーは `data-theme` の値と一致させる
- 選んだテーマは `localStorage` に `<アプリ名>.theme` の鍵で保存する。`system` を選んだら `data-theme` を外す
- **描画の前に適用する**。React の中（`useEffect`）で適用すると、最初の 1 枚が既定の色で出てちらつく
- テーマで描き分けるもの（図・その他の配色）は、`data-theme` の変化と OS の `prefers-color-scheme` の変化の両方を見張る（`MutationObserver` + `matchMedia`、`useSyncExternalStore`）

## 💾 localStorage

- 読み書きは必ず `try` / `catch` で囲む。プライベートモードや容量の上限で投げることがある
- 読めないとき・決めた値でないときは既定値にする。書けないときも今の画面には反映し、そのタブの中だけで値を覚えておく
- 表示の好み（テーマ・サイドバーの幅・幅の切り替え）だけに使う。消えて困るデータは置かない
- 複数の部品で共有する設定は、`createStoredPreference(key, values, fallback)` のような共通の関数にし、`storage` の通知でほかのタブの変更にも追従させる

```ts
export function loadTheme(): ThemeChoice {
  try {
    const value = localStorage.getItem(STORAGE_KEY);
    return isThemeChoice(value) ? value : "system";
  } catch {
    return "system";
  }
}

export function saveTheme(choice: ThemeChoice): void {
  try {
    localStorage.setItem(STORAGE_KEY, choice);
  } catch {
    // 保存できなくても、今の画面には反映されるので続ける
  }
}
```

## ✅ 確かめ方

- 画面を変えたら 14 テーマのうち少なくとも白紙・古紙・夜更かし・墨・漆の 5 つで見る（明るさの両端と夜、コントラストの強いライトとダーク）
- 360px の幅で横スクロールが出ないことを確かめる。E2E もスマホの画面サイズで実行する
- 送信する操作を足したら、E2E に「連打しても 1 件しか作られない」確認を入れる
- 見た目の確認はヘッドレスのブラウザで撮った画像で行う
