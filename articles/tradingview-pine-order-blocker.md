<!--
title:   【tradingview】pineスクリプトによるオーダーブロッカーの実装方法
tags:    TradingView,pine
id:      475ac0da13fcae0053ad
private: false
-->


## オーダーブロッカーの基本原理と概要
オーダーブロッカーは、トレーダーが特定の条件を指定して取引の制御をするためのツールです。これにより、エントリーやエグジットのタイミングを制御したり、トレードの条件をカスタマイズしたりすることができます。tradingviewのpineスクリプトを使用することで、オーダーブロッカーを実装することができます。

pineスクリプトは、tradingviewのプラットフォーム上で使用されるプログラム言語です。このスクリプトを使い、トレード戦略に基づいた独自の指標やオーダーブロッカーを作成することが可能です。

また、オーダーブロッカーはバックテストやリアルトレードの両方に応用することができます。バックテストを行うことで、作成したブロッカーが過去のデータに対して効果的であるかどうかを確認することができます。そして、実際のトレードに応用することで、リスクを管理するためにトレードの制御を行うことができます。

以下では、pineスクリプトを使用してオーダーブロッカーを実装する方法について説明していきます。

## インジケーターを使用したオーダーブロッカーの実装
オーダーブロッカーを実装するためには、まずインジケーターを使用する必要があります。インジケーターは、チャート上に表示される指標のことであり、トレーダーがトレードの判断をする際の参考になります。

以下は、単純移動平均線（sma）を使用したオーダーブロッカーの実装例です。

```pinescript
//@version=4
study(title="sma order blocker", shorttitle="sma ob")

length = input(14, minval=1, title="length")
src = close

sma = sma(src, length)
blockentry = src > sma

strategy.entry("long", strategy.long, when = blockentry)
```

上記のコードは、単純移動平均線（sma）を使用してエントリーポイントを制御するオーダーブロッカーの例です。まず、長さ（length）とソース（src）を指定しています。その後、smaを計算し、ブロックエントリー（blockentry）を定義しています。この条件が満たされた場合に、strategy.entry関数を使用してエントリーを行います。

## 条件式とルールの設定方法
オーダーブロッカーでは、トレードの条件を設定するための条件式とルールが必要です。条件式は、特定の条件が成立するかどうかを判断する式であり、ルールはその条件が満たされた場合に実行されるアクションです。

以下は、rsi（relative strength index）を使用したオーダーブロッカーの実装例です。

```pinescript
//@version=4
study(title="rsi order blocker", shorttitle="rsi ob")

length = input(14, minval=1, title="length")
overboughtlevel = input(70, title="overbought level")
oversoldlevel = input(30, title="oversold level")

rsi = rsi(close, length)
overbought = rsi >= overboughtlevel
oversold = rsi <= oversoldlevel

blockentry = overbought or oversold

strategy.entry("long", strategy.long, when = blockentry)
```

上記のコードでは、rsiを使用してオーダーブロッカーを実装しています。長さ（length）、買われすぎレベル（overbought level）、売られすぎレベル（oversold level）を指定しています。rsiが買われすぎレベルを超えた場合または売られすぎレベルを下回った場合に、エントリーをブロックするようになっています。

## エントリーとエグジットの制御方法
オーダーブロッカーでは、エントリーとエグジットのタイミングを制御することができます。以下のコードは、移動平均線（sma）を使用してエントリーとエグジットを制御するオーダーブロッカーの例です。

```pinescript
//@version=4
study(title="sma entry/exit blocker", shorttitle="sma ee ob")

length = input(14, minval=1, title="length")
src = close

sma = sma(src, length)
blockentry = src > sma
blockexit = src < sma

strategy.entry("long", strategy.long, when = blockentry)
strategy.close("long", when = blockexit)
```

上記のコードでは、smaを使用してエントリーとエグジットを制御しています。ブロックエントリー（blockentry）の条件が満たされた場合にエントリーを行い、ブロックエグジット（blockexit）の条件が満たされた場合にエグジットを行います。

## バックテストと実際のトレードへの応用
オーダーブロッカーは、バックテストや実際のトレードに応用することができます。バックテストを行うには、tradingviewのバックテスト機能を使用します。

以下は、バックテストを行うためのコード例です。

```pinescript
//@version=4
strategy("backtest example", overlay=true)

length = input(14, minval=1, title="length")
src = close

sma = sma(src, length)
blockentry = src > sma

strategy.entry("long", strategy.long, when = blockentry)
```

上記のコードでは、バックテストを行うための簡単なオーダーブロッカーを実装しています。エントリーポイントは、ブロックエントリー（blockentry）の条件が満たされた場合に設定されます。

実際のトレードに応用する場合には、トレーディングプラットフォームとtradingviewを連携させる必要があります。これにより、作成したオーダーブロッカーを実際のトレードに組み込むことができます。

## まとめ
tradingviewのpineスクリプトを使用することで、オーダーブロッカーを実装することができます。オーダーブロッカーは、トレード戦略に基づいた条件式とルールを設定することで、エントリーやエグジットのタイミングを制御するためのツールです。また、バックテストや実際のトレードへの応用も可能です。

pineスクリプトを使用してオーダーブロッカーを作成する際には、まずインジケーターを選定し、条件式とルールを設定します。そして、バックテストや実際のトレードでの応用に備えて、コードを適宜改善していくことが重要です。

参考記事：
- [creating a simple indicator in tradingview](https://www.tradingview.com/script/h5scyxht-creating-a-simple-indicator-in-tradingview/)
- [implementing a custom backtester in tradingview](https://www.tradingview.com/script/xbcg9ggo-implementing-a-custom-backtester-in-tradingview/)



## 【TradingView】Pine Script関連のまとめ
https://hack-note.com/summary/tradingview-pine-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
