<!--
title: 【apache】aws lightsail上で安全なブログホスティング環境を構築するためのapache virtualhostの設定方法
tags: apache,virtualhost,aws,lightsail,let's_encrypt,ssl
id: 
private: false
-->

## aws lightsailにおけるapacheのセットアップと基本設定

### apacheをインストールする

apacheをaws lightsailインスタンスにインストールするには、まずsshクライアントを使用して接続する必要があります。接続後、以下のコマンドを実行してapacheをインストールします。

```
sudo apt update
sudo apt install apache2
```

### apacheの基本設定

apacheのインストールが完了したら、基本設定を行います。まず、以下のコマンドでapacheの設定ファイルを開きます。

```
sudo vi /etc/apache2/apache2.conf
```

設定ファイルを開いたら、以下の行を探し、`allowoverride none`を`allowoverride all`に変更します。

```
<directory /var/www/>
    options indexes followsymlinks
    allowoverride all
    require all granted
</directory>
```

変更が完了したら、apacheを再起動します。

```
sudo service apache2 restart
```

## 安全なブログホスティング環境の要件とセキュリティ対策

### ファイアウォールの設定

aws lightsailでは、インスタンスレベルのファイアウォールが提供されています。これを使って、不正アクセスをブロックすることができます。

ファイアウォールの設定は、aws lightsailダッシュボードの「ネットワーキング」セクションで行います。ここで、必要なポートを開放し、不必要なポートはブロックします。

通常、httpポート（ポート80）とhttpsポート（ポート443）を開放する必要があります。また、sshポート（ポート22）も開放されている必要がありますが、安全のために特定のipアドレスからのアクセスのみを許可することをお勧めします。

## apache virtualhostの設定手順とディレクトリ構造の作成

### virtualhostの設定

apacheで複数のサイトをホストするためには、virtualhostの設定が必要です。以下は、サンプルのvirtualhost設定の一部です。

```
<virtualhost *:80>
    servername example.com
    documentroot /var/www/example.com/public_html
    <directory /var/www/example.com/public_html>
        options -indexes +followsymlinks
        allowoverride all
    </directory>
    errorlog /var/www/example.com/logs/error.log
    customlog /var/www/example.com/logs/access.log combined
</virtualhost>
```

この設定では、サーバー名とドキュメントルートが指定されています。適宜、実際のドメイン名やディレクトリパスに置き換えてください。

### ディレクトリ構造の作成

各virtualhostのドキュメントルートには、以下のようなディレクトリ構造が必要です。

```
/var/www/example.com/
├── public_html
│   └── index.html
└── logs
    ├── access.log
    └── error.log
```

`public_html`ディレクトリには、公開するファイルを配置します。`logs`ディレクトリには、アクセスログやエラーログを保存します。

## ssl/tlsの導入とlet's encryptによる証明書の取得方法

### ssl/tlsの導入

ssl/tlsを使用するためには、まずapacheのsslモジュールを有効にする必要があります。以下のコマンドでsslモジュールを有効にします。

```
sudo a2enmod ssl
sudo service apache2 restart
```

### let's encryptによる証明書の取得

「certbot」というツールを使用して、let's encryptから無料のssl証明書を取得することができます。

以下のコマンドを実行して、certbotをインストールします。

```
sudo apt install certbot python3-certbot-apache
```

インストールが完了したら、以下のコマンドで証明書の取得を行います。

```
sudo certbot --apache
```

certbotは、証明書の取得手続きを自動的に行ってくれます。証明書が取得されたら、apacheの設定ファイルが自動的に更新され、https経由でのアクセスが可能になります。

## ログ管理とモニタリング：アクセスログとエラーログの分析と保護

### アクセスログの分析と保護

apacheでは、アクセスログを使用してウェブサイトのトラフィックや訪問者の情報を記録します。

以下のコマンドで、お使いのvirtualhostのアクセスログを表示します。

```
sudo tail -f /var/www/example.com/logs/access.log
```

ログを確認することで、不正アクセスや攻撃の兆候を検知することができます。また、ログディレクトリのパーミッションを適切に設定することで、ログの保護も行うことができます。

### エラーログの分析と保護

apacheでは、エラーログを使用してウェブサーバーのエラー情報を記録します。

以下のコマンドで、お使いのvirtualhostのエラーログを表示します。

```
sudo tail -f /var/www/example.com/logs/error.log
```

エラーログを確認することで、ウェブサーバーのエラーの原因を特定することができます。また、エラーログもログディレクトリのパーミッション設定によって保護することができます。

## おわりに

今回は、apacheについて初心者エンジニアに向けて、aws lightsail上で安全なブログホスティング環境を構築するためのapache virtualhostの設定方法を解説しました。

apacheのインストール、基本設定、ファイアウォールの設定、virtualhostの設定方法、ssl/tlsの導入、ログ管理とモニタリングについて学びました。

これらの手順を実施することで、安全なブログホスティング環境を構築することができます。ぜひ、実際に試してみてください。

参考url：
- [aws lightsail documentations](https://lightsail.aws.amazon.com/ls/docs/ja/)
- [apache http server documentation](https://httpd.apache.org/docs/)

　

## 【Apache】関連のまとめ
https://hack-note.com/summary/apache-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

