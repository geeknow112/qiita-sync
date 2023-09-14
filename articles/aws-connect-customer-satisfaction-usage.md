<!--
title:   【amazon connect】顧客満足度を向上させるための使い方
tags:    Amazon,connect
id:      0503ae78e7560a1a72b4
private: false
-->


## amazon connectについて初心者エンジニアに向けて

こんにちは。今回は、amazon connectについて初心者エンジニアに向けて、顧客満足度を向上させるための使い方についてご紹介します。amazon connectは、クラウドベースのコンタクトセンターのサービスであり、企業が顧客対応を効率化し、顧客満足度を高めることができます。本記事では、amazon connectのアカウント作成方法からレポートの作成方法まで、詳しく解説していきます。

## アカウントの作成方法

### step1: awsアカウントの作成
amazon connectを使用するためには、まずawsアカウントが必要です。以下のリンクからawsアカウントを作成しましょう。

[【参考リンク】awsアカウントの作成](https://aws.amazon.com/jp/premiumsupport/knowledge-center/create-and-activate-aws-account/)

### step2: amazon connectのセットアップ
awsアカウントを作成したら、コンソールにログインし、amazon connectのセットアップを行います。以下の手順に従って、amazon connectをセットアップしましょう。

1. コンソールの「サービス」から「connect」を選択して、amazon connectのダッシュボードを開きます。
2. ダッシュボード上部のバナーにある「get started」をクリックし、セットアップウィザードを開始します。

## フローの作成方法

### step1: フローライターの起動
フローを作成するためには、フローライターを起動する必要があります。以下のコマンドを実行して、フローライターを起動しましょう。

```python
import boto3

connect = boto3.client("connect")

response = connect.start_contact_flow_execution(
    instanceid='your_instance_id',
    contactflowid='your_contact_flow_id',
    description='your_description',
    attributes={
        'your_attribute_key': 'your_attribute_value'
    },
    sourcephonenumber='your_phone_number',
    destinationphonenumber='customer_phone_number'
)

print(response)
```

### step2: フローの作成
フローライターを起動したら、フローを作成しましょう。以下の手順に従って、フローを作成します。

1. フローライターの画面左側にある「add block」をクリックして、フローにブロックを追加します。
2. 各ブロックの設定を行い、必要なアクションや条件分岐を設定します。

## 電話番号の設定方法

### step1: 電話番号の購入
amazon connectでは、電話番号の購入が必要です。以下の手順に従って、電話番号を購入しましょう。

1. ダッシュボードの左側にある「phone numbers」をクリックします。
2. 「add phone number」をクリックして、新しい電話番号を購入します。

### step2: 電話番号の設定
電話番号を購入したら、それをamazon connectに設定しましょう。以下のコマンドを実行して、電話番号を設定します。

```python
response = connect.associate_phone_number(
    instanceid='your_instance_id',
    phonenumber='your_phone_number',
    phonenumbertype='your_phone_number_type'
)

print(response)
```

## キューの作成方法

### step1: キューの作成
キューを作成することで、着信コールを効率的に処理することができます。以下のコマンドを実行して、キューを作成しましょう。

```python
response = connect.create_queue(
    instanceid='your_instance_id',
    queuename='your_queue_name',
    description='your_queue_description',
    maxcontacts=10,
    quickconnectids=[
        'your_quick_connect_id',
    ],
    tags={
        'your_tag_key': 'your_tag_value'
    }
)

print(response)
```

## エージェントの追加方法

### step1: グループの作成
エージェントを追加するためには、まずグループを作成する必要があります。以下のコマンドを実行して、グループを作成しましょう。

```python
response = connect.create_routing_profile(
    name='your_routing_profile_name',
    defaultoutboundqueueid='your_queue_id',
    description='your_routing_profile_description',
    mediaconcurrencies=[
        {
            'channel': 'voice',
            'concurrency': 1
        },
    ],
    queueconfigs=[
        {
            'priority': 1,
            'queuereference': {
                'queueid': 'your_queue_id',
                'channel': 'voice'
            },
            'delay': 0
        },
    ],
    tags={
        'your_tag_key': 'your_tag_value'
    }
)

print(response)
```

### step2: エージェントの追加
グループを作成したら、エージェントを追加しましょう。以下のコマンドを実行して、エージェントを追加します。

```python
response = connect.create_user(
    username='your_username',
    password='your_password',
    identityinfo={
        'firstname': 'your_first_name',
        'lastname': 'your_last_name'
    },
    phoneconfig={
        'phonenumber': 'your_phone_number',
        'phonetype': 'soft_phone'
    },
    routingprofileid='your_routing_profile_id',
    securityprofileids=[
        'your_security_profile_id',
    ],
    instanceid='your_instance_id'
)

print(response)
```

## レポートの作成方法

### step1: レポートの作成
amazon connectでは、さまざまなレポートを作成することができます。以下のコマンドを実行して、レポートを作成しましょう。

```python
response = connect.get_metric_data(
    instanceid='your_instance_id',
    starttime='your_start_time',
    endtime='your_end_time',
    filters=[
        {
            'name': 'your_filter_name',
            'values': [
                'your_filter_value',
            ]
        },
    ],
    historicalmetrics=[
        {
            'name': 'your_metric_name',
            'threshold': 0,
            'statistic': 'your_statistic',
            'unit': 'your_unit'
        },
    ],
    groupings=[
        'queue',
    ]
)

print(response)
```

以上が、amazon connectの顧客満足度を向上させるための使い方についての解説でした。アカウントの作成方法からレポートの作成方法まで、ステップバイステップで解説しましたので、ぜひ参考にしてみてください。amazon connectを活用して、顧客満足度の向上に取り組んでみましょう！



## 【Amazon Connect】まとめ
https://hack-note.com/summary/aws-connect-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
