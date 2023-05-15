<!--
title: 【基礎】aws lightsailで無料sslを設定する方法
tags: aws,lightsail,無料,手順
id: 
private: false
-->

こんにちは。今回は、awsについて初心者エンジニアに向けて、aws lightsailで無料sslを設定する方法についてご紹介します。

## aws lightsail 無料sslとは？

aws lightsailは、awsのクラウドコンピューティングサービスの一つで、amazon ec2のようにクラウドサーバーを提供するサービスです。無料sslとは、暗号化通信のためのssl証明書を無料で提供するサービスです。

## aws lightsailで無料sslを使わない場合の選択肢

無料sslを使わない場合は、有料のssl証明書を購入する必要があります。ssl証明書を購入する場合、オンラインストアや金融サイトなどのセキュアな通信を行うためのhttps通信を実現することができます。

## aws lightsailで無料sslを設定する手順

aws lightsailで無料sslを設定する手順を以下に示します。

1. aws lightsailにログインし、対象のインスタンスを選択します。

2. メニューバーの「ネットワーキング」を選択し、「ssl/tls証明書」をクリックします。

3. 「ssl/tls証明書」のページで、「新しい証明書の作成」をクリックします。

4. 「証明書の作成」画面で、ssl証明書に関する情報を入力します。必要な情報を入力したら、「作成」をクリックします。

5. 「ssl/tls証明書」ページに戻り、作成されたssl証明書が表示されることを確認します。

6. 対象のインスタンスを選択し、メニューバーの「接続」を選択し、「https接続の設定」をクリックします。

7. 「https接続の設定」ページで、「ssl/tls証明書」を選択し、設定したssl証明書を選択します。「保存」をクリックして設定を保存します。

以上が、aws lightsailで無料sslを設定する手順になります。

## 注意点

ssl証明書の有効期限が切れると、https接続ができない場合があります。ssl証明書の有効期限が近づいている場合は、早めに更新するようにしましょう。

また、aws lightsailは初心者でも扱いやすいサービスですが、セキュリティに関する知識が不十分だと問題が発生する場合があります。aws lightsailを利用する際には、マルウェア対策やファイアウォールの設定など、セキュリティについても十分注意して利用するようにしましょう。

以上が、aws lightsailで無料sslを設定する方法についてのご紹介です。

参考記事：

https://aws.amazon.com/jp/premiumsupport/knowledge-center/lightsail-create-ssl-certificate/

https://hacknote.jp/archives/53272/

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)

