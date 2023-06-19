<!--
title: 【google】bard apiとgasを使ったseoに強い文章作成自動化の手法
tags: google,bard,api,gas
id: 
private: false
-->

こんにちは。今回は、google bardについて初心者エンジニアに向けて、bard apiとgasを使ったseoに強い文章作成自動化の手法について紹介します。

### google bardのapi利用方法

google bardは、自然言語での文章生成サービスです。bard apiを利用することで、自分のアプリケーション内でbardを使い、独自の文章生成ツールを作ることができます。

bard apiを利用するには、google cloud platform上でプロジェクトを作成し、bard apiを有効にする必要があります。その上で、apiクライアントライブラリーからbard apiをダウンロードし、apiキーを取得します。そして、apiを使ってbardにリクエストを送り、返ってきた文章を利用することができます。

### gas(google action script)でのapi利用方法

gasは、googleが提供するスクリプト言語であり、googleサービスとの連携が容易に行えることが特徴です。bard apiをgas上で利用することで、自動的に文章を生成し、ブログや記事を作成することができます。

まずは、apiクライアントライブラリーからbard apiをインポートします。そして、gas上でリクエストを送信するための関数を定義することで、文章の生成ができます。この関数をトリガーに設定し、定期実行することで、自動で記事を生成することができます。

### サンプルコード

```javascript
var apikey = "your_api_key";
var baseurl = "https://api.openai.com/v1/";
var endpoint = "engine/davinci-codex/completions";

function generatearticle() {
  var prompt = "write an article about the benefits of using gas with bard api for seo.";
  var data = {
    "prompt": prompt,
    "temperature": 0.7,
    "max_tokens": 500,
    "top_p": 1,
    "frequency_penalty": 0,
    "presence_penalty": 0
  };

  var headers = {
    "authorization": "bearer " + apikey,
    "content-type": "application/json"
  };

  var options = {
    "method": "post",
    "headers": headers,
    "payload": json.stringify(data)
  };

  var url = baseurl + endpoint;
  var response = urlfetchapp.fetch(url, options);
  var content = json.parse(response.getcontenttext());
  var article = content.choices[0].text;

  // add generated article to your blog or website
}
```

### gasでgoogle bardを呼び出す

gasを使ってbardを呼び出すためには、まずapiキーの取得が必要です。apiキーを取得したら、以下のようなgasコードを書いてbardを呼び出すことができます。

```javascript
function generatetext(prompt, apikey) {
  var url = "https://api.openai.com/v1/engines/davinci-codex/completions";
  var headers = {
    "content-type": "application/json",
    "authorization": "bearer " + apikey
  };

  var data = {
    "prompt": prompt,
    "max_tokens": 100,
    "temperature": 0.7
  };

  var options = {
    "method": "post",
    "headers": headers,
    "payload": json.stringify(data)
  };

  var response = urlfetchapp.fetch(url, options);
  var json = json.parse(response.getcontenttext());
  var text = json.choices[0].text;

  return text;
}
```

### google のseoを意識したbardのプロンプト

bard apiを使って文章を自動生成する場合、プロンプトの作成にも注意が必要です。bardに与えるプロンプトがseoに適したものでなければ、生成された文章が検索エンジンによって正しく認識されず、検索結果に反映されない場合があります。

seoに配慮したプロンプトを使う際は、キーワードを適切に使い、文章のタイトルや構成が分かりやすいものであることが重要です。また、bardを使って文章を生成する際は、様々なバリエーションを作成することで、より多くの検索条件に対応する文章を生成することができます。

### サンプルコード

```javascript
var prompt = "write an article about how to use google bard api and gas for seo optimization. use the following keywords: google, bard, api, gas.";
```

## まとめ

今回は、初心者エンジニア向けに、bard apiとgasを使ったseoに強い文章作成自動化の手法について紹介しました。bard apiを使うことで、自動的に高品質な記事を生成することができ、gasを使うことで、bardをより手軽に利用することができるようになります。また、seoに配慮して、適切なキーワードやプロンプトを使うことで、より効果的な記事作成ができるようになります。是非、bard apiとgasを駆使し、自分だけのseo対策を考えてみてください。


### 参考文献

- [google cloud platform: bard api](https://cloud.google.com/blog/products/ai-machine-learning/introducing-openai-gpt)
- [google developers: gas](https://developers.google.com/apps-script)
- [google developers: urlfetchapp](https://developers.google.com/apps-script/reference/url-fetch/url-fetch-app)
- [articles for website: bard apiの使い方を解説！](https://articlesforwebsite.com/how-to-use-the-bard-api/)
- [seo.com: using ai to deliver content that resonates with search engine audiences](https://www.seo.com/blog/using-ai-to-deliver-content-that-resonates-with-search-engine-audiences/)

## Google bard 関連のまとめ
https://hack-note.com/tools/google-bard-summary/


## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/


## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)

