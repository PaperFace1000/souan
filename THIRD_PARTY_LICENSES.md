# ⚖️ 第三者の素材とライセンス

souan で使っている、ほかの人が作ったフォント・アイコンと、そのライセンスの一覧です。

> **ライセンスは配布元が変えることがあります。最新の条件は、必ず下の表の「公式のライセンス」のページで確かめること。**
> このファイルに写した全文は、取り込んだ時点（2026-10-23）の控えです。食い違うときは公式のページが正です。

## 📋 一覧

| 素材 | 使っているところ | このリポジトリに含むもの | ライセンス | 公式のライセンス |
|---|---|---|---|---|
| [Lucide](https://lucide.dev/) | アイコン全般。`samples/*.html` の SVG、`tokens/icons.json` | アイコンの図形（SVG）。`tokens/icons.json` はアイコンの名前だけ | ISC。Feather 由来のアイコンは MIT | <https://lucide.dev/license>（全文: <https://github.com/lucide-icons/lucide/blob/main/LICENSE>） |
| [Fraunces](https://github.com/undercasetype/Fraunces) | ロゴの文字 | 含まない（`font-family` で名前を指すだけ） | SIL Open Font License 1.1 | <https://github.com/undercasetype/Fraunces/blob/master/OFL.txt> |
| Noto Sans JP | 本文の文字（ヒラギノが無い環境） | 含まない（名前を指すだけ） | SIL Open Font License 1.1 | <https://fonts.google.com/noto/specimen/Noto+Sans+JP/license> |
| ヒラギノ角ゴ | 本文の文字（Mac・iPhone） | 含まない（OS に付属のものを名前で指すだけ） | OS の使用許諾に従う。フォントのファイルを配らない | — |
| OS の等幅フォント（SF Mono・Menlo など） | コード・キー | 含まない（名前を指すだけ） | OS の使用許諾に従う。フォントのファイルを配らない | — |

- ロゴの図形（`samples/*.html` のヘッダーの重なった紙の絵）は souan で描いたもので、第三者の素材ではない
- 色の値・色の名前（和の伝統色の名前）・部品の寸法は souan で決めたもの
- 文書の中で名前を出しているライブラリ（React Aria Components・Shiki など）は、使い方を書いているだけで、コードは含まない。アプリで使うときは、それぞれのライセンスに従うこと

## 🧷 Lucide の許諾文（2026-10-23 時点の控え）

ISC の条件により、アイコンの図形を含むファイルには著作権表示と許諾文を添える。`samples/*.html` には、同じ文をページの中（`@license:lucide` の印の間）にも入れている。最新の文は <https://lucide.dev/license> を見ること。

```text
ISC License

Copyright (c) 2026 Lucide Icons and Contributors

Permission to use, copy, modify, and/or distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

---

The following Lucide icons are derived from the Feather project:

airplay, alert-circle, alert-octagon, alert-triangle, aperture, arrow-down-circle, arrow-down-left, arrow-down-right, arrow-down, arrow-left-circle, arrow-left, arrow-right-circle, arrow-right, arrow-up-circle, arrow-up-left, arrow-up-right, arrow-up, at-sign, calendar, cast, check, chevron-down, chevron-left, chevron-right, chevron-up, chevrons-down, chevrons-left, chevrons-right, chevrons-up, circle, clipboard, clock, code, columns, command, compass, corner-down-left, corner-down-right, corner-left-down, corner-left-up, corner-right-down, corner-right-up, corner-up-left, corner-up-right, crosshair, database, divide-circle, divide-square, dollar-sign, download, external-link, feather, frown, hash, headphones, help-circle, info, italic, key, layout, life-buoy, link-2, link, loader, lock, log-in, log-out, maximize, meh, minimize, minimize-2, minus-circle, minus-square, minus, monitor, moon, more-horizontal, more-vertical, move, music, navigation-2, navigation, octagon, pause-circle, percent, plus-circle, plus-square, plus, power, radio, rss, search, server, share, shopping-bag, sidebar, smartphone, smile, square, table-2, tablet, target, terminal, trash-2, trash, triangle, tv, type, upload, x-circle, x-octagon, x-square, x, zoom-in, zoom-out

The MIT License (MIT) (for the icons listed above)

Copyright (c) 2013-present Cole Bemis

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## 🖋️ Fraunces（OFL 1.1）について

- souan はフォントのファイルを含まないので、このリポジトリには OFL の全文を写していない
- アプリに同梱するときは、配布元の著作権表示と OFL の全文を、その時点の最新のものから写して添えること（守ることは `docs/typography.md` の「OFL 1.1 で守ること」と `docs/licenses.md`）
- 著作権表示（2026-10-23 時点）: `Copyright 2018 The Fraunces Project Authors (https://github.com/undercasetype/Fraunces)`
