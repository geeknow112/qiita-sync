<!--
title:   【twitter】無料で有効活用するapi
tags:    API,Twitter,無料
id:      b30d682042b839e4f75f
private: false
-->


こんにちは。今回は、twitterについて初心者エンジニアに向けて、無料apiの有効活用方法をご紹介します。twitterは、現在最も有名なsnsの一つであり、多くのユーザーが利用しています。そのため、twitterのapiを活用することで、様々なサービスを開発することができます。しかし、apiを使いこなすには、それなりのスキルが必要です。今回は、そうした初心者の方に向けて、twitterのapiを無料で有効活用する方法を紹介します。

## 1. twitter apiとは？

twitter apiとは、twitterが提供するプログラムインタフェースのことを指します。twitter apiを利用することで、データの収集や分析などを行うことができます。twitter apiは、認証機能によってapiキーを発行し、利用することができます。twitter apiには、様々な種類がありますが、本記事では、無料で利用することができる基本的なrest apiを紹介します。

## 2. twitter apiで何ができるか？

twitter apiを使ったサービスの例をいくつか挙げます。

- ツイートの検索やリツイート数の取得
- フォロワーの情報の取得
- ツイートの自動投稿やスケジュール投稿

これらのサービスを活用することで、様々な用途に利用することができます。例えば、自分のアカウントで自動投稿するツールを作ることで、snsの運用コストを削減することができます。また、特定のキーワードを含むツイートをリアルタイムで収集することで、マーケティングに活用することができます。さらに、アカウントのフォロワーがどんな人かを分析することで、ターゲット層を特定することもできます。

## 3. twitter apiの認証方法

twitter apiを利用する場合、まずはapiキーの取得が必要です。apiキーは、twitterデベロッパーサイトから取得することができます。

1. twitterデベロッパーサイトにアクセスする
2. 「apps」を選択する
3. 「create an app」を選択する
4. 必要事項を入力し「create」を押す
5. アプリ名が表示されたら、そのアプリを選択する
6. 「keys and tokens」タブにアクセスし、apiキーを確認する

apiキーは、consumer key（api key）、consumer secret（api secret）、access token、access token secretの4つで構成されます。これらのキーを使用して、oauth認証を行い、apiを使用することができます。

## 4. twitter apiの制限

twitter apiには、制限があります。制限に達すると、apiを利用できなくなる場合があります。何度もapiをリクエストする場合は、制限に注意してください。

1. 時間制限
   - 15分間に15回までapiを呼び出すことができます。
2. リクエスト制限
   - 同一のurlに対するリクエストは、60分間に100回までに制限されています。
3. ツイート制限
   - 同一のアカウントから24時間以内に同一のツイートを送信することはできません。

これらの制限に違反すると、apiの利用が制限される場合があります。より多くの情報については、twitterのapi利用規約を確認してください。

## 5. サンプルコード

twitter apiを利用したサンプルコードをいくつか紹介します。これらのサンプルコードを参考に、自分なりのプログラムを書いてみましょう。

### 5.1. ツイート検索

以下のコードは、指定したキーワードでツイートを検索する方法を示しています。twitter apiからjson形式で取得したデータを、pythonの辞書型に変換して表示しています。

```python
import tweepy

consumer_key = "your consumer key"
consumer_secret = "your consumer secret"
access_token = "your access token"
access_token_secret = "your access token secret"

auth = tweepy.oauthhandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.api(auth)

query = "ツイート検索する単語"
tweets = api.search(q=query, lang="ja", count=10)

for tweet in tweets:
    print(tweet._json)
```

### 5.2. フォロワー取得

以下のコードは、指定したアカウントのフォロワーを取得する方法を示しています。twitter apiからjson形式で取得したデータを、csvファイルに出力しています。

```python
import tweepy
import csv

consumer_key = "your consumer key"
consumer_secret = "your consumer secret"
access_token = "your access token"
access_token_secret = "your access token secret"

auth = tweepy.oauthhandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.api(auth)

screen_name = "アカウントのスクリーンネーム"

with open('followers.csv', 'w', encoding='utf-8', newline='') as f:
    writer = csv.writer(f)
    writer.writerow(['id', 'screen_name', 'name', 'description', 'created_at'])
    for follower in tweepy.cursor(api.followers, screen_name).items():
        writer.writerow([follower.id, follower.screen_name, follower.name, follower.description, follower.created_at])
```

## 6. まとめ

初心者エンジニアに向けて、twitterの無料apiの有効活用方法を紹介しました。apiキーの取得方法から、制限まで、基本的な情報については十分に理解しました。サンプルコードも参考にして、自分なりのアプリケーションを開発してみましょう。また、これらのサンプルコードの改良や、新しいサービスのアイデアを思いつくかもしれません。twitter apiを活用して、世界に羽ばたくアプリケーションを開発してみましょう。

## 参考文献

- [twitter apiの使い方](https://qiita.com/rubytomato@github/items/7c5d8ba291d463c705e5)
- [starting with python and twitter api](https://www.digitalocean.com/community/tutorials/how-to-authenticate-a-python-application-with-twitter-using-tweepy-on-ubuntu-14-04)


## Twitter関連のまとめ
https://hack-note.com/tools/twitter-summary/


## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
