<!--
title:   【tradingview】pineスクリプトでの自動売買手法
tags:    TradingView,pine
id:      10522ac774b4182faf14
private: false
-->


## 自動売買手法の基礎：pineスクリプト入門

こんにちは。今回は、tradingview pine scriptについて初心者エンジニアに向けて、自動売買手法の基礎について解説します。pineスクリプトは、tradingviewプラットフォーム上で使用される独自のプログラミング言語であり、トレード戦略の自動化やテクニカル指標の作成に利用されます。この記事では、pineスクリプトの基本的な構文や関数、データの取得方法について説明し、自動売買手法の作成に必要な知識を身につけることができるでしょう。

### pineスクリプトの基本構文

pineスクリプトは、c言語に似た構文を持っています。プログラムは1つ以上のスクリプトブロックで構成され、それぞれのブロックは"//@version"ディレクティブで始まります。以下は、最も基本的なpineスクリプトの構文です。

```pine
//@version=4
study(title="my script", shorttitle="ms")
```

- "@version"ディレクティブは、スクリプトがどのバージョンのpineスクリプトを使用しているかを指定します。現在のバージョンは4です。
- "study"関数は、トレーディングビューのチャート上に指標を表示するために使用されます。"title"と"shorttitle"の引数には、それぞれ指標の完全なタイトルと短縮タイトルを設定します。

### エントリーシグナルの作成と条件設定方法

エントリーシグナルは、トレードを開始するための条件を定義するものです。pineスクリプトでは、トレーディングビューの組み込み関数を使用してエントリーシグナルを作成することができます。

以下の例では、単純な移動平均線（sma）のクロスオーバーをエントリーシグナルとします。

```pine
//@version=4
study(title="moving average crossover", shorttitle="ma cross")

// 短期smaのパラメーター
shortsma = sma(close, 10)

// 長期smaのパラメーター
longsma = sma(close, 30)

// エントリーシグナルの条件
entrysignal = crossover(shortsma, longsma)

// エントリーシグナルがtrueの場合に青色の三角形を表示する
plotshape(entrysignal, title="entry signal", style=shape.triangleup, color=color.blue)
```

この例では、"sma"関数を使用して短期smaと長期smaを計算します。そして、"crossover"関数を使用して短期smaが長期smaを上回った場合にtrueを返します。エントリーシグナルがtrueの場合には、青色の上向きの三角形が表示されます。

### 利益確定と損切り戦略の実装手順

利益確定と損切り戦略は、トレードの利益を最大化し損失を最小に抑えるために重要な要素です。pineスクリプトでは、"strategy.exit"関数を使用して利益確定と損切りの条件を設定することができます。

以下の例では、エントリーシグナルがtrueの場合に買いポジションを取り、利益確定と損切りの条件を設定します。

```pine
//@version=4
strategy(title="profit target and stop loss", shorttitle="pt/sl")

// エントリーシグナルの条件
entrysignal = crossover(shortsma, longsma)

// 買いポジションの取得
if (entrysignal)
    strategy.entry("buy", strategy.long)

// 利益確定の条件（取引量の2倍の利益）
profittarget = strategy.position_avg_price * 2
strategy.exit("sell", "buy", limit=profittarget)

// 損切りの条件（取引量の1倍の損失）
stoploss = strategy.position_avg_price * 1
strategy.exit("stop loss", "buy", stop=stoploss)
```

この例では、"strategy.entry"関数を使用してエントリーシグナルがtrueの場合に買いポジションを取得します。そして、"strategy.exit"関数を使用して利益確定と損切りの条件を設定します。利益確定の条件は、ポジションの平均価格の2倍、損切りの条件はポジションの平均価格の1倍です。

### ポジション管理とリスク管理のベストプラクティス

トレードにおいては、ポジション管理とリスク管理が非常に重要です。pineスクリプトでは、"strategy.position\_size"および"strategy.risk"関数を使用してポジションサイズとリスク設定を行うことができます。

以下の例では、口座の資産の10％をリスクとし、トレードのたびにそのリスクに基づいて最適なポジションサイズを計算します。

```pine
//@version=4
strategy(title="position and risk management", shorttitle="pos/risk")

// リスク設定
riskpercentage = 0.1

// リスクに基づいて最適なポジションサイズを計算
positionsize = strategy.equity * riskpercentage / close

// エントリーシグナルの条件
entrysignal = crossover(shortsma, longsma)

// 買いポジションの取得
if (entrysignal)
    strategy.entry("buy", strategy.long, qty=positionsize)
```

この例では、"strategy.equity"を使用して現在の口座の資産を取得し、その10％をリスクとして設定します。そして、リスクに基づいて最適なポジションサイズを計算します。エントリーシグナルがtrueの場合には、計算されたポジションサイズで買いポジションを取得します。

### バックテストと最適化：戦略の評価と改善

最後に、pineスクリプトを使用してバックテストを行い、戦略の評価と改善を行う方法を見ていきましょう。tradingviewでは、バックテストエンジンを使用して過去のデータに基づいて戦略をテストすることができます。

以下の例では、"strategy.backtest"関数を使用してバックテストを実行し、取引所の手数料やスリッページを考慮した戦略の評価を行います。

```pine
//@version=4
strategy(title="backtest and optimization", shorttitle="backtest")

// エントリーシグナルの条件
entrysignal = crossover(shortsma, longsma)

// 買いポジションの取得
if (entrysignal)
    strategy.entry("buy", strategy.long)

// ストラテジーのバックテストと最適化
strategy.backtest("backtest", "buy", commission_type=strategy.commission.percent, commission_value=0.1)
```

この例では、"strategy.backtest"関数を使用してバックテストを実行します。第一引数にはバックテストの名前を指定し、第二引数にはエントリーシグナルの買い注文を指定します。また、"commission_type"引数と"commission_value"引数を使用して取引所の手数料を設定します。バックテスト結果を元に最適な戦略を見つけて改善することができます。

以上が、tradingview pine scriptについて初心者エンジニア向けの自動売買手法の基礎についての解説でした。pineスクリプトは強力なツールであり、自動売買手法の作成や戦略の評価・改善に役立ちます。さらに詳しい情報や応用的な使い方を学ぶために、下記の参考記事をご覧ください。

- [pine script tutorial](https://www.tradingview.com/script/tutorials/)
- [pine script language reference manual](https://www.tradingview.com/pine-script-reference/v4/)



## 【TradingView】Pine Script関連のまとめ
https://hack-note.com/summary/tradingview-pine-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
