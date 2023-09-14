<!--
title:   【google colaboratory】入門：jupyter notebookの基本操作と使い方
tags:    Google,Python,colaboratory
id:      48f3ec148682fbab2a6d
private: false
-->


## 【google colaboratory】入門：jupyter notebookの基本操作と使い方

こんにちは。今回は、google colaboratoryについて初心者エンジニアに向けて、基本操作と使い方を紹介します。

google colaboratory（以下、colab）は、クラウドベースのpython開発環境であり、jupyter notebookをベースとしています。colabを利用することで、自分のデスクトップやラップトップにpython環境をインストールせずに、ブラウザ上でpythonコードを実行できます。また、colabは無料で提供されており、googleのインフラストラクチャを使用しているため、高速な処理や大規模なデータセットの処理も行えます。

本記事では、colabの基本操作と使い方について詳しく解説していきます。colabの基本的な使い方から、セルの種類やショートカットキー、マークダウンセルの使い方、グラフの描画方法、そしてnotebookの共有方法までを順に紹介します。

### jupyter notebookとは？
jupyter notebookは、プログラミング言語を使用したドキュメントを作成するためのオープンソースのwebアプリケーションです。python、r、juliaなど様々なプログラミング言語に対応しており、コードや結果、説明文をセルという単位で作成します。セルごとにコードの実行や編集が可能であり、インタラクティブな開発やデータ解析に向いています。

jupyter notebookの特徴は、プログラムの実行結果をその場で表示できることです。セルごとに実行結果や出力結果が表示されるため、データ処理やグラフの表示など、複数のステップで成り立つ作業を一つのファイルにまとめて記述できます。また、マークダウンセルを利用することで、文章の書き込みも可能です。

以下に、jupyter notebookの基本的な使い方を紹介します。

```python
# このコードセルはpythonのコードを実行するためのセルです
# ショートカットキーで「shift + enter」を押すことで、実行可能です

# 変数の定義
x = 10
y = 20

# 足し算の実行と結果の表示
result = x + y
result
```

このように、セルごとにコードを実行して結果を表示することができます。

### notebookの基本的な使い方とセルの種類
jupyter notebookでは、セル単位でコードやテキストを実行できます。セルは大きく分けてcodeセルとmarkdownセルの2つがあります。

codeセルは、プログラムの入力や実行を行うためのセルです。pythonコードを書くことができ、shift + enterを押すことで実行結果が表示されます。

markdownセルは、テキストやマークダウン形式の文章を記述するためのセルです。セルタイプをmarkdownに設定すると、セル内に文章を記述することができます。セル内でhtmlやlatexといった記法を使用することもできます。

以下に、セルの種類ごとにサンプルコードを示します。

#### codeセルのサンプルコード
```python
# これはpythonのコードセルです
# pythonのコードを記述して実行できます

# 変数の定義
x = 10
y = 20

# 足し算の実行と結果の表示
result = x + y
result
```

#### markdownセルのサンプルコード
```markdown
# これはmarkdownのセルです

これは段落のテキストです。**太字**や*斜体*といった装飾も可能です。

リストも作成することができます。
- リスト1
- リスト2
- リスト3

テーブルも作成することができます。

| header 1 | header 2 |
|----------|----------|
|   cell 1 |   cell 2 |
|   cell 3 |   cell 4 |
```

セルの実行方法は、shift + enterで実行され、次のセルに移動します。ctrl + enterを押すと実行されますが、次のセルに移動せずに現在のセルに留まります。また、セルを追加するには、メニューバーの「+コードセル」または「+テキストセル」をクリックします。

### ショートカットキーの紹介：便利な操作方法
jupyter notebookでは、便利なショートカットキーが用意されています。これらのショートカットキーを活用することで、よりスムーズな開発が可能です。

以下に、いくつかの主なショートカットキーを紹介します。

- **shift + enter**: 現在のセルを実行し、次のセルに移動
- **ctrl + enter**: 現在のセルを実行し、現在のセルに留まる
- **a**: 現在のセルの上に新しいセルを追加
- **b**: 現在のセルの下に新しいセルを追加
- **m**: 現在のセルのタイプをmarkdownに変更
- **y**: 現在のセルのタイプをcodeに変更
- **d、d**（dを2回押す）: 現在のセルを削除
- **shift + tab**: 関数やメソッドの最初のカッコの前で押すと、ツールチップが表示
- **ctrl + shift + -**（ハイフン）: カーソルの位置でセルを分割

### マークダウンセルの使い方：見やすく整形した文章の作成
マークダウンセルは、テキストやマークダウン形式の文章を記述するためのセルです。マークダウンセルでは、htmlやlatexといったマークアップ言語や数式を使用することができます。

マークダウンセルでは、以下のように様々な装飾を行うことができます。

- **見出し**: `#`（シャープ）を使用して見出しを設定できます。`#`の数を増やすと、見出しのレベルが下がります。例えば、`##`は2番目のレベルの見出しを作成します。
- **強調**: `*`（アスタリスク）または`_`（アンダースコア）で囲むことで、テキストを強調することができます。単一の`*`や`_`は斜体、2つの`*`や`_`は太字になります。
- **リスト**: `-`や`1.`を使ってリストを作成することができます。
- **画像**: `![テキスト](画像のurl)`と記述することで、画像を挿入することができます。また、画像のサイズや配置を指定することも可能です。

以下に、マークダウンセルのサンプルコードを示します。

```markdown
# これはマークダウンのセルです

これは段落のテキストです。**太字**や*斜体*といった装飾も可能です。

リストも作成することができます。
- リスト1
- リスト2
- リスト3

画像も挿入することができます。
![google colab](https://colab.research.google.com/assets/colab-badge.svg)
```

### グラフの描画方法：matplotlibを使った可視化
jupyter notebookでは、グラフの描画にも便利なツールが用意されています。特に、pythonの標準的な可視化ライブラリであるmatplotlibを利用することで、データの可視化を簡単に行うことができます。

まずは、matplotlibの基本的な使い方を説明します。以下のサンプルコードを実行すると、簡単な折れ線グラフが描画されます。

```python
import matplotlib.pyplot as plt

# データの準備
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

# 折れ線グラフの描画
plt.plot(x, y)

# グラフのタイトルと軸ラベルを設定
plt.title("sample line graph")
plt.xlabel("x-axis")
plt.ylabel("y-axis")

# グラフの表示
plt.show()
```

このように、データを用意して`plt.plot()`関数でグラフを作成します。`plt.title()`や`plt.xlabel()`、`plt.ylabel()`などの関数を使用してグラフのタイトルや軸ラベルを設定します。最後に`plt.show()`関数を使ってグラフを表示します。

### notebookの共有方法：githubやgoogleドライブでの共有方法
jupyter notebookのnotebookファイルは、githubやgoogleドライブを使って簡単に共有することができます。

#### githubでの共有方法
1. プロジェクトのリポジトリにnotebookファイルをアップロードします。
2. リポジトリのurlをコピーします。
3. [nbviewer](https://nbviewer.jupyter.org/)などのサービスを使って、notebookファイルを表示します。

#### googleドライブでの共有方法
1. googleドライブにnotebookファイルをアップロードします。
2. 共有したいファイルを選択し、右クリックします。
3. 「共有」を選択し、共有リンクを生成します。

以上の方法で、jupyter notebookのnotebookファイルを簡単に共有することができます。

まとめると、初心者エンジニア向けにgoogle colaboratory（colab）の基本操作と使い方を紹介しました。colabの基本的な使い方から、セルの種類やショートカットキー、マークダウンセルの使い方、グラフの描画方法、そしてnotebookの共有方法までを解説しました。colabは使いやすく、googleのインフラストラクチャを利用するため高速な処理や大規模なデータセットの処理も行えます。これからcolabを使ってpythonの開発やデータ解析を始めてみましょう。

【参考資料】
- [colab 公式ドキュメント](https://colab.research.google.com/notebooks/intro.ipynb)
- [google colabでpythonプログラミングをはじめよう](https://www.kabanoki.net/841/)



## 【Google Colaboratory】まとめ
https://hack-note.com/summary/gcolab-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
