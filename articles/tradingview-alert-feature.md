<!--
title:   【tradingview】アラート機能の活用とトレードへの応用
tags:    Python,TradingView,pine
id:      8c4cdffd07b988e5de9d
private: false
-->


## tradingviewについて初心者エンジニアに向けて、アラート機能の活用とトレードへの応用

こんにちは。今回は、tradingviewについて初心者エンジニアに向けて、アラート機能の活用とトレードへの応用についてご紹介します。

tradingviewは、株式や仮想通貨、外国為替などのテクニカルチャート分析ツールであり、多機能なアラート機能も備えています。アラート機能を活用することで、特定の条件が満たされた際に通知を受け取り、トレードのエントリー・エグジットなどのタイミングを見逃さずに行うことができます。

本記事では、アラートの設定方法や通知の受け方、さらにはプライスアラートやテクニカル指標アラート、ボリンジャーバンドアラート、移動平均線アラートなどの具体的な活用方法について解説します。さらに、アラートをトレードへの応用してエントリー・エグジットのタイミングを判断する方法についても触れます。

それでは、早速アラートの設定と通知の受け方から見ていきましょう。

## アラートの設定と通知の受け方

アラートの設定方法は、tradingviewのチャート画面上部にある「アラート」ボタンをクリックすることで行うことができます。アラートの設定には、価格、テクニカル指標、ボリンジャーバンド、移動平均など、様々な条件を組み合わせることができます。

以下は、価格アラートの設定サンプルコードです。

```python
//@version=4
study(title="example price alert", shorttitle="price alert", overlay=false)

// アラート対象の価格
alert_price = 100

// 現在の価格
current_price = close

// 価格がアラート対象の価格に達したらアラートを出す
if current_price >= alert_price
    alert("price alert triggered! current price: " + tostring(current_price))
```

このサンプルコードでは、tradingviewのpineエディタを利用しています。study関数を使い、チャートにインジケーターを表示することができます。

まず、`study`関数の引数には、`title`と`shorttitle`を指定します。これにより、チャート上にインジケーターのタイトルが表示されます。

次に、`alert_price`という変数にアラート対象の価格を設定します。現在の価格を取得するために、`close`関数を使って`current_price`という変数に格納します。

最後に、`if current_price >= alert_price`という条件分岐を行い、現在の価格がアラート対象の価格に達した場合に`alert`関数を使ってアラートを出します。`tostring`関数を使って変数を文字列に変換し、アラートメッセージに表示します。

アラートの通知方法は複数あり、通知設定ではメールやデスクトッププッシュ通知、sms、line notifyなど、様々な通知方法を選択することができます。各通知方法の設定方法については、tradingviewの公式ドキュメントや以下のブログ記事を参考にしてください。

- [tradingview 公式ドキュメント - アラート通知の設定方法](https://www.tradingview.com/ja/support/solutions/43000529348-%e3%82%a2%e3%83%a9%e3%83%bc%e3%83%88%e9%80%9a%e7%9f%a5-%e9%80%9a%e7%9f%a5%e3%81%ae%e3%81%be%e3%81%a8%e3%82%81/#2_%e3%81%82%e3%82%8b%e3%81%84%e3%81%a6%e3%81%af%e3%80%81%e3%81%9d%e3%82%8c%e3%82%92%e5%8f%97%e3%81%91%e3%81%a6%e3%81%be%e3%81%99%e3%81%8b%ef%bc%9f)

- [tradingviewのアラート一覧【音声設定】【取引所登録】【連携先】【通知先】](https://support.coinchek.net/hc/ja/articles/360018282473-tradingview%e3%81%ae%e3%82%a2%e3%83%a9%e3%83%bc%e3%83%88%e4%b8%80%e8%a6%a7-%e9%9f%b3%e5%a3%b0%e8%a8%ad%e5%ae%9a-%e5%8f%96%e5%bc%95%e6%89%80%e7%99%bb%e9%8c%b2-%e9%80%a3%e6%90%ba%e5%85%88-%e9%80%9a%e7%9f%a5%e5%85%88)

アラートの設定方法と通知の受け方について説明しましたが、次にプライスアラートの活用とサポート・レジスタンスの監視について見ていきましょう。

## プライスアラートの活用とサポート・レジスタンスの監視

プライスアラートは、特定の価格に到達した際に通知を受けることができる機能です。価格がサポートやレジスタンスラインといった重要な水準に到達した場合、アラートを設定しておくことで、重要なトレードのタイミングを見逃すことがありません。

以下は、比較演算子を使ったサンプルコードです。

```python
//@version=4
study(title="example support and resistance alert", shorttitle="s&r alert", overlay=false)

// サポートとレシスタンスの価格帯
support_price = 100
resistance_price = 200

// 現在の価格
current_price = close

// 価格がサポートラインに到達したらアラートを出す
if current_price <= support_price
    alert("support line alert triggered! current price: " + tostring(current_price))

// 価格がレジスタンスラインに到達したらアラートを出す
if current_price >= resistance_price
    alert("resistance line alert triggered! current price: " + tostring(current_price))
```

このサンプルコードでは、`support_price`と`resistance_price`という変数にサポートラインとレジスタンスラインの価格帯を設定します。現在の価格を取得し、それぞれの水準に到達した場合にアラートを出すように設定しています。

これにより、価格がサポートラインやレジスタンスラインに到達した際にアラートが発生し、重要なトレードのチャンスを逃すことがありません。

プライスアラートの他にも、tradingviewでは様々なテクニカル指標アラートを設定することができます。テクニカル指標アラートの設定方法とトレンド転換の検知については次の節で解説します。

## テクニカル指標アラートの使い方とトレンド転換の検知

テクニカル指標アラートを使うことで、株式や仮想通貨、外国為替などのチャートに表示される各種テクニカル指標の変化を検知し、トレンド転換のタイミングを把握することができます。

以下は、テクニカル指標アラートの設定サンプルコードです。

```python
//@version=4
study(title="example technical indicator alert", shorttitle="indicator alert", overlay=false)

// 移動平均線の長期線と短期線
ma_short = sma(close, 10)
ma_long = sma(close, 50)

// 移動平均線がクロスしたらアラートを出す
if crossover(ma_short, ma_long)
    alert("moving average crossover alert!")

// ボリンジャーバンドの上限と下限
bb_upper = security(syminfo.tickerid, "d", high) + (stdev(high, 20) * 2)
bb_lower = security(syminfo.tickerid, "d", low) - (stdev(low, 20) * 2)

// 価格がボリンジャーバンドから外れたらアラートを出す
if close > bb_upper
    alert("price above upper bollinger band!")
if close < bb_lower
    alert("price below lower bollinger band!")
```

このサンプルコードでは、tradingviewのビルトイン関数を使っていくつかのテクニカル指標を設定しています。

まず、`sma`関数を使って移動平均線の長期線と短期線を計算し、`ma_short`と`ma_long`という変数に格納します。

次に、`crossover`関数を使って移動平均線がクロスした場合にアラートが発生するように設定しています。移動平均線の短期線が長期線を上回った場合に、"moving average crossover alert!"というアラートメッセージが表示されます。

さらに、ボリンジャーバンドの上限と下限を計算し、`bb_upper`と`bb_lower`という変数に格納します。

最後に、価格がボリンジャーバンドから外れた場合にアラートが発生するように設定しています。価格がボリンジャーバンドの上限を上回った場合に"price above upper bollinger band!"というアラートメッセージが表示され、価格がボリンジャーバンドの下限を下回った場合に"price below lower bollinger band!"というアラートメッセージが表示されます。

これにより、テクニカル指標の変化を検知し、トレンド転換のタイミングを見逃すことなくトレードすることができます。

続いて、ボリンジャーバンドアラートの活用と相場のボラティリティ通知について見ていきましょう。

## ボリンジャーバンドアラートの活用と相場のボラティリティ通知

ボリンジャーバンドアラートを使うことで、相場のボラティリティに応じたエントリーやエグジットのタイミングを見極めることができます。ボリンジャーバンドは、価格の変動を示す指標であり、ボリンジャーバンドアラートを設定することで、価格がボリンジャーバンドから外れた場合にアラートを受けることができます。

以下は、ボリンジャーバンドアラートの設定サンプルコードです。

```python
//@version=4
study(title="example bollinger band alert", shorttitle="bb alert", overlay=false)

// ボリンジャーバンドの上限と下限
bb_upper = security(syminfo.tickerid, "d", high) + (stdev(high, 20) * 2)
bb_lower = security(syminfo.tickerid, "d", low) - (stdev(low, 20) * 2)

// 価格がボリンジャーバンドから外れたらアラートを出す
if close > bb_upper
    alert("price above upper bollinger band!")
if close < bb_lower
    alert("price below lower bollinger band!")
```

先程のサンプルコードでも使用したボリンジャーバンドの上限と下限を計算し、価格がボリンジャーバンドから外れた場合にアラートが発生するように設定しています。

価格がボリンジャーバンドの上限を上回った場合に"price above upper bollinger band!"というアラートメッセージが表示され、価格がボリンジャーバンドの下限を下回った場合に"price below lower bollinger band!"というアラートメッセージが表示されます。

ボリンジャーバンドアラートは、相場のボラティリティに応じたエントリーやエグジットのタイミングを見極める際に役立つ機能です。相場がボラティリティを増した場合は、価格がボリンジャーバンドから外れる




## 【TradingView】関連のまとめ
https://hack-note.com/summary/tradingview-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
