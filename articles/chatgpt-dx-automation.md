<!--
title:   ChatGPTを使って、自社のサービスを自動化しよう！
tags:    API,ChatGPT,OpenAI,自動化
id:      228f81b0d5d99cdf9d3b
private: false
-->


---
はじめに

こんにちは。今回は、ChatGPTについて初心者エンジニアに向けて、自社のサービスを自動化する方法について解説します。ChatGPTとは、自然言語処理技術に基づき、文章の自動生成や自然言語対話システムを構築することができるAPIです。私たちが開発するサービスでも、ChatGPTを使って自動化することで、効率的かつ正確な処理を行うことができます。

本記事では、ChatGPTを使って自社のサービスを自動化する方法について解説します。まずは、ChatGPTについての基本的な知識から説明します。

ChatGPTとは何か
---
ChatGPT（Generative Pre-trained Transformer 2）は、OpenAIが開発した自然言語処理のプログラムです。BERT（Bidirectional Encoder Representations from Transformers）と同じく、大量のテキストを使って訓練された言語モデルをベースにしています。

ChatGPTは、文章の生成や質問応答、対話システムなどに利用されます。ChatGPTは、幅広い分野の言語モデルを提供しており、初めての言語ファインチューニングでも使いやすいのが特徴です。

APIを使った自動化の基本
---
API（Application Programming Interface）を使った自動化には、下記のような流れがあります。

1. APIの取得
APIを取得するには、API提供元のウェブサイトからAPIキーを取得する必要があります。APIキーは、APIを呼び出すための認証トークンであり、APIにアクセスするための権限を持っています。

2. APIの呼び出し
APIを呼び出すときは、APIエンドポイントにリクエストを送信します。リクエストの中には、APIキー、HTTPメソッド、レスポンス形式などが含まれます。APIからのレスポンスには、JSONやXML形式でデータが返されます。

3. レスポンスの解析
APIから返されたデータを解析するためのプログラムを作成します。プログラムは、レスポンスデータを分析し、必要な情報を抽出して処理します。

ChatGPT APIを使った自動化
---
ChatGPTのAPIを使った自動化には、下記のような流れがあります。

1. APIの取得
ChatGPTのAPIを使うには、OpenAIのウェブサイト（https://beta.openai.com/docs/）でAPIキーを取得する必要があります。APIキーを取得したら、APIエンドポイントを特定し、APIリクエストの形式を理解する必要があります。

2. APIの呼び出し
APIを呼び出すためには、HTTPリクエストを送信する必要があります。ChatGPTのAPIには、テキスト情報を送信するエンドポイントが用意されています。このエンドポイントにテキスト情報を送信することで、ChatGPTから生成された文章を取得することができます。

3. レスポンスの解析
ChatGPTから返された文章を解析し、必要な情報を抽出するプログラムを作成する必要があります。例えば、生成された文章を自社のデータベースに格納したり、自社のサービスに反映することができます。

サンプルコード1：PythonでChatGPT APIを使って文章を生成する方法
---
ChatGPTのAPIを使って、文章を生成するPythonのサンプルコードを紹介します。

```python
import openai
openai.api_key = "YOUR_API_KEY"

def generate_text(prompt):
    completions = openai.Completion.create(
        engine="davinci-codex",
        prompt=prompt,
        max_tokens=1024,
        n=1,
        stop=None,
        temperature=0.7,
    )

    message = completions.choices[0].text
    return message.strip()
```

サンプルコード2：PHPでChatGPT APIを使って文章を生成する方法
---
ChatGPTのAPIを使って、文章を生成するPHPのサンプルコードを紹介します。

```php
<?php
$api_key = "YOUR_API_KEY";
$url = "https://api.openai.com/v1/engines/davinci-codex/completions";

$data = [
    "prompt" => $prompt,
    "max_tokens" => 1024,
    "temperature" => 0.7,
    "n" => 1
];

$options = array(
    "http" => array(
        "header"  => "Content-type: application/json\r\nAuthorization: Bearer ".$api_key."\r\n",
        "method"  => "POST",
        "content" => json_encode($data)
    )
);

$context  = stream_context_create($options);
$response = file_get_contents($url, false, $context);
$response = json_decode($response, true);

$message = $response["choices"][0]["text"];
echo $message;
?>
```

まとめ
---
ChatGPTは、OpenAIが開発した自然言語処理プログラムであり、自動生成や自然言語対話システムなどに利用されます。ChatGPTを利用することで、自社のサービスの自動化が可能になります。Chat GPTのAPIを利用して、開発したサービスに応用することができます。実際に上記のサンプルコードを使いながら、自社のサービスを何らかの操作を自動化することができるチャンスがあります。


【参考記事】
- 「PythonとChatGPTで自動会話ボットを作ろう！」
（https://future-codex.com/python-chat-gpt/）
- 「OpenAIのGPT-3を使ってテキスト自動生成してみた」
（https://koi-chan.com/openai-api/）

## AIでスキルを強化
bardやchatGPTを使ってて思うのは、まだ仕事が奪われる段階ではないってことです。
むしろAIを使ってスキルを強化していけるという思いが強くなりました。
今まで手間だった簡単なプログラミングはAIに任せて、
より高度なものをやったり、ディレクションしたりが、人間の仕事になると思います。

AIでいかに単純作業を効率化していけるかが技術力の分岐点になるので、
今のうちに基礎固めにプログラミングスクールを使ってみるのもありだと思います。
参考に載せておきます。

https://hack-note.com/programming-schools/#toc13

