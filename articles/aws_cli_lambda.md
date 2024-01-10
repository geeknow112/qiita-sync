<!--
title:   【aws cli】lambda関数の作成とデプロイ
tags:    AWS,CLI
id:      52f253c8bb54ff39c427
private: false
-->


## aws cliを使用したlambda関数の作成手順

こんにちは。今回は、aws cliについて初心者エンジニアに向けて、lambda関数の作成とデプロイについて解説します。

### aws cliとは

aws cli（command line interface）は、awsのリソースやサービスをコマンドラインから操作するためのツールです。aws management consoleを使用せずに、ターミナル上でawsの操作が行えるため、効率的にawsリソースを管理することができます。

### aws cliのインストール

まずは、aws cliをインストールしましょう。インストール方法は、公式ドキュメント（https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html）を参考にしてください。

### lambda関数の作成

aws cliを使用して、lambda関数を作成する方法を説明します。

#### ステップ1: 関数の作成

以下のコマンドを実行して、lambda関数を作成します。

```bash
aws lambda create-function --function-name my-function --runtime python3.8 --role arn:aws:iam::123456789012:role/service-role/my-function-role --handler lambda_function.lambda_handler --timeout 10 --memory-size 128
```

上記のコマンドでは、以下のパラメータを指定しています。

- `--function-name`：関数の名前を指定します。
- `--runtime`：関数のランタイム（使用するプログラミング言語）を指定します。
- `--role`：関数の実行に使用するiamロールのarnを指定します。
- `--handler`：関数のエントリーポイントを指定します。
- `--timeout`：関数のタイムアウト時間を指定します。
- `--memory-size`：関数のメモリサイズを指定します。

#### ステップ2: コードのアップロード

作成した関数に対して、コードをアップロードします。

```bash
aws lambda update-function-code --function-name my-function --zip-file fileb://path/to/code.zip
```

上記のコマンドでは、`--zip-file`パラメータでアップロードするzipファイルのパスを指定します。

#### ステップ3: 関数のデプロイ

関数をデプロイし、実行できる状態にします。

```bash
aws lambda publish-version --function-name my-function
```

上記のコマンドでは、関数をバージョン管理するために、バージョンを作成します。

以上で、lambda関数の作成とデプロイが完了しました。

## lambda関数のコードの作成とデプロイ方法

lambda関数のコードを作成し、デプロイする方法について説明します。

### ステップ1: コードの作成

まずは、lambda関数のコードを作成しましょう。使用するプログラミング言語に応じたコードを作成します。

以下は、pythonを使用する場合のサンプルコードです。

```python
import json

def lambda_handler(event, context):
    # 受け取ったイベントデータを出力
    print(json.dumps(event))

    # レスポンスを作成
    response = {
        'statuscode': 200,
        'body': json.dumps('hello from lambda!')
    }

    return response
```

### ステップ2: コードのパッケージ化

作成したコードをzipファイルにパッケージ化します。

```bash
zip -r code.zip lambda_function.py
```

上記のコマンドでは、`lambda_function.py`ファイルを`code.zip`という名前のzipファイルにパッケージ化しています。

### ステップ3: コードのデプロイ

パッケージ化されたコードを、lambda関数にデプロイします。

```bash
aws lambda update-function-code --function-name my-function --zip-file fileb://code.zip
```

上記のコマンドでは、`my-function`という名前の関数に、`code.zip`ファイルをアップロードしています。

これで、lambda関数のコードの作成とデプロイが完了しました。

## aws cliでのlambda関数の環境変数と設定の管理

aws cliを使用して、lambda関数の環境変数と設定を管理する方法について説明します。

### ステップ1: 環境変数の設定

以下のコマンドを実行して、lambda関数の環境変数を設定します。

```bash
aws lambda update-function-configuration --function-name my-function --environment variables={key1=value1,key2=value2}
```

上記のコマンドでは、`--environment`パラメータで環境変数を設定しています。複数の環境変数を設定する場合は、keyとvalueの組み合わせをカンマ区切りで指定してください。

### ステップ2: 設定の取得

設定を取得する場合は、以下のコマンドを実行します。

```bash
aws lambda get-function-configuration --function-name my-function
```

上記のコマンドでは、`--function-name`パラメータで関数の名前を指定し、関数の設定を取得しています。

### ステップ3: 設定の更新

設定を更新する場合は、以下のコマンドを実行します。

```bash
aws lambda update-function-configuration --function-name my-function --timeout 15 --memory-size 256
```

上記のコマンドでは、`--timeout`パラメータでタイムアウト時間、`--memory-size`パラメータでメモリサイズを設定しています。

これで、lambda関数の環境変数と設定の管理ができるようになりました。

## lambda関数のトリガーの設定とイベントソースの統合

aws cliを使用して、lambda関数のトリガーの設定とイベントソースの統合を行う方法について説明します。

### ステップ1: トリガーの設定

以下のコマンドを実行して、lambda関数のトリガーを設定します。

```bash
aws lambda create-event-source-mapping --function-name my-function --event-source-arn arn:aws:sqs:ap-northeast-1:123456789012:my-queue --starting-position latest
```

上記のコマンドでは、`--event-source-arn`パラメータでトリガーのarnを指定し、`--starting-position`パラメータでイベントの処理を開始する位置を指定しています。

### ステップ2: トリガーの確認

設定したトリガーの情報を確認する場合は、以下のコマンドを実行します。

```bash
aws lambda list-event-source-mappings --function-name my-function
```

上記のコマンドでは、`--function-name`パラメータで関数の名前を指定し、関数のトリガーの一覧を取得しています。

### ステップ3: トリガーの削除

設定したトリガーを削除する場合は、以下のコマンドを実行します。

```bash
aws lambda delete-event-source-mapping --uuid c1234567-89ab-cdef-0123-456789abcdef
```

上記のコマンドでは、`--uuid`パラメータでトリガーのuuidを指定しています。

これで、lambda関数のトリガーの設定とイベントソースの統合が完了しました。

## aws cliを使ったlambda関数の監視とログの分析

aws cliを使用して、lambda関数の監視とログの分析を行う方法について説明します。

### ステップ1: ログの有効化

まずは、lambda関数のログを有効化します。

```bash
aws lambda update-function-configuration --function-name my-function --tracing-config mode=active
```

上記のコマンドでは、`--tracing-config`パラメータでトレースの設定を有効化しています。

### ステップ2: ログの確認

ログを確認する場合は、以下のコマンドを実行します。

```bash
aws logs describe-log-groups --log-group-name-prefix /aws/lambda/my-function
```

上記のコマンドでは、`--log-group-name-prefix`パラメータでロググループのプレフィックスを指定し、関数のロググループの一覧を取得しています。

### ステップ3: ログの分析

ログを分析する場合は、以下のコマンドを実行します。

```bash
aws logs filter-log-events --log-group-name /aws/lambda/my-function --filter-pattern "error"
```

上記のコマンドでは、`--log-group-name`パラメータでロググループの名前を指定し、指定したパターンに一致するログイベントをフィルタリングしています。

これで、lambda関数の監視とログの分析ができるようになりました。

以上で、aws cliを使用したlambda関数の作成とデプロイ、環境変数と設定の管理、トリガーの設定とイベントソースの統合、監視とログの分析について解説しました。aws cliを活用して、効率的にlambda関数を管理しましょう。

参考記事：
- [awsのcliツール「aws cli」の使い方を解説！](https://eng-entrance.com/aws-cli)
- [aws lambdaをaws cliで操作する方法](https://dev.classmethod.jp/articles/lambda-with-aws-cli/)



## 【aws cli】関連のまとめ
https://hack-note.com/summary/aws-cli-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
