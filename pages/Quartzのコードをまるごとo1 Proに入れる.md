---
title: "Quartzのコードをまるごとo1 Proに入れる"
---

[[プロジェクトのソースコードをまとめてクリップボードに入れるツール]]作ったので試す

<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>
このコードは、静的サイト生成フレームワークである Quartz 用の各種コンポーネント、リソース変換関数、およびページエミッタ（404ページ、コンテンツページ、フォルダページ、タグページなど）を定義している。
`util/` ディレクトリの `resources.tsx` では、JS・CSSリソースを `<script>` や `<link>` に変換する関数や、`StaticResources` 型が定義されている。
`util/jsx.tsx` は hast 形式の HTML AST を Preact の JSX へ変換し、カスタムコンポーネント (e.g. `<table>`) を指定できる。
`util/og.tsx` は Satori を使った Open Graph 用画像生成関連の処理、`util/resources.tsx` はスクリプトやスタイルリソースの要素化関数、`plugins/emitters` ディレクトリは404ページやフォルダ一覧、タグページ一覧などを出力するロジックを提供し、`components/` 配下はタイトル、目次、タグリスト、検索、コメント欄などのUIコンポーネント群を定義。
全体として、Quartzを用いてマークダウンコンテンツを HTML 化、スタイル付与、ナビゲーションやメタ情報付加、OG画像生成などを行うためのモジュール群がまとめられている。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>逆リンクなどの処理をしている部分はどこ？

<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>逆リンク（backlinks）の処理は `components/Backlinks.tsx` に実装されている。
このコンポーネント内で、`allFiles` を走査して現在のページ(`slug`)にリンクするファイルを抽出し、その一覧を表示している。具体的には `backlinkFiles = allFiles.filter((file) => file.links?.includes(slug))` のようなコードで逆リンク先を取得している。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>グローバルなデータ構造を作らずに各ページごとに全部のページを読んでるの？

<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>`allFiles` はビルドプロセス中に一括で読み込まれ、処理された全ページのデータをまとめて保持した配列やオブジェクトとなっている（ビルドパイプラインで生成）。各ページレンダリング時には、この `allFiles` がコンポーネントのプロパティとして渡される。そのため、個別ページが独自に他のページを再読み込みするわけではなく、ビルド段階でグローバルにまとめられたデータ構造 `allFiles` に対して各ページがフィルタや検索をかけているだけである。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>メモリには置いてるとしてもO(N^2)だよね？

<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>確かに、この実装上、allFiles を各ページごとのレンダリング時に走査している処理（例えば逆リンク抽出）があるため、ページ数を N とすると、最悪 O(N^2) の計算量を要することになる。
ビルド時点で全ページ分の allFiles データ構造をメモリ上に用意し、ページごとの処理時にはその allFiles を都度フィルタリングするため、そのままではスケールが大きくなると非効率になる可能性がある。
