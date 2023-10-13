<!--
title: 【javascript】最新のニュースを取得！rssリーダーの作り方
tags: javascript,rss
id: 
private: false
-->

## プロジェクトのセットアップと環境構築
### 必要なツールのインストール
node.jsを使用するため、まずはnode.jsのインストールを行いましょう。

```
// ターミナルで以下のコマンドを実行してnode.jsのバージョンを確認
node -v

// node.jsがインストールされていない場合は、公式サイトからインストーラをダウンロードしてインストール
https://nodejs.org/ja/download/
```

### プロジェクトの作成
次に、プロジェクトのディレクトリを作成し、必要なファイルを準備しましょう。

```
// プロジェクトのディレクトリを作成
mkdir js-rss-reader

// プロジェクトのディレクトリに移動
cd js-rss-reader

// package.jsonファイルを作成
npm init -y
```

### 必要なパッケージのインストール
rssフィードを処理するためのパッケージである"rss-parser"をインストールしましょう。

```
// rss-parserパッケージのインストール
npm install rss-parser
```

## rssフィードのurl取得と選択
### ニュースサイトからのrssフィードurl取得
rssフィードを取得するためには、まず対象となるニュースサイトのrssフィードのurlを取得する必要があります。以下は、javascriptのニュースサイトである「javascript weekly」のrssフィードのurlを取得する方法です。

```javascript
const fetch = require('node-fetch');
const cheerio = require('cheerio');

const getrssfeedurl = async () => {
  const url = 'https://javascriptweekly.com/';
  const res = await fetch(url);
  const html = await res.text();
  const $ = cheerio.load(html);
  const rssfeedurl = $('link[type="application/rss+xml"]').attr('href');
  return rssfeedurl;
};

getrssfeedurl().then((rssfeedurl) => {
  console.log(rssfeedurl);
});
```

## フィードの読み込みとデータの取得
### rssフィードの読み込み
次に、取得したrssフィードのurlを使用して、実際にフィードを読み込みましょう。

```javascript
const parser = require('rss-parser');

// フィードを読み込む関数
const getfeed = async (url) => {
  const parser = new parser();
  const feed = await parser.parseurl(url);
  return feed;
};

const rssfeedurl = 'https://example.com/rss'; // 実際のrssフィードのurlを指定
getfeed(rssfeedurl).then((feed) => {
  console.log(feed);
});
```

### フィードからデータを取得
フィードを読み込んだら、記事のタイトルや本文など、必要なデータを取得しましょう。

```javascript
const rssfeedurl = 'https://example.com/rss'; // 実際のrssフィードのurlを指定
getfeed(rssfeedurl).then((feed) => {
  // フィードのタイトルを表示
  console.log(feed.title);

  // 各記事の情報を表示
  feed.items.foreach((item) => {
    console.log(item.title);
    console.log(item.content);
  });
});
```

## ニュース記事の表示とデザインのカスタマイズ
### ニュース記事をhtmlで表示
取得したニュース記事をhtmlで表示するために、以下のようなhtmlファイルを作成しましょう。

```html
<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>javascript rss reader</title>
  <style>
    /* ニュース記事のスタイルを定義 */
    .article {
      margin-bottom: 20px;
      padding: 10px;
      border: 1px solid #ccc;
    }

    .title {
      font-weight: bold;
    }

    .content {
      margin-top: 10px;
    }

    .link {
      display: block;
      margin-top: 10px;
      color: blue;
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <h1>javascript rss reader</h1>
  <div id="articles"></div>

  <script src="main.js"></script>
</body>
</html>
```

### ニュース記事を表示するjavascriptの実装
htmlに用意した記事表示用の要素に、javascriptを使ってニュース記事を表示しましょう。

```javascript
const rssfeedurl = 'https://example.com/rss'; // 実際のrssフィードのurlを指定
getfeed(rssfeedurl).then((feed) => {
  const articleselement = document.getelementbyid('articles');

  // 各記事の情報を表示
  feed.items.foreach((item) => {
    // 記事の要素を作成
    const articleelement = document.createelement('div');
    articleelement.classname = 'article';

    // タイトルを表示
    const titleelement = document.createelement('h2');
    titleelement.textcontent = item.title;
    titleelement.classname = 'title';
    articleelement.appendchild(titleelement);

    // コンテンツを表示
    const contentelement = document.createelement('div');
    contentelement.innerhtml = item.content;
    contentelement.classname = 'content';
    articleelement.appendchild(contentelement);

    // リンクを表示
    const linkelement = document.createelement('a');
    linkelement.href = item.link;
    linkelement.textcontent = 'read more';
    linkelement.classname = 'link';
    articleelement.appendchild(linkelement);

    // 記事を表示
    articleselement.appendchild(articleelement);
  });
});
```

## リンク先の読み込みと記事の詳細表示機能
### リンク先の読み込み
ニュース記事のリンクをクリックすると、その記事の詳細ページを新しいタブで表示する機能を追加しましょう。

```javascript
const rssfeedurl = 'https://example.com/rss'; // 実際のrssフィードのurlを指定
getfeed(rssfeedurl).then((feed) => {
  const articleselement = document.getelementbyid('articles');

  // 各記事の情報を表示
  feed.items.foreach((item) => {
    // 記事の要素を作成
    const articleelement = document.createelement('div');
    articleelement.classname = 'article';

    // タイトルを表示
    const titleelement = document.createelement('h2');
    titleelement.textcontent = item.title;
    titleelement.classname = 'title';
    articleelement.appendchild(titleelement);

    // コンテンツを表示
    const contentelement = document.createelement('div');
    contentelement.innerhtml = item.content;
    contentelement.classname = 'content';
    articleelement.appendchild(contentelement);

    // リンクを表示
    const linkelement = document.createelement('a');
    linkelement.href = item.link;
    linkelement.target = '_blank'; // リンクを新しいタブで開く
    linkelement.textcontent = 'read more';
    linkelement.classname = 'link';
    articleelement.appendchild(linkelement);

    // 記事を表示
    articleselement.appendchild(articleelement);
  });
});
```

以上が、javascriptについて初心者エンジニア向けのrssリーダーの作成方法です。

参考記事:
- [【初心者向け】rssリーダーの作り方](https://example.com/rss-reader-1)
- [javascriptを使用してrssフィードを取得する方法](https://example.com/rss-reader-2)

　

## 【Javascript】関連のまとめ
https://hack-note.com/summary/javascript-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

