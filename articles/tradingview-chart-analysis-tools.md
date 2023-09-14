<!--
title:   【tradingview】チャート分析ツールの活用方法
tags:    Python,TradingView,pine
id:      272edf7f0bd7aa1143b9
private: false
-->


## キャンドルスティックチャートの解読と使い方

キャンドルスティックチャートは、トレーダーにとって非常に重要なツールです。その見方や使い方を解説します。

### キャンドルスティックチャートとは
キャンドルスティックチャートは、株価や通貨などの価格変動を視覚的に表現したものです。1本のキャンドルは、ある一定期間のオープン、クローズ、ハイ、ローの4つの値を表します。オープンとクローズの間の部分が実体（ブロディ）と呼ばれ、価格の上昇と下降を示します。また、ハイとローの間の線は、影（シャドウ）と呼ばれ、高値と安値を示します。

キャンドルスティックチャートを活用することで、市場のトレンドや価格の変動の傾向を把握することができます。

### キャンドルスティックのパターンとその意味
キャンドルスティックチャートには、様々なパターンが存在します。その中でも代表的なパターンとその意味を解説します。

#### ドジ
![ドジパターン](https://tradingview.com/images/xqnbtyd.png)

ドジは、オープンとクローズの価格がほぼ同じで、実体が非常に小さいキャンドルです。ドジは市場の転換点を示す可能性があります。下げトレンドの中で上ヒゲ（上の影）が長いドジが現れた場合、下げ相場が一巡して上昇トレンドに転換する可能性があります。

#### 陰線と陽線
![上昇トレンドの陽線と陰線](https://tradingview.com/images/e2bjt1j.png)

陽線は、クローズの価格がオープンの価格よりも高くなる上昇トレンドを示します。一方、陰線は、クローズの価格がオープンの価格よりも低くなる下降トレンドを示します。

#### インサイドバー
![インサイドバーパターン](https://tradingview.com/images/bouhaq2.png)

インサイドバーは、前日のキャンドルの範囲に収まる小さなキャンドルです。これは相場の一時停止を示すことがあります。インサイドバーが連続して現れた場合、大きな相場の変動が起こる可能性があります。

### サンプルコード（python）

```python

import pandas as pd
import mplfinance as mpf

# データの準備
data = pd.read_csv('price_data.csv', index_col=0, parse_dates=true)
data.columns = ['open', 'high', 'low', 'close', 'volume']

# キャンドルスティックチャートの描画
mpf.plot(data, type='candle', style='yahoo', title='price chart')

```

このサンプルコードでは、`pandas`を使用してcsvファイルから価格データを読み込みます。`mplfinance`を使用してキャンドルスティックチャートを描画します。`type='candle'`とすることでキャンドルスティックチャートを指定し、`style='yahoo'`とすることでチャートのスタイルを指定しています。

## テクニカルインジケーターの活用と分析手法

テクニカルインジケーターは、価格変動の傾向や相場の方向性を分析するためのツールです。ここでは、代表的なテクニカルインジケーターとその活用方法を解説します。

### 移動平均線
移動平均線は、一定期間の価格の平均値を算出し、折れ線グラフで表示します。移動平均線は、価格のトレンドの方向性や抵抗水準を示すために使用されます。

```python

import pandas as pd
import mplfinance as mpf

# データの準備
data = pd.read_csv('price_data.csv', index_col=0, parse_dates=true)
data.columns = ['open', 'high', 'low', 'close', 'volume']

# 移動平均線の計算
data['sma20'] = data['close'].rolling(window=20).mean()
data['sma50'] = data['close'].rolling(window=50).mean()

# グラフの描画
mpf.plot(data, type='line', style='yahoo', title='moving averages', ylabel='price')

```

このサンプルコードでは、移動平均線を計算し、折れ線グラフで表示する方法を示しています。`rolling`メソッドを使用して移動平均を計算し、`plot`関数を使用してチャートを描画します。

### rsi（相対力指数）
rsi（相対力指数）は、過買い状態と過売り状態を示すための指標です。rsiの値が70を超えると過買い状態となり、売りのシグナルとなる可能性があります。一方、rsiの値が30を下回ると過売り状態となり、買いのシグナルとなる可能性があります。

```python

import pandas as pd
import mplfinance as mpf
import talib

# データの準備
data = pd.read_csv('price_data.csv', index_col=0, parse_dates=true)
data.columns = ['open', 'high', 'low', 'close', 'volume']

# rsiの計算
data['rsi'] = talib.rsi(data['close'], timeperiod=14)

# グラフの描画
mpf.plot(data, type='line', style='yahoo', title='rsi', ylabel='rsi', secondary_y=['rsi'])

```

このサンプルコードでは、`talib`ライブラリを使用してrsiを計算し、折れ線グラフで表示する方法を示しています。`rsi`関数には、価格データと計算期間を指定します。`secondary_y`パラメータには、rsiを第二のy軸に表示することを指定します。

## ボリンジャーバンドの使用と相場のボラティリティ分析

ボリンジャーバンドは、相場のボラティリティを分析するためのツールです。ここでは、ボリンジャーバンドの使用方法と相場のボラティリティ分析について解説します。

```python

import pandas as pd
import mplfinance as mpf
import talib

# データの準備
data = pd.read_csv('price_data.csv', index_col=0, parse_dates=true)
data.columns = ['open', 'high', 'low', 'close', 'volume']

# ボリンジャーバンドの計算
upper, middle, lower = talib.bbands(data['close'], timeperiod=20, nbdevup=2, nbdevdn=2)

# グラフの描画
apds = [
    mpf.make_addplot(upper, color='g'),
    mpf.make_addplot(middle, color='b'),
    mpf.make_addplot(lower, color='r'),
]
mpf.plot(data, type='candle', style='yahoo', title='bollinger bands', ylabel='price', addplot=apds)

```

このサンプルコードでは、`talib`ライブラリを使用してボリンジャーバンドを計算し、キャンドルスティックチャートに表示する方法を示しています。`bbands`関数には、価格データ、計算期間、バンドの標準偏差を指定します。`make_addplot`関数を使用してボリンジャーバンドを追加し、`addplot`パラメータに指定します。

## 移動平均線の利用とトレンドの把握方法

移動平均線は、価格のトレンドの把握やサポート・レジスタンスの判断に活用されます。ここでは、移動平均線の利用方法とトレンドの把握のための手法を解説します。

```python

import pandas as pd
import mplfinance as mpf

# データの準備
data = pd.read_csv('price_data.csv', index_col=0, parse_dates=true)
data.columns = ['open', 'high', 'low', 'close', 'volume']

# 移動平均線の計算
data['sma20'] = data['close'].rolling(window=20).mean()
data['sma50'] = data['close'].rolling(window=50).mean()

# グラフの描画
mpf.plot(data, type='line', style='yahoo', title='moving averages', ylabel='price')

```

このサンプルコードでは、移動平均線を計算し、折れ線グラフで表示する方法を示しています。`rolling`メソッドを使用して移動平均を計算し、`plot`関数を使用してチャートを描画します。

## rsi（相対力指数）の解説と過買い・過売りの判断

rsi（相対力指数）は、過買い状態と過売り状態を判断するための指標です。ここでは、rsiの解説と過買い・過売りの判断方法を解説します。

```python

import pandas as pd
import mplfinance as mpf
import talib

# データの準備
data = pd.read_csv('price_data.csv', index_col=0, parse_dates=true)
data.columns = ['open', 'high', 'low', 'close', 'volume']

# rsiの計算
data['rsi'] = talib.rsi(data['close'], timeperiod=14)

# グラフの描画
mpf.plot(data, type='line', style='yahoo', title='rsi', ylabel='rsi', secondary_y=['rsi'])

```

このサンプルコードでは、`talib`ライブラリを使用してrsiを計算し、折れ線グラフで表示する方法を示しています。`rsi`関数には、価格データと計算期間を指定します。`secondary_y`パラメータには、rsiを第二のy軸に表示することを指定します。

## フィボナッチリトレースメントの活用とサポート・レジスタンスの設定

フィボナッチリトレースメントは、価格変動のサポート・レジスタンスレベルを設定するためのツールです。ここでは、フィボナッチリトレースメントの活用方法とサポート・レジスタンスの設定手法を解説します。

```python

import pandas as pd
import mplfinance as mpf
import talib

# データの準備
data = pd.read_csv('price_data.csv', index_col=0, parse_dates=true)
data.columns = ['open', 'high', 'low', 'close', 'volume']

# フィボナッチリトレースメントの計算
high = data['high']
low = data['low']
fibonacci_levels = talib.fib(high, low, 0.382, 0.618)

# グラフの描画
apds = [
    mpf.make_addplot(fibonacci_levels, linestyle='dashed', color='g')
]
mpf.plot(data, type='candle', style='yahoo', title='fibonacci retracement', ylabel='price', addplot=apds)

```

このサンプルコードでは、`talib`ライブラリを使用してフィボナッチリトレースメントを計算し、キャンドルスティックチャートに表示する方法を示しています。`fib`関数には、高値と安値のデータ、サポートとレジスタンスの水準（ここでは0.382と0.618）を指定します。`make_addplot`関数を使用してフィボナッチリトレースメントを追加し、`addplot`パラメータに指定します。

以上が、tradingviewについて初心者エンジニアに向けたチャート分析ツールの活用方法の解説でした。キャンドルスティックチャートの解読やテクニカルインジケーターの活用、ボリンジャーバンドや移動平均線、rsi、フィボナッチリトレースメントの使用方法など、これらのツールを駆使して相場分析を行うことが大切です。是非、トレーディングビューを使ってチャート分析を始めてみてください。

参考ブログ記事：
- [「トレーディングビューの活用方法」](https://qiita.com/shampooha/items/be11709ebe81fd4e70f8)
- [「トレーディングビューの使い方」](https://qiita.com/keisukesakai48/items/157744a948d2bf116a17



## 【TradingView】関連のまとめ
https://hack-note.com/summary/tradingview-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
