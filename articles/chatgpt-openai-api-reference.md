<!--
title:   【初心者向け】OpenAIのリファレンス解説！chatGPTの使い方を学ぼう！
tags:    API,ChatGPT,OpenAI,リファレンス
id:      300467591172e2825ba8
private: false
-->


## はじめに

こんにちは。今回は、CHATGPTについて初心者エンジニアに向けて、その使い方について解説します。

CHATGPTは、OpenAIが公開した自然言語処理APIの一つで、言語生成を中心に様々なタスクに利用できます。CHATGPTは、例えば対話AIのように、人工的に文章を生成することができます。

本記事では、CHATGPTの基本的な使い方、APIの概要、実際の用途について説明します。

## 入手方法

CHATGPTの使用には、OpenAIのアカウントが必要です。OpenAIのアカウントを作成後、APIキーを取得できます。APIキーを設定することで、CHATGPT APIを使用できます。

利用する際には、APIキーを環境変数として設定することをお勧めします。

```python
import openai_secret_manager

assert "openai" in openai_secret_manager.get_services()
secrets = openai_secret_manager.get_secret("openai")

print(secrets)
```

## CHATGPT APIの概要

CHATGPT APIは、人工的な文章の生成に利用できます。APIには、2つのエンドポイントがあります。

1. 完全なcontextが与えられた場合、APIは特定のタスクを実行します。
2. 完全なcontextが与えられていない場合、APIは自動的に適切なcontextを生成します。

## CHATGPT APIの基本的な使い方

CHATGPT APIを使用する手順は、以下の通りです。

1. OpenAI APIキーを取得します。
2. 'openai' Pythonライブラリをインストールします。
3. APIにアクセスする必要があるPythonプログラムを記述します。

以下のコードは、GPT3 APIの概要を示します。

```python
import openai
import os

def generate_text(prompt):
    model_engine = "text-davinci-002"
    prompt = prompt
    max_tokens = 1024
    temperature = 0.8
    top_p = 1
    frequency_penalty = 0
    presence_penalty = 0
    stop = "\n\n"
    openai.api_key = os.environ["OPENAI_API_KEY"]
    completions = openai.Completion.create(
        engine=model_engine,
        prompt=prompt,
        max_tokens=max_tokens,
        n=1,
        stop=stop,
        temperature=temperature,
        top_p=top_p,
        frequency_penalty=frequency_penalty,
        presence_penalty=presence_penalty,
    )
    message = completions.choices[0].text.strip()
    return message
```

APIにアクセスするPythonプログラムを記述する場合、次のようなサンプルコードを使用できます。

```python
prompt = "Hello, can you help me with a programming problem?"

response = generate_text(prompt)
```

## 実際の用途

CHATGPT APIは、言語生成を中心に様々なタスクに利用できます。

1. 自然言語の文章を自動生成するAIチャットボット。
2. 翻訳アプリケーションで、よりスムーズな翻訳を提供する。
3. プログラミングに関する質問に対する回答を自動応答で行う。

## まとめ

本記事では、初心者エンジニア向けに、CHATGPTの基本的な使い方、APIの概要、実際の用途について解説しました。CHATGPTは、様々なタスクに活用でき、AIチャットボットや翻訳アプリケーションに役立ちます。今後、CHATGPTを活用してより多くのアプリケーションを開発していくことが期待されます。

## 参考記事

1. [Quickstart | OpenAI](https://beta.openai.com/docs/quickstart)
2. [openai - PyPI](https://pypi.org/project/openai/)
3. [OpenAI APIを使って自然言語を生成してみる - Qiita](https://qiita.com/kijima_m/items/29be326b9452ce78013c)
4. [Pythonを用いたOpenAI GPT-3 APIの使い方 - Qiita](https://qiita.com/yoheikikuta/items/e240e331fcbe8bcc81be)

## AIでスキルを強化
bardやchatGPTを使ってて思うのは、まだ仕事が奪われる段階ではないってことです。
むしろAIを使ってスキルを強化していけるという思いが強くなりました。
今まで手間だった簡単なプログラミングはAIに任せて、
より高度なものをやったり、ディレクションしたりが、人間の仕事になると思います。

AIでいかに単純作業を効率化していけるかが技術力の分岐点になるので、
今のうちに基礎固めにプログラミングスクールを使ってみるのもありだと思います。
参考に載せておきます。

https://hack-note.com/programming-schools/#toc13

