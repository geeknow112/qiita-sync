<!--
title:   【解説】雇用統計が出た時にtradingviewチャートを活かしきるpineコード
tags:    Python,TradingView,pine,投資
id:      2441ca281b39e3bb264b
private: false
-->


こんにちは。今回は、tradingviewについて初心者エンジニアに向けて、雇用統計の発表を活かすpineコードについて解説します。

tradingviewとは、世界中のトレーダーが利用している、チャート分析を行なうためのオンラインツールです。pine codeとは、tradingviewの独自のプログラミング言語で、ユーザーが自分自身のアイディアをテストしたり、指標を計算したりすることができます。また、pythonのような既存の言語とのポートフォリオのapi接続も可能です。

このようなtradingviewの魅力を知り、pineコードの基礎を学んだ後は、雇用統計の発表を利用するpineコードを作成することができます。雇用統計は、経済の健康度を示す重要な指標であり、市場を大きく動かす可能性があるため、トレーダーにとって欠かせない情報です。

雇用統計が発表されるたびに、市場は大きく揺れます。しかし、tradingviewのpineコードを活用することで、自動的に雇用統計の発表を検知し、チャートに反映させることができます。これにより、何度もチャートを監視しなくても、トレーディングアイディアを形成することができます。

具体的なpineコードの例を挙げると、以下のようなものがあります。

```
// 非農業部門雇用者数と失業率の平均値
value = (nonfarm_payrolls + unemployment_rate) / 2
plot(value)
```

上記のコードは、非農業部門雇用者数と失業率の平均値を計算し、`plot()`関数でグラフに表示します。このように、pineコードを活用することで、チャート上で雇用統計を確認することができます。

また、pythonを利用することで、pineコードとtradingviewのapiを接続し、パフォーマンスを向上させることができます。例えば、以下のようなpythonコードを書くことができます。

```
import ccxt
import talib
import pandas as pd

exchange = ccxt.binance({
    'apikey': 'your_api_key',
    'secret': 'your_secret',
})

data = exchange.fetch_ohlcv('btc/usdt', '1h')
df = pd.dataframe(data)
df.columns = ['time', 'open', 'high', 'low', 'close', 'volume']

sma = talib.sma(df['close'], timeperiod=20)

print(sma)
```

上記のpythonコードは、binanceのapiを使用して、btc/usdtの価格情報を取得し、20期間の単純移動平均を算出します。これをtradingviewに反映させることで、より精密なトレーディングシグナルを得ることができます。

まとめると、tradingviewのpineコードを活用することで、雇用統計の発表を自動的に検知し、チャートに反映させることができます。また、pythonを利用することで、apiとの接続を確立し、より詳細なパフォーマンスを実現することができます。これらのコードを学ぶことで、トレードの経験を豊かにし、より優れた投資を行なうことができます。

参考：

- https://www.tradingview.com/pine-script-docs/en/v4/
- https://www.tradingview.com/blog/en/programming-with-tradingview-16380/
- https://www.backtrader.com/docu/quickstart/quickstart/
- https://www.quantopian.com/docs/algorithm-api-reference

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
