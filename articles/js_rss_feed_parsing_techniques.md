<!--
title:   【javascript】簡単にrssフィードをパース！ライブラリとテクニック
tags:    JavaScript,RSS
id:      d0a9324ed552705af8ae
private: false
-->


## ライブラリの選定と導入：簡単なrssパーサーの紹介

こんにちは。今回は、javascriptについて初心者エンジニアに向けて、簡単にrssフィードをパースする方法について解説していきます。

rssフィードは、ウェブサイトやブログの最新情報を取得するために使用されるxml形式のデータです。これをパースして、コンテンツを取得したり表示したりすることができます。

まずは、rssフィードをパースするためのライブラリを選定しましょう。javascriptでは、いくつかの優れたライブラリが存在しますが、今回は以下の2つのライブラリを紹介します。

### 1. feedparser.js
feedparser.jsは、シンプルで軽量なrssパーサーライブラリです。シンプルなapiを提供しており、初心者にも扱いやすい特徴があります。githubでの評判も高く、多くのプロジェクトで利用されています。

feedparser.jsの使い方は以下の通りです。

```javascript
// ライブラリのインポート
const feedparser = require('feedparser');

// フィードのurl
const feedurl = 'https://example.com/rss-feed';

// フィードの取得とパース
const feedparser = new feedparser();
const req = request(feedurl);
req.on('response', function(res) {
  if (res.statuscode !== 200) {
    this.emit('error', new error('bad status code'));
  } else {
    res.pipe(feedparser);
  }
});
feedparser.on('readable', function() {
  const stream = this;
  let item;
  while ((item = stream.read())) {
    console.log('title:', item.title);
    console.log('content:', item.description);
  }
});
```

### 2. rssparser.js
rssparser.jsは、より高度な機能を備えたrssパーサーライブラリです。エラーハンドリングやパースオプションのカスタマイズなど、さまざまな機能が利用できます。また、promiseベースのapiも提供しているため、非同期処理も簡単に行えます。

rssparser.jsの使い方は以下の通りです。

```javascript
// ライブラリのインポート
const parser = require('rss-parser');

// フィードのurl
const feedurl = 'https://example.com/rss-feed';

// パーサーのインスタンス化
const parser = new parser();

// フィードの取得とパース
(async () => {
  try {
    const feed = await parser.parseurl(feedurl);
    feed.items.foreach(item => {
      console.log('title:', item.title);
      console.log('content:', item.content);
    });
  } catch (error) {
    console.error(error);
  }
})();
```

いずれのライブラリを選んでも、簡単にrssフィードをパースすることができます。次は、パース方法の基本とxml解析ライブラリの活用法について見ていきましょう。

## パース方法の基本とxml解析ライブラリの活用法

rssフィードをパースする方法はいくつかありますが、基本的な手法は以下の通りです。

1. フィードのurlを指定して、フィードのデータを取得する。
2. 取得したデータをパースして、利用可能な形式に変換する。
3. 必要な情報を抽出して利用する。

javascriptでは、xml解析には標準の`domparser`クラスを使用することができます。以下のようなコードで、フィードデータをパースすることができます。

```javascript
// フィードのurl
const feedurl = 'https://example.com/rss-feed';

// フィードの取得とパース
fetch(feedurl)
  .then(response => response.text())
  .then(data => {
    const parser = new domparser();
    const xmldoc = parser.parsefromstring(data, "text/xml");

    // パース結果の利用
    const items = xmldoc.queryselectorall("item");
    items.foreach(item => {
      const title = item.queryselector("title").textcontent;
      const content = item.queryselector("description").textcontent;
      console.log('title:', title);
      console.log('content:', content);
    });
  })
  .catch(error => {
    console.error(error);
  });
```

また、xml解析の際には、`xpath`という言語を利用することで、より効率的かつ柔軟に情報を抽出することができます。以下のようなコードで、`xpath`を使用してパースすることができます。

```javascript
// フィードのurl
const feedurl = 'https://example.com/rss-feed';

// フィードの取得とパース
fetch(feedurl)
  .then(response => response.text())
  .then(data => {
    const parser = new domparser();
    const xmldoc = parser.parsefromstring(data, "text/xml");

    // xpathを使用して情報を抽出
    const titleelements = xmldoc.evaluate("//item/title", xmldoc, null, xpathresult.any_type);
    let title = titleelements.iteratenext();
    while(title) {
      console.log('title:', title.textcontent);
      title = titleelements.iteratenext();
    }

    const contentelements = xmldoc.evaluate("//item/description", xmldoc, null, xpathresult.any_type);
    let content = contentelements.iteratenext();
    while(content) {
      console.log('content:', content.textcontent);
      content = contentelements.iteratenext();
    }
  })
  .catch(error => {
    console.error(error);
  });
```

このように、xml解析ライブラリを活用することで、より効率的にフィードデータをパースすることができます。

次は、フィード情報の抽出と表示の方法について見ていきましょう。

## フィード情報の抽出と表示：パース結果の利用方法

パースしたrssフィードから必要な情報を抽出して表示する方法について説明します。

パース結果は、ライブラリによって異なる形式で取得されますが、一般的にはオブジェクトの配列として扱うことができます。各オブジェクトは、フィードの各項目（タイトル、リンク、日付など）をプロパティとして持っています。

以下のコードでは、パース結果を取得し、タイトルとリンクを取り出して表示します。

```javascript
// フィードのurl
const feedurl = 'https://example.com/rss-feed';

// フィードの取得とパース
const parser = new rssparser();
parser.parseurl(feedurl, function(err, feed) {
  if (err) {
    console.error(err);
    return;
  }

  // パース結果の利用
  feed.items.foreach(item => {
    console.log('title:', item.title);
    console.log('link:', item.link);
  });
});
```

また、パース結果をhtml要素として表示する場合は、以下のようにすればよいでしょう。

```javascript
// フィードのurl
const feedurl = 'https://example.com/rss-feed';

// フィードの取得とパース
const parser = new rssparser();
parser.parseurl(feedurl, function(err, feed) {
  if (err) {
    console.error(err);
    return;
  }

  // パース結果の利用
  const container = document.getelementbyid("feed-container");
  feed.items.foreach(item => {
    const titleelement = document.createelement("h2");
    titleelement.textcontent = item.title;

    const linkelement = document.createelement("a");
    linkelement.href = item.link;
    linkelement.textcontent = "read more";

    const articleelement = document.createelement("article");
    articleelement.appendchild(titleelement);
    articleelement.appendchild(linkelement);

    container.appendchild(articleelement);
  });
});
```

このようにして、パース結果を利用してフィード情報を抽出し、適切に表示することができます。

次は、リンクや画像の取得と利用方法について見ていきましょう。

## リンクや画像の取得と利用：コンテンツの拡張手法

パースしたrssフィードからリンクや画像を取得し、コンテンツを拡張する方法について説明します。

rssフィードには、各項目に関連するリンクや画像が存在することがあります。これらの情報を取得して表示することで、ユーザーにより豊かなコンテンツを提供することができます。

例えば、以下のようにすれば、各項目の画像を表示することができます。

```javascript
// フィードのurl
const feedurl = 'https://example.com/rss-feed';

// フィードの取得とパース
const parser = new rssparser();
parser.parseurl(feedurl, function(err, feed) {
  if (err) {
    console.error(err);
    return;
  }

  // パース結果の利用
  feed.items.foreach(item => {
    console.log('title:', item.title);
    console.log('link:', item.link);
    console.log('image:', item.enclosure.url);

    // 画像の表示
    const imageelement = document.createelement("img");
    imageelement.src = item.enclosure.url;
    document.body.appendchild(imageelement);
  });
});
```

また、リンクをクリックした際に別ウィンドウで開くようにするには、以下のようにすればよいでしょう。

```javascript
// フィードのurl
const feedurl = 'https://example.com/rss-feed';

// フィードの取得とパース
const parser = new rssparser();
parser.parseurl(feedurl, function(err, feed) {
  if (err) {
    console.error(err);
    return;
  }

  // パース結果の利用
  feed.items.foreach(item => {
    console.log('title:', item.title);
    console.log('link:', item.link);

    // リンクの表示
    const linkelement = document.createelement("a");
    linkelement.href = item.link;
    linkelement.textcontent = item.title;
    linkelement.target = "_blank";
    document.body.appendchild(linkelement);
  });
});
```

このようにして、リンクや画像を取得してコンテンツを拡張することができます。

最後に、エラーハンドリングと例外処理について見ていきましょう。

## エラーハンドリングと例外処理：パースの安定性向上

パース時に発生するエラーをハンドリングし、例外処理を行うことで、パースの安定性を向上させることができます。

rssフィードのパース時には、様々なエラーが発生する可能性があります。たとえば、フィードのurlが無効であったり、パースに必要な要素が存在しなかったりする場合です。

以下のように、エラーハンドリングを行うことで、パース時のエラーに対処することができます。

```javascript
// フィードのurl
const feedurl = 'https://example.com/rss-feed';

// フィードの取得とパース
const parser = new rssparser();
parser.parseurl(feedurl, function(err, feed) {
  if (err) {
    console.error(err);
    return;
  }

  // パース結果の利用
  feed.items.foreach(item => {
    console.log('title:', item.title);
    console.log('link:', item.link);
  });
});
```

また、例外処理を行うには、`try...catch`構文を使用します。

```javascript
// ライブラリのインポート
const feedparser = require('feedparser');

// フィードのurl
const feedurl = 'https://example.com/rss-feed';

// フィードの取得とパース
const feedparser = new feedparser();
const req = request(feedurl);
req.on('response', function(res) {
  if (res.statuscode !== 200) {
    throw new error('bad status code');
  } else {
    res.pipe(feedparser);
  }
});
feedparser.on('readable', function() {
  try {
    const stream = this;
    let item;
    while ((item = stream.read())) {
      console.log('title:', item.title);
      console.log('content:', item.description);
    }
  } catch (error) {
    console.error(error);
  }
});
```

このようにして、エラーハンドリングと例外処理を行うことで、パースの安定性を向上させることができます。

以上、javascriptについて初心者エンジニアを対象に、簡単にrssフィードをパースする方法について解説しました。feedparser.jsやrssparser.jsといったライブラリを活用することで、より効率的かつ柔軟なパースが可能です。エラーハンドリングや例外処理も忘れずに行い、安定した動作を実現しましょう。参考になるブログ記事としては、以下のurlをご参照ください。

- [how to parse a simple rss feed with javascript](https://www.taniarascia.com/how-to-parse-a-simple-rss-feed-with-javascript/)
- [parsing rss feeds in javascript - the basics](https://dev.to/pluralsight/parsing-rss-feeds-in-javascript---the-basics-40bp)

これらの記事は、より詳細な情報や応用的なテクニックを学ぶのに役立つでしょう。是非、実際にコードを書いて試してみてください。javascriptの理解が深まり、rssフィードのパースに対する理解も高まることでしょう。



## 【Javascript】関連のまとめ
https://hack-note.com/summary/javascript-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
