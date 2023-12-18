<!--
title:   【tradingview】pineスクリプト：変数とデータ型
tags:    TradingView,pine
id:      3880179a715fd5ccfa65
private: false
-->


こんにちは。今回は、tradingview pine scriptについて初心者エンジニアに向けて、変数とデータ型について解説していきたいと思います。

## 変数の宣言と初期化方法
変数は、データを一時的に保持するためのメモリ領域であり、プログラム内での計算や処理に使用されます。pineスクリプトでは、変数を宣言する際には「var」キーワードを使用します。以下に、変数の宣言と初期化方法を示します。

```pine
//@version=4
study("変数の宣言と初期化方法", overlay=true)

// 数値型変数の宣言と初期化
var int myinteger = 10
var float myfloat = 3.14

// 文字列型変数の宣言と初期化
var string mystring = "hello, tradingview!"

// ブール型変数の宣言と初期化
var bool mybool = true

// 配列の宣言と初期化
var float[] myarray = array.new_float(5)

// 変数の利用
plot(myinteger)
plot(myfloat)
plot(mystring)
plot(mybool)
plot(array.get(myarray, 0))
```

上記のコードでは、`var`キーワードを使用して、整数型、浮動小数点型、文字列型、ブール型の変数を宣言しています。また、配列の宣言方法も示しています。宣言後は、`plot`関数を使用して、各変数をプロットしています。

参考記事：
- [tradingview プログラミング入門 - variable(変数) -](https://tradingview.guide/tradingview-programing-introduction-variable/)
- [pine scriptの基本 - 変数 用語と文法](https://retail.arrowsmath.jp/pinescriptsyntax/)

## 数値型データの利用方法
pineスクリプトでは、数値型のデータを処理する際にいくつかの演算子を使用することができます。以下に、演算子の利用方法とサンプルコードを示します。

```pine
//@version=4
study("数値型データの利用方法", overlay=true)

// 数値型データの演算
var float a = 5
var float b = 3

var float addition = a + b // 加算
var float subtraction = a - b // 減算
var float multiplication = a * b // 乗算
var float division = a / b // 除算
var float modulo = a % b // 剰余

plot(addition, color=color.blue)
plot(subtraction, color=color.green)
plot(multiplication, color=color.red)
plot(division, color=color.yellow)
plot(modulo, color=color.orange)
```

上記のコードでは、加算、減算、乗算、除算、剰余などの演算子を使用して、数値型の変数を計算しています。それぞれの演算結果をプロットしています。

参考記事：
- [pine scriptの基本 - 数値](https://retail.arrowsmath.jp/pinescriptsyntax/)

## 文字列型変数の操作テクニック
文字列型の変数を操作する際には、いくつかのテクニックがあります。以下に、文字列型変数の操作テクニックとサンプルコードを示します。

```pine
//@version=4
study("文字列型変数の操作テクニック", overlay=true)

// 文字列型変数の操作
var string mystring = "hello, tradingview!"
var string uppercase = str.tostring(str.upper(mystring)) // 大文字に変換
var string lowercase = str.tostring(str.lower(mystring)) // 小文字に変換
var string length = str.tostring(str.len(mystring)) // 文字数の取得

plot(uppercase, color=color.red)
plot(lowercase, color=color.green)
plot(length, color=color.blue)
```

上記のコードでは、文字列型の変数を操作するために、`str.tostring`、`str.upper`、`str.lower`、`str.len`関数などを使用しています。それぞれの関数を使って、文字列型変数を大文字、小文字に変換したり、文字数を取得したりしています。

参考記事：
- [トレードビュー（tradingview）のpineスクリプトを使ったバイナリーオプション戦略 | ポジティブマネー](https://posmoney.jp/articles/44432)

## ブール型と条件文の活用法
ブール型は、真偽値を表現するためのデータ型であり、条件分岐やループなどの制御フローで活用されます。以下に、ブール型と条件文の活用法とサンプルコードを示します。

```pine
//@version=4
study("ブール型と条件文の活用法", overlay=true)

// ブール型と条件文の活用
var bool condition = true

if condition
    plot(1, color=color.green)
else
    plot(0, color=color.red)

var bool isgreaterthan = 5 > 3
var bool islessthan = 5 < 3

if isgreaterthan
    plot(1, color=color.green)
else if islessthan
    plot(0, color=color.red)
```

上記のコードでは、ブール型と条件文を使用して、特定の条件が成立する場合にプロットの色を変更しています。また、比較演算子（`>`、`<`）を使用して、2つの値を比較し、結果に基づいてプロットの色を変更しています。

参考記事：
- [tradingview プログラミング入門 - boolean(ブール) -](https://tradingview.guide/tradingview-programing-introduction-boolean/)
- [pine scriptの基本 - conditional and control statement](https://retail.arrowsmath.jp/pinescriptsyntax/)

## 配列とリストの操作手法
配列は、複数のデータをまとめて管理するためのデータ構造であり、pineスクリプトにおいても重要な役割を果たします。以下に、配列とリストの操作手法とサンプルコードを示します。

```pine
//@version=4
study("配列とリストの操作手法", overlay=true)

// 配列とリストの操作
var int[] myarray = array.new_int(3)

// 値の設定
array.set(myarray, 0, 10)
array.set(myarray, 1, 20)
array.set(myarray, 2, 30)

// 値の取得
var int value1 = array.get(myarray, 0)
var int value2 = array.get(myarray, 1)
var int value3 = array.get(myarray, 2)

plot(value1, color=color.green)
plot(value2, color=color.red)
plot(value3, color=color.blue)
```

上記のコードでは、配列を宣言し、`array.set`関数を使用して値を設定し、`array.get`関数を使用して値を取得しています。取得した値をプロットしています。

参考記事：
- [tradingview プログラミング入門 - array(配列)とlist(リスト) -](https://tradingview.guide/tradingview-programing-introduction-array-list/)

以上が、tradingview pine scriptについて初心者エンジニア向けの変数とデータ型の解説でした。各項目では、変数の宣言と初期化方法、数値型データの利用方法、文字列型変数の操作テクニック、ブール型と条件文の活用法、配列とリストの操作手法について解説しました。これらの基本的な知識を身につけることで、より高度なpineスクリプトの作成が可能になります。是非、実際のプロジェクトで活用してみてください。



## 【TradingView】Pine Script関連のまとめ
https://hack-note.com/summary/tradingview-pine-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
