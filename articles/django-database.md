<!--
title:   【django】ormを使ったデータベース操作の基本的な方法
tags:    Django,Python
id:      a6226ce36aba08e04605
private: false
-->


## django ormとは何か？ 〜ormの基本概念の説明〜

orm（object-relational mapping）とは、データベースとオブジェクト指向プログラミング言語の間に存在するミドルウェアのことです。django ormは、pythonのオープンソースウェブアプリケーションフレームワークであるdjangoに組み込まれているormです。

### ormの基本概念

ormは、データベースとオブジェクトの間でデータのマッピングを行います。つまり、データベースのテーブルとオブジェクトのインスタンスを相互に変換することができます。

例えば、以下のようなテーブルがあるとします。

```sql
create table users (
    id serial primary key,
    name varchar(255),
    age integer
);
```

このテーブルを基にuserというモデルクラスを作成することができます。

```python
from django.db import models

class user(models.model):
    name = models.charfield(max_length=255)
    age = models.integerfield()
```

django ormは、このuserモデルを通じてデータベースの処理を行うことができます。

## データベースの接続方法と設定

djangoではデフォルトでsqliteを使用していますが、他のデータベースに接続することも可能です。設定は`settings.py`ファイルに記述されており、以下のような形式でデータベース設定を行います。

```python
databases = {
    'default': {
        'engine': 'django.db.backends.postgresql',
        'name': 'mydatabase',
        'user': 'mydatabaseuser',
        'password': 'mypassword',
        'host': 'localhost',
        'port': '5432',
    }
}
```

上記の例では、postgresqlのデータベースに接続する設定がされています。

## モデルの作成とマイグレーションの実行方法

モデルは、データベースのテーブルと対応する構造を持ったpythonのクラスです。モデルを作成するためには、`models.py`ファイルの中にクラスを定義します。

例えば、以下のようなモデルを作成することができます。

```python
from django.db import models

class book(models.model):
    title = models.charfield(max_length=255)
    author = models.charfield(max_length=255)
    published_date = models.datefield()
```

モデルの作成が完了したら、マイグレーションを実行する必要があります。マイグレーションは、データベースにモデルを適用するための手順です。

以下のコマンドを実行すると、マイグレーションファイルが生成されます。

```shell
python manage.py makemigrations
```

生成されたマイグレーションファイルを実行するためには、以下のコマンドを実行します。

```shell
python manage.py migrate
```

## データの取得方法：全件取得、条件指定、ソート

データベースからデータを取得する方法はいくつかあります。

### 全件取得

全てのデータを取得するには、以下のコードを実行します。

```python
books = book.objects.all()
```

### 条件指定

特定の条件に合致するデータのみを取得する場合は、以下のコードを実行します。

```python
recent_books = book.objects.filter(published_date__year=2021)
```

上記の例では、"published_date"が2021年の書籍のみを取得しています。

### ソート

データのソートも簡単に行うことができます。

```python
sorted_books = book.objects.order_by('-published_date')
```

上記の例では、"published_date"フィールドを降順でソートした結果を取得しています。

## データの作成・更新方法：オブジェクトの生成、属性の変更、保存

データを作成・更新する方法について説明します。

### オブジェクトの生成

新しいデータを作成するためには、モデルのインスタンスを生成します。

```python
new_book = book(title='新しい本', author='著者名', published_date='2022-01-01')
```

### 属性の変更

生成したオブジェクトの属性に値を設定することで、データを更新することができます。

```python
new_book.title = '新しいタイトル'
new_book.save()
```

### 保存

データの変更を反映するためには、`save()`メソッドを呼び出します。

```python
new_book.save()
```

## データの削除方法：オブジェクトの削除、条件に合致するレコードの削除

データを削除する方法について説明します。

### オブジェクトの削除

データベースから特定のオブジェクトを削除するには、`delete()`メソッドを使用します。

```python
book = book.objects.get(title='削除する本')
book.delete()
```

### 条件に合致するレコードの削除

特定の条件に合致するレコードを一括で削除する場合は、`filter`メソッドを使用して条件を指定し、`delete()`メソッドを呼び出します。

```python
book.objects.filter(published_date__year=2020).delete()
```

上記の例では、"published_date"が2020年の書籍を一括で削除しています。


参考記事:
- [djangoのオブジェクト操作（orm）入門](https://qiita.com/marumaru1759/items/ffc2206094663a11e302)
- [djangoチュートリアル オブジェクト操作の部分を詳細に解説](https://qiita.com/sho_yamane/items/7746dd5ff3d9d26c517a)



## Django 関連のまとめ
https://hack-note.com/summary/django-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
