<!--
title: 【手順】google bardを始める手順を簡単にまとめました！
tags: google,bard,簡単,手順
id: 
private: false
-->

こんにちは。今回は、google bardについて初心者エンジニアに向けて、簡単な手順をまとめました！

google bardは、googleが提供している自然言語処理技術を用いたテキスト生成モデルです。この記事では、初心者エンジニアの方々がgoogle bardを始めるための手順を簡単にまとめましたので、ぜひ参考にしてください。

## 1. google bardとは

まず、google bardについて簡単に説明します。google bardは、自然言語処理技術と深層学習を用いた文章生成システムで、人工知能が文章を生成することができます。例えば、誰かが「料理のレシピを教えて！」と問いかけた際、あらかじめ用意されたデータを基に、簡単な料理のレシピを自動生成することができます。

google bardは、大量の特定のデータを用いて学習することで、自然な文章を生成することができます。具体的には、wikipediaやニュース記事、書籍などの大量の文章データを使用しています。

## 2. google bardを始める手順

google bardを始めるには、以下の手順を踏んでください。

### ステップ1：google cloud platformのアカウント登録
まず、[google cloud platform](https://cloud.google.com/)のアカウントを作成する必要があります。登録には、クレジットカードの登録が必要ですが、月額300ドル以下の使用量であれば、無料枠で利用することができます。

### ステップ2：プロジェクトの作成
google cloud platformにログインしたら、新しいプロジェクトを作成します。プロジェクトを作成することで、google bardを利用するための必要なコンポーネントが利用可能になります。

### ステップ3：apiキーの発行
次に、google cloud platformでapiキーを発行します。apiキーは、google cloud platformを利用する上で認証のために必要なものです。

### ステップ4：google bardのインストール
google bardを利用するためには、pythonのライブラリ「google-auth」「google-auth-oauthlib」「google-auth-httplib2」「google-cloud-language」をインストールする必要があります。以下のコマンドを実行して、必要なライブラリをインストールしてください。

```bash
pip install google-auth google-auth-oauthlib google-auth-httplib2 google-cloud-language
```

### ステップ5：google bardを実行する
google bardの実行は、terminal（macos、linux）または、command prompt（windows）で実行することができます。以下は、pythonからgoogle bardを利用した例です。

```python
# モジュールのインポート
from google.cloud import language_v1
from google.cloud.language_v1 import enums
import os

# api鍵の指定
os.environ["google_application_credentials"] = "/path/to/key.json"

# クライアントの生成
client = language_v1.languageserviceclient()

# 入力となるテキストの生成
text_content = 'こんにちは、google bard！'

# ドキュメントの生成
document = language_v1.document(
  content=text_content,
  type_=enums.document.type.plain_text)

# アノテーションの生成
response = client.annotate_text(
  document=document,
  features=features)

# 結果の表示
for sentence in response.sentences:
  print(sentence.text.content)
```

以上の手順で、google bardを使用する準備ができました。

## 3. おわりに

今回は、google bardについて初心者エンジニアに向けて、簡単な手順をまとめました。google bardは、様々な自然言語処理技術を持つモデルのひとつであり、文章生成の自動化に活用されます。是非、上記の手順を参考に、google bardを始めてみてください。

参考記事：

- [google cloud natural language apiを使って何ができる?](https://qiita.com/morimoris/items/bfe10d54e4c5d4f23b74)
- [新しい言語系 api「cloud natural language api」を試してみる](https://cloud.google.com/blog/ja/products/gcp/new-language-apis-help-decipher-insight-from-text-sdk-now-available-in-python-ruby/)

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)


## AIでスキルを強化
bardやchatGPTを使ってて思うのは、まだ仕事が奪われる段階ではないってことです。
むしろAIを使ってスキルを強化していけるという思いが強くなりました。
今まで手間だった簡単なプログラミングはAIに任せて、
より高度なものをやったり、ディレクションしたりが、人間の仕事になると思います。

AIでいかに単純作業を効率化していけるかが技術力の分岐点になるので、
今のうちに基礎固めにプログラミングスクールを使ってみるのもありだと思います。
参考に載せておきます。

https://hack-note.com/programming-schools/#toc13

