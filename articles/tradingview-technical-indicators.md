<!--
title:   【tradingview】テクニカルインジケーターの使い方と設定方法
tags:    Python,TradingView,pine
id:      9d21cbcb0e5bf23a0e6c
private: false
-->


## テクニカルインジケーターの基本と種類の紹介

こんにちは。今回は、tradingviewについて初心者エンジニアに向けて、テクニカルインジケーターの使い方と設定方法について解説します。

テクニカルインジケーターは、株式や仮想通貨などの価格チャートから得られるデータを分析し、投資やトレードの判断を支援するためのツールです。tradingviewは、テクニカルインジケーターを使った分析に優れたプラットフォームとして人気があります。また、tradingviewはpythonのプログラミング言語を使用して、独自のテクニカルインジケーターを開発することもできます。

テクニカルインジケーターには、さまざまな種類があります。それぞれの指標がどのような情報を提供するのか、それぞれの特徴や使い方を紹介していきます。

## テクニカルインジケーターの設定とパラメーターの調整方法

テクニカルインジケーターを使用するには、まずチャートを表示し、指標を追加する必要があります。tradingviewでは、チャートの上部メニューから「テクニカルインジケーター」を選択し、表示したい指標を選ぶことができます。また、指標のパラメーターを調整することも可能です。

テクニカルインジケーターの設定方法について詳しく解説します。具体的な指標の設定例やパラメーターの調整方法を紹介します。

## 移動平均線の使い方と異なる期間の設定

移動平均線は、価格の平均値を計算し、その結果をグラフ上にプロットする指標です。移動平均線を使うことで、トレンドの方向性や転換のタイミングを把握することができます。移動平均線の期間を変更することで、異なるトレンドのサイクルに対応することも可能です。

以下に、移動平均線の使い方と異なる期間の設定方法の一例を示します。

```python
//@version=4
study(title="moving averages", shorttitle="ma", overlay=true)
len = input(20, minval=1, title="length")
src = input(close, title="source")
sma = sma(src, len)
plot(sma, color=color.blue)
```

移動平均線には、さまざまな種類があります（単純移動平均線、指数平滑移動平均線、加重移動平均線など）。それぞれの移動平均線の特徴や使い方についても紹介します。

## macd（移動平均収束拡散）の活用とトレンド反転のシグナル

macd（moving average convergence divergence）は、移動平均線の収束と拡散を調べることで、トレンドの強さと転換のシグナルを提供する指標です。macdは、シグナル線とmacdヒストグラムから成り立っており、それぞれの要素の値や相互の関係を分析することが重要です。

以下に、macdの活用とトレンド反転のシグナルを得るための一例を示します。

```python
//@version=4
study(title="moving average convergence divergence", shorttitle="macd", overlay=false)
[macdline, signalline, _] = macd(close, 12, 26, 9)
plot(macdline - signalline, title="macd histogram", color=color.blue)
plot(macdline, title="macd line", color=color.red)
plot(signalline, title="signal line", color=color.green)
```
macdの解説に加えて、macdヒストグラムやシグナル線の意味と使い方についても説明します。

## rsi（相対力指数）の設定と過買い・過売りの判断方法

rsi（relative strength index）は、過買い・過売りの判断やトレンドの逆転ポイントの特定に役立つ指標です。rsiは、一定期間の上昇幅と下落幅を比較し、価格の強さを示す数値を計算します。通常は14日間を使用しますが、設定は自由に変更することができます。

以下に、rsiの設定と過買い・過売りの判断方法の一例を示します。

```python
//@version=4
study("relative strength index", shorttitle="rsi", overlay=true)
rsiperiod = input(14, title="rsi period")
overboughtlevel = input(70, title="overbought level")
oversoldlevel = input(30, title="oversold level")
rsivalue = rsi(close, rsiperiod)
plot(rsivalue, title="rsi", color=color.blue)
hline(overboughtlevel, title="overbought level", color=color.red)
hline(oversoldlevel, title="oversold level", color=color.green)
```

rsiの使い方や設定方法について解説します。また、過買い・過売りの判断方法や、rsiを使ったトレード戦略についても紹介します。

## ボリンジャーバンドの活用と相場のボラティリティ分析

ボリンジャーバンドは、相場のボラティリティを分析するための指標です。ボリンジャーバンドは、価格の移動平均線を中心に、価格の変動幅を示す上下のバンドで構成されています。価格がバンド内に収束している場合は静かな相場であり、価格がバンド外に逸脱している場合はボラティリティが高い相場となります。

以下に、ボリンジャーバンドの活用と相場のボラティリティ分析の一例を示します。

```python
//@version=4
study(title="bollinger bands", shorttitle="bb", overlay=true)
length = input(20, minval=1, title="length")
mult = input(2.0, minval=0.1, maxval=5, title="multiplier")
src = input(close, title="source")
basis = sma(src, length)
dev = mult * stdev(src, length)
upper = basis + dev
lower = basis - dev
plot(basis, title="basis", color=color.blue)
p1 = plot(upper, title="upper band", color=color.green)
p2 = plot(lower, title="lower band", color=color.red)
fill(p1, p2, color=color.gray, transp=90)
```

ボリンジャーバンドの使い方やパラメーターの設定方法について解説します。また、ボリンジャーバンドを使ったトレード戦略や相場のボラティリティ分析手法についても紹介します。

以上が、tradingviewにおけるテクニカルインジケーターの使い方と設定方法についての解説です。テクニカルインジケーターはトレードや投資の助けとなる重要なツールであり、正しい使い方を知ることが成功の鍵となります。ぜひ、この記事を参考にして、tradingviewでのテクニカルインジケーターの活用を始めてみてください。

参考url:
1. [tradingview公式ドキュメンテーション](https://jp.tradingview.com/support/solutions/43000065650-%e3%83%86%e3%82%af%e3%83%8b%e3%82%ab%e3%83%ab-%e9%96%8b%e7%99%ba-%e8%a8%80%e8%aa%9e-pine-%e3%81%a8-type%e3%81%a8-tv%e7%b7%b4%e7%bf%92%e5%88%b8%e3%81%ab%e3%81%a4%e3%81%84%e3%81%a6/)
2. [為替チャートの達人](https://forexpedia.jp/%e3%83%86%e3%82%af%e3%83%8b%e3%82%ab%e3%83%ab%e3%82%a4%e3%83%b3%e3%82%b8%e3%82%b1%e3%83%bc%e3%82%bf%e3%83%bc/)



## 【TradingView】関連のまとめ
https://hack-note.com/summary/tradingview-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
