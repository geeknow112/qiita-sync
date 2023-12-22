<!--
title:   【aws cli】基本コマンドと使い方
tags:    AWS,CLI
id:      030ab545ea2ae219dd87
private: false
-->


## aws cliの基本コマンドと使い方

こんにちは。今回は、aws cliについて初心者エンジニアに向けて、基本コマンドと使い方について解説します。

### aws cliのインストールと環境設定

まずは、aws cliをインストールし、環境設定を行いましょう。

aws cliのインストール方法は、公式ドキュメントを参考にすると良いでしょう。以下のurlからダウンロードできます。

- [https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)

インストールが完了したら、`aws configure`コマンドを実行して、アクセスキーとシークレットアクセスキーを設定します。

```shell
$ aws configure
aws access key id [none]: your_access_key
aws secret access key [none]: your_secret_access_key
default region name [none]: us-west-2
default output format [none]: json
```

アクセスキーとシークレットアクセスキーは、awsのiamユーザーの設定画面から取得できます。

### aws cliでの認証情報の設定方法

aws cliで認証情報を設定する方法は以下の通りです。

1. `aws configure`コマンドを実行して、アクセスキーとシークレットアクセスキーを設定します。先ほどのインストールと環境設定の手順と同じです。

2. 環境変数を使って認証情報を渡す方法もあります。以下は、linuxやmacosで環境変数を設定する方法です。

```shell
export aws_access_key_id=your_access_key
export aws_secret_access_key=your_secret_access_key
```

3. aws cliのプロファイルを使って複数の認証情報を切り替えることもできます。`aws configure --profile`コマンドを実行してプロファイルを指定することができます。

### aws cliでのリージョンの指定と切り替え

aws cliでのリージョンの指定と切り替えは、以下のように行います。

1. `aws configure`コマンドを実行する際に、デフォルトのリージョンを設定することもできます。先ほどのインストールと環境設定の手順と同じです。

2. コマンド実行時に`--region`オプションを指定してリージョンを指定することもできます。

```shell
$ aws s3 ls --region us-east-1
```

3. aws cliのプロファイルを使って、プロファイルごとに異なるリージョンを指定することもできます。

### aws cliでのコマンドの構文とオプションの解説

aws cliのコマンドは次のような構文になっています。

```shell
$ aws <service> <command> [options]
```

- `<service>`: awsの各サービスの識別子を指定します。例えば、s3の操作を行う場合は`s3`を指定します。
- `<command>`: 実行するコマンドを指定します。例えば、オブジェクトの一覧を取得する場合は`ls`を指定します。
- `[options]`: オプションを指定することができます。例えば、`--profile`オプションを使ってプロファイルを指定したり、`--region`オプションを使ってリージョンを指定することができます。

各サービスごとに対応するコマンドやオプションが異なるため、公式ドキュメントを参考にしてください。以下のurlから、各サービスごとのcliリファレンスを確認できます。

- [https://awscli.amazonaws.com/v2/documentation/api/latest/index.html](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html)

### aws cliを使ったリソースの作成と管理

aws cliを使って、さまざまなリソースの作成や管理を行うことができます。以下にいくつかのサンプルコードを示します。

#### s3バケットの作成

```shell
$ aws s3api create-bucket --bucket my-bucket --region us-west-2
```

#### ec2インスタンスの起動

```shell
$ aws ec2 run-instances --image-id ami-12345678 --instance-type t2.micro --key-name my-key --subnet-id subnet-12345678
```

#### rdsデータベースの作成

```shell
$ aws rds create-db-instance --db-instance-identifier my-db --engine mysql --allocated-storage 10 --db-instance-class db.t2.micro --master-username myuser --master-user-password mypassword
```

以上がaws cliの基本コマンドと使い方の解説です。aws cliは様々なサービスを効率的に操作するための強力なツールですので、ぜひ活用してみてください。参考になるブログ記事も以下のurlから閲覧できます。

- [https://qiita.com/tukiyo3/items/c6a1416e926a2be5ae7f](https://qiita.com/tukiyo3/items/c6a1416e926a2be5ae7f)
- [https://dev.classmethod.jp/articles/aws/aws-cli-getting-started/](https://dev.classmethod.jp/articles/aws/aws-cli-getting-started/)



## 【AWS CLI】関連のまとめ
https://hack-note.com/summary/aws-cli-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
