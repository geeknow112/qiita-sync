<!--
title:   【django】テンプレートエンジンを使ったwebページの動的生成方法
tags:    Django,Python
id:      94174b560af078fbccd0
private: false
-->


## djangoのテンプレートエンジンとは？

djangoのテンプレートエンジンは、webページの動的生成を行うために使用される重要な機能の1つです。テンプレートエンジンを使うことにより、htmlやcssなどの静的なコードに対して、動的な要素を組み込むことができます。これにより、同じデザインのwebページでも、異なるデータを表示することが可能になります。

djangoのテンプレートエンジンは、独自のテンプレート言語を使用しています。このテンプレート言語を使うことで、簡潔で分かりやすいテンプレートを作成することができます。また、テンプレート内で変数や条件分岐、繰り返し処理などを行うこともできます。

## テンプレートを使ったwebページの基本的な構成と書き方

djangoでテンプレートを使ったwebページを生成するためには、まずテンプレートファイルを作成する必要があります。テンプレートファイルは、htmlファイルとして作成しますが、拡張子は`.html`ではなく`.html`とします。

以下は、基本的なテンプレートファイルの構成例です。

```html
<!doctype html>
<html lang="ja">
<head>
    <meta charset="utf-8">
    <title>{% block title %}ページタイトル{% endblock %}</title>
</head>
<body>
    {% block content %}
    <h1>メインコンテンツ</h1>
    {% endblock %}
</body>
</html>
```

テンプレートファイルでは、`{% %}`で囲まれたタグや変数を使用することができます。また、`{% %}`内にはpythonのコードを書くこともできます。

## テンプレート内での変数の扱い方とは？

テンプレート内で変数を扱うためには、ビューからテンプレートへデータを渡す必要があります。ビューでは、`render()`関数を使ってテンプレートをレンダリングし、変数を渡すことができます。

以下は、変数をテンプレートに渡すビューの例です。

```python
from django.shortcuts import render

def blog_detail(request):
    title = "djangoテンプレートエンジンの使い方"
    content = "この記事では、djangoのテンプレートエンジンについて解説します。"

    context = {
        'title': title,
        'content': content
    }

    return render(request, 'blog_detail.html', context)
```

上記の例では、`title`と`content`という変数をテンプレートに渡しています。テンプレート内では、`{{ 変数名 }}`のようにして変数を表示することができます。

```html
<!doctype html>
<html lang="ja">
<head>
    <meta charset="utf-8">
    <title>{{ title }}</title>
</head>
<body>
    <h1>{{ content }}</h1>
</body>
</html>
```

## フィルターを使ったテンプレートのデータ加工方法とは？

テンプレートでは、フィルターを使ってデータの加工や整形を行うことができます。フィルターは、データに対して特定の処理を行い、結果を表示するために使用されます。たとえば、文字列の一部を大文字にしたり、リストの要素を並び替えたりすることができます。

以下は、フィルターを使ったテンプレートの例です。

```html
<!doctype html>
<html lang="ja">
<head>
    <meta charset="utf-8">
    <title>{% block title %}ページタイトル{% endblock %}</title>
</head>
<body>
    {% block content %}
    <h1>{{ title|upper }}</h1>
    <ul>
        {% for item in items|order_by:"-name" %}
        <li>{{ item.name }}</li>
        {% endfor %}
    </ul>
    {% endblock %}
</body>
</html>
```

上記の例では、`{{ title|upper }}`の部分で、`title`変数の値を大文字に変換して表示しています。また、`{% for item in items|order_by:"-name" %}`の部分では、`items`リストの要素を`name`で降順に表示しています。

## テンプレート内での条件分岐と繰り返し処理の書き方とは？

テンプレートでは、条件分岐や繰り返し処理を行うための制御構文を使用することができます。これにより、データの内容に応じて異なる表示を行うことができます。

以下は、条件分岐と繰り返し処理の例です。

```html
<!doctype html>
<html lang="ja">
<head>
    <meta charset="utf-8">
    <title>{% block title %}ページタイトル{% endblock %}</title>
</head>
<body>
    {% block content %}
    {% if items %}
    <h1>アイテム一覧</h1>
    <ul>
        {% for item in items %}
        <li>{{ item.name }}</li>
        {% endfor %}
    </ul>
    {% else %}
    <p>アイテムがありません。</p>
    {% endif %}
    {% endblock %}
</body>
</html>
```

上記の例では、`{% if items %}`の部分で、`items`リストが空でない場合にはアイテムの一覧を表示し、空の場合にはメッセージを表示しています。

## テンプレートの継承を使ったwebページの共通部分の効率的な管理方法

テンプレートの継承を使うことにより、webページの共通部分を効率的に管理することができます。継承を利用すると、共通のレイアウトやヘッダー、フッターなどを親テンプレートに記述し、個々のページごとに異なる内容を子テンプレートに記述することができます。

以下は、テンプレートの継承を使ったwebページの例です。

base.html（親テンプレート）
```html
<!doctype html>
<html lang="ja">
<head>
    <meta charset="utf-8">
    <title>{% block title %}ページタイトル{% endblock %}</title>
</head>
<body>
    <header>
        <h1>共通ヘッダー</h1>
    </header>
    <main>
        {% block content %}
        <p>共通コンテンツ</p>
        {% endblock %}
    </main>
    <footer>
        <p>共通フッター</p>
    </footer>
</body>
</html>
```

index.html（子テンプレート）
```html
{% extends 'base.html' %}

{% block title %}トップページ{% endblock %}

{% block content %}
<h1>トップページ</h1>
<p>トップページのコンテンツ</p>
{% endblock %}
```

上記の例では、`base.html`という親テンプレートを作成し、`index.html`という子テンプレートで継承しています。子テンプレートでヘッダーやフッターの内容を書き換えることができます。

以上が、djangoのテンプレートエンジンを使ったwebページの動的生成方法についての解説です。初心者エンジニアの方にとって、この情報が役立つことを願っています。

参考記事：
- [djangoでテンプレートエンジンを使ってwebページを動的に生成する方法](https://qiita.com/username/items/itemid)
- [djangoでテンプレートエンジンを使用して動的なwebページを作成する](https://<qiita.com/username/items/itemid)



## Django 関連のまとめ
https://hack-note.com/summary/django-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
