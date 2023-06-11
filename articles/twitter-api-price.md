<!--
title:   【twitter】apiの有料化【無料でできること】
tags:    API,Twitter,有料化,無料
id:      29cc4242cf6494859bb7
private: false
-->



こんにちは。今回は、twitterについて初心者エンジニアに向けて、api有料化について説明します。

## twitter apiとは

twitter apiは、外部のアプリケーションがtwitterのデータにアクセスするためのプログラムインターフェースです。apiを使用することで、ユーザーは、例えば、自分のタイムラインの一部を表示したり、新しいつぶやきを投稿したり、フォロワー数を取得したりすることができます。

## twitter apiの無料仕様

以前は、twitter apiには、無料で使える仕様がありました。この無料仕様では、ユーザーには800回までのアクセスが許可されました。しかし、これは2018年8月に変更され、現在はapiの使用にお金がかかるようになりました。

## twitter apiの有料仕様

現在、twitter apiの有料仕様は、開発者が使用するために料金がとられます。料金は主に、apiにアクセスする回数に基づいて決定されます。開発者がapiにアクセスするたびに、twitterはそのアクセスに応じて料金を請求します。

twitter apiの有料仕様には、3つの価格設定があります。1つ目は月額99ドルのessentialプランで、20万回のapiアクセスが可能です。2つ目は月額399ドルのelevateプランで、100万回のapiアクセスが可能です。3つ目は月額2,499ドルのendpointプランで、無制限のapiアクセスが可能です。

## 無料でできること

twitter apiが有料になったとはいえ、無料でできることもまだまだあります。以下は、無料でできるtwitter apiの使用例です。

### 1. ユーザーのタイムラインから最新のツイートを取得する

```
import tweepy

consumer_key = "ここにあなたのconsumer keyを入力してください"
consumer_secret = "ここにあなたのconsumer secretを入力してください"
access_token = "ここにあなたのaccess tokenを入力してください"
access_token_secret = "ここにアクセストークンシークレットを入力してください"

auth = tweepy.oauthhandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.api(auth)

user_tweets = api.home_timeline()
for tweet in user_tweets:
    print(tweet.text)
```

### 2. ハッシュタグでつぶやきを検索する

```
import tweepy

consumer_key = "ここにあなたのconsumer keyを入力してください"
consumer_secret = "ここにあなたのconsumer secretを入力してください"
access_token = "ここにあなたのaccess tokenを入力してください"
access_token_secret = "ここにアクセストークンシークレットを入力してください"

auth = tweepy.oauthhandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.api(auth)

search_results = api.search(q="#python", count=100)
for tweet in search_results:
    print(tweet.text)
```

### 3. 特定のユーザーが発言したつぶやきを取得する

```
import tweepy

consumer_key = "ここにあなたのconsumer keyを入力してください"
consumer_secret = "ここにあなたのconsumer secretを入力してください"
access_token = "ここにあなたのaccess tokenを入力してください"
access_token_secret = "ここにアクセストークンシークレットを入力してください"

auth = tweepy.oauthhandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.api(auth)

user_tweets = api.user_timeline(screen_name="twitter")
for tweet in user_tweets:
    print(tweet.text)
```

## まとめ

twitter apiが有料になったことにより、開発者はapiの使用にある程度の費用を負担する必要があります。しかし、それでも、無料でできることはまだまだあります。この記事を読んで、初心者エンジニアの方々がtwitter apiを使って自分たちのアプリケーションを開発する際に有益な情報を得ることができたら幸いです。

### 参考文献

- [twitter api | developer policy, agreement, and rules](https://developer.twitter.com/en/developer-terms/agreement-and-policy)
- [twitter apiがoauth 1.0a からoauth 2.0 に変更に、メモ](https://qiita.com/takanoritakeuchi/items/3cabbbe74e2ae933128d)
- [tweepy document](http://docs.tweepy.org/)


## Twitter関連のまとめ
https://hack-note.com/tools/twitter-summary/


## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
