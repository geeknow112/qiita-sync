<!--
title:   【aws cli】vpcの作成とネットワーキング
tags:    AWS,CLI
id:      d69fbec0e11325655587
private: false
-->


## aws cliを使用したvpcの作成手順

こんにちは。今回は、aws cliについて初心者エンジニアに向けて、vpcの作成とネットワーキングについて解説します。

aws cli（command line interface）は、awsの各種サービスをコマンドラインから操作するためのツールです。guiでの操作に比べて直感的ではありませんが、一度コマンドを覚えてしまえば、繰り返し操作を行う際には非常に効率的です。

今回は、vpc（virtual private cloud）の作成からネットワーキングまでをaws cliを使用して実施します。

### 参考記事：
- [【aws cli】vpcの作成方法](https://example.com/blog1)
- [【aws cli】vpcの設定手順の解説](https://example.com/blog2)


まず最初に、vpcの作成手順を解説します。

### 1. aws cliのインストール

aws cliを利用するためには、まずaws cliをインストールする必要があります。

```shell
$ pip install awscli
```

### 2. aws cliの設定

aws cliを使うためには、awsのアクセスキーとシークレットキーが必要です。これらの情報を設定するためには、以下のコマンドを実行します。

```shell
$ aws configure
aws access key id [none]: your_access_key
aws secret access key [none]: your_secret_access_key
default region name [none]: us-west-2
default output format [none]: json
```

### 3. vpcの作成

aws cliを使ってvpcを作成するには、以下のコマンドを実行します。

```shell
$ aws ec2 create-vpc --cidr-block 10.0.0.0/16
```

上記の例では、cidrブロックが`10.0.0.0/16`のvpcを作成します。

### 4. サブネットの作成とルートテーブルの設定

次に、vpc内にサブネットを作成し、ルートテーブルを設定します。

まずはサブネットの作成です。

```shell
$ aws ec2 create-subnet --vpc-id your_vpc_id --cidr-block 10.0.0.0/24
```

上記の例では、cidrブロックが`10.0.0.0/24`のサブネットを作成します。

次に、ルートテーブルの作成と関連付けを行います。

```shell
$ aws ec2 create-route-table --vpc-id your_vpc_id
$ aws ec2 associate-route-table --subnet-id your_subnet_id --route-table-id your_route_table_id
```

上記の例では、vpcのid、サブネットのid、ルートテーブルのidを指定して関連付けを行います。

### 5. vpcピアリングとプライベートリンクの構成

vpc間の通信を実現するために、vpcピアリングやプライベートリンクの構成が必要な場合があります。

vpcピアリングを構成するには、以下のコマンドを実行します。

```shell
$ aws ec2 create-vpc-peering-connection --vpc-id your_vpc_id --peer-vpc-id peer_vpc_id
```

上記の例では、vpc間のピアリング接続を作成します。vpcのidと接続先のvpcのidを指定します。

プライベートリンクを構成するには、以下のコマンドを実行します。

```shell
$ aws ec2 create-vpc-endpoint --vpc-id your_vpc_id --service-name service_name
```

上記の例では、vpcエンドポイントを作成します。vpcのidとエンドポイントするサービスの名前を指定します。

### 6. セキュリティグループとネットワークaclの管理

vpc内の通信制御を行うために、セキュリティグループやネットワークaclを設定する必要があります。

セキュリティグループを作成するには、以下のコマンドを実行します。

```shell
$ aws ec2 create-security-group --vpc-id your_vpc_id --group-name group_name --description description
```

上記の例では、vpc内にセキュリティグループを作成します。vpcのid、グループ名、説明を指定します。

ネットワークaclを作成するには、以下のコマンドを実行します。

```shell
$ aws ec2 create-network-acl --vpc-id your_vpc_id
```

上記の例では、vpc内にネットワークaclを作成します。vpcのidを指定します。

### 7. vpcエンドポイントの作成と接続

最後に、vpcエンドポイントを作成し、他のサービスと接続します。

```shell
$ aws ec2 create-vpc-endpoint --vpc-id your_vpc_id --service-name service_name
```

上記の例では、vpcエンドポイントの作成を行います。vpcのidとエンドポイントするサービスの名前を指定します。

このように、aws cliを使ってvpcの作成とネットワーキングの設定を行うことができます。初心者の方でも、この手順に従って実行すればスムーズにvpcの構築を行うことができるでしょう。

今回はaws cliを使用したvpcの作成手順について解説しましたが、他にもaws cliには様々な機能があります。ぜひ、公式ドキュメントや参考記事を参考にしてaws cliの活用方法を学んでみてください。



## 【aws cli】関連のまとめ
https://hack-note.com/summary/aws-cli-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
