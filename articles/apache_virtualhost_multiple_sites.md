<!--
title: 【apache】複数のサイトをホストするためのvirtualhostの設定方法
tags: apache,virtualhost,aws,lightsail,let's_encrypt,ssl
id: 
private: false
-->

こんにちは。今回は、apacheについて初心者エンジニアに向けて、複数のサイトをホストするためのvirtualhostの設定方法についてご説明します。

## virtualhostの基本概念と設定手順
apacheのvirtualhostは、1台のサーバー上で複数のウェブサイトをホストするための機能です。複数のipアドレスを使用する場合と同じサーバーに複数のドメインをホストする場合でも、virtualhostを使用することで各ドメインごとに異なる設定を行うことができます。

### 設定手順
1. apacheの設定ファイル（httpd.conf）を開きます。
2. namevirtualhostディレクティブを有効にし、ipアドレスとポート番号の指定を行います。
   ```
   namevirtualhost *:80
   ```
3. virtualhostディレクティブを使用して、各サイトの設定を行います。
   ```
   <virtualhost *:80>
     servername www.example.com
     documentroot /var/www/example
   </virtualhost>
   ```
   上記の例では、www.example.comというドメイン名のウェブサイトを/var/www/exampleというディレクトリにホストする設定を行っています。

4. 設定を保存してapacheを再起動します。

## 複数のサイトを識別するためのservernameとserveraliasの活用方法
apacheのvirtualhostを使って複数のサイトをホストする場合、各サイトを識別するためにはservernameディレクティブとserveraliasディレクティブを活用します。

### 設定例
```
<virtualhost *:80>
   servername www.example.com
   serveralias example.com
   documentroot /var/www/example
</virtualhost>
```
上記の例では、www.example.comとexample.comの2つのドメイン名でアクセスされた場合に/var/www/exampleにあるファイルを表示します。

## 各サイトのルートディレクトリの設定とドキュメントルートの指定方法
各サイトのルートディレクトリの設定とドキュメントルートの指定は、virtualhostディレクティブ内でdocumentrootディレクティブを使用して行います。

### 設定例
```
<virtualhost *:80>
   servername www.example.com
   documentroot /var/www/example
</virtualhost>

<virtualhost *:80>
   servername www.example2.com
   documentroot /var/www/example2
</virtualhost>
```
上記の例では、www.example.comとwww.example2.comという2つのドメイン名でアクセスされた場合に、それぞれ/var/www/exampleと/var/www/example2にあるファイルを表示します。

## サイトごとのログの分離とカスタムログフォーマットの設定手法
各サイトのログを分離するためには、customlogディレクティブを使用します。また、ログのフォーマットをカスタマイズするためには、logformatディレクティブを使用します。

### 設定例
```
<virtualhost *:80>
   servername www.example.com
   documentroot /var/www/example
   customlog /var/log/apache2/example-access.log common
</virtualhost>

<virtualhost *:80>
   servername www.example2.com
   documentroot /var/www/example2
   customlog /var/log/apache2/example2-access.log combined
</virtualhost>
```
上記の例では、それぞれのサイトのアクセスログを/var/log/apache2/example-access.logと/var/log/apache2/example2-access.logに記録します。ログのフォーマットはcommonとcombinedを使用していますが、これはapacheのデフォルトのログフォーマットです。

## バーチャルホストの優先順位とデフォルトホストの設定方法
複数のバーチャルホストが設定されている場合、どのバーチャルホストが優先されるかは設定の順序に依存します。また、リクエストされたドメインに対応するバーチャルホストが存在しない場合に表示されるデフォルトのホストも設定することができます。

### 設定手法
1. 設定ファイルの先頭にあるバーチャルホストが最優先となります。
2. リクエストされたドメインに対応するバーチャルホストが存在しない場合、最後のバーチャルホストがデフォルトのホストとして使用されます。
3. デフォルトのホストを設定するためには、設定ファイルの最後に以下のようなバーチャルホストを記述します。
   ```
   <virtualhost _default_:80>
      documentroot /var/www/default
   </virtualhost>
   ```
   上記の例では、リクエストされたドメインに対応するバーチャルホストが存在しない場合に、"/var/www/default"ディレクトリにあるファイルが表示されます。

以上がapacheのvirtualhostを使用して複数のサイトをホストするための設定方法です。ご参考までに、以下に関連するブログ記事のurlを掲載しておきます。

- [how to set up apache virtual hosts on centos 7](https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-centos-7)
- [how to use apache virtual hosts on ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-apache-virtual-hosts-on-ubuntu-18-04)

是非、これらの情報を参考に実際に設定を行ってみてください。apacheのvirtualhostを使えば、1台のサーバー上で複数のウェブサイトをホスティングすることができます。初心者エンジニアのみなさんも、ぜひチャレンジしてみてください。

　

## 【Apache】関連のまとめ
https://hack-note.com/summary/apache-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)


