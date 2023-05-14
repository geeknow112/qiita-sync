<!--
title:   【比較】Google Bardとは？ChatGPTとの比較
tags:    Bard,Google,比較
id:      8654aa062e1ff1422ffa
private: false
-->


## はじめに

こんにちは。今回は、google bardについて初心者エンジニアに向けて、chatgptとの比較を交えながら解説していきます。最近注目を浴びている自然言語処理技術の中でも、bardはgoogleが開発したもので、人工知能を活用し、文章内に含まれる意図や目的を理解し、状況に応じた回答を生成することができます。chatgptとの比較からそれぞれの特徴を掴んで、どちらを使うか検討するための情報を提供します。

## google bardとは？

google bardは、2021年に開発されたgoogleの自然言語処理技術で、人工知能を活用し、自分自身が人と会話をしているかのような感覚で説明したり、質問に答えたりすることができる特徴があります。bardは、語感、特徴、性格、状況などを把握して質問に答えるため、より実際的なものになります。bardは、エンジニア向けの技術文書に問い合わせる場合、googleのアカウントとの高いセキュリティが保たれています。

## chatgptとの比較

chatgptは、自然言語処理技術で、人工知能によって生成された文章の自動化技術で、新しい文章を生成することができます。chatgptは、googleのbertモデルと同じく、文脈から言葉の背後にある意味を理解することができます。chatgptは、ニッチな問い合わせにも対応し、一般認識を多数持っているため、誰でも使えるという特徴があります。

google bardとchatgptは、共通点と異なる点があります。

共通点は、どちらも自然言語処理技術を用いていることです。また、エンジニア向けのテキストドキュメントを理解することができます。どちらの技術も、クエリーから検索相手の意図を理解します。

異なる点は、計算上のポイントです。bardは、より高速で正確な検索を提供するため、googleの検索技術をベースにしています。一方、chatgptは、より一般的な単語や句を理解するため、より強力な検索と生成技術を持っています。

どちらの技術を使うべきかは、用途やニーズによって異なります。エンジニア向けの技術ドキュメントには、正確性とスピードが必要なので、bardが適しています。

一方、一般的な文書に対してはchatgptが適しているでしょう。chatgptは、質問に対して意思決定を行うことができ、多様な用途に応用できます。

## サンプルコード１

### bard apiの使い方
```
#gcpの認証情報を環境変数に設定する
export google_application_credentials="my first project-1234567abcdef.json"

#bard apiのセットアップ
pip install --upgrade google-cloud-bard

#必要なライブラリーのインポート
from google.cloud import bard

#bardクライアントのインスタンスを作成する
client = bard.languageserviceclient()

#文章の準備
content = '上野の動物園はどこにありますか？'

#テキストエンティティの作成
document = bard.document(content=content, uri='ueno-zoo')

#テキストエンティティの集約
response = client.annotate_text(request={'document': document})

#回答の表示
answer = response.answer
confidence = response.confidence
print(f'answer: {answer}\nconfidence: {confidence}')
```

## サンプルコード２

### chatgpt apiの使い方

```
#gcpの認証情報を環境変数に設定する
export google_application_credentials=path/to/my/keyfile.json

#chatgpt apiのセットアップ
pip install --upgrade google-cloud-language

#必要なライブラリーのインポート
from google.cloud import language_v1

#文章の準備
text_content = 'どこで上野動物園のチケットを購入できますか？'

#コンテンツタイプの設定
type_ = language_v1.document.type.plain_text

#コンテンツの言語の設定
language = "ja"
document = {"content": text_content, "type_": type_, "language": language}

#chatgpt apiのエンドポイントの設定
client = language_v1.languageserviceclient()

#features設定
features = {"extract_syntax": true, "extract_entities": true, "extract_document_sentiment": true, "classify_text": true}

#gpt2設定
gpt_config = {"model_language_code": "ja", "gpt2": true}

#問い合わせの送信
request = {"document": document, "features": features, "gpt_config": gpt_config}
response = client.annotate_text(request=request)

#回答の表示
print(response.answer)
```

## まとめ

今回は、google bardとchatgptについて初心者エンジニア向けに解説しました。両方の技術は、自然言語処理を活用するため、異なる特性があります。bardは、迅速で正確なエンジニア向けの技術ドキュメントに適しています。一方、chatgptは、ニッチな問い合わせや一般的な文書に適しています。これらの特長から、今後のプロジェクトに応じて、用途に合わせて選択することが重要です。bard apiとchatgpt apiを使用して、自分のニーズに合った技術を選択してください。