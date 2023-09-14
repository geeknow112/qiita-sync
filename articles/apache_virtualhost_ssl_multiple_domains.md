<!--
title:   【apache】virtualhostを使用して複数ドメインのssl対応サイトを構築する方法
tags: apache,virtualhost,ssl
id:      af3478c05516cf1135e5
private: false
-->


こんにちは。今回は、apacheについて初心者エンジニアに向けて、virtualhostを使用して複数ドメインのssl対応サイトを構築する方法について解説します。

## virtualhostと複数ドメインの関連付け方法

まずは、apacheのvirtualhostと複数ドメインの関連付け方法について説明します。apacheでは、複数のドメインやサブドメインに対してそれぞれ別の設定を行うために、virtualhostを使用します。

まずは、apacheの設定ファイルを編集します。設定ファイルは通常、以下の場所にあります。

```
/etc/httpd/conf/httpd.conf
```

設定ファイルを開き、以下のように設定します。

```apache
<virtualhost *:80>
    servername example.com
    documentroot /var/www/html
</virtualhost>

<virtualhost *:80>
    servername example2.com
    documentroot /var/www/html/example2
</virtualhost>
```

上記の設定では、example.comとexample2.comという2つのドメインに対してそれぞれ別のドキュメントルートを設定しています。これにより、ドメインごとに異なるコンテンツを表示することができます。

## ssl証明書の取得と設定手順

次に、ssl証明書の取得と設定手順について説明します。ssl証明書を使用することで、httpsでの通信を安全にすることができます。

まずは、ssl証明書を取得します。ここでは、let's encryptを使用したssl証明書の取得方法を説明します。

1. certbotのインストール

let's encryptを使用するには、certbotというツールを利用します。certbotをインストールするためには、以下のコマンドを実行します。

```
sudo apt-get install certbot
```

2. ssl証明書の取得

certbotを使用してssl証明書を取得するには、以下のコマンドを実行します。

```
sudo certbot certonly --webroot -w /var/www/html -d example.com -d www.example.com
```

上記のコマンドでは、example.comとwww.example.comという2つのドメインに対してssl証明書を取得しています。取得したssl証明書は、`/etc/letsencrypt/live/example.com/`ディレクトリに保存されます。

3. ssl証明書の設定

ssl証明書を設定するためには、apacheの設定ファイルを編集します。設定ファイルを開き、以下のように設定します。

```apache
<virtualhost *:443>
    servername example.com
    documentroot /var/www/html
    sslengine on
    sslcertificatefile /etc/letsencrypt/live/example.com/fullchain.pem
    sslcertificatekeyfile /etc/letsencrypt/live/example.com/privkey.pem
</virtualhost>
```

上記の設定では、example.comというドメインに対してssl証明書を設定しています。

## 複数ドメインのhttpsリダイレクト設定方法

次に、複数ドメインのhttpsリダイレクト設定方法について説明します。httpsリダイレクトを設定することで、httpでアクセスされた場合に自動的にhttpsにリダイレクトすることができます。

apacheの設定ファイルを以下のように編集します。

```apache
<virtualhost *:80>
    servername example.com
    redirect / https://example.com/
</virtualhost>

<virtualhost *:443>
    servername example.com
    documentroot /var/www/html
    sslengine on
    sslcertificatefile /etc/letsencrypt/live/example.com/fullchain.pem
    sslcertificatekeyfile /etc/letsencrypt/live/example.com/privkey.pem
</virtualhost>
```

上記の設定では、example.comへのhttpアクセスをhttpsにリダイレクトする設定を行っています。

## サブドメインごとの設定とssl対応

さらに、サブドメインごとの設定とssl対応について説明します。複数ドメインの中には、サブドメインを使ってコンテンツを分けたり、サービスを提供したりする場合もあります。そのような場合には、サブドメインごとに設定を行い、ssl対応を行います。

apacheの設定ファイルを以下のように編集します。

```apache
<virtualhost *:80>
    servername example.com
    redirect / https://example.com/
</virtualhost>

<virtualhost *:443>
    servername example.com
    documentroot /var/www/html
    sslengine on
    sslcertificatefile /etc/letsencrypt/live/example.com/fullchain.pem
    sslcertificatekeyfile /etc/letsencrypt/live/example.com/privkey.pem
</virtualhost>

<virtualhost *:80>
    servername subdomain.example.com
    redirect / https://subdomain.example.com/
</virtualhost>

<virtualhost *:443>
    servername subdomain.example.com
    documentroot /var/www/html/subdomain
    sslengine on
    sslcertificatefile /etc/letsencrypt/live/subdomain.example.com/fullchain.pem
    sslcertificatekeyfile /etc/letsencrypt/live/subdomain.example.com/privkey.pem
</virtualhost>
```

上記の設定では、example.comとsubdomain.example.comという2つのドメインに対してそれぞれ異なる設定を行っています。

## サイトごとのカスタム設定とドメイン別のリソース管理

最後に、サイトごとのカスタム設定とドメイン別のリソース管理について説明します。apacheでは、各ドメインごとにカスタム設定を行うことができます。また、ドメインごとに異なるリソースを管理することもできます。

以下のようなディレクトリ構造を想定します。

```
/var/www/html
│
├── example.com
│   ├── index.html
│   └── css
│       └── style.css
│
└── example2.com
    ├── index.html
    └── css
        └── style.css
```

apacheの設定ファイルを以下のように編集します。

```apache
<virtualhost *:80>
    servername example.com
    documentroot /var/www/html/example.com
    customlog /var/log/httpd/example.com-access.log combined
    errorlog /var/log/httpd/example.com-error.log
</virtualhost>

<virtualhost *:80>
    servername example2.com
    documentroot /var/www/html/example2.com
    customlog /var/log/httpd/example2.com-access.log combined
    errorlog /var/log/httpd/example2.com-error.log
</virtualhost>
```

上記の設定では、example.comとexample2.comという2つのドメインに対してそれぞれ異なるログファイルを設定しています。また、ドキュメントルートもそれぞれのドメインごとに設定しています。

以上で、apacheのvirtualhostを使用して複数ドメインのssl対応サイトを構築する方法について説明しました。初心者の方でも理解しやすいように、各手順のコードを示しましたので、参考にしてください。

参考資料：
- [how to set up apache virtual hosts on centos 7 - digitalocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-centos-7)
- [how to secure apache with let's encrypt on centos 7 - digitalocean](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-centos-7)



## 【Apache】関連のまとめ
https://hack-note.com/summary/apache-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
