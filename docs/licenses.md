# ⚖️ フォント・アイコンのライセンス

souan とアプリで使うフォント・アイコンは、どれも配布元のライセンスに従って使う。一覧と許諾文の控えは、リポジトリ直下の `THIRD_PARTY_LICENSES.md`。

> **ライセンスは配布元が変えることがある。最新の条件は、必ず配布元の公式のページで確かめること。**
> souan の文書や `THIRD_PARTY_LICENSES.md` に書いた内容は、書いた時点の控え。食い違うときは公式のページが正。

## 📌 使っている素材

| 素材 | 用途 | ライセンス | 公式のライセンス |
|---|---|---|---|
| Lucide | アイコン（画面のアイコンはこれだけ） | ISC。Feather 由来のアイコンは MIT | <https://lucide.dev/license> |
| Fraunces | ロゴの文字 | SIL Open Font License 1.1 | <https://github.com/undercasetype/Fraunces/blob/master/OFL.txt> |
| Noto Sans JP | 本文の文字（ヒラギノが無い環境） | SIL Open Font License 1.1 | <https://fonts.google.com/noto/specimen/Noto+Sans+JP/license> |
| ヒラギノ角ゴ・OS の等幅フォント | 本文・コードの文字 | OS の使用許諾 | — |

## 🧷 アイコン（Lucide）

- アプリでは npm の `lucide-react` を使う。パッケージに入っている `LICENSE` が、その版の正しい許諾文
- ビルドした画面を配る（公開する）アプリは、Lucide の著作権表示と許諾文を、第三者のライセンスの一覧（`THIRD_PARTY_LICENSES` など）に入れて添える。写すときは、使っている版のパッケージの `LICENSE` から写す
- SVG をファイルや HTML に直接書き写すとき（souan の `samples/*.html` など）は、同じファイルの中に許諾文を添える
- アイコンの形を変えて使うときも、Lucide のライセンスの条件はそのまま残る

## 🖋️ フォント

- 本文は OS のフォントを名前で指すだけにし、フォントのファイルを配らない（`docs/typography.md`）
- OS に付属のフォント（ヒラギノ・游明朝・SF など）のファイルを、アプリやリポジトリに入れて配らない。ロゴにも使わない
- ロゴの Fraunces は、npm の `@fontsource-variable/fraunces` で同梱する。同梱するアプリは、配布元の著作権表示と OFL の全文を添える。OFL で守ることは `docs/typography.md` の「OFL 1.1 で守ること」
- 文字を輪郭（パス）に変えたロゴの SVG や画像は、フォントの同梱にあたらないので、OFL の全文を添えなくてよい

## ➕ 新しい素材を足すとき

1. 配布元の公式のページで、ライセンスを確かめる。改変と再配布が認められたもの（ISC・MIT・Apache 2.0・OFL など）だけを使う。商用のフォントや、利用の条件がはっきりしないものは使わない
2. `THIRD_PARTY_LICENSES.md` の表に、素材・使っているところ・ライセンス・公式のライセンスのページを足す
3. 素材そのもの（SVG・フォントのファイル・画像など）をリポジトリに入れるときは、許諾文の控えも `THIRD_PARTY_LICENSES.md` に足し、ライセンスが求める場所（同じファイルの中など）にも添える
4. このページの「使っている素材」の表も同じに直す

## 🔄 ライセンスを見直すとき

- Lucide・Fraunces の版を上げたときや、配布元がライセンスを変えたと知ったときは、公式のページを見て `THIRD_PARTY_LICENSES.md` と `samples/*.html` の `@license:lucide` の間の許諾文を最新に直す
- souan 自身のライセンスは未定。決めるときは、第三者の素材がそれぞれのライセンスのまま残ることを README に書く
