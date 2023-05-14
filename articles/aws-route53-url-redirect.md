<!--
title: 【基礎】aws route53でリダイレクトする方法
tags: aws,route53,手順
id: 
private: false
-->
こんにちは。今回は、awsについて初心者エンジニアに向けて、aws route53でリダイレクトする方法について解説します。

## aws route53とは？

aws route53は、amazon web services（aws）が提供するdnsサービスです。dnsとは、ネットワーク上で使用されるホスト名とipアドレスの対応表を管理するシステムです。route53は、高速・高信頼・スケーラブルなdnsサービスを提供することで、ユーザーのwebサイトやアプリケーションの可用性を向上させることができます。

## aws route53でリダイレクトする方法

aws route53を使って、別のurlへリダイレクトする方法について説明します。

1. ホストゾーン作成

まず、awsコンソールで「route53」を選択し、「ホストゾーンの作成」をクリックします。適切なドメイン名を入力し、作成します。

2. aレコードの作成

次に、リダイレクト先のipアドレスを指定するため、aレコードを作成します。ホストゾーンに移動し、「レコードの作成」にて、aレコードを追加します。

3. s3バケットの作成

リダイレクト先となるs3バケットを作成します。s3コンソールに移動し、「バケットの作成」から、バケットを作成します。バケット名はリダイレクト用のドメイン名と同じに設定します。

4. s3バケットへのリダイレクト設定

s3バケットに移動し、設定画面から「プロパティ」をクリックします。次に「静的ウェブサイトのホスティング」を開き、「リダイレクト設定」をクリックします。適切な情報を入力し、「保存」をクリックします。これで、s3バケットへのリダイレクト設定が完了します。

5. リダイレクトを有効化

最後に、route53の設定画面で、aレコードを編集し、s3バケットのurlにリダイレクトするよう設定します。この時、s3バケットのurlは、リダイレクト用のドメイン名と一致するように設定する必要があります。

以上の手順で、aws route53を使って別のurlへリダイレクトする設定が完了します。

## 注意点

aws route53を使用する際には、リダイレクト先のdnsとs3バケットの設定にも注意が必要です。また、リダイレクトのタイムアウト設定や、リダイレクト時に伝えるhttpステータスコードなど、細かい設定にも詳しくなるとより柔軟な対応ができるようになります。

参考記事：
- [aws公式ドキュメント - amazon route 53 でドメインをリダイレクトする](https://docs.aws.amazon.com/ja_jp/route53/latest/developerguide/routing-to-an-s3-bucket.html)
- [qiita - aws route53 でドメインを s3 バケットにリダイレクトする方法](https://qiita.com/daiki-murakami/items/1c9d55e84887bff7aec5)

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)

