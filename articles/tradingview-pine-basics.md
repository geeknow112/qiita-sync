<!--
title: 【tradingview】pineスクリプトの基礎知識と使い方解説
tags: tradingview,pine
id: 
private: false
-->

こんにちは。今回は、tradingview pine scriptについて初心者エンジニアに向けて、基礎知識と使い方を解説します。

## pineスクリプトの概要と基本構造

pineスクリプトは、トレーディングビューの独自のスクリプト言語で、価格チャートの解析やインジケーターの作成に使用されます。pineスクリプトは、シンプルで直感的な文法を持つため、初心者にも扱いやすいです。

pineスクリプトの基本的な構造は以下のようになります。

```pinescript
//@version=4
study(title="sample study", overlay=true)

// 変数の定義
length = input(14, minval=1, title="length")

// データの取得
smavalue = sma(close, length)

// プロット
plot(smavalue, title="sma", color=color.blue)
```

`//@version=4`は、pineスクリプトのバージョンを指定するためのディレクティブです。現在のバージョンは4です。

`study()`関数は、トレーディングビューでカスタムインジケーターを作成する際に必要な関数で、スクリプトのタイトルやオーバーレイの設定を行います。

`input()`関数は、ユーザーからの入力を受け取るための関数で、スクリプトのパラメーターを設定できます。

`sma()`関数は、単純移動平均を計算するための関数です。

`plot()`関数は、計算結果やデータをグラフ上にプロットするための関数です。

## 変数とデータ型：pineスクリプトの基礎要素

pineスクリプトでは、様々なデータ型を使用することができます。代表的なデータ型は以下の通りです。

- `int`：整数型
- `float`：浮動小数点型
- `bool`：真偽値型
- `string`：文字列型
- `color`：色を表す型

```pinescript
//@version=4
study(title="sample study", overlay=true)

// 変数の定義
length = 14
count = 3
isabove = true
message = "hello, world!"
col = color.red

plot(length, title="length", color=col)
plot(count, title="count", color=color.yellow)
plot(isabove, title="is above", color=color.green)
plot(message, title="message", color=color.blue)
```

上記の例では、それぞれのデータ型を使用して変数を定義し、それをプロットしています。

## 条件文と演算子：ロジックの組み立て方

pineスクリプトでは、条件文と演算子を使用してロジックを組み立てることができます。代表的な条件文と演算子の例を以下に示します。

### 条件文

- `if`文：指定した条件が真の場合に実行される。

```pinescript
if close > sma(close, length)
    strategy.entry("buy", strategy.long)
    strategy.exit("sell", strategy.short)
```

### 演算子

- `>`：より大きい
- `<`：より小さい
- `==`：等しい
- `!=`：等しくない
- `>=`：以上
- `<=`：以下

```pinescript
if close > sma(close, length)
    strategy.entry("buy", strategy.long)
    strategy.exit("sell", strategy.short)

if close < sma(close, length)
    strategy.entry("sell", strategy.short)
    strategy.exit("cover", strategy.long)
```

上記の例では、`if`文を使用して条件に応じたエントリーポイントとエグジットポイントを指定しています。

## インジケーターと関数の使用方法

pineスクリプトでは、様々な組み込み関数を使用してインジケーターを作成することができます。代表的な関数の使用方法を以下に示します。

```pinescript
//@version=4
study(title="sample study", overlay=true)

// 変数の定義
length = input(14, minval=1, title="length")

// インジケーターの計算
smavalue = sma(close, length)

// プロット
plot(smavalue, title="sma", color=color.blue)
plot(close - smavalue, title="deviation", color=color.yellow)
```

上記の例では、`sma()`関数を使用して単純移動平均を計算し、それをプロットしています。また、`plot()`関数を使用して価格と単純移動平均の偏差をプロットしています。

## pineスクリプトのチャート描画とアノテーション機能

pineスクリプトでは、チャートに直接描画する機能や、テキストやラベルを表示するアノテーション機能を使用することができます。

```pinescript
//@version=4
study(title="sample study", overlay=true)

// 変数の定義
length = input(14, minval=1, title="length")

// インジケーターの計算
smavalue = sma(close, length)

// プロット
plot(smavalue, title="sma", color=color.blue)

// ラベル表示
label.new(x=bar_index, y=close, text="sma", color=color.blue, textcolor=color.white)
```

上記の例では、`plot()`関数を使用して単純移動平均をプロットし、`label.new()`関数を使用してラベルを表示しています。

以上が、tradingview pine scriptの基礎知識と使い方の解説でした。これらの基本的な要素を理解し、応用することでさまざまなインジケーターやトレード戦略を作成することができます。

参考記事：
- [pine script language tutorial - tradingview](https://www.tradingview.com/pine-script-docs/en/v4/introduction/pine_script_language_reference.html)
- [pine script language tutorial - pine script introduction](https://www.tradingview.com/pine-script-docs/en/v4/essential/pine_script_language_reference.html)

　

## 【TradingView】Pine Script関連のまとめ
https://hack-note.com/summary/tradingview-pine-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
