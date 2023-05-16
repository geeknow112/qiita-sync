<!--
title:   【基礎】aws msadとは？active directoryを簡単に使うには
tags:    AWS,active-directory,msad,手順,簡単
id:      c687f21939cf33400c4a
private: false
-->


こんにちは。今回は、awsについて初心者エンジニアに向けて、aws msadについて解説します。

## aws msad とは？

aws managed microsoft active directory (aws msad) は、windowsアプリケーションをaws cloud上で実行している企業や開発者向けに提供されるサービスです。このサービスにより、aws cloudとオンプレミスのactive directory（以下、ad）の連携が容易になり、ハイブリッド環境でのアプリケーション開発や管理が促進されます。

## aws msadの料金は？

aws msadの料金は、以下のようになっています。

* ネットワーク接続: $0.05/時
* 毎月のアクティブユーザー数: $0.40/アクティブユーザー/月
* 毎月のアクティブデバイス数: $0.60/アクティブデバイス/月

ただし、上限があるため、詳細についてはaws公式サイトを確認してください。

## aws msadとactivedirectoryでできることの違い

aws msadは、aws cloud環境とオンプレミスのadを連携することができ、ハイブリッド環境でのアプリケーション開発や管理を容易にすることができます。一方で、オンプレミスのadには限界があるため、aws cloud環境に移行することも必要となっています。

## 使用上の注意点

aws msadを利用するためには、以下の点に注意する必要があります。

* ハードウェア、os、アプリケーションのライセンスが必要。
* セキュリティ設定が必要。
* awsマネジメントコンソールを利用して、adの設定や管理が必要。

以上の点にご注意いただき、aws msadをご活用いただければ幸いです。

## 参考となるブログ記事のurlを2個以上掲載してください。

* [aws msad overview](https://aws.amazon.com/jp/directoryservice/ms_ad/)
* [aws msadの性能とメリット・デメリットについて考える](https://aws-blog.jp/archives/8582)

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
