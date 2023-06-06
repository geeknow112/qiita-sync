<!--
title:   【解説】aws reachability analyzer超便利！検証作業が超効率化！
tags:    AWS,reachability-analyzer,使い方
id:      11b4392170b56a506010
private: false
-->


こんにちは。今回は、awsについて初心者エンジニアに向けて、reachability-analyzerの使い方についてお伝えします。aws reachability analyzerは、awsネットワークにおけるルーティングとセキュリティ設定に対する視覚化された分析を提供するawsツールの一つです。このツールを用いることで、ネットワーク構成の問題を早期に発見し、正確な把握をすることができます。それでは、詳細を見てみましょう。

## aws reachability analyzerとは

aws reachability analyzerは、awsのネットワークトラフィックのルーティングを分析し、セキュリティ設定を監視することができます。

awsが提供するクラウドサービスでは、複雑なネットワーク構成で動作する機能が含まれます。ネットワーク構成が複雑であるため、問題を早く発見、解決することが大変困難であり、人手での監視は非常に困難です。 このツールは ipv4 と ipv6 アドレス、プロトコル、ポート番号、サービス障害およびセキュリティグループを使用し、awsのネットワークのルーティングかどうか、およびセキュリティグループが構成されているかどうかを確認します。

## reachability-analyzerの使い方

1. コンソールにログイン
まずは、awsのコンソールにログインします。ログイン後、awsサービスのウェブページにアクセスし、「reachability analyzer」を選択します。

2. アナライザーの開始
「reachability-analyzer」画面が表示されます。「start」ボタンをクリックし、アナライザーを開始します。この際、アナライザーが使用するロールを選択して、iamポリシーが適用されたアカウントで開始する必要があります。

3. エージェントのデプロイ
次に、エージェントをデプロイする必要があります。aws cloudformationスタックを使用してデプロイすることもできますが、簡単にデプロイするには、コマンドラインからエージェントをデプロイすることができます。具体的には、以下の手順を実行します。

```
aws analyzer create-analyzer --analyzer-name your_analyzer_name --type account
```

```
aws analyzer create-archive-rule --filter=' {"type": "path","value": "/","key": "equals"}' --analyzer-name your_analyzer_name
```

```
aws analyzer create-archive-rule --filter='{"type": "payload","key": "policytype","value": "resource_policy"}' --analyzer-name your_analyzer_name
```

ここまで実行することで、エージェントをawsネットワークにデプロイすることができます。

4. 分析の実行
最後に、「reachability-analyzer」画面で「analyze vpc」をクリックして分析を実行します。分析を実行することで、ルーティングとセキュリティ設定に対する分析結果が表示されます。

このツールには設定をカスタマイズすることができるため、あなたが任意のフィルターリストの追加や、ip範囲の変更、分析執行のロックのトリガーなどを設定することができます。

## まとめ

aws reachability analyzerは、awsネットワークのルーティングとセキュリティ設定に対する視覚化された分析を提供するツールです。このツールを用いることで、ネットワーク構成の問題を早期に発見し、正確な把握をすることができます。アナライザーが自動的に実行されるため、セキュリティの設定やネットワークのスピードを改善することができます。reachability-analyzerの使い方を把握することで、awsをより効率化し、より快適に運用することができます。ぜひ、使い方を覚えてみてください。

参考：
https://aws.amazon.com/jp/reachability-analyzer/
https://docs.aws.amazon.com/reachability-analyzer/latest/userguide/getting-started.html

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
