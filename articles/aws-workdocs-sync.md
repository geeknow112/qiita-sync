<!--
title: 【基礎】aws workdocsにバックアップする時の同期について
tags: aws,workdocs
id: 
private: false
-->

こんにちは。今回は、awsについて初心者エンジニアに向けて、aws workdocsにデータをバックアップする方法と、同期、差分同期、継続的にバックアップする方法について解説します。

## aws workdocs にデータをバックアップするには
aws workdocsは、企業内でドキュメントを共有・管理しやすくするためのサービスです。このworkdocsにバックアップを取る場合、まずはaws consoleにログインし、workdocsのページに移動します。ここで、「ユーザーの追加」をし、バックアップするためのユーザーアカウントを作成してください。

次に、バックアップするフォルダを作成します。workdocsのページで「フォルダの追加」をし、バックアップする内容に応じて任意の名前をつけます。

そして、aws cliをインストールします。インストール方法については、[こちらのブログ記事](https://qiita.com/memakura/items/68c650b0dfbd4ca60623)が参考になります。

aws cliをインストールしたら、まずはアクセスキーの設定を行います。「aws configure」コマンドを実行すると、アクセスキーを聞かれるので、設定してください。

これで、aws workdocsにバックアップを取る準備が整いました。

## aws workdocs のバックアップしたファイルの同期方法
aws workdocsにバックアップしたファイルの同期方法についてです。同期には、「aws s3 sync」というコマンドを用います。例えば、以下のようなコマンドで、ローカルファイルの「mydir」フォルダとバックアップ先の「backup/」フォルダを同期することができます。

```
$ aws s3 sync mydir/ s3://mybucket/backup/
```

同期を実行すると、新しく追加されたファイルや変更されたファイルがaws workdocsに自動的にアップロードされ、同時に、aws workdocsにバックアップされているファイルがローカルファイルに自動的にダウンロードされます。

## aws workdocs のバックアップの時の差分同期がされる？
aws workdocsにバックアップを取る場合、差分同期が自動的に実行されます。差分同期とは、変更された部分だけを同期することで、同期時間を短縮できる機能です。例えば、以下のようなコマンドで、先ほどの「aws s3 sync」コマンドを再実行した場合、変更されたファイルや追加されたファイルだけが同期されます。

```
$ aws s3 sync mydir/ s3://mybucket/backup/
```

差分同期は、workdocsとローカルフォルダで変更がある場合に自動的に反映されるため、手動で差分同期を行う必要はありません。

## aws workdocs で継続的にバックアップするには？
aws workdocsで継続的にバックアップするには、バックアップを自動的に実行するようにスケジュールを設定することが必要です。aws cloudwatch eventsを使用することで、一定の頻度でバックアップを定期的に実行することができます。

こちらの[公式ドキュメント](https://docs.aws.amazon.com/ja_jp/amazoncloudwatch/latest/events/whatiscloudwatchevents.html)を参考に、aws cloudwatch eventsの設定を行ってください。

以上、aws workdocsにデータをバックアップするための同期、差分同期、継続的にバックアップする方法について解説しました。

参考記事：
- [aws workdocsの概要](https://aws.amazon.com/jp/workdocs/)
- [aws workdocsによるファイル共有サービスの構築手順](https://qiita.com/key-k/items/6aa018db45a025c3771f)
- [aws cliの使い方を徹底解説してみた](https://qiita.com/memakura/items/68c650b0dfbd4ca60623)

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)

