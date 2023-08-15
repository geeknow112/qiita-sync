<!--
title:   【django】プラグイン開発の応用テクニック：カスタム管理画面やapi拡張を実現しよう
tags:    Django,Python
id:      86a78846453daa695097
private: false
-->


## カスタム管理画面の作成と拡張

### カスタム管理画面の作成とは？
カスタム管理画面の作成とは、djangoのデフォルトの管理画面を拡張し、独自の機能やデザインを追加することです。デフォルトの管理画面では実現できない特定の要件やビジネスロジックを追加したい場合に便利です。

### カスタム管理画面の作成手順
1. `admin.py`ファイルにアプリケーションのモデルを登録する
2. `admin.py`ファイルにカスタムのモデル管理クラスを作成する
3. カスタムモデル管理クラスの属性やメソッドをオーバーライドして機能を追加する

```python
from django.contrib import admin
from .models import mymodel

class mymodeladmin(admin.modeladmin):
    list_display = ('id', 'name', 'created_at', 'updated_at')
    list_filter = ('created_at', 'updated_at')
    search_fields = ('name',)
    ordering = ('-created_at',)

admin.site.register(mymodel, mymodeladmin)
```

### 参考記事
1. [カスタム管理画面作成の公式ドキュメント](https://docs.djangoproject.com/en/3.2/ref/contrib/admin/)
2. [django 管理画面のカスタマイズについて](https://qiita.com/koty/items/1cc7a45dedbea315b413)

## django管理画面のカスタムモデル表示とフィールド設定

### カスタムモデル表示方法
カスタムモデル表示とは、管理画面でモデルの一覧や詳細を表示する際に表示するフィールドや順序をカスタマイズすることです。

#### カスタムモデル表示の設定方法

```python
class mymodeladmin(admin.modeladmin):
    list_display = ('title', 'author', 'published_date')

admin.site.register(mymodel, mymodeladmin)
```

### フィールド設定方法
フィールド設定とは、フィールドの詳細表示方法や編集可能なフィールドの制御方法などをカスタマイズすることです。

#### フィールド設定の例

```python
class mymodeladmin(admin.modeladmin):
    fields = ('title', 'author', 'published_date')
    readonly_fields = ('published_date',)

admin.site.register(mymodel, mymodeladmin)
```

### 参考記事
1. [カスタムモデル表示とフィールド設定の公式ドキュメント](https://docs.djangoproject.com/en/3.2/ref/contrib/admin/#modeladmin-objects)
2. [djangoの管理画面でモデルの表示順序や表示項目を独自にカスタマイズする](https://qiita.com/zenwerk/items/6ff7f7be3c5ba1e1daae)

## 管理画面のアクションとフィルタのカスタマイズ

### アクションのカスタマイズ方法
アクションとは、管理画面で選択したオブジェクトに対して一括で実行できる処理のことです。

#### アクションのカスタマイズ方法

```python
class mymodeladmin(admin.modeladmin):
    actions = ['make_published']

    def make_published(modeladmin, request, queryset):
        queryset.update(status='published')
    make_published.short_description = "選択した記事を公開済みに変更する"

admin.site.register(mymodel, mymodeladmin)
```

### フィルタのカスタマイズ方法
フィルタとは、管理画面でオブジェクトを絞り込むための条件やルールのことです。

#### フィルタのカスタマイズ方法

```python
class mymodeladmin(admin.modeladmin):
    list_filter = ('published_date', 'author')

admin.site.register(mymodel, mymodeladmin)
```

### 参考記事
1. [アクションとフィルタのカスタマイズ公式ドキュメント](https://docs.djangoproject.com/en/3.2/ref/contrib/admin/actions/)
2. [djangoの管理画面でアクションとフィルタを追加する](https://qiita.com/zenwerk/items/5a9946d0f2db80c0dbb4)

## 管理画面の外観とテーマの変更方法

### スタティックファイルを使ったカスタム画面の作成方法
スタティックファイルとは、cssやjavascriptなどの静的なファイルのことです。これを使って管理画面のデザインやテーマをカスタマイズすることができます。

#### スタティックファイルを使ったカスタム画面の作成方法

1. `static/admin`ディレクトリを作成する
2. カスタマイズしたいcssやjavascriptファイルを作成する
3. `admin/base_site.html`を作成し、カスタムスタティックファイルを読み込むようにする

### テーマの変更方法
テーマとは、管理画面の見た目やカスタマイズされたオブジェクトのスタイルを一括で変更するための設定のことです。

#### テーマの変更方法

```python
from django.contrib import admin
from django.contrib.admin import adminsite

class customadminsite(adminsite):
    site_header = 'カスタム管理画面'

admin_site = customadminsite(name="admin")

admin.site.site_title = 'カスタム管理画面'
admin.site.site_header = 'カスタム管理画面'
admin.site.index_title = 'メニュー'

admin_site.register(mymodel, mymodeladmin)
```

### 参考記事
1. [カスタムスタティックファイルの作成方法](https://docs.djangoproject.com/en/3.2/howto/static-files/)
2. [djangoの管理画面をカスタマイズする](https://qiita.com/zenwerk/items/eb82074235e73e7f7d61)

## django rest frameworkを使用したapiの拡張

### django rest frameworkとは？
django rest framework（以下drf）は、djangoを使って簡単にrest apiを作成するためのフレームワークです。デフォルトの管理画面だけではなく、apiにも特化して機能を拡張できます。

### apiの作成手順
1. `serializers.py`でシリアライザを作成する
2. `views.py`でビューを作成する
3. `urls.py`でurlパターンを設定する

#### apiの作成例

`serializers.py`

```python
from rest_framework import serializers
from .models import mymodel

class mymodelserializer(serializers.modelserializer):
    class meta:
        model = mymodel
        fields = '__all__'
```

`views.py`

```python
from rest_framework import viewsets
from .models import mymodel
from .serializers import mymodelserializer

class mymodelviewset(viewsets.modelviewset):
    queryset = mymodel.objects.all()
    serializer_class = mymodelserializer
```

`urls.py`

```python
from django.urls import include, path
from rest_framework import routers
from .views import mymodelviewset

router = routers.defaultrouter()
router.register(r'mymodel', mymodelviewset)

urlpatterns = [
    path('', include(router.urls)),
]
```

### 参考記事
1. [drf公式ドキュメント](https://www.django-rest-framework.org/)
2. [django rest frameworkでapiを作成する](https://qiita.com/koty/items/35610a4c650e915ea5ce)

## カスタムapiエンドポイントの作成と認証の実装

### カスタムapiエンドポイントの作成方法
カスタムapiエンドポイントの作成とは、drfを使って独自のapiエンドポイントを作成し、特定の要件やビジネスロジックを追加することです。

#### カスタムapiエンドポイントの作成手順

1. `views.py`でビューを作成する
2. `urls.py`でurlパターンを設定する

#### カスタムapiエンドポイントの作成例

`views.py`

```python
from rest_framework.views import apiview
from rest_framework.response import response

class mycustomendpoint(apiview):
    def get(self, request, format=none):
        data = {'message': 'hello, world!'}
        return response(data)
```

`urls.py`

```python
from django.urls import path
from .views import mycustomendpoint

urlpatterns = [
    path('mycustom', mycustomendpoint.as_view()),
]
```

### 認証の実装方法
api認証とは、apiエンドポイントに対してアクセス制御やセキュリティを実装することです。

#### 認証の実装例

```python
from rest_framework.authentication import sessionauthentication, basicauthentication
from rest_framework.permissions import isauthenticated

class mycustomendpoint(apiview):
    authentication_classes = [sessionauthentication, basicauthentication]
    permission_classes = [isauthenticated]

    def get(self, request, format=none):
        data = {'message': 'hello, world!'}
        return response(data)
```

### 参考記事
1. [カスタムapiエンドポイントの作成方法](https://www.django-rest-framework.org/api-guide/views/#function-based-views)
2. [django rest frameworkでカスタムapiエンドポイントを作成する](https://qiita.com/zenwerk/items/8d6ecef6d0d2107b3b9f)



## 【Django】関連のまとめ
https://hack-note.com/summary/django-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
