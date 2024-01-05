<!--
title: 【aws cli】セキュリティグループの設定と管理
tags: aws,cli
id: 
private: false
-->

## aws cli】セキュリティグループの設定と管理

こんにちは。今回は、aws cliについて初心者エンジニアに向けて、セキュリティグループの設定と管理方法について解説します。

## はじめに

aws cliは、aws command line interfaceのことで、ターミナルやコマンドプロンプトを利用してawsの各種サービスを操作することができます。セキュリティグループは、awsのネットワークレベルのファイアウォールの役割を果たし、インスタンスやアプリケーションへのアクセスを制御するための重要な機能です。今回は、aws cliを使用してセキュリティグループの作成、ルールの設定・編集・削除、適用と関連リソースへの割り当て、ロギングと監視の方法について説明します。

## aws cliでのセキュリティグループの作成手順

セキュリティグループを作成するためには、以下のaws cliコマンドを使用します。

```bash
aws ec2 create-security-group --group-name mysecuritygroup --description "my security group"
```

上記のコマンドでは、`create-security-group`というサブコマンドを使用し、`--group-name`オプションでセキュリティグループの名前を指定し、`--description`オプションでセキュリティグループの説明を指定します。

## セキュリティグループのインバウンドルールとアウトバウンドルールの設定

セキュリティグループのインバウンドルールとアウトバウンドルールの設定は、`authorize-security-group-ingress`と`authorize-security-group-egress`というaws cliのサブコマンドを使用します。

まず、インバウンドルールを設定するためには、以下のコマンドを使用します。

```bash
aws ec2 authorize-security-group-ingress --group-name mysecuritygroup --protocol tcp --port 22 --cidr 203.0.113.0/24
```

上記のコマンドでは、`authorize-security-group-ingress`というサブコマンドを使用し、`--group-name`オプションでセキュリティグループの名前を指定し、`--protocol`オプションで通信プロトコルを指定し、`--port`オプションで通信ポートを指定します。

同様に、アウトバウンドルールを設定するためには、以下のコマンドを使用します。

```bash
aws ec2 authorize-security-group-egress --group-name mysecuritygroup --protocol tcp --port 80 --cidr 0.0.0.0/0
```

上記のコマンドでは、`authorize-security-group-egress`というサブコマンドを使用し、`--group-name`オプションでセキュリティグループの名前を指定し、`--protocol`オプションで通信プロトコルを指定し、`--port`オプションで通信ポートを指定します。

## aws cliを使用したセキュリティグループのルールの編集と削除

セキュリティグループのルールを編集するためには、`update-security-group-rule-descriptions-ingress`と`update-security-group-rule-descriptions-egress`というaws cliのサブコマンドを使用します。

まず、インバウンドルールの説明を変更するためには、以下のコマンドを使用します。

```bash
aws ec2 update-security-group-rule-descriptions-ingress --group-name mysecuritygroup --protocol tcp --port 22 --description "allow ssh access"
```

上記のコマンドでは、`update-security-group-rule-descriptions-ingress`というサブコマンドを使用し、`--group-name`オプションでセキュリティグループの名前を指定し、`--protocol`オプションで通信プロトコルを指定し、`--port`オプションで通信ポートを指定し、`--description`オプションで新しい説明を指定します。

同様に、アウトバウンドルールの説明を変更するためには、以下のコマンドを使用します。

```bash
aws ec2 update-security-group-rule-descriptions-egress --group-name mysecuritygroup --protocol tcp --port 80 --description "allow http access"
```

上記のコマンドでは、`update-security-group-rule-descriptions-egress`というサブコマンドを使用し、`--group-name`オプションでセキュリティグループの名前を指定し、`--protocol`オプションで通信プロトコルを指定し、`--port`オプションで通信ポートを指定し、`--description`オプションで新しい説明を指定します。

セキュリティグループのルールを削除するためには、`revoke-security-group-ingress`と`revoke-security-group-egress`というaws cliのサブコマンドを使用します。

まず、インバウンドルールを削除するためには、以下のコマンドを使用します。

```bash
aws ec2 revoke-security-group-ingress --group-name mysecuritygroup --protocol tcp --port 22 --cidr 203.0.113.0/24
```

上記のコマンドでは、`revoke-security-group-ingress`というサブコマンドを使用し、`--group-name`オプションでセキュリティグループの名前を指定し、`--protocol`オプションで通信プロトコルを指定し、`--port`オプションで通信ポートを指定します。

同様に、アウトバウンドルールを削除するためには、以下のコマンドを使用します。

```bash
aws ec2 revoke-security-group-egress --group-name mysecuritygroup --protocol tcp --port 80 --cidr 0.0.0.0/0
```

上記のコマンドでは、`revoke-security-group-egress`というサブコマンドを使用し、`--group-name`オプションでセキュリティグループの名前を指定し、`--protocol`オプションで通信プロトコルを指定し、`--port`オプションで通信ポートを指定します。

## セキュリティグループの適用と関連リソースへの割り当て方法

セキュリティグループをインスタンスやアプリケーションに適用するためには、以下のaws cliコマンドを使用します。

```bash
aws ec2 authorize-security-group-ingress --group-name mysecuritygroup --protocol tcp --port 22 --source-group myothersecuritygroup
```

上記のコマンドでは、`authorize-security-group-ingress`というサブコマンドを使用し、`--group-name`オプションでセキュリティグループの名前を指定し、`--protocol`オプションで通信プロトコルを指定し、`--port`オプションで通信ポートを指定し、`--source-group`オプションで関連するセキュリティグループの名前を指定します。

## aws cliでのセキュリティグループのロギングと監視

セキュリティグループのログを取得するためには、aws cloudtrailを使用します。cloudtrailを有効化し、ロググループを作成すると、セキュリティグループのログをリアルタイムで監視することができます。

詳細な手順については、以下のブログ記事を参考にしてください。

- [aws cli でセキュリティグループの設定と管理を行う方法](https://example.com/article1)
- [aws cli を使用してセキュリティグループのルールを作成、編集、削除する方法](https://example.com/article2)

以上が、aws cliを使用したセキュリティグループの設定と管理方法の紹介でした。aws cliを使えるようになると、より効率的にawsのリソースを操作できるので、ぜひ活用してみてください。

　

## 【aws cli】関連のまとめ
https://hack-note.com/summary/aws-cli-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

