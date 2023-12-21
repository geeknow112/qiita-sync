<!--
title: 【tradingview】pineスクリプト：変数のスコープとグローバル変数の利用
tags: tradingview,pine
id: 
private: false
-->

## tradingview pineスクリプト：変数のスコープとグローバル変数の利用

こんにちは。今回は、tradingview pine scriptについて初心者エンジニアに向けて、変数のスコープとグローバル変数の利用についてご説明します。

tradingviewは、株式や仮想通貨などのトレードを行うためのプラットフォームです。pineスクリプトは、tradingviewで使用するための独自のスクリプト言語であり、取引アルゴリズムを独自に作成することができます。

pineスクリプトでは、変数のスコープとグローバル変数の利用方法が重要です。これらを理解することで、より柔軟なトレードアルゴリズムの作成が可能になります。

## 変数のスコープとは何か

変数のスコープとは、変数がどの範囲で有効かを指します。pineスクリプトでは、3つのスコープがあります。

1. グローバルスコープ: スクリプト全体で使用できる変数のスコープです。
2. 関数スコープ: 関数内でのみ使用できる変数のスコープです。
3. ブロックスコープ: ブロック内でのみ使用できる変数のスコープです。

例えば、以下のコードを考えてみましょう。

```pine
//@version=4
study("variable scope example", shorttitle="scope example")

// グローバル変数
globalvariable = 10

// 関数スコープ
myfunction() =>
    functionvariable = 20
    var blockvariable = 30
    plot(globalvariable + functionvariable + blockvariable)

// ブロックスコープ
if(close > 50)
    var blockvariable = 40
    plot(globalvariable + blockvariable)

myfunction()
```

このコードでは、グローバルスコープに`globalvariable`という変数を宣言しています。また、`myfunction`という関数が定義されており、関数内のスコープで`functionvariable`と`blockvariable`を宣言しています。さらに、条件分岐のブロック内で`blockvariable`が宣言されています。

## ローカル変数とグローバル変数の違い

pineスクリプトでは、ローカル変数とグローバル変数の違いを理解することも重要です。

ローカル変数とは、関数内やブロック内で宣言され、そのスコープ内でのみアクセス可能な変数のことです。一方、グローバル変数とは、スクリプト全体で宣言される変数で、どのスコープからでもアクセス可能な変数のことです。

ローカル変数には、関数や条件分岐のブロック内でのみ有効な制約があります。関数を呼び出すたびに、関数スコープの変数は初期化され、前回の呼び出しの値は破棄されます。同様に、条件分岐のブロック内で宣言された変数も、それぞれのブロック実行時に初期化されます。

一方、グローバル変数はスクリプト全体で有効なため、関数やブロックの内外からアクセスできます。ただし、グローバル変数はメモリを使用するため、使用する変数が少ない限り、必要に応じて使用するようにしましょう。

## グローバル変数の宣言と初期化方法

pineスクリプトでグローバル変数を宣言するには、`var`キーワードを使用します。次に、変数名とその初期値を指定します。

例えば、以下のコードでは、グローバル変数`globalvariable`を宣言しています。

```pine
var globalvariable = 10
```

グローバル変数は、スクリプトのどの位置でも使用できます。同じ変数が複数回宣言された場合でも、最後の宣言が有効になります。

```pine
var globalvariable = 10

if(close > 50)
    var globalvariable = 20

plot(globalvariable)
```

この例では、条件式が評価されるときに、`globalvariable`が2回宣言されていますが、最後の宣言である`var globalvariable = 20`が有効になり、グローバルスコープ全体で`globalvariable`の値が20になります。

## グローバル変数の利点と注意点

グローバル変数を使用することには、いくつかの利点があります。まず、グローバル変数はスクリプトのどの位置でも使用できます。これにより、関数やブロックの内外から同じ変数にアクセスできるため、コードの柔軟性が大幅に向上します。

また、グローバル変数は永続的な状態を保持することができます。関数スコープやブロックスコープの変数は、それぞれのスコープ内でのみ有効であり、スコープが終了すると変数の値も消えます。しかし、グローバル変数はスクリプト全体で有効なため、値が保持され続けます。

ただし、グローバル変数を使用する際には注意が必要です。特に、変数名の衝突に注意する必要があります。複数の関数やブロックで同じ変数名を使用すると、予期しない動作が発生する可能性があります。

さらに、グローバル変数はメモリを使用するため、必要以上に大量のグローバル変数を宣言すると、パフォーマンスに影響を与える可能性があります。必要な変数のみを宣言し、メモリの使用を最小限に抑えるようにしましょう。

## スコープの考慮に基づく変数の適切な使用法

pineスクリプトでは、変数のスコープを適切に考慮することが重要です。関数やブロックが互いに影響を与えず、期待通りの動作をするためには、以下のようなポイントに注意する必要があります。

1. グローバル変数の使用を最小限に抑える。
2. 同じ変数名を複数のスコープで使用しない。
3. 関数スコープやブロックスコープ内でのみ使用する変数は、ローカル変数として宣言する。
4. 変数の初期化は、値が必要なときに行う。

これらのポイントに注意することで、スクリプトがクリーンで効率的な動作をすることが期待できます。

## まとめ

pineスクリプトの変数のスコープとグローバル変数の利用について学びました。変数のスコープによって、変数がどの範囲で有効かが決まります。また、グローバル変数はスクリプト全体で使用でき、関数やブロックの内外からアクセスが可能です。ただし、変数名の衝突やメモリ使用量に注意しながら、グローバル変数を適切に利用するようにしましょう。

pineスクリプトを使用したトレードアルゴリズムの作成においては、変数のスコープとグローバル変数の利用方法を理解し、適切に使い分けることが重要です。

【参考ブログ記事】
- [variables](https://www.tradingview.com/pine-script-docs/en/v5/concepts/local_vs_global_variables.html)
- [understanding scopes in pine script](https://medium.com/analytics-vidhya/understanding-scopes-in-pine-script-6b1cdc98968e)

　

## 【TradingView】Pine Script関連のまとめ
https://hack-note.com/summary/tradingview-pine-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

