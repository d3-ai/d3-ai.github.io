# d3-ai.github.io
D3-AIプロジェクトのWebサイトの管理用リポジトリ

## 利用環境

- [GitHub Pages](https://docs.github.com/ja/pages/getting-started-with-github-pages/about-github-pages)
- [Hugo](https://gohugo.io/)
- Huge theme: [Northendlab Light](https://github.com/gethugothemes/northendlab-light)
  - [forkしてチューニングしたもの](https://github.com/takasehideki/northendlab-light)を利用している

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

### 新規の「お知らせ」ページの作成方法

まずは下記のコマンドを実行する．

```bash
$ hugo new news/hoge-fuga.md
```

次のようなファイルが `content/news/hoge-fuga.md` として生成される．ファイル名の文脈区切りは `-` がHugoの推奨らしい．

```
+++
title = "Test Page"
date = 2021-09-27T16:36:09+09:00
draft = false
categories = ["News", "arch", "theory", "IoT", "data"]
tags = ["news", "arch", "theory", "IoT", "data"]
image = ""
type = "post"
+++

```

属性の意味はそれぞれ下記のとおり．適宜で修正していく．

- `title`: ページのタイトル．日本語可．
- `date`: ページの作成日時．
  - あとで変更可能．
  - 未来の日時にするとその時間以降にビルドするまでTOPや「お知らせ」の一覧に表示されなくなる．
- `draft`: `true`にするとドラフト記事下書き扱いになる．基本は`false`のままで良い．
- `categories`: 記事の所属するカテゴリ．
  - 不要なものは除いてよい．"See Also" で良い感じにしてくれる（はず）
  - イベントの案内は `"イベント"` を追加する．日本語で！
- `tags`: 記事の所属するカテゴリ．
  - `categories` とぶっちゃけ一緒．要らないかもしれない．
- `image`: 記事の冒頭に差し込みたい画像．
  - 画像は `/static/images/news` に配置する．
  - `image = "/images/news/d3-ai-logo.png"` のように書く．
  - サムネイル（OGP）にもなるっぽい．
  - 文中で `![d3-ai-logo](/images/news/d3-ai-logo.png)` のように差し込むこともできる（この場合はサムネイルにならない？）
- `type = "post"`: お知らせ用の属性．必ず付ける．

最後に， `+++` 以降にお知らせの本文を書く．
