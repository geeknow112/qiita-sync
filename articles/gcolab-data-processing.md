<!--
title: 【google colaboratory】入門：データの読み込みと前処理の基本
tags: google,colaboratory,python
id: 
private: false
-->

## 【google colaboratory】入門：データの読み込みと前処理の基本

こんにちは。今回は、google colaboratoryについて初心者エンジニアに向けて、データの読み込みと前処理の基本について解説します。

## データの種類：csv、excel、json、sqlなど

データの種類として、主に以下の形式がよく使われます。

- csv（comma-separated values）：カンマで区切られたテキスト形式データ
- excel（.xlsx、.xls）：microsoft excelのスプレッドシート形式データ
- json（javascript object notation）：キーと値のペアでデータを表す軽量なデータ交換フォーマット
- sql（structured query language）：データベースへの問い合わせや操作をするための言語

それぞれのデータ形式には、データのフォーマットや表現方法が異なるため、読み込みや前処理の方法も異なります。

## データの読み込み方法：pandasを使ったデータ読み込み

データを読み込むためには、pythonのライブラリであるpandasを使用します。pandasはデータの操作や分析を容易にするための高性能なツールです。

### csvファイルの読み込み
csvファイルを読み込むには、pandasの`read_csv()`関数を使用します。以下は、csvファイルを読み込んでデータフレームに格納する例です。

```python
import pandas as pd

# csvファイルを読み込む
df = pd.read_csv('data.csv')
```
ここで、`data.csv`は読み込むcsvファイルのパスです。

### excelファイルの読み込み
excelファイルを読み込むには、pandasの`read_excel()`関数を使用します。以下は、excelファイルを読み込んでデータフレームに格納する例です。

```python
import pandas as pd

# excelファイルを読み込む
df = pd.read_excel('data.xlsx')
```
ここで、`data.xlsx`は読み込むexcelファイルのパスです。

### jsonファイルの読み込み
jsonファイルを読み込むには、pandasの`read_json()`関数を使用します。以下は、jsonファイルを読み込んでデータフレームに格納する例です。

```python
import pandas as pd

# jsonファイルを読み込む
df = pd.read_json('data.json')
```
ここで、`data.json`は読み込むjsonファイルのパスです。

### sqlデータベースの読み込み
sqlデータベースからデータを読み込むには、pandasの`read_sql()`関数を使用します。以下は、sqlのselect文を実行してデータを読み込んでデータフレームに格納する例です。

```python
import pandas as pd
import sqlite3

# sqliteデータベースに接続する
conn = sqlite3.connect('sample.db')

# sqlのselect文を実行してデータを読み込む
df = pd.read_sql('select * from mytable', conn)

# 接続を閉じる
conn.close()
```
ここで、`sample.db`は読み込むsqliteデータベースのパスです。

## データの前処理方法：欠損値、重複、異常値の処理
データの前処理は、データを分析や予測モデルに適用する前に、データの品質を高めるための重要なステップです。主な前処理の方法としては、欠損値、重複、異常値の処理があります。

### 欠損値の処理
欠損値とは、データの中に空白やnullなどの値が存在することを指します。欠損値がある場合、それをそのまま分析に使用すると予測結果が誤る原因となることがあります。欠損値を処理する方法は、以下の通りです。

1. 欠損値を含む行または列を削除する
2. 欠損値を他の値（平均や中央値）で置き換える

```python
import pandas as pd

# 欠損値を含む行または列を削除する
df.dropna()

# 欠損値を他の値で置き換える（この例では平均値）
df.fillna(df.mean())
```

### 重複の処理
データの中には、同じ値を持つ重複した行が存在することがあります。重複した行は、集計や分析の際に不要な結果をもたらす可能性があります。重複を処理する方法は、以下の通りです。

```python
import pandas as pd

# 重複した行を削除する
df.drop_duplicates()
```

### 異常値の処理
異常値とは、他のデータから大幅に外れた値のことを指します。異常値は、分析や予測モデルに悪影響を及ぼす可能性があるため、適切な処理が必要です。異常値を処理する方法は、以下の通りです。

1. 異常値を含む行または列を削除する
2. 異常値を他の値で置き換える（平均や中央値など）

```python
import pandas as pd

# 異常値を含む行または列を削除する
df = df[(df['column'] > lower_threshold) & (df['column'] < upper_threshold)]

# 異常値を他の値で置き換える（この例では平均値）
df.loc[df['column'] > upper_threshold, 'column'] = df['column'].mean()
```

## データの加工方法：列の追加、削除、変換
データの加工とは、元のデータフレームに対して新しい列を追加したり、既存の列を削除したり、列を変換したりする処理のことです。

### 列の追加
新しい列を追加するには、pandasの`insert()`メソッドを使用します。以下は、新しい列を追加する例です。

```python
import pandas as pd

# 列の追加
df.insert(loc=2, column='new_column', value='new_value')
```

### 列の削除
既存の列を削除するには、pandasの`drop()`メソッドを使用します。以下は、既存の列を削除する例です。

```python
import pandas as pd

# 列の削除
df.drop(['column1', 'column2'], axis=1, inplace=true)
```

### 列の変換
既存の列を変換するには、pandasの`apply()`メソッドを使用します。以下は、既存の列を変換する例です。

```python
import pandas as pd

# 列の変換
df['column'] = df['column'].apply(lambda x: x*2)
```

## データの集計方法：pandasを使った集計方法
データの集計とは、データセット全体や特定の列に対して統計的な操作を行うことです。集計を行うことで、データの特徴や傾向を把握することができます。

### 回数のカウント
特定の列の各要素の出現回数をカウントするには、pandasの`value_counts()`メソッドを使用します。

```python
import pandas as pd

# 回数のカウント
counts = df['column'].value_counts()
```

### 平均、中央値、最大値、最小値の算出
特定の列の平均、中央値、最大値、最小値を算出するには、pandasの`mean()`、`median()`、`max()`、`min()`メソッドを使用します。

```python
import pandas as pd

# 平均値の算出
mean = df['column'].mean()

# 中央値の算出
median = df['column'].median()

# 最大値の算出
max_value = df['column'].max()

# 最小値の算出
min_value = df['column'].min()
```

### グループごとの集計
特定のカテゴリごとにデータをグループ分けして集計するには、pandasの`groupby()`メソッドを使用します。以下は、`column1`の値に基づいてグループ分けし、`column2`の平均値を算出する例です。

```python
import pandas as pd

# グループごとの集計
agg_df = df.groupby('column1')['column2'].mean()
```

## データの可視化方法：matplotlibを使ったグラフの描画
データの可視化とは、データをグラフやチャートなどの視覚的な手段で表現することです。可視化により、データの傾向や関係を直感的に理解することができます。

### ヒストグラムの描画
データの分布を表現するためにヒストグラムを使用することがあります。pandasの`plot()`メソッドを使用してヒストグラムを描画することができます。

```python
import pandas as pd

# ヒストグラムの描画
df['column'].plot(kind='hist')
```

### 折れ線グラフの描画
データの時間的な変化やトレンドを表現するために折れ線グラフを使用することがあります。pandasの`plot()`メソッドを使用して折れ線グラフを描画することができます。

```python
import pandas as pd

# 折れ線グラフの描画
df['column'].plot(kind='line')
```

### 散布図の描画
2つのデータセットの間の相関関係を表現するために散布図を使用することがあります。pandasの`plot()`メソッドを使用して散布図を描画することができます。

```python
import pandas as pd

# 散布図の描画
df.plot(kind='scatter', x='column1', y='column2')
```

以上が、google colaboratoryを使用したデータの読み込みと前処理の基本についての解説です。データの種類や読み込み方法、前処理方法、加工方法、集計方法、可視化方法など、データ処理において基本的な操作を習得することは、データ分析や機械学習の基礎となる重要なスキルです。ぜひ、google colaboratoryを使ってデータの処理に挑戦してみてください。

参考記事：
1. [google colab + pandasを使ってデータ加工！実務でよく使う基本操作まとめ](https://qiita.com/fkubota/items/18d3f151f87db511a5d4)
2. [【python pandas】データ処理でよく使う関数まとめ](https://qiita.com/mooon_stone/items/929559baf6dfcb6f6bb9)

　

## 【Google Colaboratory】まとめ
https://hack-note.com/summary/gcolab-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

