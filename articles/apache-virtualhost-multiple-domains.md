<!--
title: 【apache】virtualhost設定：複数ドメインのブログをホストしよう
tags: apache,virtualhost
id: 
private: false
-->

## 複数ドメインの仮想ホストの設定手順

apacheは非常にパワフルなウェブサーバーソフトウェアであり、複数のドメインを同じサーバーで運用するときに便利です。この記事では、apacheの仮想ホスト機能を使用して、複数のドメインを運用する方法を紹介します。

### 1. ドメインの設定

まず、運用するドメインを整理しましょう。apacheの仮想ホスト機能を使用するには、各ドメインに対してdnsの設定を行う必要があります。ドメインの設定方法はドメインの登録業者によって異なるため、業者のドキュメンテーションを参照してください。

### 2. サーバーの設定

apacheの設定ファイル（httpd.conf）を編集して、仮想ホストの設定を追加します。

```apacheconf
# 仮想ホストの設定
<virtualhost *:80>
    servername example.com
    documentroot /var/www/example
</virtualhost>
```

上記のコードでは、example.comというドメインを/var/www/exampleというディレクトリに設定しています。このように、各ドメインに対して別々のdocumentrootを指定します。

### 3. サーバーの再起動

設定ファイルを保存したら、apacheのサーバーを再起動します。

```bash
sudo service apache2 restart
```

これにより、新しい設定が適用されます。

## ドメイン別のディレクトリ構造の作成方法

仮想ホストを設定したら、各ドメインのディレクトリ構造を作成します。これにより、各ドメインのコンテンツを個別に管理することができます。

### 1. ディレクトリの作成

以下のコマンドを使用して、各ドメインに対応するディレクトリを作成します。

```bash
sudo mkdir /var/www/example
sudo mkdir /var/www/example2
```

上記の例では、example.comとexample2.comに対応するディレクトリを作成しています。

### 2. ディレクトリの所有者とパーミッションの設定

ディレクトリを作成したら、所有者とパーミッションを設定します。これにより、apacheのプロセスがディレクトリにアクセスできるようになります。

```bash
sudo chown -r www-data:www-data /var/www/example
sudo chown -r www-data:www-data /var/www/example2
sudo chmod -r 755 /var/www/example
sudo chmod -r 755 /var/www/example2
```

上記の例では、www-dataというユーザーとグループがディレクトリの所有者になり、755のパーミッションが設定されています。

### 3. インデックスページの作成

それぞれのディレクトリ内にインデックスページを作成し、ブラウザでアクセスしたときに表示されるようにします。

```bash
echo "hello, example.com!" | sudo tee /var/www/example/index.html
echo "hello, example2.com!" | sudo tee /var/www/example2/index.html
```

上記の例では、example.comとexample2.comに対応するインデックスページが作成されます。

## サブドメインの仮想ホストの設定手順

仮想ホストは、サブドメインに対しても設定することができます。サブドメインとは、メインドメインの下に作成されるドメインのことです。

### 1. dnsの設定

まず、サブドメインに対応するdnsの設定を行います。これにより、サブドメインがメインドメインのipアドレスに紐付けられます。

### 2. サーバーの設定

次に、apacheの設定ファイル（httpd.conf）を編集して、サブドメインの仮想ホストを追加します。

```apacheconf
# サブドメインの仮想ホストの設定
<virtualhost *:80>
    servername subdomain.example.com
    documentroot /var/www/subdomain
</virtualhost>
```

上記のコードでは、subdomain.example.comというサブドメインを/var/www/subdomainというディレクトリに設定しています。

### 3. サーバーの再起動

設定ファイルを保存したら、apacheのサーバーを再起動します。

```bash
sudo service apache2 restart
```

これにより、新しい設定が適用されます。

## ssl証明書の適用とhttps接続の設定方法

ウェブサイトのセキュリティを向上させるためには、ssl証明書を適用し、https接続を設定することが重要です。以下では、apacheでssl証明書を適用する手順を説明します。

### 1. ssl証明書の取得

まず、ssl証明書を取得します。ssl証明書は認証局から購入することができます。または、let's encryptなどの無料の証明書を使用することもできます。

### 2. 証明書の配置

取得したssl証明書をapacheの設定ディレクトリに配置します。

```bash
sudo cp example.crt /etc/apache2/ssl/
sudo cp example.key /etc/apache2/ssl/
```

上記の例では、example.crtとexample.keyというssl証明書ファイルを/etc/apache2/ssl/ディレクトリに配置しています。

### 3. 設定の変更

apacheの設定ファイル（httpd.conf）を編集して、ssl証明書を適用する設定を追加します。

```apacheconf
# ssl証明書の適用設定
<virtualhost *:443>
    servername example.com
    documentroot /var/www/example
    sslengine on
    sslcertificatefile /etc/apache2/ssl/example.crt
    sslcertificatekeyfile /etc/apache2/ssl/example.key
</virtualhost>
```

上記のコードでは、ポート443でssl証明書を適用する設定が追加されています。

### 4. サーバーの再起動

設定ファイルを保存したら、apacheのサーバーを再起動します。

```bash
sudo service apache2 restart
```

これにより、新しい設定が適用されます。

## 仮想ホストのテストとトラブルシューティングのポイント

仮想ホストの設定が完了したら、ブラウザで各ドメインにアクセスして動作を確認しましょう。もし、正しく動作しない場合は以下の点を確認してみてください。

- ドメインのdns設定が正しく行われているか確認してください。
- apacheの設定ファイル（httpd.conf）にエラーがないか確認してください。
- ディレクトリ、ファイルのパーミッションが正しいか確認してください。
- ssl証明書の設定が正しく行われているか確認してください。

上記のポイントを確認しても問題が解決しない場合は、apacheのエラーログを確認してみてください。エラーログは通常、/var/log/apache2/error.logに保存されています。

## conclusion

以上、apacheの仮想ホスト機能を使用して複数のドメインを運用する方法をご紹介しました。apacheの仮想ホスト機能を利用することで、複数のドメインを簡単に運用することができます。ぜひ、実際に試してみてください。

参考：
- [apache virtual host documentation](https://httpd.apache.org/docs/2.4/vhosts/)
- [how to set up apache virtual hosts on ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-18-04)

　

## 【Apache】関連のまとめ
https://hack-note.com/summary/apache-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

