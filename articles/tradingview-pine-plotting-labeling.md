<!--
title:   【tradingview】pineスクリプト：プロットとラベルの描画
tags:    TradingView,pine
id:      b794ac1b4de5cd16a641
private: false
-->


## tradingview pine scriptについて初心者エンジニアに向けて

こんにちは。今回は、tradingview pine scriptについて初心者エンジニアに向けて、プロットとラベルの描画方法について解説したいと思います。pineスクリプトは、取引所やチャート分析プラットフォームであるtradingviewで使用される独自のスクリプト言語です。この記事では、pineスクリプトでのプロットとラベルの描画方法について詳しく説明していきます。

### プロットの基本的な描画方法

まずは、pineスクリプトを使用してプロットを描画する基本的な方法を紹介します。プロットは、チャート上に縦線や点などの形状でデータを可視化するために使用されます。以下のサンプルコードを見てみましょう。

```pine
//@version=4
study(title="simple plot example", shorttitle="spx")
plot(close)
```

このコードでは、`plot`関数を使用して現在の終値`close`を描画しています。`plot`関数は、1つのシリーズデータを受け取り、デフォルトの線の色でグラフ上にプロットします。

### プロットのスタイルとカスタマイズ

次に、プロットのスタイルやカスタマイズオプションについて説明します。プロットのスタイルを変更することで、線の色や種類、サイズなどをカスタマイズすることができます。以下のサンプルコードを見てみましょう。

```pine
//@version=4
study(title="custom plot example", shorttitle="spx")
plot(close, color=color.red, linewidth=2, style=plot.style_circles)
```

このコードでは、`plot`関数の引数に`color`、`linewidth`、`style`のオプションを追加しています。`color`オプションでは、プロットの色を指定することができます。ここでは赤色を指定しています。`linewidth`オプションでは、プロットの線の太さを指定することができます。ここでは2を指定しています。`style`オプションでは、プロットのスタイルを指定することができます。ここでは、円形の点を指定しています。

### ラベルの追加と表示位置の調整

次に、pineスクリプトでのラベルの追加と表示位置の調整方法について解説します。ラベルは、プロットに付随するテキストであり、データや情報を表示するために使用されます。以下のサンプルコードを見てみましょう。

```pine
//@version=4
study(title="label example", shorttitle="spx")
plot(close, color=color.red, linewidth=2, style=plot.style_circles)
label.new(x=bar_index, y=close, text="close", color=color.blue, textcolor=color.white, style=label.style_label_down)
```

このコードでは、`label.new`関数を使用してラベルを追加しています。`x`オプションは、ラベルの横位置を指定します。ここでは現在のバーのインデックスを指定しています。`y`オプションは、ラベルの縦位置を指定します。ここでは現在の終値`close`を指定しています。`text`オプションは、ラベルに表示するテキストを指定します。ここでは"close"というテキストを指定しています。`color`オプションは、ラベルの背景色を指定します。ここでは青色を指定しています。`textcolor`オプションは、ラベルのテキストの色を指定します。ここでは白色を指定しています。`style`オプションは、ラベルのスタイルを指定します。ここでは下向きのラベルを指定しています。

### プロットとラベルの色やサイズの変更

pineスクリプトでは、プロットやラベルの色やサイズをカスタマイズすることもできます。以下のサンプルコードを見てみましょう。

```pine
//@version=4
study(title="custom plot and label example", shorttitle="spx")
plot(close, color=color.blue, linewidth=2, style=plot.style_circles)
label.new(x=bar_index, y=close, text="close", color=color.yellow, textcolor=color.black, style=label.style_label_up)
```

このコードでは、プロットとラベルの色を変更しています。`plot`関数の`color`オプションでは、プロットの色を青色に変更しています。`label.new`関数の`color`オプションでは、ラベルの背景色を黄色に変更しています。また、`textcolor`オプションでは、ラベルのテキストの色を黒色に変更しています。このように、pineスクリプトではプロットやラベルの色やサイズをカスタマイズすることができます。

### プロットとラベルを活用した情報の可視化

最後に、プロットとラベルを活用してデータや情報を可視化する方法について説明します。プロットとラベルを組み合わせることで、テクニカル指標やトレンドラインなど、さまざまな分析結果をチャート上に表示することができます。

例えば、以下のようなコードを作成してみましょう。

```pine
//@version=4
study(title="rsi and bollinger bands example", shorttitle="spx")

length = input(14, minval=1, title="length")
src = close

rsivalue = rsi(src, length)
plot(rsivalue, color=color.blue, title="rsi")

upperband = rsivalue + 10
lowerband = rsivalue - 10

plot(upperband, color=color.red, title="upper band")
plot(lowerband, color=color.green, title="lower band")

label.new(x=bar_index, y=rsivalue, text="rsi", color=color.blue, textcolor=color.white, style=label.style_label_up)
```

このコードでは、rsi(相対力指数)とボリンジャーバンドを計算し、プロットとラベルを使用してテクニカル指標を可視化しています。`rsi`関数を使用してrsiを計算し、`plot`関数を使用してrsiの値を描画しています。また、rsiの値に対して上限と下限を設定し、ボリンジャーバンドを表示しています。さらに、`label.new`関数を使用してrsiのラベルを表示しています。

これらのプロットとラベルを活用した可視化方法は、トレードの意思決定支援やトレンドの分析など、さまざまな分野で活用することができます。

### まとめ

以上、tradingview pine scriptにおけるプロットとラベルの描画方法について解説しました。pineスクリプトを使用することで、チャート上にデータや情報を視覚的に表示することができます。プロットやラベルのスタイルやカスタマイズオプションを用いることで、より見やすいチャートを作成することができます。また、プロットとラベルを組み合わせることで、テクニカル指標やトレンドラインなどの情報を可視化することができます。これらの方法を活用して、自分自身の取引戦略や分析手法に応じたチャートを作成してみてください。tradingview pine scriptの学習は、トレードにおける意思決定のサポートや戦略の開発において非常に役立つスキルです。是非、積極的に取り組んでみてください。

### 参考ブログ記事

- [tradingview公式ドキュメント：plot](https://jp.tradingview.com/pine-script-reference/v4/#fun_plot)
- [tradingview公式ドキュメント：label](https://jp.tradingview.com/pine-script-reference/v4/#fun_label)

## プロットの基本的な描画方法

プロットは、チャート上に縦線や点などの形状でデータを可視化するために使用されます。pineスクリプトでは、プロットを描画するための`plot`関数を使用します。`plot`関数は、1つのシリーズデータを受け取り、デフォルトの線の色でグラフ上にプロットします。

以下に、プロットの基本的な描画方法のサンプルコードを示します。

```pine
//@version=4
study(title="simple plot example", shorttitle="spx")
plot(close)
```

このコードでは、現在の終値`close`をプロットしています。`plot`関数の引数には、プロットしたいデータを指定します。ここでは終値を指定しています。プロットされた結果は、デフォルトの線の色でグラフ上に表示されます。

## プロットのスタイルとカスタマイズ

プロットのスタイルをカスタマイズすることで、線の色や種類、サイズなどを変更することができます。pineスクリプトでは、`plot`関数のオプションを使用して、プロットのスタイルを指定することができます。以下に、プロットのスタイルとカスタマイズのサンプルコードを示します。

```pine
//@version=4
study(title="custom plot example", shorttitle="spx")
plot(close, color=color.red, linewidth=2, style=plot.style_circles)
```

このコードでは、`plot`関数の引数に`close`を指定して終値をプロットしています。また、`color`オプションでプロットの色を赤に指定し、`linewidth`オプションでプロットの線の太さを2に指定しています。さらに、`style`オプションで円形の点をプロットのスタイルとして指定しています。

## ラベルの追加と表示位置の調整

ラベルは、プロットに付随するテキストであり、データや情報を表示するために使用されます。pineスクリプトでは、`label.new`関数を使用してラベルを追加することができます。また、`label.new`関数のオプションを使用することで、ラベルの表示位置などを調整することができます。以下に、ラベルの追加と表示位置の調整のサンプルコードを示します。

```pine
//@version=4
study(title="label example", shorttitle="spx")
plot(close, color=color.red, linewidth=2, style=plot.style_circles)
label.new(x=bar_index, y=close, text="close", color=color.blue, textcolor=color.white, style=label.style_label_down)
```

このコードでは、`label.new`関数を使用してラベルを追加しています。`x`オプションには、ラベルの横位置を指定します。ここでは現在のバーのインデックスを指定しています。`y`オプションには、ラベルの縦位置を指定します。ここでは現在の終値`close`を指定しています。`text`オプションには、ラベルに表示するテキストを指定します。ここでは"close"というテキストを指定しています。`color`オプションには、ラベルの背景色を指定します。ここでは青色を指定しています。`textcolor`オプションには、ラベルのテキストの色を指定します。ここでは白色を指定しています。`style`オプションには、ラベルのスタイルを指定します。ここでは下向きのラベルを指定しています。

## プロットとラベルの色やサイズの変更

プロットやラベルの色やサイズをカスタマイズすることも可能です。`plot`や`label.new`のオプションを使用して、色やサイズを指定することができます。以下に、プロットとラベルの色やサイズを変更するサンプルコードを示します。

```pine
//@version=4
study(title="custom plot and label example", shorttitle="spx")
plot(close, color=color.blue, linewidth=2, style=plot.style_circles)
label.new(x=bar_index, y=close, text="close", color=color.yellow, textcolor=color.black, style=label.style_label_up)
```



## 【TradingView】Pine Script関連のまとめ
https://hack-note.com/summary/tradingview-pine-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
