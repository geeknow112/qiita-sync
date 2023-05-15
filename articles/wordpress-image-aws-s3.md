<!--
title:   【解説】wordpressの画像をAWS S3に置く方法
tags:    AWS,S3,WordPress
id:      b4c6b0b6fcc509bcec90
private: false
-->


こんにちは。今回は、wordpressについて初心者エンジニアに向けて、aws s3にwordpressの画像データを格納する方法について解説します。

## aws s3について
aws s3は、amazonが提供するオブジェクトストレージサービスです。データのセキュリティ保護、高い信頼性、拡張性を提供しています。wordpressの画像データの格納先としては、aws s3を使用することで、高速な読み込みが実現でき、サイトのスピードアップに繋がります。

## wordpressの画像データの格納先
wordpressのデフォルトでは、画像データはwordpress内部に保存されます。しかし、画像が多くなる場合、wordpressの容量を圧迫し、サイトの速度低下に繋がります。そのため、aws s3に画像を格納することで、容量の節約に繋がり、サイトスピードアップが期待できます。

## wordpressの画像データを移行するには
aws s3への画像データの移行には、3つの方法があります。

1. wordpress backup to dropboxプラグインを使用する方法
2. wp offload media liteプラグインを使用する方法
3. aws cliを使用する方法

上記のプラグインを使用した方法は、プラグインをインストールして設定を行うだけで移行が可能です。aws cliを使用する方法は、aws s3に慣れ親しんでいるエンジニア向けの方法です。ここでは、プラグインを使用した方法を紹介します。

## プラグインを使って移行する場合、おススメのプラグイン
お勧めのプラグインは、wp offload media liteプラグインです。

- wp offload media lite
https://ja.wordpress.org/plugins/amazon-s3-and-cloudfront/

wp offload media liteプラグインは、wordpressの画像データをaws s3に移行するためのプラグインです。プレミアムバージョンもありますが、無料のlite版でも十分な機能があります。10万ダウンロード以上と、多くのユーザーが使っている事から、多くのエンジニアやweb制作者からも支持を得ているプラグインです。

以上が、aws s3にwordpressの画像データを格納する方法について解説しました。aws s3を使用することで、wordpressの画像データの管理が容易になり、維持管理の手間を省くことができます。

## Wordpress + AWSを学ぶには下記もおススメ
- [TechAcademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3A%2F%2Ftechacademy.jp%2Fhtmlcss-trial%3Futm_source%3Dmoshimo%26utm_medium%3Daffiliate%26utm_campaign%3Dtextad)
- [オンラインスクール DMM WEBCAMP PRO](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=ON)

参考となるブログ記事：

- 【aws s3】wordpressの画像データをaws s3に移管して表示速度を改善する方法
https://www.topshare.co.jp/blog/amazonaws/wordpress-aws-s3

- wp offload media lite を使って wordpress のメディア（画像）ファイルを aws s3 上に置く
https://tech.wordflow.jp/2018/06/26/wp-offload-media-lite-s3/