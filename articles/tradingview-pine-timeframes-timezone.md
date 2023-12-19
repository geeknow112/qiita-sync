<!--
title: 【tradingview】pineスクリプト：時間枠とタイムゾーンの設定
tags: tradingview,pine
id: 
private: false
-->

## pineスクリプトでの時間枠の指定方法

pineスクリプトを使用する際には、チャートの時間枠を指定する必要があります。時間枠を正確に指定することは、トレード戦略の適用において非常に重要です。pineスクリプトでは、以下のようにして時間枠を指定することができます。

```pinescript
//@version=4
study(title="timeframe example", shorttitle="tf", overlay=true)

tf = input("d", "timeframe", input.resolution)
op = security(syminfo.tickerid, tf, open)
hi = security(syminfo.tickerid, tf, high)
lo = security(syminfo.tickerid, tf, low)
cl = security(syminfo.tickerid, tf, close)

plot(cl, color=color.blue)
```

このコードでは、`input.resolution`で時間枠を指定することができます。上記の例では、デフォルトで「日足(daily)」として設定していますが、必要に応じて時間枠を変更することができます。このようにすることで、トレード戦略を特定の時間枠に適用することができます。

参考記事：
- [pine script初心者向けq&a【基礎】 - qiita](https://qiita.com/kenchan0130/items/e45116eda6fd53f38311#timeframe%e6%99%82%e9%96%93%e6%9e%a0%e3%82%92%e6%8c%87%e5%ae%9a%e3%81%99%e3%82%8b)

## タイムゾーン設定の重要性と使い方

pineスクリプトでは、タイムゾーンの設定も非常に重要です。タイムゾーンの設定によって、チャート上の価格データや指標の計算結果が異なる場合があります。特に国際的なトレードを行う場合には、正確なタイムゾーンの設定が必要となります。

pineスクリプトでは、以下のようにしてタイムゾーンを設定することができます。

```pinescript
//@version=4
study(title="timezone example", shorttitle="tz", overlay=true)

timezone = input("utc", "timezone", input.string)
offset = input(title="timezone offset", type=input.integer, defval=0)

time = time + offset * 60 * 60 * 1000

plot(time, color=color.red)
```

上記の例では、`input.string`を使用してタイムゾーンを指定することができます。デフォルトでは「utc」に設定していますが、必要に応じてタイムゾーンを変更することができます。さらに、`input.integer`を使用してタイムゾーンのオフセットを指定することもできます。このようにすることで、チャート上の時間データを正確に設定できます。

参考記事：
- [pine scriptのタイムゾーンとセッションブレーク - qiita](https://qiita.com/regidrogado/items/db05831a3d5196c1094f#%e6%99%82%e9%96%93%e6%9e%a0%e3%81%ae%e6%8c%87%e5%ae%9a)
- [【pinescript】時間とタイムゾーン - qiita](https://qiita.com/emo_birb/items/7121e0f4640837d07681#%e7%b5%90%e8%ab%96)

　

## 【TradingView】Pine Script関連のまとめ
https://hack-note.com/summary/tradingview-pine-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

