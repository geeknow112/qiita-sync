<!--
title:   【基礎】Google Search Consoleの使い方
tags:    Google,google-search-console,使い方
id:      1ebf85de6f6f232f7f41
private: false
-->

## はじめに

こんにちは。今回は、google search consoleについて初心者エンジニアに向けて、基礎的な使い方をご紹介します。google search consoleは、googleの検索エンジンを使用してウェブサイトを運営するために必要不可欠なツールの1つです。このツールを使うことで、自分のウェブサイトの検索ランキングを調べたり、クロールエラーを見つけたり、さまざまな情報を分析することができます。

まず、google search consoleについて正しく理解するために、その役割と機能について説明します。

## google search consoleとは

google search consoleとは、googleが提供するwebマスターサービスのことです。主に、自分のウェブサイトの検索ランキングや表示ページ数、クロール状況などの情報を収集・分析するためのツールです。

このツールを使うことで、自分のウェブサイトがgoogleにどのように表示されているかを可視化し、改善点を見つけたり、サイトのseo対策を行ったりすることができます。また、googleからのクロールエラーやマニュアルアクションの通知を受け取ることもできるため、サイトの運営において非常に重要な役割を果たします。

## 使い方の基礎

google search consoleを使用するためには、ウェブサイトを所有していることが必要です。ウェブサイトの所有者であれば、googleアカウントを作成し、そのアカウントでログインすることでgoogle search consoleを使用することができます。

### 1. サイトの登録

google search consoleを利用するためには、まず自分のウェブサイトを登録する必要があります。登録方法は以下の通りです。

1. google search consoleのウェブサイトにアクセスします。
2. 右上の「サインイン」ボタンをクリックして、googleアカウントにログインします。
3. 「プロパティを追加する」ボタンをクリックします。
4. ウェブサイトのドメインを入力し、「続行」ボタンをクリックします。
5. 確認方法を選択し、指示に従って確認します。

### 2. ウェブサイトの分析

ウェブサイトを登録したら、今度は様々な情報を分析することができます。例えば、以下のような情報を調べることができます。

・検索ワード
・クリック数
・表示回数
・ページのインデックス数
・html改善の提案
・クロールエラー

これらの情報を分析することで、自分のウェブサイトの問題点や改善点を見つけられます。例えば、検索ランキングが低い場合は、キーワードの選定やコンテンツの充実などの改善点を見つけることができます。

### 3. クロール状況の確認

自分のウェブサイトのクロール状況を確認することもできます。クロールとは、googleが自分のウェブサイトを定期的にチェックすることを指します。google search consoleを使用することで、クロールの頻度やエラーが発生しているページを確認することができます。

例えば、一部のページがクロールされていない場合は、それらのページに不備がある可能性があります。また、クロールエラーが発生している場合は、そのエラーの原困を見つけ、修正することができます。

## サンプルコード1

下記コードは、google search consoleを使用して、ウェブサイトの検索ワードを分析するためのものです。

```python
import requests

url = "https://www.googleapis.com/webmasters/v3/sites/your_site_url/searchanalytics/query"
headers = {"content-type": "application/json"}

params = {
    "startdate": "2020-01-01",
    "enddate": "2020-01-31",
    "dimensions": ["query"],
    "rowlimit": 10
}

response = requests.post(url, headers=headers, json=params)

json_data = response.json()
for row in json_data["rows"]:
    print(row)
```

## サンプルコード2

下記コードは、google search consoleを使用して、ウェブサイトのhtml改善点を提案するためのものです。

```python
import requests

url = "https://www.googleapis.com/webmasters/v3/sites/your_site_url/searchappearance/mobilefriendlyissues"
headers = {"content-type": "application/json"}

response = requests.get(url, headers=headers)

json_data = response.json()
for issue in json_data["mobilefriendlyissues"]:
    print(issue["rule"])
```

## まとめ

今回は、google search consoleの基礎的な使い方についてご紹介しました。google search consoleは、自分のウェブサイトを分析するために必要不可欠なツールであり、サイトのseo対策などに欠かせないものです。

まずは、自分のウェブサイトを登録し、様々な情報を分析してみることをおすすめします。そして、分析結果に応じて適切な対策を行い、自分のウェブサイトをより良いものにしていきましょう。

参考url：
1. https://techacademy.jp/magazine/27675
2. https://www.seoresearch.jp/google-search-console-easy-to-understand-discussion-and-how-to-use-it/