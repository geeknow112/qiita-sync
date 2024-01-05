<!--
title: 【aws cli】cloudformationスタックの作成と更新
tags: aws,cli
id: 
private: false
-->

## aws cliを使用したcloudformationスタックの作成手順

こんにちは。今回は、aws cliについて初心者エンジニアに向けて、cloudformationスタックの作成と更新方法について解説します。

aws cliとは、aws command line interfaceの略で、コマンドラインからawsの各種サービスを操作するためのツールです。cloudformationは、awsのサービスの1つであり、インフラストラクチャをコードとして扱うことができるサービスです。このcloudformationスタックをaws cliを使用して作成および更新する方法について説明していきます。

### 手順1: cloudformationテンプレートの作成とパラメータの設定方法

まずは、cloudformationテンプレートを作成しましょう。cloudformationテンプレートは、スタックを作成するための設計図のようなもので、yamlまたはjson形式で記述します。

以下のサンプルコードは、ec2インスタンスを作成するcloudformationテンプレートの一部です。このテンプレートでは、インスタンスタイプやキーペアの名前などのパラメータを指定できるようになっています。

```
awstemplateformatversion: "2010-09-09"
resources:
  myec2instance:
    type: "aws::ec2::instance"
    properties:
      imageid: "ami-xxxxxxxx"
      instancetype: !ref instancetype
      keyname: !ref keyname
```

これを、任意のファイル名（例: `template.yaml`）で保存します。

次に、aws cliを使ってcloudformationスタックを作成するコマンドを実行します。以下のサンプルコードは、テンプレートファイルとパラメータを指定してスタックを作成するコマンドです。

```
aws cloudformation create-stack --stack-name mystack --template-body file://template.yaml --parameters parameterkey=instancetype,parametervalue=t2.micro parameterkey=keyname,parametervalue=mykeypair
```

このコマンドでは、`--stack-name`オプションでスタック名を指定し、`--template-body`オプションでテンプレートファイルを指定します。また、`--parameters`オプションでパラメータを指定します。パラメータは、テンプレート内で定義されているパラメータと対応させる必要があります。

### 手順2: aws cliでのcloudformationスタックの更新と変更セットの適用

作成したcloudformationスタックを更新する場合は、`aws cloudformation update-stack`コマンドを使用します。

以下のサンプルコードは、ec2インスタンスのインスタンスタイプを変更するcloudformationテンプレートの一部です。

```
awstemplateformatversion: "2010-09-09"
resources:
  myec2instance:
    type: "aws::ec2::instance"
    properties:
      imageid: "ami-xxxxxxxx"
      instancetype: !ref newinstancetype
      keyname: !ref keyname
```

まず、テンプレートファイルを更新します。そして、以下のコマンドを実行してスタックを更新します。

```
aws cloudformation update-stack --stack-name mystack --template-body file://updated-template.yaml --parameters parameterkey=newinstancetype,parametervalue=t3.micro
```

このコマンドでは、更新後のテンプレートファイルを指定し、`--parameters`オプションで新しいパラメータを指定します。

また、cloudformationでは、変更セットを作成してから適用することで、変更の影響範囲を事前に確認できます。変更セットを作成するコマンドは以下の通りです。

```
aws cloudformation create-change-set --stack-name mystack --change-set-name mychangeset --template-body file://updated-template.yaml --parameters parameterkey=newinstancetype,parametervalue=t3.micro
```

変更セットを作成したら、以下のコマンドを実行して変更セットを適用します。

```
aws cloudformation execute-change-set --stack-name mystack --change-set-name mychangeset
```

### 手順3: cloudformationスタックのステータスの監視とロールバック処理

cloudformationスタックの作成や更新は、時間がかかることがあります。そのため、ステータスの監視を行い、スタックの作成や更新が成功したかどうかを確認する必要があります。

以下のコマンドは、スタックのステータスを取得するためのコマンドです。

```
aws cloudformation describe-stacks --stack-name mystack
```

スタックのステータスが`create_complete`または`update_complete`であれば、作成や更新が成功しています。それ以外の場合は、エラーが発生している可能性があります。

また、cloudformationでは、ロールバック機能も提供されています。スタックの作成や更新中にエラーが発生した場合、自動的にロールバックが行われ、以前のスタックの状態に戻ります。ロールバックを無効にする場合は、テンプレート内の`rollbackconfiguration`セクションの設定を変更します。

### 手順4: aws cliを使ったcloudformationスタックの削除とリソースのクリーンアップ

cloudformationスタックを削除する場合は、`aws cloudformation delete-stack`コマンドを使用します。

```
aws cloudformation delete-stack --stack-name mystack
```

このコマンドを実行すると、指定したスタックが削除されます。

ただし、スタックの削除だけではリソースが完全にクリーンアップされない場合があります。cloudformationでは、削除ポリシーを指定することができます。削除ポリシーは、スタックの削除時にリソースを再帰的に削除するかどうかを設定するものです。

以下のコマンドは、スタックの削除時にリソースを再帰的に削除する削除ポリシーを指定するコマンドです。

```
aws cloudformation delete-stack --stack-name mystack --retain-resources logicalresourceid1 logicalresourceid2
```

`--retain-resources`オプションを使用して、削除をスキップしたいリソースの論理idを指定します。

以上が、aws cliを使用したcloudformationスタックの作成と更新方法についての解説でした。初心者エンジニアの方にとって参考になれば幸いです。

参考:
- [aws cli document](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html)
- [aws cloudformation user guide](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/index.html)

　

## 【aws cli】関連のまとめ
https://hack-note.com/summary/aws-cli-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

