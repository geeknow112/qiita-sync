<!--
title:   【django】管理サイトの使い方：データの追加や編集、削除方法
tags:    Django,Python
id:      c890d9fb274afeecb1e4
private: false
-->


## djangoの管理サイトの概要と設定方法
djangoの管理サイトは、データの追加や編集、削除などの機能を提供するための強力なツールです。初心者エンジニアの方にとっては、データベース操作の知識がなくても簡単に操作することができるため、非常に便利です。

管理サイトを使うためには、まずdjangoプロジェクトを作成する必要があります。以下のコマンドを実行して、新しいプロジェクトを作成します。

```python
django-admin startproject mysite
```

このコマンドを実行すると、`mysite`という名前の新しいプロジェクトが作成されます。次に、管理サイトを有効にするために、プロジェクトの`settings.py`ファイルを編集します。

```python
installed_apps = [
    ...
    'django.contrib.admin',
    ...
]
```

`installed_apps`リストに`django.contrib.admin`を追加することで、管理サイトを有効にすることができます。

## モデルの作成と管理サイトへの登録方法
管理サイトを使うためには、まずモデルを作成する必要があります。モデルは、データベースのテーブルに相当するものであり、データの定義や操作を行います。

以下のコマンドを実行して、新しいアプリケーションを作成します。

```python
python manage.py startapp blog
```

このコマンドを実行することで、`blog`という名前の新しいアプリケーションが作成されます。次に、モデルを作成し、管理サイトへ登録します。

```python
from django.db import models

class blog(models.model):
    title = models.charfield(max_length=200)
    content = models.textfield()

    def __str__(self):
        return self.title
```

上記のコードでは、`blog`というモデルを作成しています。`title`と`content`は、それぞれタイトルと記事の内容を保存するためのフィールドです。

モデルの作成が完了したら、管理サイトへ登録するために`admin.py`ファイルを編集します。

```python
from django.contrib import admin
from .models import blog

admin.site.register(blog)
```

`admin.py`ファイルで、`blog`モデルを`admin.site.register(blog)`によって登録します。

## 管理サイトでのデータの閲覧と検索方法
管理サイトにアクセスするためには、サーバーを起動し、以下のurlにアクセスします。

```
http://localhost:8000/admin/
```

上記のurlにアクセスすると、管理サイトのログイン画面が表示されます。初めてアクセスする場合は、`createsuperuser`コマンドを実行して管理者ユーザーを作成する必要があります。

```python
python manage.py createsuperuser
```

ユーザー名とパスワードを設定してログインすると、管理サイトのトップページが表示されます。ここでは、登録されているデータの一覧を閲覧することができます。

データの検索も簡単に行うことができます。管理サイトのトップページにある検索フィールドにキーワードを入力すると、該当するデータが表示されます。

## 管理サイトでのデータの追加と保存方法
管理サイトで新しいデータを追加するには、管理サイトのトップページから対象のモデルを選択し、「追加」ボタンをクリックします。

追加画面では、各フィールドの値を入力することができます。データの入力が完了したら、「保存」ボタンをクリックしてデータを保存します。

以下のコードでは、モデルのインスタンスを作成し、フィールドに値を設定して保存しています。

```python
blog = blog(title='タイトル', content='内容')
blog.save()
```

## 管理サイトでのデータの編集と更新方法
管理サイトで既存のデータを編集するには、管理サイトのトップページから対象のモデルを選択し、一覧画面から編集したいデータを選択します。

編集画面では、各フィールドの値を変更することができます。データの変更が完了したら、「保存」ボタンをクリックしてデータを更新します。

以下のコードでは、モデルのインスタンスを取得し、フィールドの値を変更して保存しています。

```python
blog = blog.objects.get(id=1)
blog.title = '新しいタイトル'
blog.save()
```

## 管理サイトでのデータの削除方法
管理サイトでデータを削除するには、管理サイトのトップページから対象のモデルを選択し、一覧画面から削除したいデータを選択します。

削除確認画面で「削除」ボタンをクリックすると、データが削除されます。

以下のコードでは、モデルのインスタンスを取得し、`delete()`メソッドを呼び出してデータを削除しています。

```python
blog = blog.objects.get(id=1)
blog.delete()
```

以上が、初心者エンジニア向けのdjangoの管理サイトの使い方についての解説です。管理サイトを利用することで、データの追加や編集、削除を簡単に行うことができます。是非、活用してみてください。

参考記事：
- [djangoのデータベース操作入門](https://qiita.com/kaki_k/items/2a7869c65dc0703c4f8c)
- [djangoで簡単なwebアプリを作成してみよう](https://qiita.com/kaki_k/items/7ee5660d7c5f3bed9b03)



## Django 関連のまとめ
https://hack-note.com/summary/django-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
