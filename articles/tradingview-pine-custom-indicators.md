<!--
title: 【tradingview】pineスクリプトのカスタムインジケーター作成入門
tags: tradingview,pine
id: 
private: false
-->

## 【tradingview】pineスクリプトのカスタムインジケーター作成入門

こんにちは。今回は、tradingview pine scriptについて初心者エンジニアに向けて、カスタムインジケーターの作成方法について説明します。

トレーディングビュー（tradingview）は、世界中のトレーダーや投資家に利用されている人気の高いチャートプラットフォームです。pineスクリプトは、トレーディングビュー上でインジケーターやトレードアラートを作成するために使用される言語です。サインやアラートを表示するだけでなく、テクニカル指標のカスタマイズや独自のトレード戦略の実装も可能です。

本記事では、pineスクリプトの基本的な構造やデータ操作、プロットとカラーリング、条件分岐とループの活用方法、そして最適化とパフォーマンス向上のためのテクニックについて解説します。pineスクリプトの初心者から上級者まで、幅広いトレーダーやプログラマーに役立つ知識を提供します。

それでは、まずはpineスクリプトの基礎から学んでいきましょう。

## インジケーターの基本構造とpineスクリプトの基礎

まずは、pineスクリプトの基本構造について説明します。

pineスクリプトは、`study`関数とその中に含まれる`plot`関数を使用してインジケーターを作成します。以下は、簡単な移動平均線インジケーターの例です。

```pine
//@version=4
study("移動平均線", overlay=true)

length = input(14, minval=1, title="期間")
src = input(close, title="ソース")
ma = sma(src, length)

plot(ma, color=color.blue, title="移動平均線")
```

このスクリプトでは、`study`関数を使用して「移動平均線」のインジケーターを作成しています。`input`関数を使用してパラメーターを設定し、`sma`関数を使用して移動平均を計算しています。最後に、`plot`関数を使用して移動平均線をチャート上に表示しています。

このように、pineスクリプトでは、`study`関数と`plot`関数を組み合わせることでインジケーターを作成することができます。

pineスクリプトには、様々な関数や演算子が用意されており、データの操作や条件分岐、ループなどの制御構造を利用することができます。次に、それらの活用方法について見ていきましょう。

## pineスクリプトのデータ操作と算術演算子の活用方法

pineスクリプトでは、データ操作や算術演算子を利用してインジケーターやアラートを作成することができます。

たとえば、以下は、移動平均線のクロスオーバーアラートを作成する例です。

```pine
//@version=4
study("移動平均線クロスオーバーアラート", overlay=true)

length1 = input(14, minval=1, title="期間1")
length2 = input(28, minval=1, title="期間2")
src = input(close, title="ソース")
ma1 = sma(src, length1)
ma2 = sma(src, length2)

condition = crossover(ma1, ma2)
plotshape(condition, title="クロスオーバーアラート", location=location.belowbar, color=color.red, style=shape.labelup, text="クロス")

alertcondition(condition, title="クロスオーバーアラート", message="移動平均線がクロスしました！")
```

このスクリプトでは、`crossover`関数を使用して移動平均線のクロスオーバー条件を判定し、`plotshape`関数を使用してアラート条件が満たされた場合にチャート上にアラートを表示しています。さらに、`alertcondition`関数を使用してアラート条件が満たされた場合にメッセージを表示するアラートを設定しています。

このように、pineスクリプトではデータの操作や条件判定、アラートの表示などが簡単に行えるようになっています。

次に、プロットとカラーリングについて見ていきましょう。

## プロットとカラーリング：チャート上での情報表示と見やすさの向上

pineスクリプトでは、`plot`関数を使用してチャート上に情報を表示することができます。

たとえば、以下は、移動平均線の値をチャート上にプロットし、上昇トレンドと下降トレンドを色分けする例です。

```pine
//@version=4
study("移動平均線トレンド", overlay=true)

length = input(14, minval=1, title="期間")
src = input(close, title="ソース")
ma = sma(src, length)

plot(ma, color=color.blue, title="移動平均線")

uptrend = ma > ma[1]
downtrend = ma < ma[1]

bgcolor(uptrend ? color.green : downtrend ? color.red : na, transp=90)
```

このスクリプトでは、`sma`関数で計算した移動平均値を`plot`関数でチャート上にプロットしています。さらに、`uptrend`と`downtrend`というブール型の変数を定義し、`bgcolor`関数を使用して上昇トレンドの場合は緑、下降トレンドの場合は赤で背景を色分けしています。

このように、`plot`関数を活用してチャート上に情報を表示し、見やすさやトレンドの把握をサポートすることができます。

次に、条件分岐とループの活用方法について見ていきましょう。

## 条件分岐とループ：トレードシグナルの生成と複雑な戦略の実装

pineスクリプトでは、条件分岐やループを利用してトレードシグナルの生成や複雑なトレード戦略の実装が可能です。

たとえば、以下は、移動平均線のクロスオーバーを検出してエントリーポイントを生成する例です。

```pine
//@version=4
study("移動平均線トレードシグナル", overlay=true)

length1 = input(14, minval=1, title="期間1")
length2 = input(28, minval=1, title="期間2")
src = input(close, title="ソース")
ma1 = sma(src, length1)
ma2 = sma(src, length2)

condlong = crossover(ma1, ma2)
condshort = crossunder(ma1, ma2)

plotshape(condlong, title="買いシグナル", location=location.belowbar, color=color.green, style=shape.labelup, text="買い")
plotshape(condshort, title="売りシグナル", location=location.abovebar, color=color.red, style=shape.labeldown, text="売り")
```

このスクリプトでは、`crossover`関数と`crossunder`関数を使用して移動平均線のクロスオーバーやクロスアンダーを検出し、`plotshape`関数を使用してエントリーポイントのシグナルをチャート上に表示しています。

このように、条件分岐やループを活用することで、自分のトレード戦略に合わせた複雑なトレードシグナルやエントリーポイントの生成が可能です。

最後に、インジケーターの最適化とパフォーマンス向上のためのテクニックについて見ていきましょう。

## インジケーターの最適化とパフォーマンス向上のためのテクニック

pineスクリプトで作成したインジケーターは、パフォーマンスの改善や最適化が求められる場合があります。

たとえば、以下は、移動平均線の計算回数を減らすための最適化例です。

```pine
//@version=4
study("最適化例", overlay=true)

length = input(14, minval=1, title="期間")
src = input(close, title="ソース")

ma = na
ma := bar_index % length == 0 ? sma(src, length) : ma[1]

plot(ma, color=color.blue, title="移動平均線")
```

このスクリプトでは、`bar_index`を使用して現在のバーのインデックスを取得し、`bar_index % length == 0`という条件判定を行っています。これにより、移動平均線の計算は一定間隔ごとに行われるため、計算回数が減ってパフォーマンスが向上します。

pineスクリプトでは、他にも計算の最適化やバックテストの精度向上のためのテクニックがあります。これらのテクニックを活用することで、より効率的なインジケーターの作成が可能です。

## まとめ

本記事では、tradingview pine scriptについて初心者エンジニアに向けて、カスタムインジケーターの作成方法について解説しました。

pineスクリプトの基本構造やデータ操作、算術演算子の活用方法、プロットとカラーリング、条件分岐とループの活用方法、そしてインジケーターの最適化とパフォーマンス向上のためのテクニックについて学びました。

トレーディングビューでのインジケーター作成は、pineスクリプトを使用することで簡単に行うことができます。ぜひ、これらの知識を活用して自分だけのオリジナルなインジケーターやトレード戦略を作成してみてください。

　

## 【TradingView】Pine Script関連のまとめ
https://hack-note.com/summary/tradingview-pine-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

