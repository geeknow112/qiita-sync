<!--
title:   【twitter】apiを使ってプログラムで自動投稿する方法
tags:    API,Twitter,自動化
id:      70c1da3d3fc2b9eea046
private: false
-->


こんにちは。今回は、twitterについて初心者エンジニアに向けて、apiを使った自動投稿の方法を紹介します。

## twitterとは？

twitterとは、140字以内のメッセージ（ツイート）を投稿することができるsnsです。twitterには、多くの有名人や企業、政治家などがアカウントを持っており、様々な情報や意見が発信されています。また、広告効果を狙って企業がアカウントを持ち、商品やサービスを宣伝することも多くあります。

## apiとは？

apiとは、application programming interfaceの略で、アプリケーション同士が情報をやり取りするための仕組みです。webサイトやsnsなどの多くのサービスがapiを提供しており、自分が欲しい情報をプログラムから取得することができます。

## apiを使った自動投稿の方法

twitter apiを使うことで、自動的にツイートを投稿することができます。以下の手順に従って、apiを使った自動投稿の方法を紹介します。

### 1. twitter apiの取得

twitter apiを利用するには、先にtwitter apiの開発者登録が必要です。登録方法は下記のブログ記事を参考にしてください。

- [twitter apiの取得について](https://www.apps-gcp.com/twitterapi/)

### 2. apiキーの取得と設定

twitter apiを取得したら、apiキーの取得と設定を行います。apiキーは、twitter apiを利用するためのキーで、各apiで利用するために必要なキーです。

### 3. アクセストークンの取得と設定

アクセストークンは、ユーザー認証を行うためのトークンで、ログイン情報を含んでいます。アクセストークンを取得するには、twitter apiの開発者スイート内のアプリケーションテストページから取得することができます。

### 4. プログラムの作成

apiキーとアクセストークンを取得したら、プログラムに組み込むことができます。以下は、pythonを使ったプログラム例です。

```python
import tweepy

# apiキー取得
api_key = 'あなたのapiキー'
api_secret = 'あなたのapiシークレット'
# アクセストークン取得
access_token = 'あなたのアクセストークン'
access_secret = 'あなたのアクセストークンシークレット'

def main():
    # oauth認証
    auth = tweepy.oauthhandler(api_key, api_secret)
    auth.set_access_token(access_token, access_secret)
    api = tweepy.api(auth)

    # ツイートを投稿する
    tweet = "hello world!"
    api.update_status(status=tweet)

if __name__ == "__main__":
    main()
```

上記の例では、oauth認証を行い、`api.update_status()`でツイートを投稿しています。実行すると、"hello world!"というツイートが投稿されます。

## まとめ

twitter apiを使った自動投稿の方法について紹介しました。apiキーとアクセストークンを取得し、プログラムに組み込むことで自動投稿を行うことができます。apiを使うことで、より簡単に効率的にツイートを投稿することができます。初心者エンジニアの方は、是非活用してみてください。

参考記事：
- [twitter apiを使った自動メッセージの投稿方法](https://marapuru.dev/2019/12/06/twitter-api-tweepy/)
- [pythonでtwitterに自動投稿する方法【初心者向け】](https://qiita.com/masato44gm/items/6f73bbdbcd8d69c1cc60)

## Twitter関連のまとめ
https://hack-note.com/tools/twitter-summary/

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
