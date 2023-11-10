<!--
title:   【aws system manager】基本機能と活用方法
tags:    AWS,SSM,system_manager
id:      8b25fa005fb06e6858f7
private: false
-->


## aws system manager【基本機能と活用方法】

こんにちは。今回は、awsについて初心者エンジニアに向けて、aws system managerの基本機能と活用方法について解説します。

awsでは、インフラストラクチャを維持、管理するためのツールとしてaws system managerが提供されています。このツールを活用することで、ec2インスタンスやオンプレミスサーバーを統合的に管理し、自動化することが可能です。

本記事では、aws system managerの概要と利点、インスタンス管理と自動化の手法、パッチ管理とセキュリティのベストプラクティス、セッションマネージャーの活用法とセキュアなリモートアクセス、カスタムドキュメントとスクリプトの管理について順に解説します。

## システムマネージャーの概要と利点

aws system managerは、awsリソースの運用管理とタスクの自動化を容易にするための統合ツールです。以下にその主な利点をまとめました。

- セキュアなリモートアクセス：セッションマネージャーを使用してec2インスタンスにセキュアにリモートアクセスできます。sshキーの管理やセキュアなトンネリングなどを手軽に設定することができます。

- インフラストラクチャの可視化：システムマネージャーのコンソールは、awsリソース（ec2インスタンス、vpc、セキュリティグループなど）をグラフィカルに表示することができます。管理対象のリソースが一目でわかり、状態の監視も容易に行えます。

- パフォーマンスの監視：インスタンスのパフォーマンスメトリクスを監視し、障害の早期発見やインスタンスのスケーリングを行うことができます。

- タスクの自動化：aws system managerは、インスタンスの設定変更やパッチ適用などのタスクを自動化する機能を提供します。リソースの状態を確認し、必要なタスクを定義することで、運用管理の効率化が図れます。

上記のような利点を活かして、aws system managerを使いこなしていきましょう。

## インスタンス管理と自動化の手法

aws system managerを使用すると、ec2インスタンスやオンプレミスサーバーの管理を効率化できます。以下では、具体的な手法を紹介します。

### インスタンスの管理機能

aws system managerでは、インスタンスの管理タスクを実行するためのコマンドラインインターフェース（cli）やsdkが提供されています。これを活用することで、以下のようなタスクを行うことができます。

- インスタンスの詳細な情報の取得：`describe-instance-information`コマンドを使用して、インスタンスの詳細情報（インスタンスid、ipアドレス、インスタンスの状態など）を取得することができます。

```bash
aws ssm describe-instance-information
```

- インスタンスへのコマンド実行：`send-command`コマンドを使用して、インスタンスに対してコマンドを実行することができます。例えば、特定のパッケージのインストールやファイルのダウンロードなどのタスクを実行することができます。

```bash
aws ssm send-command --instance-ids i-1234567890abcdef0 --document-name "aws-runshellscript" --comment "install apache" --parameters commands=stop apache\,update apache\,start apache --timeout-seconds 600 --output text
```

上記のコマンドでは、ec2インスタンスに対して「apacheのインストール」と「apacheのアップデート」を行った後、apacheを起動するコマンドを実行しています。

### パラメータストアの利用

aws system managerには、パラメータストアと呼ばれる機能があります。これを使うことで、構成の管理やタスクの自動化を簡単に行うことができます。

パラメータストアは、キー/バリュー形式でデータを保存できるストレージです。以下のような利点があります。

- 機密情報や設定情報の保存：パラメータストアは、暗号化されたデータベースとして機能し、機密情報の保存に最適です。例えば、データベースの接続情報やapiキーなどの設定情報を安全に管理できます。

- バージョン管理と履歴の確認：パラメータストアは、キーごとにバージョン管理が行われ、過去のバージョンとその内容を確認することができます。

- イベントトリガーとの連携：パラメータストアの変更イベントを利用して、lambda関数やcloudwatchイベントルールなどと連携させることができます。データの変更があった場合に、自動的にタスクを実行することができます。

パラメータストアの利用方法や設定の詳細については、[公式ドキュメント](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html)を参照してください。

## パッチ管理とセキュリティのベストプラクティス

aws system managerは、パッチ管理とセキュリティ管理においても効果的なツールです。以下では、その活用方法とベストプラクティスについて解説します。

### パッチ管理

aws system managerのパッチマネージャーは、ec2インスタンスのパッチ管理を自動化するための機能です。以下の手順で使用することができます。

1. パッチマネージャーの設定：awsコンソールの「パッチマネージャー」ページで、パッチの自動適用に関する設定を行います。インスタンスのセキュリティパッチだけでなく、アプリケーションやドライバのパッチも適用することができます。

2. スケジュールの設定：パッチの自動適用をスケジュールすることができます。例えば、毎週の特定の曜日や時間帯にパッチを適用するようスケジュールすることができます。

3. 監視と自動適用：パッチマネージャーは、適用するパッチのリストを表示し、インスタンスの状態を監視します。自動適用が有効になっている場合、パッチはスケジュール通りに自動的に適用されます。

### セキュリティのベストプラクティス

aws system managerを使用してセキュリティを強化するためのベストプラクティスを紹介します。

- インスタンスへのセキュアなアクセス：セッションマネージャーを使用して、ec2インスタンスに安全かつトレース可能なリモートアクセスを提供します。sshキーの管理やバージョン管理が煩雑になることなく、リモートアクセスを実現できます。

- インスタンスの自動修復：aws system managerの自動修復機能を使用することで、リソースの状態に異常がある場合に自動的に修復することができます。例えば、ファイアウォールの設定が不正な場合には、自動的に正しい設定に修正することができます。

以上が、パッチ管理とセキュリティのベストプラクティスについての概要です。詳細な手順や設定方法については、[公式ドキュメント](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)を参照してください。

## セッションマネージャーの活用法とセキュアなリモートアクセス

aws system managerのセッションマネージャーは、ec2インスタンスにセキュアなリモートアクセスを提供するための機能です。以下では、その活用法とセキュアなリモートアクセスについて解説します。

セッションマネージャーは、ec2インスタンスへのリモートアクセスにsshキーを使用せず、aws identity and access management（iam）のロールベースのアクセス制御を利用します。以下の手順でセッションマネージャーを使用することができます。

1. セッションマネージャープラグインのインストール：ローカルマシン（windows、macos、linux）にセッションマネージャープラグインをインストールします。インストール手順は、[公式ドキュメント](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html)を参照してください。

2. セッションマネージャーでのセッション開始：セッションを開始するには、以下のコマンドを使用します。

```bash
aws ssm start-session --target instance-id
```

上記のコマンドでは、`instance-id`にはec2インスタンスのidを指定します。

3. セッションの終了：セッションを終了するには、以下のコマンドを使用します。

```bash
exit
```

セッションマネージャーを使用することで、セキュアかつトレース可能なリモートアクセスを実現することができます。また、セッションマネージャーでは、ターミナルへのアクセスだけでなく、scpやsftpなどのファイル転送も行うことができます。

## カスタムドキュメントとスクリプトの管理

aws system managerでは、カスタムドキュメントやスクリプトを管理するための機能も提供されています。以下では、その活用方法と管理手法について解説します。

### カスタムドキュメント

カスタムドキュメントは、ec2インスタンスへのコマンドを指定するためのjsonドキュメントです。これを使用することで、aws system managerのコマンドと同等のタスクを実行することができます。

カスタムドキュメントの作成手順は以下の通りです。

1. カスタムドキュメントの作成：json形式でカスタムドキュメントを作成します。例えば、以下のようなカスタムドキュメントを作成することができます。

```json
{
  "schemaversion": "2.2",
  "description": "run script to install and configure application",
  "mainsteps": [
    {
      "action": "aws:runshellscript",
      "name": "installandconfigure",
      "inputs": {
        "runcommand": [
          "wget https://example.com/install.sh -o /tmp/install.sh",
          "chmod +x /tmp/install.sh",
          "/tmp/install.sh"
        ]
      }
    }
  ]
}
```

上記のカスタムドキュメントでは、`runshellscript`コマンドを使用して`install.sh`スクリプトを実行しています。

2. カスタムドキュメントの登録：以下のコマンドを使用して、カスタムドキュメントを登録します。

```bash
aws ssm create-document --content file://my-custom-document.json --name "mycustomdocument"
```

上記のコマンドでは、`my-custom-document.json`という名前のファイルにカスタムドキュメントを保存し、それを`mycustomdocument`という名前で登録しています。

### スクリプトの管理

aws system managerでは、スクリプトの管理も行うことができます。スクリプトの管理は、カスタムドキュメントと連携して使用することができます。

スクリプトの管理手法は、以下のようなものがあります。

- カスタムドキュメントにスクリプトを埋め込む：カスタムドキュメント内の`runshellscript`コマンドを使用してスクリプトを埋め込むことができます。この場合、スクリプトの修正や管理が容易になります。



## 【AWS System Manager】関連のまとめ
https://hack-note.com/summary/aws-ssm-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
