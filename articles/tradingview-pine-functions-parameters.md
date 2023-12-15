<!--
title:   【tradingview】pineスクリプト：関数の使用とパラメータ
tags:    TradingView,pine
id:      aae69169726413c34886
private: false
-->


## 関数の定義と呼び出し方

pineスクリプトでは、関数を使用することで特定の処理をまとめて記述することができます。関数は、指定されたパラメータを受け取り、それに基づいて処理を実行し、結果を戻り値として返す役割を持ちます。

以下は、関数の定義と呼び出し方のサンプルコードです。

```pine
//@version=4
study(title="simple moving average", shorttitle="sma", overlay=true)

// 関数の定義
sma(source, length) =>
    sum = 0.0
    for i = 0 to length - 1
        sum := sum + source[i]
    sum / length

// 関数の呼び出し
length = input(14, minval=1, title="length")
smaclose = sma(close, length)

// 結果のプロット
plot(smaclose, color=color.blue)
```

上記のコードでは、`sma`という名前の関数を定義しています。この関数は、指定されたソースデータ（`source`）と長さ（`length`）を用いて、単純移動平均（sma）を計算します。`sum`変数にはソースデータの合計を、`for`ループを使って計算しています。最後に、合計を長さで割ることでsmaの値を求めています。

関数を呼び出す際には、関数名に続けてカッコ内にパラメータを指定します。上記の例では、`sma(close, length)`のように呼び出しています。この場合、`close`と`length`がパラメータとして渡されます。

## パラメータの設定とデフォルト値

関数のパラメータとは、関数内で使用する変数のことです。パラメータを使うことで、関数の柔軟性を高めることができます。pineスクリプトでは、パラメータのデフォルト値を指定することもできます。

以下は、パラメータの設定とデフォルト値のサンプルコードです。

```pine
//@version=4
study(title="simple moving average with default parameters", shorttitle="sma", overlay=true)

// 関数の定義
sma(source, length=14) =>
    sum = 0.0
    for i = 0 to length - 1
        sum := sum + source[i]
    sum / length

// 関数の呼び出し
smaclose = sma(close)

// 結果のプロット
plot(smaclose, color=color.blue)
```

上記のコードでは、`length`パラメータのデフォルト値を設定するために、`length=14`という形式を使用しています。これにより、関数を呼び出す際に`length`パラメータを省略することができます。省略された場合は、デフォルト値が使用されます。

## 内部関数と外部関数の違い

pineスクリプトでは、内部関数と外部関数の2種類の関数が利用できます。内部関数はpineスクリプトの一部として定義され、そのまま使用することができます。一方、外部関数はライブラリとして提供され、インポートしてから使用する必要があります。

以下は、内部関数と外部関数の違いを示すサンプルコードです。

```pine
//@version=4
study(title="internal function vs external function", shorttitle="internal vs external", overlay=true)

// 内部関数
internalfunction(a, b) =>
    a + b

a = 3
b = 5
internalresult = internalfunction(a, b)

plot(internalresult, color=color.blue)

// 外部関数
//@version=4
study(title="external function", shorttitle="external", overlay=true)

// 外部関数のインポート
//@version=3
study(title="external function import", shorttitle="external import", overlay=true)
//@import=math
dummy = ma(close, 14)

// インポートした関数の呼び出し
length = input(14, minval=1, title="length")
externalresult = ma(close, length)

plot(externalresult, color=color.blue)
```

上記のコードでは、`internalfunction`という名前の内部関数を定義しています。この関数は、引数`a`と`b`を足し合わせた結果を返します。内部関数は、定義した場所から直接呼び出すことができます。

また、外部関数を使用する場合は、`@import`ディレクティブを使ってモジュールをインポートする必要があります。上記の例では、`ma`関数を使うために`@import=math`と記述しています。これにより、`ma`関数を使用することができます。

## 関数の戻り値の活用方法

関数の戻り値は、関数の結果を表す値です。この戻り値を利用することで、計算結果や処理結果などを取得したり、別の処理に利用したりすることができます。

以下は、関数の戻り値の活用方法のサンプルコードです。

```pine
//@version=4
study(title="function return value", shorttitle="return value", overlay=true)

// 関数の定義
calcsum(a, b) =>
    a + b

calcmultiply(a, b) =>
    a * b

// 関数の戻り値を利用
sumresult = calcsum(3, 5)
multiplyresult = calcmultiply(3, 5)

// 結果のプロット
plot(sumresult, color=color.blue)
plot(multiplyresult, color=color.red)
```

上記のコードでは、`calcsum`と`calcmultiply`という2つの関数を定義しています。`calcsum`関数は2つの引数を足し合わせた結果を返し、`calcmultiply`関数は2つの引数を掛け合わせた結果を返します。

これらの関数を呼び出すと、戻り値を変数に代入して利用することができます。上記の例では、`calcsum(3, 5)`の結果を`sumresult`変数に代入し、`calcmultiply(3, 5)`の結果を`multiplyresult`変数に代入しています。

## ビルトイン関数とカスタム関数の利用法

pineスクリプトでは、ビルトイン関数とカスタム関数の両方を利用することができます。ビルトイン関数はpineスクリプトで予め定義された関数であり、特定の目的や処理を提供します。一方、カスタム関数はユーザーが独自に定義した関数であり、目的や処理は自由にカスタマイズすることができます。

以下は、ビルトイン関数とカスタム関数の利用法のサンプルコードです。

```pine
//@version=4
study(title="built-in and custom functions", shorttitle="built-in vs custom", overlay=true)

// ビルトイン関数の利用
smaclose = sma(close, 14)
emaclose = ema(close, 14)

plot(smaclose, color=color.blue)
plot(emaclose, color=color.red)

// カスタム関数の定義と利用
// ステップ関数：閾値を超えると1になる関数
stepfunction(value, threshold) =>
    value > threshold ? 1 : 0

stepresult = stepfunction(close, 50)
plot(stepresult, color=color.green)
```

上記のコードでは、ビルトイン関数である`sma`と`ema`を使用しています。これらの関数は、単純移動平均（sma）と指数移動平均（ema）を計算するために利用されています。

また、カスタム関数として`stepfunction`を定義しています。この関数は、指定された値（`value`）が閾値（`threshold`）を超える場合に1を返し、超えない場合に0を返します。上記の例では、`close`というビルトイン関数で取得した現在の終値を利用して、閾値50を超えるかどうか判定しています。

以上が、pineスクリプトで関数を使用するための基本的な方法やパラメータの設定、内部関数と外部関数の違い、関数の戻り値の活用方法、ビルトイン関数とカスタム関数の利用法についてご紹介した内容です。これらの知識を活用して、より高度なpineスクリプトの開発に取り組んでみてください。

【参考ブログ記事】
- [introduction to pine script](https://www.tradingview.com/blog/en/introduction-to-pine-script-20967/)
- [pine script language reference manual](https://www.tradingview.com/pine-script-reference/v4/)

いかがでしたでしょうか。今回は、tradingview pine scriptについて初心者エンジニアに向けて、関数の使用とパラメータについてご紹介しました。関数を使用することで、特定の処理をまとめて記述し、プログラムの柔軟性を高めることができます。パラメータの設定やデフォルト値の指定も可能であり、関数の戻り値を活用することで計算結果や処理結果を取得できます。また、ビルトイン関数とカスタム関数の両方を利用することで、さまざまな目的に応じた処理を実装することができます。

tradingview pine scriptについてさらに学びたい場合は、[introduction to pine script](https://www.tradingview.com/blog/en/introduction-to-pine-script-20967/)や[pine script language reference manual](https://www.tradingview.com/pine-script-reference/v4/)などの参考ブログ記事をご覧ください。これらの資料を活用しながら、pineスクリプトの開発を極めていきましょう。



## 【TradingView】Pine Script関連のまとめ
https://hack-note.com/summary/tradingview-pine-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
