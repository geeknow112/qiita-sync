<!--
title:   【aws system manager】クラウドウォッチログとアラート設定
tags:    AWS,SSM,system_manager
id:      76f1e2e779a2d05906be
private: false
-->


## クラウドウォッチログの概要と活用シナリオ
awsについて初心者エンジニアに向けて、awsのシステムマネージャー（aws systems manager、以下ssm）を使ったクラウドウォッチログとアラート設定について解説します。

### クラウドウォッチログとは
クラウドウォッチログは、awsのリソースの情報やアプリケーションのログを収集するためのサービスです。これにより、アプリケーションの問題や障害の追跡、運用監視などを効果的に行うことができます。

### クラウドウォッチログの活用シナリオ
クラウドウォッチログは、以下のような活用シナリオで利用されます。

1. ログのトラブルシューティング: システムやアプリケーションの問題を特定し、ログを調査して原因を追跡するために使用されます。
2. パフォーマンスの監視: amazon ec2などのリソースのパフォーマンスを監視し、リソースの利用状況や負荷を把握するために使用されます。
3. セキュリティの監視: セキュリティに関連するイベントやログを監視し、セキュリティ侵害の検知や対策を行うために使用されます。

以上のような活用シナリオで、クラウドウォッチログを利用することができます。次に、クラウドウォッチログの収集と設定手順について説明します。

## クラウドウォッチログの収集と設定手順
クラウドウォッチログの収集と設定手順は、以下の通りです。

1. iamロールの作成: ssmがログを収集できるようにするためには、iamロールが必要です。iamコンソールで新しいロールを作成し、必要な権限を割り当てます。

```json
{
  "version": "2012-10-17",
  "statement": [
    {
      "effect": "allow",
      "action": [
        "logs:putlogevents",
        "logs:createloggroup",
        "logs:createlogstream"
      ],
      "resource": "arn:aws:logs:*:*:*"
    }
  ]
}
```

2. クラウドウォッチエージェントのインストール: インスタンスにクラウドウォッチエージェントをインストールし、設定ファイルを作成します。

```
# install cloudwatch agent
sudo yum install -y amazon-cloudwatch-agent

# create cloudwatch agent configuration file
sudo nano /opt/aws/amazon-cloudwatch-agent/bin/config.json

# paste the following configuration
{
  "metrics": {
    "append_dimensions": {
      "autoscalinggroupname": "${aws:autoscalinggroupname}",
      "imageid": "${aws:imageid}",
      "instanceid": "${aws:instanceid}",
      "instancetype": "${aws:instancetype}"
    },
    "metrics_collected": {
      "procstat": [
        {
          "pidfile": "/var/run/httpd.pid",
          "recursive": false,
          "metricname": "httpd_cpu_utilization",
          "namespace": "custom"
        }
      ]
    }
  }
}
```

3. クラウドウォッチログの設定: cloudwatchエージェントを使用して収集するログの設定を行います。設定ファイルにロググループ名、ログストリーム名、ログデータのパスなどを指定します。

```
{
  "logs": {
    "logs_collected": {
      "files": {
        "collect_list": [
          {
            "file_path": "/var/log/httpd/access_log",
            "log_group_name": "mywebapp/accesslog",
            "log_stream_name": "{instance_id}-access-log",
            "timezone": "utc"
          },
          {
            "file_path": "/var/log/httpd/error_log",
            "log_group_name": "mywebapp/errorlog",
            "log_stream_name": "{instance_id}-error-log",
            "timezone": "utc"
          }
        ]
      }
    }
  }
}
```

以上の手順で、クラウドウォッチログの収集と設定が完了します。次に、アラートルールの作成とトリガー設定について説明します。

## アラートルールの作成とトリガー設定
クラウドウォッチログを活用する上で重要なのが、異常を検知した時に通知を受けることです。アラートルールを作成し、トリガーを設定することで、異常を検知した際に自動的に通知を受けることができます。

アラートルールの作成手順を以下に示します。

1. アラートルールの作成: cloudwatchコンソールでアラートルールを作成します。以下の例では、cpu使用率が90%を超えた場合にアラートを発生させるルールを作成しています。

2. トリガーの設定: アラートルールの作成後、アラートがトリガーされた際に実行するアクションを設定します。たとえば、snsトピックを指定してアラート通知を行うことができます。

以上の手順で、アラートルールの作成とトリガー設定が完了します。次に、ログデータの分析と異常検知方法について説明します。

## ログデータの分析と異常検知方法
クラウドウォッチログに収集されたログデータを分析し、異常を検知する方法について説明します。

1. クラウドウォッチログダッシュボード: cloudwatchコンソールのログダッシュボードを使用すると、ログデータの可視化やグラフ化が簡単に行えます。異常を検知するためには、適切なメトリックスやフィルタリングを設定することが重要です。

2. ログデータのクエリ: cloudwatch logs insightsを使用してログデータをクエリすることで、特定のイベントやパターンを検索することができます。異常検知のためには、適切なクエリを設定し、必要な情報を抽出することが重要です。

以上の手法を活用して、ログデータの分析と異常検知を行うことができます。最後に、アラート通知のカスタマイズとレポート作成について説明します。

## アラート通知のカスタマイズとレポート作成
アラート通知をより柔軟にカスタマイズする方法や、ログデータのレポート作成方法について説明します。

1. snsトピックのカスタマイズ: アラート通知をカスタマイズするためには、snsトピックを使用します。snsトピックには、通知先、メッセージのフォーマットなどをカスタマイズするための機能があります。

2. ログデータのエクスポート: cloudwatch logsは、ログデータをs3バケットにエクスポートする機能も提供しています。エクスポートしたログデータを使用して、カスタムレポートを作成することができます。

以上の手法を活用して、アラート通知のカスタマイズとログデータのレポート作成を行うことができます。

本記事では、awsのシステムマネージャー（ssm）を使用したクラウドウォッチログとアラート設定について解説しました。初心者エンジニアの方にとって、awsのネットワーク監視やトラブルシューティングに役立つ内容となっていると思います。

参考記事:
- [aws ドキュメント - クラウドウォッチログの設定](https://docs.aws.amazon.com/ja_jp/amazoncloudwatch/latest/logs/cwl_gettingstarted.html)
- [aws ドキュメント - cloudwatchエージェントの設定](https://docs.aws.amazon.com/ja_jp/amazoncloudwatch/latest/monitoring/install-cloudwatch-agent.html)



## 【AWS System Manager】関連のまとめ
https://hack-note.com/summary/aws-ssm-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
