<!--
title: 【解決】aws fsxをセルフマネージドadで起動時にestablishエラー
tags: aws,fsx,active-directory,問題
id: 
private: false
-->

こんにちは。今回は、awsについて初心者エンジニアに向けて、aws fsxをセルフマネージドadで起動時にestablishエラーが発生してしまった場合の解決方法についてお話しします。

aws fsxは、windowsファイルサーバをクイックにデプロイできるサービスで、その中でもセルフマネージドadを使ってfsxを起動することで、オンプレミスのadドメインを維持しながらクラウド上でファイルサーバを運用することができます。しかし、セルフマネージドadで起動する際に、establishエラーが発生してしまうことがあります。

エラーメッセージの内容は、以下の通りです。

```
file system creation failed. 
amazon fsx is unable to establish a connection with your microsoft active directory domain controller(s).
this is because the organizational unit you specified either doesn't exist or isn't accessible to the service account provided. to fix this problem, delete your file system and create a new one specifying an organizational unit
 to which the service account can join the file system
 as recommended in the amazon fsx user guide: https://docs.aws.amazon.com/fsx/latest/windowsguide/self-manage-prereqs.html.
```

このエラーメッセージの原因は、サービスアカウントがフィルタリングされているouへアクセスできず、サービスアカウントがfsxファイルシステムに参加できなかったことにあります。これを解決するには、以下の手順に従ってください。

1. aws managed microsoft adであれば、amazonfsxを起動するouにサービスアカウントを移動することが必要です。
2. ファイルサーバを作成するために使用するコンピューターオブジェクトに必要な権限を付与するグループポリシーオブジェクトを作成します。
3. aws fsx管理コンソールで、既存のファイルシステムを削除し、最初から新しいファイルシステムを作成します。
4. ファイルシステムを作成するときに、サービスアカウントがアクセスできるouを指定してください。

以上の手順に従うことで、establishエラーを解決することができます。

また、より詳細な手順を知りたい方は、以下のaws公式ドキュメントを参照してください。
- amazon fsx for windows file server の自己管理型前提条件
https://docs.aws.amazon.com/ja_jp/fsx/latest/windowsguide/self-manage-prereqs.html

今回は、aws fsxをセルフマネージドadで起動時にestablishエラーが発生した場合の解決方法についてお伝えしました。初心者の方でも理解しやすいように、手順を細かく説明していますので、ぜひ参考にしてください。

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)

