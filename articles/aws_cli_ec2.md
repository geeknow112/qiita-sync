<!--
title: 【AWS CLI】EC2インスタンスの起動と停止
tags: aws,cli
id: 
private: false
-->

## aws cliを使用したec2インスタンスの起動手順

aws cli（amazon web services command line interface）を使用することで、コマンドラインからec2インスタンスを簡単に起動することができます。aws cliを活用することで、guiを使用せずに効率的にec2インスタンスを操作することができます。

aws cliを使用したec2インスタンスの起動手順を説明します。

### 1. aws cliのインストール

まずはじめに、aws cliをインストールする必要があります。aws cliのインストール方法は以下の公式ドキュメントを参考にしてください。

- [aws cli のインストール - linux や macos](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/install-linux-macos.html)
- [aws cli のインストール - windows](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/install-windows.html)

### 2. aws cliの設定

aws cliをインストールした後、設定を行う必要があります。以下のコマンドを実行し、aws cliの設定を行ってください。

```
aws configure
```

コマンドを実行すると、以下の項目を入力するように求められます。

- aws access key id: awsのアクセスキーidを入力します。
- aws secret access key: awsのシークレットアクセスキーを入力します。
- default region name: 使用するリージョンを入力します。
- default output format: 出力形式を入力します。（例: json）

これにより、設定が完了します。

### 3. ec2インスタンスの起動

aws cliを使用してec2インスタンスを起動するには、以下のコマンドを実行します。

```
aws ec2 run-instances --image-id ami-xxxxxxxx --instance-type t2.micro --key-name my-key-pair
```

- `--image-id` : 使用するamazon machine image（ami）のidを指定します。
- `--instance-type` : 起動するインスタンスのタイプを指定します。
- `--key-name` : インスタンスに関連付けられるキーペアの名前を指定します。

このコマンドを実行することで、ec2インスタンスの起動が行われます。

以上が、aws cliを使用したec2インスタンスの起動手順です。より詳しい情報については、以下の参考記事をご覧ください。

- [aws cli を使用して ec2 インスタンスを起動する](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-ec2-launch.html)

## ec2インスタンスのタイプとサイズの選択方法

ec2インスタンスのタイプとサイズの選択は、アプリケーションの要件や予算、利用目的によって異なります。aws cliを使用してec2インスタンスを起動する際には、適切なタイプとサイズを選択する必要があります。

### インスタンスタイプの選択

インスタンスタイプは、インスタンスが持つリソース（cpu、メモリ、ネットワーク）や機能（gpu、fpgaなど）によって異なります。適切なインスタンスタイプを選択するためには、以下のポイントを考慮する必要があります。

- 使用用途：インスタンスがどのような用途に使用されるかによって、必要なリソースが異なります。例えば、データベースサーバーには高いメモリが必要ですが、webサーバーにはcpuパワーが重要です。
- ユースケースに合わせたインスタンスタイプ：awsでは、各ユースケースに適したインスタンスファミリーを提供しており、それぞれ異なる特性を持っています。例えば、コンピューティングを重視する場合には、「c5」といったファミリーを選択することができます。
- 無料利用枠の活用：awsでは、一部のインスタンスタイプを無料で利用することができます。開発やテスト環境などで利用する場合には、無料利用枠の範囲内でインスタンスを選択することができます。

### インスタンスサイズの選択

インスタンスサイズは、インスタンスが持つリソースの量を示します。インスタンスのサイズは、以下の要素を考慮して選択する必要があります。

- cpuパフォーマンス：インスタンスサイズによって、利用可能なcpuコアが異なります。アプリケーションの要件に合わせて適切なcpuパフォーマンスを選択することが重要です。
- メモリ：インスタンスサイズによって、利用可能なメモリサイズが異なります。アプリケーションが大量のメモリを必要とする場合には、メモリに優れたインスタンスサイズを選択する必要があります。
- ストレージ：インスタンスサイズによって、利用可能なストレージ容量やストレージのi/o性能が異なります。アプリケーションの要件に合わせて適切なストレージを選択することが重要です。

インスタンスタイプとサイズの選択は、アプリケーションの要件や予算、利用目的によって異なります。詳細な情報については、以下の参考記事をご覧ください。

- [amazon ec2 インスタンスタイプ](https://aws.amazon.com/jp/ec2/instance-types/)
- [ec2 インスタンスのサイズの選択](https://aws.amazon.com/jp/premiumsupport/knowledge-center/ec2-instance-size/)

## aws cliでのec2インスタンスの起動時のユーザーデータの設定

ec2インスタンスを起動する際に、ユーザーデータを設定することができます。ユーザーデータを指定することで、インスタンスの起動時に自動的にスクリプトやコマンドを実行することができます。

aws cliを使用してec2インスタンスを起動する際に、ユーザーデータを設定する方法を説明します。

### ユーザーデータの作成

まず、ユーザーデータを作成します。ユーザーデータは、スクリプトやコマンドをテキストファイルとして作成します。

以下は、ユーザーデータの例です。

```
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
```

上記のユーザーデータでは、インスタンス起動時に `yum` コマンドを用いてパッケージの更新とインストールを行い、`httpd` サーバを起動するスクリプトを実行しています。

### ec2インスタンスの起動とユーザーデータの設定

次に、ec2インスタンスを起動する際にユーザーデータを設定します。以下のコマンドを使用します。

```
aws ec2 run-instances --image-id ami-xxxxxxxx --instance-type t2.micro --key-name my-key-pair --user-data file://user-data.txt
```

- `--image-id` : 使用するamazon machine image（ami）のidを指定します。
- `--instance-type` : 起動するインスタンスのタイプを指定します。
- `--key-name` : インスタンスに関連付けられるキーペアの名前を指定します。
- `--user-data file://user-data.txt` : ユーザーデータを設定するためのオプションです。`file://` を接頭辞としてテキストファイルを指定します。

このコマンドを実行することで、ec2インスタンスの起動とユーザーデータの設定が行われます。

以上が、aws cliでのec2インスタンスの起動時のユーザーデータの設定方法です。詳細な情報については、以下の参考記事をご覧ください。

- [aws cli を使用して ec2 インスタンスを起動する](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-ec2-launch.html)

## ec2インスタンスのステータスの監視と制御方法

ec2インスタンスのステータスの監視と制御は、適切な運用と管理のために不可欠な要素です。aws cliを使用することで、コマンドラインからec2インスタンスのステータスを監視し、必要に応じて制御することができます。

### ステータスの監視

ec2インスタンスのステータスを監視するには、以下のコマンドを使用します。

```
aws ec2 describe-instance-status --instance-ids i-xxxxxxxx
```

- `--instance-ids` : 監視したいインスタンスのidを指定します。

このコマンドを実行すると、指定したインスタンスのステータス情報が表示されます。例えば、インスタンスが実行中であるか、停止中であるか、エラーが発生しているかなどが表示されます。

### ステータスの制御

ec2インスタンスのステータスを制御するには、以下のコマンドを使用します。

#### インスタンスの停止

```
aws ec2 stop-instances --instance-ids i-xxxxxxxx
```

- `--instance-ids` : 停止したいインスタンスのidを指定します。

このコマンドを実行すると、指定したインスタンスが停止されます。

#### インスタンスの再起動

```
aws ec2 reboot-instances --instance-ids i-xxxxxxxx
```

- `--instance-ids` : 再起動したいインスタンスのidを指定します。

このコマンドを実行すると、指定したインスタンスが再起動されます。

以上が、ec2インスタンスのステータスの監視と制御方法です。詳細な情報については、以下の参考記事をご覧ください。

- [describe-instance-status (aws cli command reference)](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-instance-status.html)
- [stop-instances (aws cli command reference)](https://docs.aws.amazon.com/cli/latest/reference/ec2/stop-instances.html)
- [reboot-instances (aws cli command reference)](https://docs.aws.amazon.com/cli/latest/reference/ec2/reboot-instances.html)

## aws cliを使ったec2インスタンスの停止と再起動

aws cliを使用してec2インスタンスの停止と再起動を行うことができます。これにより、コマンドラインから簡単にインスタンスの管理を行うことができます。

### インスタンスの停止

ec2インスタンスを停止するには、以下のコマンドを使用します。

```
aws ec2 stop-instances --instance-ids i-xxxxxxxx
```

- `--instance-ids` : 停止したいインスタンスのidを指定します。

このコマンドを実行すると、指定したインスタンスが停止されます。

### インスタンスの再起動

ec2インスタンスを再起動するには、以下のコマンドを使用します。

```
aws ec2 reboot-instances --instance-ids i-xxxxxxxx
```

- `--instance-ids` : 再起動したいインスタンスのidを指定します。

このコマンドを実行すると、指定したインスタンスが再起動されます。

以上が、aws cliを使ったec2インスタンスの停止と再起動の手順です。詳細な情報については、以下の参考記事をご覧ください。

- [stop-instances (aws cli command reference)](https://docs.aws.amazon.com/cli/latest/reference/ec2/stop-instances.html)
- [reboot-instances (aws cli command reference)](https://docs.aws.amazon.com/cli/latest/reference/ec2/reboot-instances.html)

## まとめ

今回は、aws cliについて初心者エンジニアに向けて、ec2インスタンスの起動と停止について解説しました。aws cliを使用することで、コマンドラインから簡単にec2インスタンスの操作が行えます。

具体的には、aws cliをインストールし、設定を行った後、ec2インスタンスの起動と停止のコマンドを実行することで操作が行えます。また、インスタンスのタイプとサイズの選択やユーザーデータの設定方法、ステータスの監視と制御方法についても説明しました。

　

## 【AWS CLI】関連のまとめ
https://hack-note.com/summary/aws-cli-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)


