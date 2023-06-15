<!--
title:   【簡単】google bardの始め方を解説！賢い使い方
tags:    Bard,Google,使い方
id:      0fe0996e65a36c972da3
private: false
-->
こんにちは。今回は、google bardについて初心者エンジニアに向けて、簡単な始め方を解説していきます。

## google bard を使うための最初の準備
google bardを使用する前に、googleアカウントが必要になります。アカウントを持っていない場合は、googleのサイトから作成することができます。

また、bardを使うには、まずgoogle colaboratoryを開きます。google colaboratoryを開く方法は簡単で、googleドライブを開き、「新規」→「その他」→「google colaboratory」と選択します。

## google bard を使ってみよう
実際に、google bardを使って文章を生成してみます。以下のコードをコピーして、colaboratoryに貼り付けてください。

```
!pip install openai
import openai
openai.api_key = "your_api_key"
model_engine = "babbage"

def bard(prompt, model, access_token):
  model_engine = model
  completions = openai.completion.create(
      engine=model_engine,
      prompt=prompt,
      max_tokens=1024,
      n=1,
      stop=none,
      temperature=0.7,
  )
  message = completions.choices[0].text
  return message

access_token = "your_access_token"
prompt = (f"hello, i am a robot and i will generate a story for you. once upon a time")

message = bard(prompt, model_engine, access_token)
print(message)
```

上記のコードは、bardを使用するために必要なライブラリをインストールしています。また、apiキーとアクセストークンを設定し、プロンプトとモデルエンジンを設定しています。プロンプトは、bardに生成して欲しい文章の初めの部分を指定します。

実行すると、google bardがランダムな文章を生成してくれます。文章を生成するためには、プロンプトを変更することで、様々な文章を生成することができます。

## google bard オススメのプロンプト
google bardは、様々なプロンプトを使用することができます。以下に、オススメのプロンプトをいくつか紹介します。

・「once upon a time」で始まるストーリーを生成する
`
prompt = (f"once upon a time")
`

・科学的な文章を生成する
`
prompt = (f"the laws of thermodynamics state")
`

・会話を生成する
`
prompt = (f"person 1: hello, how are you? \nperson 2: ")
`

## google bard 一歩進んだ使い方の提案
google bardを一歩進んだ使い方としては、自分が開発したアプリケーションに統合することが挙げられます。bardはapiとして提供されており、多くのプログラミング言語に対応しています。apiを使うことで、自分が開発したアプリケーションに文生成の機能を追加することができます。

以上、google bardの始め方について紹介しました。bardの活用にあたり、apiキーとアクセストークンが必要になりますので、必ず自分のものを用いてください。

参考となるブログ記事url：

- [openaiのgpt-3 api(beta)を使ってみた](https://qiita.com/berry-clione/items/3d3d370a08f94daeeb9c)
- [【gpt-2】意外と簡単！ python環境とgpt-2モデルの準備から文章生成まで](https://qiita.com/kazuto_hayakawa/items/5e856df40a2fd04bc74b)

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