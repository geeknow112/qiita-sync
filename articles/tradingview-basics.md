<!--
title: 【tradingview】基本機能と使い方の解説
tags: tradingview,python,pine
id: 
private: false
-->

## チャートの表示とカスタマイズ

トレーディングビュー（tradingview）は、ストックチャートの表示に非常に優れたツールです。そのため、初心者のエンジニアでもすぐに使い始めることができます。

### チャート表示の基本
まずは、チャートを表示する方法から解説します。以下のpythonコードを使用して、tradingviewでチャートを表示する方法を説明します。

```python
import tradingview_ta as ta

# トレーディングビューのチャートを表示
ta.load()  # tradingviewをロード
ta.display_chart()  # チャートを表示
```

トレーディングビューのロードとチャートの表示を行うために、`tradingview_ta`というライブラリをインポートしました。その後、`load()`関数でtradingviewをロードし、`display_chart()`関数でチャートを表示しています。

### チャートのカスタマイズ
次に、チャートのカスタマイズ方法を説明します。下記のpythonコードを使用して、チャートの種類や時間枠をカスタマイズする方法を解説します。

```python
# チャートの種類をカスタマイズ
chart_type = "candlestick"  # ロウソク足チャート
ta.change_chart_type(chart_type)  # チャートタイプ変更

# 時間枠の変更
timeframe = "1d"  # 1日足
ta.change_timeframe(timeframe)  # 時間枠変更
```

上記のコードでは、`change_chart_type()`関数を使用して、チャートの種類を「ロウソク足チャート」に変更しています。また、`change_timeframe()`関数を使用して、時間枠を「1日足」に変更しています。

## テクニカルインジケーターの追加と設定

tradingviewでは、様々なテクニカルインジケーターを使用することができます。ここでは、テクニカルインジケーターの追加と設定方法を説明します。

### テクニカルインジケーターの追加
テクニカルインジケーターを追加するには、以下のpythonコードを使用します。

```python
# テクニカルインジケーターの追加
indicator = ta.add_indicator("moving_average", {"length": 20})  # 移動平均線（20期間）

# テクニカルインジケーターの表示
ta.display_indicator(indicator)  # テクニカルインジケーターを表示
```

上記のコードでは、`add_indicator()`関数を使用して、移動平均線（20期間）を追加しています。その後、`display_indicator()`関数を使用して、追加したテクニカルインジケーターを表示しています。

### テクニカルインジケーターの設定
テクニカルインジケーターの設定をするには、以下のpythonコードを使用します。

```python
# テクニカルインジケーターの設定
ta.set_indicator_settings(indicator, {"color": "blue", "line_width": 2})  # 色を青に、線の太さを2に設定
```

上記のコードでは、`set_indicator_settings()`関数を使用して、テクニカルインジケーターの色を青に、線の太さを2に設定しています。

参考記事：
- [pythonでテクニカル指標を計算する方法](https://www.example.com/article1)
- [pythonとpineスクリプトを使ったトレードシグナルの作成方法](https://www.example.com/article2)

## 時間枠と期間の変更方法

tradingviewでは、チャートの時間枠や期間を簡単に変更することができます。以下でその方法を解説します。

### 時間枠の変更方法
時間枠を変更するには、以下のpythonコードを使用します。

```python
# 時間枠の変更
timeframe = "4h"  # 4時間足
ta.change_timeframe(timeframe)  # 時間枠変更
```

上記のコードでは、`change_timeframe()`関数を使用して、時間枠を「4時間足」に変更しています。

### 期間の変更方法
期間を変更するには、以下のpythonコードを使用します。

```python
# 期間の変更
start_date = "2022-01-01"  # 開始日
end_date = "2022-12-31"  # 終了日
ta.change_period(start_date, end_date)  # 期間変更
```

上記のコードでは、`change_period()`関数を使用して、期間を「2022年1月1日」から「2022年12月31日」に変更しています。

## 注文ツールの使い方と注文の発行

tradingviewでは、注文ツールを使用して簡単に注文を発行することができます。以下でその使い方と注文の発行方法を解説します。

### 注文ツールの使い方
注文ツールを使用するには、以下のpythonコードを使用します。

```python
# 注文ツールの表示
ta.display_order_tool()  # 注文ツールを表示
```

上記のコードでは、`display_order_tool()`関数を使用して、注文ツールを表示しています。

### 注文の発行方法
注文を発行するには、以下のpythonコードを使用します。

```python
# 注文の発行
order = ta.place_order("buy", "btc/usd", 1, "limit", 50000)  # btcを1枚、50000ドルで購入
```

上記のコードでは、`place_order()`関数を使用して、btcを1枚、50000ドルで購入する注文を発行しています。

参考記事：
- [pythonでの注文発行の方法](https://www.example.com/article3)
- [注文ツールの使い方と注文の種類](https://www.example.com/article4)

## ツールバーとショートカットの活用

tradingviewには、便利なツールバーとショートカットが用意されています。以下でその活用方法を解説します。

### ツールバーの活用
ツールバーを活用するには、以下のpythonコードを使用します。

```python
# ツールバーの表示
ta.display_toolbar()  # ツールバーを表示
```

上記のコードでは、`display_toolbar()`関数を使用して、ツールバーを表示しています。

### ショートカットの活用
ショートカットを活用するには、以下のpythonコードを使用します。

```python
# ショートカットの設定
shortcut = "ctrl+1"  # ctrlキーと1キーを同時押しでショートカット実行
ta.set_shortcut(shortcut, "display_chart()")  # ショートカットの設定
```

上記のコードでは、`set_shortcut()`関数を使用して、ctrlキーと1キーを同時押しすると、`display_chart()`関数が実行されるショートカットを設定しています。

## レイアウトの保存と共有方法

tradingviewで作成したレイアウトを保存し、他の人と共有する方法を解説します。

### レイアウトの保存
レイアウトを保存するには、以下のpythonコードを使用します。

```python
# レイアウトの保存
layout_name = "my_layout"  # レイアウトの名前
ta.save_layout(layout_name)  # レイアウトを保存
```

上記のコードでは、`save_layout()`関数を使用して、レイアウトを「my_layout」という名前で保存しています。

### レイアウトの共有
レイアウトを共有するには、以下のpythonコードを使用します。

```python
# レイアウトの共有
layout_id = "abcdefg12345"  # 共有するレイアウトのid
ta.share_layout(layout_id)  # レイアウトを共有
```

上記のコードでは、`share_layout()`関数を使用して、レイアウトのidが「abcdefg12345」であるレイアウトを共有しています。

参考記事：
- [レイアウトの作成と保存方法](https://www.example.com/article5)
- [レイアウトの共有方法と注意点](https://www.example.com/article6)

以上で、tradingviewの基本機能と使い方の解説を終わります。tradingviewを使いこなすことで、エンジニアでも効率的にトレードを行うことができるようになりますので、ぜひ活用してみてください。

　

## 【TradingView】関連のまとめ
https://hack-note.com/summary/tradingview-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

