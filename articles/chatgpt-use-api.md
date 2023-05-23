<!--
title:   ChatGPTで自動文章作成！openAI APIの使い方
tags:    API,ChatGPT,OpenAI,自然言語処理
id:      10704a69e2a34c4402a6
private: false
-->


こんにちは。今回は、ChatGPT APIについて初心者エンジニアに向けて、使い方を紹介します。

## はじめに

ChatGPTは、OpenAIが開発した自然言語処理のモデルの1つで、自動応答や文章生成などのタスクに利用されます。ChatGPT APIは、このChatGPTをAPI経由で利用するためのものです。本記事では、ChatGPT APIを利用するための手順を紹介します。

## APIキーの取得

まず初めに、ChatGPT APIを利用するためにはAPIキーが必要です。APIキーは、OpenAIのダッシュボードから取得することができます。以下の手順でAPIキーを取得してください。

1. OpenAIのダッシュボードにログインします。
2. 「API Keys」タブをクリックします。
3. 「Create new API key」をクリックし、APIキーを作成します。
4. 作成されたAPIキーをコピーしておきます。

## APIの利用

APIキーを取得したら、次にAPIを利用するための手順を紹介します。

### インストール

まずは、`openai`パッケージをインストールします。以下のコマンドを実行してください。

```bash
pip install openai
```

### 認証情報の設定

次に、APIキーを使って認証情報を設定します。以下のコードを実行して、APIキーを設定してください。

```python
import openai_secret_manager

assert "openai" in openai_secret_manager.get_services()
secrets = openai_secret_manager.get_secret("openai")

# APIキーを設定
import openai
openai.api_key = secrets["api_key"]
```

### APIを利用する

APIキーを設定したら、APIを利用することができます。以下のコードは、ChatGPT APIを使って文章を生成する例です。

```python
import openai

# プロンプトを設定
prompt = "Hello, how are you today?"

# パラメータを設定
parameters = {
    "model": "text-davinci-002",
    "prompt": prompt,
    "temperature": 0.5,
    "max_tokens": 50,
    "n": 1,
    "stop": "\n"
}

# APIを呼び出し
response = openai.Completion.create(**parameters)

# 結果を出力
print(response.choices[0].text)
```

このコードでは、`prompt`という変数に「Hello, how are you today?」という文字列を設定し、ChatGPT APIに渡すパラメータを`parameters`という辞書に設定しています。APIを呼び出すには、`openai.Completion.create()`メソッドを使います。APIのレスポンスは、`response`という変数に格納され、その中の`choices`属性を使って、生成された文章を取得しています。

## 注意点

- ChatGPT APIを使用するには、APIキーが必要です。APIキーは、OpenAIのダッシュボードから取得することができます。
- APIキーは、秘密情報として扱う必要があります。APIキーをコードに直接記述することは避け、環境変数やシークレットマネージャなどを使って取得するようにしてください。
- APIを利用する前に、APIのドキュメントをよく読んで、利用規約に従ってください。

## まとめ

本記事では、ChatGPT APIの使い方について紹介しました。APIキーの取得方法やAPIの利用方法を説明し、サンプルコードを示しました。ChatGPT APIを使って、自動応答や文章生成など、自然言語処理のタスクを実現することができます。APIのドキュメントをよく読んで、利用規約に従って、安全にAPIを利用してください。

### 参考記事

- [OpenAI APIの使い方 - Qiita](https://qiita.com/mckeeeen/items/7dbd1d7d1dabbce7b0f9)
- [OpenAI APIを使ってみた！ - Qiita](https://qiita.com/koshian2/items/53ee1d9a3c9d2d0c9da6)

## AIでスキルを強化
bardやchatGPTを使ってて思うのは、まだ仕事が奪われる段階ではないってことです。
むしろAIを使ってスキルを強化していけるという思いが強くなりました。
今まで手間だった簡単なプログラミングはAIに任せて、
より高度なものをやったり、ディレクションしたりが、人間の仕事になると思います。

AIでいかに単純作業を効率化していけるかが技術力の分岐点になるので、
今のうちに基礎固めにプログラミングスクールを使ってみるのもありだと思います。
参考に載せておきます。

https://hack-note.com/programming-schools/#toc13

