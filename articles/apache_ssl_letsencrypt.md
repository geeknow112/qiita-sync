<!--
title: 【apache】let's encryptのssl証明書を導入する方法
tags: apache,virtualhost,aws,lightsail,let's_encrypt,ssl
id: 
private: false
-->

## 【apache】let's encryptのssl証明書を導入する方法

こんにちは。今回は、apacheについて初心者エンジニアに向けて、apacheでlet's encryptのssl証明書を導入する方法について解説します。

## let's encryptとは？ssl証明書の基本とメリット

まず初めに、let's encryptとは何かを説明します。let's encryptは、無料で利用できるオープンソースのssl証明書の発行・管理を行っているプロジェクトです。ssl証明書があると、ウェブサイトへのアクセスが暗号化され、データのやり取りが安全に行われます。

ssl証明書を導入することには以下のメリットがあります。

- 暗号化通信によるデータセキュリティの向上
- ウェブサイトやアプリケーションの信頼性向上
- seoの向上（googleがhttpsサイトを優先表示するため）

次に、certbotを使用してlet's encryptのssl証明書を取得する手順について説明します。

## certbotを使用したlet's encryptのssl証明書の取得手順

certbotは、let's encryptのssl証明書を取得するためのツールです。以下の手順でcertbotを使用してssl証明書を取得します。

### ステップ1: certbotのインストール

まず、certbotをインストールします。以下のコマンドを実行して、certbotをインストールします。

```shell
$ sudo apt-get update
$ sudo apt-get install certbot python-certbot-apache
```

### ステップ2: ssl証明書の取得

次に、certbotを使用してssl証明書を取得します。以下のコマンドを実行して、certbotを利用してssl証明書を取得します。

```shell
$ sudo certbot --apache
```

certbotは自動的にapacheの設定を解析し、適切な証明書の取得手続きを行います。

以上でlet's encryptのssl証明書を取得する手順は完了です。

## apacheでlet's encryptのssl証明書を設定する方法

次に、apacheでlet's encryptのssl証明書を設定する方法について説明します。以下の手順で設定を行います。

### ステップ1: apacheの設定ファイルの編集

まず、apacheの設定ファイルを編集します。以下のコマンドを実行して、設定ファイルを編集します。

```shell
$ sudo nano /etc/apache2/sites-available/default-ssl.conf
```

設定ファイルを開き、`sslcertificatefile`と`sslcertificatekeyfile`のパスをcertbotが取得した証明書のパスに変更します。

```conf
sslcertificatefile /etc/letsencrypt/live/example.com/fullchain.pem
sslcertificatekeyfile /etc/letsencrypt/live/example.com/privkey.pem
```

### ステップ2: apacheの再起動

設定ファイルを編集したら、apacheを再起動します。以下のコマンドを実行して、apacheを再起動します。

```shell
$ sudo service apache2 restart
```

これで、apacheでlet's encryptのssl証明書が正しく設定されました。

## ssl証明書の自動更新と期限切れの管理手法

ssl証明書は有効期限があり、定期的に更新する必要があります。幸いにも、let's encryptの証明書は90日で期限が切れるため、自動更新が推奨されています。

certbotは自動更新機能を提供しており、以下のコマンドを実行することで自動更新を設定できます。

```shell
$ sudo certbot renew
```

自動更新は、cronなどのスケジューラーによって、定期的に実行されるように設定することが一般的です。

## let's encryptのssl証明書を確認する方法とhttps接続のテスト

最後に、let's encryptのssl証明書を確認する方法とhttps接続のテスト方法について説明します。

ブラウザでウェブサイトにアクセスし、urlバーの左側にある鍵のアイコンをクリックすると、証明書の詳細情報を確認することができます。

また、ssl証明書が正しく設定されているかを確認するためには、https接続のテストを行うことができます。以下のコマンドを実行して、https接続をテストします。

```shell
$ curl -i https://example.com
```

正常に接続できれば、httpステータスコード200が返ってくるはずです。

以上で、apacheでlet's encryptのssl証明書を導入する方法について説明しました。初心者エンジニアの方でも、手順に従って順番に進めれば簡単に設定することができます。是非、試してみてください。

参考記事：
- [how to secure apache with let's encrypt on ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-20-04)
- [how to set up let's encrypt with apache on ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-let-s-encrypt-with-apache-on-ubuntu-18-04)

　

## 【Apache】関連のまとめ
https://hack-note.com/summary/apache-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

