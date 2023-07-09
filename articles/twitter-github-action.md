<!--
title:   【twitter】api自動投稿 github actionsがおススメ
tags:    API,GitHub-Actions,Twitter
id:      dbe4872f44ff08587c8b
private: false
-->


こんにちは。今回は、twitterについて初心者エンジニアに向けて、twitterのapiを使った自動投稿の方法について説明します。
twitterは、世界中で使われているsnsの一つであり、多くの人々が日々使っています。しかし、自分で毎日投稿するのは大変ですよね。そこでTwitter API + github actionsを使って自動投稿する方法を紹介しますので、是非参考にしてください。

## twitter apiとは

twitter apiとは、twitterが提供するプログラムのことで、外部からtwitterのデータや機能を利用できるようにするためのものです。具体的には、アカウントの情報取得や、投稿などを行うことができます。twitter apiは、twitterの開発者向けに提供されており、無料で利用できます。

twitter apiを使って自動投稿を行う場合、まずapi keyを取得する必要があります。以下の記事が参考になります。

[【初心者向け】twitter apiの使い方とoauth認証の手順 | hatena tech blog](https://tech.hatenablog.com/entry/2020/03/12/093000)

## github actionsとは

github actionsとは、githubが提供する自動化ツールであり、ci/cdパイプラインの機能を持っています。github actionsを使用することで、自動的にビルドやテストを行い、さらにデプロイまで行うことができます。

github actionsを使った自動投稿の方法については、以下の記事が参考になります。

[github actionsでtwitter botを構築する | qiita](https://qiita.com/ryz310/items/f17d63bdf8ff61ff9ce9)

## github actionsを使ったtwitter自動投稿の例

以下は、github actionsを使ってtwitter自動投稿を行う例です。

```yml
name: "auto tweet"
on:
  schedule:
    - cron: '0 12 * * *'
jobs:
  auto_tweet:
    runs-on: ubuntu-latest
    steps:
      - name: checkout code
        uses: actions/checkout@v2
      - name: use node.js
        uses: actions/setup-node@v1
        with:
          node-version: '10'
      - name: install dependencies
        run: npm install
      - name: auto tweet
        run: |
          npm run build
          npm run tweet
        env:
          twitter_consumer_key: ${{ secrets.twitter_consumer_key }}
          twitter_consumer_secret: ${{ secrets.twitter_consumer_secret }}
          twitter_access_token_key: ${{ secrets.twitter_access_token_key }}
          twitter_access_token_secret: ${{ secrets.twitter_access_token_secret }}
```

上記の例では、定期的に投稿するようにスケジュール設定されています。また、node.jsとnpmを使用しているため、前提としてこれらをインストールする必要があります。

## まとめ

本記事では、twitter apiを使った自動投稿の方法と、github actionsを使った自動投稿の方法について紹介しました。twitter apiを使った自動投稿は、api keyの取得が必要ですが、github actionsを使うことでより簡単に自動投稿を行うことができます。是非、参考にしてみてください。


## Twitter関連のまとめ
https://hack-note.com/tools/twitter-summary/


## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
