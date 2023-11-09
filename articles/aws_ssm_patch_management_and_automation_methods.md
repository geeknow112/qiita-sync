<!--
title: 【aws system manager】パッチ管理と自動化手法
tags: aws,ssm,system_manager
id: 
private: false
-->

## aws system manager】パッチ管理と自動化手法

こんにちは。今回は、awsについて初心者エンジニアに向けて、aws systems managerの機能を利用したパッチ管理と自動化手法についてご紹介します。

### パッチ管理の重要性とベストプラクティス

パッチ管理は、システムのセキュリティと安定性を確保するために非常に重要なプロセスです。定期的なパッチ適用が行われないと、新たな脆弱性やバグのリスクが高まります。aws systems managerを使用することで、全てのawsリソースでのパッチ管理を簡単に実施することができます。

以下のベストプラクティスを参考に、効果的なパッチ管理手法を実施することが推奨されています。

1. パッチベースラインの設定と管理

システム全体のパッチ管理の基礎となるのが「パッチベースライン」の設定です。パッチベースラインは、awsが提供するパッチデータベースと比較して、どのパッチを適用するかを決定するためのルールセットです。systems managerのパッチマネージャを使用して、パッチベースラインを設定することができます。

以下は、パッチベースラインの設定例です。

```json
{
  "name": "standard_baseline",
  "operatingsystem": "windows",
  "globalfilters": [
    {
      "key": "kb",
      "values": [
        "kb123456"
      ],
      "type": "equal",
      "enabled": true
    }
  ],
  "approvalrules": {
    "patchrules": [
      {
        "patchfiltergroup": {
          "patchfilters": [
            {
              "key": "msrc_severity",
              "values": [
                "critical"
              ],
              "type": "equal",
              "enabled": true
            },
            {
              "key": "classification",
              "values": [
                "securityupdates"
              ],
              "type": "equal",
              "enabled": true
            }
          ]
        },
        "approveafterdays": 0
      }
    ]
  }
}
```

2. 自動パッチ適用の設定とスケジューリング

自動パッチ適用を設定することで、手動でのパッチ適用作業の煩わしさや人的ミスを防ぐことができます。systems managerのmaintenance windowを使用して、自動パッチ適用のスケジューリングを行うことができます。

以下は、自動パッチ適用スケジュールの設定例です。

```yaml
---
- name: "patch group 1"
  description: "patch group 1."
  targets:
    - key: "tag:patch group"
      values:
        - "group 1"
  schedule:
    - cron: daily 00:00
```

3. パッチコンプライアンスの監視とレポート

パッチの適用状況をモニタリングし、非準拠のインスタンスを特定することは、パッチ管理の重要な要素です。systems managerのパッチマネージャを使用すると、パッチの適用状況を監視し、その結果をレポートすることができます。

以下は、パッチコンプライアンスの監視とレポートのためのコマンド例です。

```
aws ssm describe-instance-patch-states --query 'instancepatchstates[*].{instanceid: instanceid, patchgroup: patchgroup, patchbaselineid: patchbaselineid, failedcount: failedcount, installedcount: installedcount, missingcount: missingcount}'
```

4. パッチロールバックの手法と注意点

パッチ適用後に問題が発生した場合、ロールバックが重要となります。systems managerのパッチマネージャを使用すると、簡単にパッチロールバックを実行することができます。

以下は、パッチロールバックの手法と注意点の例です。

```yaml
---
- name: "patch rollback"
  description: "patch rollback."
  targets:
    - key: "tag:patch group"
      values:
        - "group 1"
  actions:
    - key: "aws-runpatchbaseline"
      parameters:
        operation: "uninstall"
```

以上が、aws systems managerのパッチ管理と自動化手法についての概要です。aws systems managerは、パッチ管理を自動化するための便利なツールですので、積極的に活用していきましょう。

参考記事：
- [パッチベースラインの作成と適用](https://dev.classmethod.jp/articles/patch-baseline-for-ec2-instances/)
- [aws systems manager のパッチ管理について](https://dev.classmethod.jp/articles/aws-systems-manager-patch-management/)

　

## 【AWS System Manager】関連のまとめ
https://hack-note.com/summary/aws-ssm-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

