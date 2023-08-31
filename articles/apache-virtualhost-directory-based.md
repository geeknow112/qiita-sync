<!--
title:   【apache】ディレクトリ別の仮想ホスト設定：複数のブログを管理
tags:    Apache,VirtualHost
id:      cf10d16de8e6bea29f04
private: false
-->


## ブログ管理のためのディレクトリ別仮想ホスト設定手法

こんにちは。今回は、apacheについて初心者エンジニアに向けて、ディレクトリ別の仮想ホスト設定方法についてご紹介します。apacheを使用して複数のブログを管理する際には、各ブログごとにディレクトリを作成し、仮想ホストの設定をする必要があります。ここでは、その手法について詳しく解説していきます。

### ブログごとのディレクトリ構造の作成方法

まずは、ブログごとにディレクトリを作成する方法について説明します。ディレクトリ構造を作成することで、各ブログのコンテンツを管理しやすくなります。

まず、apacheのドキュメントルートとなるディレクトリを決めます。例えば、`/var/www/html/`というディレクトリにドキュメントルートを設定した場合、このディレクトリ配下に各ブログのディレクトリを作成します。

```
/var/www/html/
├── blog1/
├── blog2/
└── blog3/
```

上記のように、blog1, blog2, blog3といった名前のディレクトリを作成します。各ディレクトリは、それぞれのブログに対応しています。ここでは、3つのブログを管理する例を示しましたが、必要に応じて作成するディレクトリの数やブログの名前を変更してください。

### ディレクトリ別仮想ホストの設定方法

次に、ディレクトリ別の仮想ホスト設定方法について説明します。仮想ホストを設定することで、各ブログにアクセスする際には、対応するディレクトリを参照するようになります。

まず、apacheの設定ファイルを開きます。一般的には、`/etc/httpd/conf/httpd.conf`や`/etc/apache2/apache2.conf`などのパスにあります。

設定ファイル内で、`<virtualhost>`タグを使用して仮想ホストを設定します。例えば、以下のような設定を追加してください。

```
<virtualhost *:80>
    servername www.blog1.com
    documentroot /var/www/html/blog1/
</virtualhost>

<virtualhost *:80>
    servername www.blog2.com
    documentroot /var/www/html/blog2/
</virtualhost>

<virtualhost *:80>
    servername www.blog3.com
    documentroot /var/www/html/blog3/
</virtualhost>
```

上記の設定では、それぞれの仮想ホストを`<virtualhost>`タグ内に記述し、`servername`ディレクティブで設定したドメイン名にアクセスされると、対応するディレクトリのコンテンツが表示されます。

設定を変更したら、apacheを再起動して設定を反映させましょう。以下のようなコマンドを実行してください。

```
sudo systemctl restart apache2
```

これで、ディレクトリ別の仮想ホスト設定が完了しました。

## ディレクトリ別仮想ホストのアクセス制御とセキュリティ対策

ブログを管理する際には、アクセス制御やセキュリティ対策も重要です。ディレクトリ別の仮想ホストでは、`.htaccess`ファイルを使用してアクセス制御やセキュリティ対策を行うことができます。

まず、各ブログのディレクトリ内に`.htaccess`ファイルを作成します。以下は、アクセス制御をする例です。

```
# deny access to all files in this directory
order allow,deny
deny from all

# allow access to index.php file
<files index.php>
    order allow,deny
    allow from all
</files>
```

上記の例では、ディレクトリに含まれる全てのファイルへのアクセスを禁止し、index.phpファイルへのアクセスのみを許可しています。

また、セキュリティ対策のためにssl証明書を使用する場合は、各仮想ホストの設定にssl証明書のパスやポート番号を追加する必要があります。以下は、例です。

```
<virtualhost *:80>
    servername www.blog1.com
    documentroot /var/www/html/blog1/
</virtualhost>

<virtualhost *:443>
    servername www.blog1.com
    documentroot /var/www/html/blog1/

    sslengine on
    sslcertificatefile /etc/apache2/ssl/blog1.crt
    sslcertificatekeyfile /etc/apache2/ssl/blog1.key
</virtualhost>
```

上記の例では、ポート番号443（https）でのアクセスのためにssl設定を追加しています。

## ディレクトリ別仮想ホストのログ管理と分析方法

ディレクトリ別の仮想ホストに対するアクセスログを管理し、分析することも重要です。apacheでは、モジュールとして`mod_log_config`が提供されており、アクセスログの設定やフォーマットをカスタマイズすることができます。

設定ファイルにログのフォーマットを記述すると、apacheは自動的に対応するログファイルを作成してくれます。

以下の例は、ログのフォーマットを指定する設定です。

```
logformat "%h %l %u %t \"%r\" %>s %b" common
```

上記の設定では、アクセス元ipアドレス、リモートログ名、リモートユーザ、アクセス日時、リクエスト行、ステータスコード、レスポンスサイズの情報をログに記録します。

また、ログの保存先を指定することもできます。以下の例は、ログの保存先を別のディレクトリにする設定です。

```
customlog /var/log/apache2/access.log common
```

上記の例では、カスタムログファイル`access.log`を`/var/log/apache2/`ディレクトリに保存します。

ログのフォーマットや保存先を設定したら、apacheを再起動して設定を反映させましょう。

## ディレクトリ別仮想ホストのカスタム設定と機能拡張手順

ディレクトリ別の仮想ホストでは、各ブログごとにカスタム設定や機能拡張を行うことも可能です。例えば、特定のブログに対してurlリライティングやキャッシュの設定などを追加することができます。

カスタム設定を行うには、各仮想ホストの設定に追加のディレクティブを記述する必要があります。以下は、urlリライティングの設定例です。

```
<virtualhost *:80>
    servername www.blog1.com
    documentroot /var/www/html/blog1/

    rewriteengine on
    rewritecond %{request_filename} !-f
    rewritecond %{request_filename} !-d
    rewriterule ^(.*)$ index.php/$1 [l]
</virtualhost>
```

上記の例では、リクエストされたurlが実在しないファイルやディレクトリでない場合、`index.php`を起点としてurlリライティングを行います。

また、特定のブログに対してキャッシュの設定を行う場合は、`<location>`ディレクティブを使用します。以下は、キャッシュの設定例です。

```
<virtualhost *:80>
    servername www.blog1.com
    documentroot /var/www/html/blog1/

    <location "/">
        fileetag none
        expiresactive on
        expiresdefault "access plus 1 week"
    </location>
</virtualhost>
```

上記の例では、全てのリクエストに対してキャッシュ設定を行い、キャッシュ有効期限を1週間に設定しています。

## まとめ

今回は、apacheを使用してディレクトリ別の仮想ホストを設定する手法について説明しました。各ブログごとにディレクトリを作成し、仮想ホストの設定を行うことで、複数のブログを管理することができます。また、アクセス制御やセキュリティ対策、ログ管理、カスタム設定など、さまざまな要素を組み合わせることで、より安全で効率的なブログ管理が可能になります。

参考文献:
- [apache - virtual hosts](https://httpd.apache.org/docs/2.4/vhosts/)
- [apache - rewrite guide](https://httpd.apache.org/docs/current/rewrite/)
- [apache - caching guide](https://httpd.apache.org/docs/current/caching.html)

## twitter関連のまとめ
https://hack-note.com/tools/twitter-summary/


## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
