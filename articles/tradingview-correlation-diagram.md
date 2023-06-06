<!--
title:   【解説】tradingviewで相関図を表示する時のpineコード
tags:    pine,“tradingview,投資”
id:      5bbb26e64859d5869c2f
private: false
-->


こんにちは。今回は、tradingviewについて初心者エンジニアに向けて、相関図を表示するためのpineコードについて解説します。

投資する際には、複数の銘柄の動向を把握することが重要です。特定の銘柄が上がったり下がったりする要因は多岐にわたりますが、株価や為替レートなど、相関する銘柄があることがあります。そのため、投資家は複数の銘柄の相関関係を把握し、リスクを分散させた投資をする必要があります。

そこで、tradingviewでは相関図という機能が用意されており、複数の銘柄の相関関係を一目で確認することができます。この記事では、tradingviewの相関図をpineコードを使って表示する方法について解説します。

【pineコードで相関図を表示する方法】

相関図を表示するためには、pineコードというプログラミング言語を使用します。pineコードは、tradingviewが提供するテクニカル指標を簡単に作成できる言語です。以下に、相関図を表示するためのpineコードを示します。

```
//@version=4
study("correlation chart", overlay=true)
src1=input(title='symbol1', type=input.string, defval='aapl')
src2=input(title='symbol2', type=input.string, defval='goog')
src3=input(title='symbol3', type=input.string, defval='tsla')
src4=input(title='symbol4', type=input.string, defval='msft')

s1 = security(src1, timeframe.period, close)
s2 = security(src2, timeframe.period, close)
s3 = security(src3, timeframe.period, close)
s4 = security(src4, timeframe.period, close)
pair1 = correlation(s1, s2, 252, 1)
pair2 = correlation(s1, s3, 252, 1)
pair3 = correlation(s1, s4, 252, 1)
pair4 = correlation(s2, s3, 252, 1)
pair5 = correlation(s2, s4, 252, 1)
pair6 = correlation(s3, s4, 252, 1)

plot(pair1)
plot(pair2)
plot(pair3)
plot(pair4)
plot(pair5)
plot(pair6)
hline(0)
```

このpineコードは、aapl、goog、tsla、msftの4つの銘柄の相関図を表示するものです。src1〜src4までのinput関数で、比較したい4つの銘柄を指定します。correlation関数を使って、2つの銘柄の相関を計算しています。plot関数を使って、計算した相関をプロットします。最後に、hline関数を使って、相関係数0の横線を引きます。

【pineコードの解説】

以下に、pineコードの各行の解説を示します。

```
//@version=4
study("correlation chart", overlay=true)
```
「//@version=4」は、pineコードのバージョンを示しています。「study("correlation chart", overlay=true)」は、チャートに反映される指標のタイトルを設定しています。

```
src1=input(title='symbol1', type=input.string, defval='aapl')
src2=input(title='symbol2', type=input.string, defval='goog')
src3=input(title='symbol3', type=input.string, defval='tsla')
src4=input(title='symbol4', type=input.string, defval='msft')
```
「input関数」は、ユーザーが指定したパラメーターを入力するための関数です。ここでは、比較したい銘柄を指定できるようにするために使用しています。

```
s1 = security(src1, timeframe.period, close)
s2 = security(src2, timeframe.period, close)
s3 = security(src3, timeframe.period, close)
s4 = security(src4, timeframe.period, close)
```
「security関数」は、別のシンボル（銘柄）のデータを取得するための関数です。ここで使用しているcloseは、その銘柄の終値を示します。

```
pair1 = correlation(s1, s2, 252, 1)
pair2 = correlation(s1, s3, 252, 1)
pair3 = correlation(s1, s4, 252, 1)
pair4 = correlation(s2, s3, 252, 1)
pair5 = correlation(s2, s4, 252, 1)
pair6 = correlation(s3, s4, 252, 1)
```
「correlation関数」は、2つのシンボル間の相関を計算するための関数です。ここでは、それぞれのシンボルの組み合わせで相関を計算しています。

```
plot(pair1)
plot(pair2)
plot(pair3)
plot(pair4)
plot(pair5)
plot(pair6)
```
「plot関数」は、チャートに指標を表示するための関数です。ここでは、計算した相関を表示しています。

```
hline(0)
```
「hline関数」は、横線を引くための関数です。ここでは、相関係数0の横線を引いています。

【まとめ】

以上が、tradingviewの相関図を表示するためのpineコードです。pineコードは、テクニカル指標を自分で作成する際に必要不可欠な言語であり、相関図を表示する際にも役立つことがあります。

今回は、初めてpineコードを使って相関図を表示するためのコードについて解説しました。投資において、複数の銘柄の相関関係を把握することは非常に重要です。是非、pineコードを使って相関図を表示して、投資の意思決定にお役立てください。

【参考ブログ記事】

- tradingview公式ブログ「pine scriptでペアトレード：相関チャート」
(https://jp.tradingview.com/blog/pair-trading-with-pine-script-correlation-chart-55409/)
- quantlabs.net「tradingview: how to create a correlation table and uses it for pair trading」
(https://quantlabs.net/blog/2018/08/tradingview-how-to-calculate-correlation-coefficient-python-pair-trading/)

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
