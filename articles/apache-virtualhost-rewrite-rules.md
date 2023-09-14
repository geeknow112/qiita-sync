<!--
title:   【apache】rewriteルールの活用：virtualhostでurlリダイレクトを設定する方法
tags:    Apache,VirtualHost
id:      4ff7f04127d75e16cb60
private: false
-->


## urlリダイレクトの基本：rewriteルールの概要と設定方法

apacheにおいてurlリダイレクトを設定するためには、rewriteルールを使用します。rewriteルールは、urlのリクエストを受け取って、別のurlに転送するためのルールを定義するものです。

rewriteルールを使用することで、urlの書き換えやリダイレクトを行うことができます。具体的には、特定のurlにアクセスがあった場合に、別のurlに転送するよう設定することができます。

まずは、rewriteルールの設定方法について説明します。

apacheの設定ファイルであるhttpd.confファイルに、以下のような設定を追加します。

```
<virtualhost *:80>
    servername yourdomain.com
    documentroot /var/www/html

    rewriteengine on
    rewritecond %{http_host} ^www\.yourdomain\.com [nc]
    rewriterule ^(.*)$ http://yourdomain.com/$1 [l,r=301]
</virtualhost>
```

上記の設定では、yourdomain.comへのアクセスがあった場合に、www.yourdomain.comへのリダイレクトが行われます。

この設定では、rewriteengineディレクティブをonに設定し、rewritecondディレクティブを使用してリダイレクト条件を指定し、rewriteruleディレクティブを使用してリダイレクト先のurlを指定しています。

## ドメイン別のurlリダイレクト設定手法

apacheでは、複数のドメインに対して異なるurlリダイレクトを設定することも可能です。

以下のサンプルコードでは、example.comとexample.jpという2つのドメインに対して異なるリダイレクトを設定しています。

```
<virtualhost *:80>
    servername example.com
    documentroot /var/www/html

    rewriteengine on
    rewriterule ^old-page$ /new-page.html [r=301]
</virtualhost>

<virtualhost *:80>
    servername example.jp
    documentroot /var/www/html

    rewriteengine on
    rewriterule ^old-file$ /new-file.html [r=301]
</virtualhost>
```

上記の例では、example.comの「/old-page」へのアクセスが「/new-page.html」へリダイレクトされるように設定されており、example.jpの「/old-file」へのアクセスが「/new-file.html」へリダイレクトされるよう設定されています。

このように、ドメインごとに異なるurlリダイレクト設定を行うことができます。

## リダイレクトの種類：301リダイレクトと302リダイレクトの違い

リダイレクトには、301リダイレクトと302リダイレクトの2つの種類があります。

301リダイレクトは、永久的なリダイレクトを表します。ブラウザやクローラーは、301リダイレクトがあった場合に、リダイレクト先のurlを新しい正規のurlとして記憶し、以降は直接新しいurlにアクセスします。

302リダイレクトは、一時的なリダイレクトを表します。ブラウザやクローラーは、302リダイレクトがあった場合に、リダイレクト先のurlを新しい一時的なurlとして記憶し、以降は元のurlにアクセスします。

以下のサンプルコードでは、301リダイレクトと302リダイレクトの設定例を示しています。

```
<virtualhost *:80>
    servername example.com
    documentroot /var/www/html

    rewriteengine on
    rewriterule ^old-page$ /new-page.html [r=301]
    rewriterule ^temporary-page$ /temporary-page.html [r=302]
</virtualhost>
```

上記の例では、「/old-page」へのアクセスが301リダイレクトで「/new-page.html」へリダイレクトされ、ブラウザやクローラーはこのリダイレクトを永続的なものとして記憶します。一方、「/temporary-page」へのアクセスが302リダイレクトで「/temporary-page.html」へリダイレクトされ、ブラウザやクローラーはこのリダイレクトを一時的なものとして記憶します。

適切なリダイレクトの種類を選択することで、効果的なurlの管理ができます。

## ワイルドカードと正規表現を使用した柔軟なリダイレクト設定

rewriteルールでは、ワイルドカードや正規表現を使用して、柔軟なリダイレクト設定を行うことができます。

以下のサンプルコードでは、urlのパスに対して正規表現を使用してリダイレクトを設定しています。

```
<virtualhost *:80>
    servername example.com
    documentroot /var/www/html

    rewriteengine on
    rewriterule ^category/(.*)$ /new-category/$1 [r=301]
    rewriterule ^product/(.*)$ /new-product/$1 [r=301]
</virtualhost>
```

上記の例では、urlのパスに「category/」や「product/」が含まれている場合に、それぞれ「/new-category/」や「/new-product/」にリダイレクトされるよう設定されています。

このように、正規表現を使用することで、パターンに一致する複数のurlに対して一括でリダイレクトを設定することができます。

## リダイレクトのテストとデバッグ：エラーのトラブルシューティング手順

rewriteルールを設定する際には、リダイレクトのテストとデバッグを行うことが重要です。リダイレクト設定に間違いがあった場合、意図しないリダイレクトが発生する可能性があります。

以下の手順を参考に、リダイレクトのテストとデバッグを行ってください。

1. リダイレクトを設定したapacheサーバーにアクセスし、正しいurlへのリダイレクトが発生することを確認します。
2. ブラウザの開発者ツールを使用して、httpリクエストとレスポンスのヘッダーを確認します。リダイレクトのステータスコードやリダイレクト先のurlが正しいことを確認します。
3. エラーログを確認し、設定に関連するエラーメッセージがないかをチェックします。エラーメッセージがある場合は、設定に誤りがある可能性があります。

以上の手順を踏むことで、リダイレクトの設定が正しく行われているかを確認することができます。

まとめると、apacheのvirtualhostでurlリダイレクトを設定するためには、rewriteルールを使用します。ドメインごとに異なるリダイレクトを行う場合や、正規表現を使用して柔軟なリダイレクト設定を行う場合も可能です。設定後には、リダイレクトのテストとデバッグを行い、意図した通りのリダイレクトが行われるかを確認することが重要です。

参考記事：
- [apache urlリダイレクトの基本 - qiita](https://qiita.com/daisukehiratake/items/affd998e7d785b97c1db)
- [apacheのrewriteruleでurlを書き換える - qiita](https://qiita.com/civic/items/6149b35809ff94c2b057)



## 【Apache】関連のまとめ
https://hack-note.com/summary/apache-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
