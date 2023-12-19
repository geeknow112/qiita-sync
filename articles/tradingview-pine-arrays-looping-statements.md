<!--
title:   【tradingview】pineスクリプト：配列とループ処理
tags:    TradingView,pine
id:      9b331954936b86957d64
private: false
-->


## 【tradingview】pineスクリプト：配列とループ処理

こんにちは。今回は、tradingview pine scriptについて初心者エンジニアに向けて、配列とループ処理について解説していきたいと思います。

tradingviewは、株式や仮想通貨などのトレードを行う際に利用されるチャート分析ツールです。pineスクリプトは、そのトレードのロジックをカスタマイズするためのプログラム言語です。配列とループ処理は、pineスクリプトの基礎的な概念であり、覚えておくと非常に便利な機能です。

以下では、配列の作成と要素へのアクセス方法、ループ処理の基本的な使い方、forループと配列の要素処理、配列の要素の追加と削除の方法、配列の要素を活用するテクニックについて順番に解説していきます。

## 配列の作成と要素へのアクセス方法

配列は、複数の要素を格納するためのオブジェクトです。pineスクリプトでは、`array`キーワードを使って配列を作成することができます。

```pinescript
//@version=5
indicator("array example")

// 配列の作成
var int[] myarray = array.new_int(3)

// 配列の要素へのアクセス
array.set(myarray, 0, 10)
array.set(myarray, 1, 20)
array.set(myarray, 2, 30)

// 配列の要素の表示
plot(array.get(myarray, 0), color = color.blue)
plot(array.get(myarray, 1), color = color.green)
plot(array.get(myarray, 2), color = color.red)
```

上記のコードでは、`array.new_int(n)`を使って整数型の要素をn個持つ配列を作成しています。その後、`array.set(array, index, value)`を使って配列の各要素に値を設定し、`array.get(array, index)`を使って配列の要素を取得して表示しています。

## ループ処理の基本的な使い方

ループ処理は、同じ処理を繰り返し行うための構造です。pineスクリプトでは、`for`キーワードを使ってループ処理を行うことができます。

```pinescript
//@version=5
indicator("loop example")

// ループ処理
for i = 0 to 5
    plot(i)
```

上記のコードでは、`for`キーワードを使って0から5までの整数を繰り返し表示しています。`to`キーワードを使って繰り返しの範囲を指定し、`plot`関数を使って表示しています。

## forループと配列の要素処理

forループと配列の要素処理を組み合わせることで、配列の要素に対して同じ処理を繰り返し行うことができます。

```pinescript
//@version=5
indicator("array element processing example")

// 配列の作成
var int[] myarray = array.new_int(3)

// 配列の要素へのアクセス
array.set(myarray, 0, 10)
array.set(myarray, 1, 20)
array.set(myarray, 2, 30)

// forループと配列の要素処理
for i = 0 to array.size(myarray) - 1
    array.set(myarray, i, array.get(myarray, i) * 2)

// 変更後の配列の要素の表示
plot(array.get(myarray, 0), color = color.blue)
plot(array.get(myarray, 1), color = color.green)
plot(array.get(myarray, 2), color = color.red)
```

上記のコードでは、`array.size(array)`を使って配列の要素数を取得し、forループの条件として使用しています。forループの中で配列の要素にアクセスし、その要素を2倍にしています。

## 配列の要素の追加と削除の方法

配列の要素を追加したり削除したりするには、`array.push()`や`array.pop()`といった関数を使用します。

```pinescript
//@version=5
indicator("array element addition and deletion example")

// 配列の作成
var string[] myarray = array.new_string(3)

// 配列の要素の追加
array.push(myarray, "apple")
array.push(myarray, "banana")
array.push(myarray, "orange")

// 配列の要素の表示
plot(myarray[0], color = color.blue)
plot(myarray[1], color = color.green)
plot(myarray[2], color = color.red)

// 配列の要素の削除
array.pop(myarray)

// 削除後の配列の要素の表示
plot(myarray[0], color = color.blue)
plot(myarray[1], color = color.green)
```

上記のコードでは、`array.new_string(n)`を使って文字列型の要素をn個持つ配列を作成しています。`array.push(array, value)`を使って配列の末尾に要素を追加し、`array.pop(array)`を使って配列の末尾の要素を削除しています。

## 配列の要素を活用するテクニック

配列の要素を活用するテクニックの一つとして、`array.max()`や`array.min()`といった関数を使用して配列の最大値や最小値を取得する方法があります。

```pinescript
//@version=5
indicator("array element utilization example")

// 配列の作成
var int[] myarray = array.new_int(5)

// 配列の要素へのアクセス
array.set(myarray, 0, 10)
array.set(myarray, 1, 20)
array.set(myarray, 2, 30)
array.set(myarray, 3, 40)
array.set(myarray, 4, 50)

// 配列の最大値と最小値の表示
var int maxvalue = array.max(myarray)
var int minvalue = array.min(myarray)
plot(maxvalue, color = color.blue)
plot(minvalue, color = color.red)
```

上記のコードでは、`array.max(array)`で配列の最大値を取得し、`array.min(array)`で配列の最小値を取得しています。これにより、配列の中から最大値や最小値を取り出して表示することができます。

以上が、tradingview pine scriptにおける配列とループ処理の基本的な使い方です。これらの機能を活用することで、より効率的なチャート分析とトレードのロジックの構築が可能となります。

参考ブログ記事：
- [pine scriptで作るトレードアラートツール](https://hiraprog.com/tradingview-pinescript-alerts/)
- [tradingviewのpineスクリプトでバックテストを行う](https://www.coinsecrets.org/tradingview-pinescript-backtest/)



## 【TradingView】Pine Script関連のまとめ
https://hack-note.com/summary/tradingview-pine-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
