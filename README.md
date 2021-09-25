# d3-ai.github.io
D3-AIプロジェクトのWebサイトの管理用リポジトリ

## 利用環境

- [GitHub Pages](https://docs.github.com/ja/pages/getting-started-with-github-pages/about-github-pages)
- [Hugo](https://gohugo.io/)
- Huge theme: [Northendlab Light](https://github.com/gethugothemes/northendlab-light)
  - [forkしてチューニングしたもの](https://github.com/takasehideki/northendlab-light)を利用している（予定）

## Webサイト管理方法の雑な説明

### 準備

```bash
$ brew install hugo
$ git clone --recursive https://github.com/d3-ai/d3-ai.github.io.git
```

### ローカルでのプレビュー

```bash
$ hugo server
```

http://localhost:1313 にアクセスする．

`-D` オプションを付けるとドラフト記事も処理される．

### ローカルでのビルド

```
$ hugo --minify
```

`${pwd}/public/` にhtmlファイル一式が生成される．

## Hugoの雑な説明

### ファイル・ディレクトリ構造

- config.toml : 各種の主要な設定・メニューバー構造の定義
- archetypes/ : `$ hugo new` でページ新規作成する際のテンプレート
- content/ : 各ページのソース（.md）
  - ディレクトリがそのままhtml/urlの階層構造になる
- static/ : 画像ファイルなどの配置先
  - ディレクトリがそのままhtml/urlの階層構造になる
  - content/ の階層と合わせたほうがよい
- data/ : YAMLとかを置く（まだ対応してない）
- layout/ : 独自のレイアウトの定義（themeでやったほうが良い？）
- themes/ : Hugoテーマの定義
- public/ resources/ : `$ hugo --minify` で生成されるページの実体

### ページの編集

基本的にはMarkdownでゴリゴリ書いていく．

コメントアウトは `<!--` `-->` で囲う．

htmlベタ書きしたい場合は
- [Shortcodes](https://gohugo.io/content-management/shortcodes/) を使う．公式の推奨方法だが，バージョンによっては使えないものあり？
- `{{< rawhtml >}}` を導入済み．文字とか画像のサイズを細かく調整したりYouTube等のembed linkとかそのまま使いたい場合は便利（[参考](https://github.com/toppers/hakoniwa/issues/5)）

### 新規ページの作成方法

T.B.A

```bash
$ 
```