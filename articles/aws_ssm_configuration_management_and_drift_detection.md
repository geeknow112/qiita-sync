<!--
title:   【aws system manager】構成管理とドリフト検出
tags:    AWS,SSM,system_manager
id:      121b32fa1416b1c8f9d9
private: false
-->


## aws system manager】構成管理とドリフト検出

こんにちは。今回は、awsについて初心者エンジニアに向けて、aws system managerを使用した構成管理とドリフト検出について解説します。

## 構成管理の重要性とベストプラクティス

構成管理とは、システムやアプリケーションの設定やリソースの管理を一元化し、管理者が状態の追跡や変更の履歴を把握できるようにすることです。aws system managerは、構成管理のためのサービスであり、ドリフト検出も含まれています。

構成管理の重要性は、以下のような理由から言えます。
1. 変更の追跡: システムやアプリケーションの構成が変更された場合、それが問題の原因である可能性があります。構成管理を行うことで、変更の追跡が容易になります。
2. リソースの可視性: システムの構成が把握できれば、リソースの可視性が高まり、適切な管理が可能になります。
3. セキュリティ: 構成管理を行うことで、セキュリティ上の問題を特定し、修正することができます。

構成管理のベストプラクティスには、以下のようなものがあります。
- 構成管理ドキュメントの作成と管理: ドキュメントを作成し、構成管理の対象となるリソースや設定を明示的に定義します。
- タグの活用: リソースにタグを付けることで、ドキュメントの関連付けや追跡が容易になります。
- ドリフト検出の設定と監視: ドリフト検出を定期的に実行し、変更の有無や問題の発生を把握します。
- ドリフト修正の自動化: ドリフトが検出された場合には、自動的に修正を行う仕組みを作成します。

### 構成管理ドキュメントの作成と管理手法

構成管理ドキュメントの作成と管理は、構成管理の基礎となる作業です。以下の手法を利用して、効果的に構成管理を行いましょう。

1. infrastructure as code (iac): iacを使用することで、インフラストラクチャの設定やリソースの管理をコードで表現します。
2. aws cloudformation: cloudformationは、awsのインフラストラクチャをコードとして管理するためのサービスです。cloudformationのテンプレートを使用して、構成をドキュメント化します。
3. aws systems manager: systems managerのドキュメントは、awsリソースの構成、アクション、および構成の管理方法を記述する json ファイルです。これらのドキュメントは、リソースの状態を管理およびレポートするために使用されます。

以下は、aws systems managerのドキュメントの例です。

```json
{
    "schemaversion": "1.2",
    "description": "sample ssm document for webserver configuration",
    "parameters": {
        "instancetype": {
            "type": "string",
            "description": "ec2 instance type",
            "default": "t2.micro"
        },
        "imageid": {
            "type": "string",
            "description": "ec2 ami id"
        },
        "securitygroupids": {
            "type": "list<string>",
            "description": "list of security group ids"
        },
        "subnetid": {
            "type": "string",
            "description": "vpc subnet id"
        }
    },
    "mainsteps": [
        {
            "action": "aws:runinstances",
            "name": "runinstances",
            "inputs": {
                "instancetype": "{{ instancetype }}",
                "imageid": "{{ imageid }}",
                "securitygroupids": "{{ securitygroupids }}",
                "subnetid": "{{ subnetid }}"
            }
        }
    ]
}
```

### ドリフト検出の設定と監視方法

ドリフト検出を設定して監視することで、リソースの変更や問題を把握し、適切な対応を行うことができます。ドリフト検出の設定と監視方法について解説します。

1. ドリフト検出の設定: aws systems managerコンソールから、ドリフト検出の設定を行います。監視対象のリソースやスケジュールなどを指定します。
2. ドリフト検出の監視: ドリフト検出は、定期的に実行することで変更の有無を把握します。aws systems managerコンソールまたはcliを使用してドリフト検出を実行します。

以下は、ドリフト検出の設定と監視方法の例です。

```bash
# ドリフト検出の設定
aws ssm create-resource-data-sync --sync-type resourcedatasync --s3-destination bucketname=my-bucket

# ドリフト検出の実行
aws ssm start-resource-data-sync --sync-name my-resource-data-sync

# ドリフト検出の結果の表示
aws ssm get-resource-data-sync --sync-name my-resource-data-sync
```

### ドリフト修正の自動化と適用手順

ドリフトが検出された場合には、自動的に修正を行い、正常な状態に戻すことが重要です。ドリフト修正の自動化と適用手順について解説します。

1. 自動修正の設定: aws systems managerコンソールから、自動修正の設定を行います。修正に必要な手順やスクリプトを指定します。
2. 修正の適用: ドリフトが検出された場合、自動修正が実行されます。修正手順やスクリプトは、自動化されたトリガーやジョブとして実行されます。

以下は、ドリフト修正の自動化と適用手順の例です。

```bash
# 自動修正の設定
aws ssm create-automation-definition --name my-automation-definition --targets "[{\"key\":\"tag:name\",\"values\":[\"my-instance\"]}]"

# 修正の自動化と実行
aws ssm create-automation-execution --automation-definition-name my-automation-definition --parameters "[{\"name\":\"instanceid\",\"values\":[\"i-12345678\"]}]"
```

### 構成の変更管理とバージョン管理

構成の変更管理とバージョン管理は、構成の変更履歴やバージョンの管理を行うための手法です。aws systems managerでは、ドキュメントのバージョン管理がサポートされています。

以下は、構成の変更管理とバージョン管理の例です。

```bash
# ドキュメントの作成
aws ssm create-document --content "{"schemaversion":"1.2","description":"my document","mainsteps":[]}"

# ドキュメントの更新
aws ssm update-document --name my-document --content "{"schemaversion":"1.2","description":"updated document","mainsteps":[]}"

# ドキュメントのバージョン表示
aws ssm describe-document --name my-document
```

以上で、「aws system manager」を使用した構成管理とドリフト検出の解説を終わります。aws system managerを活用することで、awsリソースの構成管理やドリフトの検出・修正を効率的に行うことができます。是非、試してみてください。

## 参考記事

- [aws systems manager documentation](https://docs.aws.amazon.com/systems-manager/)
- [aws systems manager sample documents](https://github.com/aws-samples/aws-systems-manager-sample-documents)



## 【AWS System Manager】関連のまとめ
https://hack-note.com/summary/aws-ssm-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
