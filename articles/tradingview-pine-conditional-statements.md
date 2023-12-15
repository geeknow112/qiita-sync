<!--
title: 【tradingview】pineスクリプト：条件文と制御フロー
tags: tradingview,pine
id: 
private: false
-->

こんにちは。今回は、tradingview pine scriptについて初心者エンジニアに向けて、条件文と制御フローについて解説します。

## if文の使用と条件式の書き方
if文は、条件に応じてプログラムの実行を分岐させるために使用する制御文です。pineスクリプトでは、if文の基本的な書き方は以下の通りです。

```pinescript
if (条件式)
    処理;
```

条件式は、真または偽を評価する式です。例えば、「xが10より大きい」という条件式をif文で表現すると以下のようになります。

```pinescript
x = 15;

if (x > 10)
    label.new(x, high, "x is greater than 10");
```

この場合、xが10より大きい場合に、指定した位置にラベルを表示する処理が実行されます。

if文と一緒に使用することができる比較演算子は以下の通りです。

- `>`: より大きい
- `<`: より小さい
- `>=`: 以上
- `<=`: 以下
- `==`: 等しい
- `!=`: 等しくない

さらに、複数の条件を組み合わせることも可能です。

## 複数の条件を組み合わせる方法
複数の条件を組み合わせる場合、and演算子（&&）またはor演算子（||）を使用します。

```pinescript
if (条件式1 && 条件式2)
    処理;
```

例えば、「xが10より大きくかつyが20より小さい」という条件をif文で表現すると以下のようになります。

```pinescript
x = 15;
y = 18;

if (x > 10 && y < 20)
    label.new(x, y, "x is greater than 10 and y is less than 20");
```

この場合、xが10より大きくかつyが20より小さい場合に、指定した位置にラベルを表示する処理が実行されます。

## else文とelseif文の活用法
else文を使用することで、条件が成立しない場合の処理を指定することができます。

```pinescript
if (条件式)
    処理1;
else
    処理2;
```

例えば、「xが10より大きい場合は a、それ以外の場合は b」という条件をif文とelse文で表現すると以下のようになります。

```pinescript
x = 15;

if (x > 10)
    label.new(x, high, "a");
else
    label.new(x, high, "b");
```

この場合、xが10より大きい場合にはラベルに「a」が表示され、それ以外の場合にはラベルに「b」が表示されます。

また、elseif文を使用することで、複数の条件をチェックすることも可能です。

```pinescript
if (条件式1)
    処理1;
elseif (条件式2)
    処理2;
else
    処理3;
```

例えば、「xが10より大きい場合は a、20より大きい場合は b、それ以外の場合は c」という条件をif文、elseif文、else文で表現すると以下のようになります。

```pinescript
x = 15;

if (x > 10)
    label.new(x, high, "a");
elseif (x > 20)
    label.new(x, high, "b");
else
    label.new(x, high, "c");
```

この場合、xが10より大きい場合にはラベルに「a」が表示され、20より大きい場合にはラベルに「b」が表示され、それ以外の場合にはラベルに「c」が表示されます。

## forループと配列の要素処理
forループを使用することで、同じ処理を繰り返し実行することができます。pineスクリプトでは、forループの基本的な書き方は以下の通りです。

```pinescript
for (変数 = 初期値; 条件式; 変数の更新)
    処理;
```

例えば、「1から5までの数字を順に表示する」という処理をforループで表現すると以下のようになります。

```pinescript
for (i = 1; i <= 5; i++)
    label.new(i, high, tostring(i));
```

この場合、1から5までの数値が順にラベルに表示されます。

配列を使用することで、複数の要素を持つ集合を管理することができます。配列の要素を処理する場合は、forループと組み合わせることが一般的です。

```pinescript
array = [要素1, 要素2, 要素3, ...];

for (変数 = 0; 変数 < array.size(); 変数++)
    処理;
```

例えば、以下のような配列を作成し、配列の要素を順に表示する処理をforループで表現すると以下のようになります。

```pinescript
array = ["apple", "banana", "orange"];

for (i = 0; i < array.size(); i++)
    label.new(i, high, array[i]);
```

この場合、配列の要素が順にラベルに表示されます。

## breakとcontinueの制御フロー
break文は、ループを途中で終了し、ループを抜けるための制御文です。pineスクリプトでは、forループやwhileループなどの繰り返し文内で使用することができます。

```pinescript
for (変数 = 初期値; 条件式; 変数の更新) {
    if (条件式)
        break;
}
```

例えば、「1から10までの数字を順に表示するが、5の倍数の場合はループを終了する」という処理をforループとbreak文で表現すると以下のようになります。

```pinescript
for (i = 0; i < 10; i++) {
    if (i % 5 == 0)
        break;
    label.new(i, high, tostring(i));
}
```

この場合、1から4までの数値が表示されますが、5の倍数である5の時点でループが終了します。

また、continue文は、ループの次の繰り返しを開始するための制御文です。pineスクリプトでは、forループやwhileループなどの繰り返し文内で使用することができます。

```pinescript
for (変数 = 初期値; 条件式; 変数の更新) {
    if (条件式)
        continue;
}
```

例えば、「1から10までの数字を順に表示するが、3の倍数の場合は次の繰り返しに進む」という処理をforループとcontinue文で表現すると以下のようになります。

```pinescript
for (i = 0; i < 10; i++) {
    if (i % 3 == 0)
        continue;
    label.new(i, high, tostring(i));
}
```

この場合、1から10までの数値が表示されますが、3の倍数である3、6、9の部分はスキップされます。

以上が、tradingview pine scriptの条件文と制御フローについての解説です。これらの基本的な文法を理解し、応用することで、より高度なトレーディング戦略を実装することができます。

参考リンク：
- [pine script language tutorial](https://www.tradingview.com/pine-script-docs/en/v5/tutorials/conditionals.html)
- [how to use if condition in pine script](https://www.tradingview.com/script/agwzwm29-srsi-rubberband-strategy/)
- [how to use loops in pine script](https://www.tradingview.com/tutorial/how-to-use-loops-in-pine-script)

　

## 【TradingView】Pine Script関連のまとめ
https://hack-note.com/summary/tradingview-pine-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

