<!--
title: 【tradingview】スクリプトエディターの使い方と自動売買戦略の作成
tags: tradingview,python,pine
id: 
private: false
-->

# tradingviewについて初心者エンジニアに向けて

こんにちは。今回は、tradingviewについて初心者エンジニアに向けて、スクリプトエディターの使い方と自動売買戦略の作成について解説します。tradingviewは、株式や暗号通貨などの価格チャートを分析し、独自の取引戦略を作成できるプラットフォームです。この記事では、tradingviewのスクリプトエディターを使用し、pythonとpine scriptを使った自動売買戦略の作成方法について詳しく解説します。

## バックテストの基本と使い方の解説

バックテストは、過去の価格データを使用して取引戦略の効果を評価する手法です。tradingviewのスクリプトエディターを使用して作成した戦略をバックテストすることで、実際の取引に役立つ戦略を見つけることができます。以下は、バックテストの基本的な使い方の解説です。

```pinescript
//@version=4
strategy("basic backtesting example")

// バックテスト期間を設定
startdate = input(timestamp("2019-01-01 00:00"), "start date")
enddate = input(timestamp("2020-01-01 00:00"), "end date")

// 戦略のエントリー条件
enterlong = crossover(sma(close, 50), sma(close, 200))
entershort = crossunder(sma(close, 50), sma(close, 200))

// エントリーポイントの指定
strategy.entry("buy", strategy.long, when=enterlong)
strategy.entry("sell", strategy.short, when=entershort)

// バックテスト結果のプロット
plot(strategy.equity)
```

このサンプルコードでは、50日移動平均線が200日移動平均線を上回ったタイミングで買いエントリーし、50日移動平均線が200日移動平均線を下回ったタイミングで売りエントリーする単純な戦略を示しています。バックテストの期間は、`input`関数を使用して設定することができます。

バックテスト結果は、`plot`関数を使用してグラフとして表示することができます。

バックテストについて詳しくは、下記の記事を参考にしてください。

- [バックテストの基本と使い方の解説](https://tradingterminal.jp/backtest)

## バックテストのパフォーマンス評価指標の活用方法

バックテストの結果を評価するためには、パフォーマンス評価指標を活用する必要があります。これにより、戦略の収益性やリスクを評価することができます。以下は、バックテストのパフォーマンス評価指標の活用方法の解説です。

```pinescript
//@version=4
strategy("performance metrics example")

strategy.entry("buy", strategy.long)
strategy.close("buy", when=strategy.position_size > 0, comment="take profit")
strategy.close("buy", when=strategy.position_size < 0, comment="stop loss")

// 個別の取引結果を表示
strategy.show("trades")

// バックテスト結果を取得
backtestresults = strategy.backtest_results

// パフォーマンス評価指標のプロット
plot(backtestresults.totaltrades)
plot(backtestresults.startingcapital)
plot(backtestresults.netprofit)
plot(backtestresults.profitfactor)

// パフォーマンス評価指標の表示
plotshape(backtestresults.totaltrades, text="total trades", location=location.top)
plotshape(backtestresults.startingcapital, text="starting capital", location=location.top)
plotshape(backtestresults.netprofit, text="net profit", location=location.top)
plotshape(backtestresults.profitfactor, text="profit factor", location=location.top)
```

このサンプルコードでは、簡単なロング戦略を示しています。ポジションが利益になった場合、`take profit`で利益を確定させ、損失になった場合は`stop loss`で損切りを行います。

`strategy.show`関数を使用して、個別の取引結果を表示することができます。また、`strategy.backtest_results`を使用してバックテスト結果を取得し、各種パフォーマンス評価指標をプロットすることができます。

パフォーマンス評価指標の詳細については、下記の記事を参考にしてください。

- [バックテストのパフォーマンス評価指標の活用方法](https://tradingterminal.jp/backtest_metrics)

## バックテストの設定とテスト期間の選び方

バックテストを行う際には、正確な結果を得るために適切な設定とテスト期間を選ぶ必要があります。以下は、バックテストの設定とテスト期間の選び方についての解説です。

```pinescript
//@version=4
strategy("backtesting settings example")

// バックテストの設定
strategy("backtesting settings")
strategy.initial_capital = 100000
strategy.commission_type = strategy.commission.percent
strategy.commission_value = 0.1

// テスト期間の選び方
strategy("choosing backtest period")
startdate = input(timestamp("2020-01-01 00:00"), "start date")
enddate = input(timestamp("2021-01-01 00:00"), "end date")

strategy.entry("buy", strategy.long)
strategy.exit("buy", "sell", limit=close * 1.02, stop=close * 0.98)

plot(strategy.equity)
```

このサンプルコードでは、バックテストの設定を変更する方法とテスト期間を選ぶ方法を示しています。`strategy.initial_capital`を使用して初期資本を設定し、`strategy.commission_type`と`strategy.commission_value`を使用して手数料を設定することができます。

テスト期間は、`input`関数を使用して選ぶことができます。以下のサンプルでは、2020年1月1日から2021年1月1日までの期間でバックテストを行います。

バックテストの設定とテスト期間の選び方の詳細については、下記の記事を参考にしてください。

- [バックテストの設定とテスト期間の選び方](https://tradingterminal.jp/backtest_settings)

## バックテスト結果の分析と改善点の特定

バックテストを行った後は、結果の分析と改善点の特定が重要です。以下は、バックテスト結果の分析と改善点の特定についての解説です。

```pinescript
//@version=4
strategy("backtest analysis example")

strategy.entry("buy", strategy.long)
strategy.exit("buy", "sell", limit=close * 1.02, stop=close * 0.98)

// バックテスト結果を取得
backtestresults = strategy.backtest_results

// バックテスト結果の分析
trades = backtestresults.trades
winningtrades = filter(isprofit, trades)
losingtrades = filter(isloss, trades)
averagewin = sum(winningtrades.profit_percentage) / len(winningtrades)
averageloss = sum(losingtrades.profit_percentage) / len(losingtrades)

// 損益曲線のプロット
plot(strategy.equity)

// バックテスト結果の表示
plotshape(averagewin, text="average win", location=location.top)
plotshape(averageloss, text="average loss", location=location.top)
```

このサンプルコードでは、バックテスト結果の分析と改善点の特定の方法を示しています。`strategy.backtest_results`を使用してバックテスト結果を取得し、トレードの勝敗や平均利益、平均損失などを分析することができます。

また、損益曲線をプロットすることで、トレードの成績を視覚化することもできます。

バックテスト結果の分析と改善点の特定については、下記の記事を参考にしてください。

- [バックテスト結果の分析と改善点の特定](https://tradingterminal.jp/backtest_analysis)

## ポートフォリオバックテストの実施と複数戦略の評価

ポートフォリオバックテストでは、複数の戦略を同時に評価することができます。以下は、ポートフォリオバックテストの実施と複数戦略の評価方法についての解説です。

```pinescript
//@version=4
strategy("portfolio backtesting example")

// 戦略1
strategy1 = sma(close, 50) > sma(close, 200)

// 戦略2
strategy2 = rsi(close, 14) > 70

// ポートフォリオバックテスト
portfolio = strategy1 or strategy2
strategy.entry("buy", strategy.long, when=portfolio)
strategy.exit("buy", "sell", when=not portfolio)

plot(strategy.equity)
```

このサンプルコードでは、ポートフォリオバックテストを行う方法を示しています。戦略1と戦略2を作成し、それぞれのエントリー条件を満たす場合にポートフォリオに追加します。戦略がポートフォリオに含まれる場合はロングポジションを持ち、それ以外の場合はポジションをクローズします。

ポートフォリオバックテストの実施と複数戦略の評価については、下記の記事を参考にしてください。

- [ポートフォリオバックテストの実施と複数戦略の評価](https://tradingterminal.jp/portfolio_backtest)

## バックテストの注意点とリアルタイム相場との違い

バックテストは、過去のデータを使用して行うため、リアルタイム相場とは異なる結果が出ることがあります。以下は、バックテストの注意点とリアルタイム相場との違いについての解説です。

```pinescript
//@version=4
strategy("backtesting tips example")

strategy.entry("buy", strategy.long)
strategy.exit("buy", "sell", limit=close * 1.02, stop=close * 0.98)

plot(strategy.equity)

// バックテストの注意点
//@todo consider slippage and commissions

// リアルタイム相場との違い
//@todo consider market conditions, liquidity, execution speed, etc.
```

このサンプルコードでは、バックテストの注意点とリアルタイム相場との違いについて述べています。バックテストでは、スリッページや手数料などの取引コストが考慮されていない場合があるため、これらの要素を考慮する必要があります。また、バックテスト結果とリアルタイム相場での取引結果には、市場の状況や流動性、実行速度などの違いがあることにも注意が必要です。

バックテストの注意点とリアルタイム相場との違いについては、下記の記事を参考にしてください。

- [バックテストの注意点とリアルタイム相場との違い](https://tradingterminal.jp/backtest_tips)

以上が、tradingviewのスクリプトエディターの使い方と自動売買戦略の作成方法についての解説です。tradingviewは、初心者エンジニアにも扱いやすいプラットフォームであり、pythonやpine scriptを使って自動売買戦略を作成することができます。バックテストの基本から評価指標の活用方法、設定とテスト期間の選び方、分析と改善点の特定、ポートフォリオバックテストの実施、注意点など、幅広いトピックを取り上げました。これらの知識を活用して、自身のトレード戦略を確立していきましょう。

## 参考記事

1. バックテストの基本と使い方の解説: [https://tradingterminal.jp/backtest](https://tradingterminal.jp/backtest)
2. バックテストのパフォーマンス評価指標の活用方法: [https://tradingterminal.jp/backtest_metrics](https://tradingterminal.jp/backtest_metrics)
3. バックテストの設定とテスト期間の選び方: [https://tradingterminal.jp/backtest_settings](https://tradingterminal.jp/backtest_settings)
4. バックテスト結果の分析と改善点の特定: [https://tradingterminal.jp/backtest_analysis](https://tradingterminal.jp/backtest_analysis)
5. ポートフォリオバックテストの実施と複数戦略の評価: [https://tradingterminal.jp/portfolio_backtest](https://tr

　

## 【TradingView】関連のまとめ
https://hack-note.com/summary/tradingview-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

