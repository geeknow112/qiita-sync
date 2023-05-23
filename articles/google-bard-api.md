<!--
title:   【基礎】Google BardをAPIで利用するには
tags:    API,Bard,Google,使い方
id:      a0e66cdc08c238ce7849
private: false
-->


# google bard api 使い方

## はじめに
こんにちは。今回は、google bardについて初心者エンジニアに向けて、google bard apiの使い方を解説します。google bard apiを使うことで、自分のwebアプリやサービスにモダンな自然語生成機能を取り入れることができます。この記事では、まずはgoogle bardとは何か、そしてどのようにapiを使って自然語生成を実現するのかについて解説します。

## google bardとは
google bardは、googleが提供する自然語生成（nlg）プラットフォームです。自然言語を理解し、論理的な文章や回答を生成することができます。これにより、人工知能による文章生成やfaqドキュメント自動生成などの用途に利用されています。

## google bard apiの利用方法
google bard apiを利用するには、google cloud platformのアカウントが必要です。アカウントを作成することで、google bard apiのキーを取得することができます。キーはダッシュボードから生成されます。キーを取得したら、apiリクエストを送信する準備が整います。

apiリクエストは、下記のapiエンドポイントに送信することができます。
```
https://language.googleapis.com/v1/documents:analyzesentiment?key=your_api_key
```

上記のエンドポイントは、google cloud natural languageを利用したセンチメント分析を実行する場合のものです。他にも、要約、分類、エンティティ検出、構文分析など、様々な自然語タスクを実行するエンドポイントが提供されています。

apiリクエストは、json形式で送信する必要があります。下記は、センチメント分析のapiリクエストの例です。

```
{
  "document": {
    "type": "plain_text",
    "content": "今日は素晴らしい日です！"
  },
  "encodingtype": "utf8"
}
```

上記の例では、"今日は素晴らしい日です！"という文章のセンチメント分析を実行しています。apiから返されるレスポンスはjson形式で返され、センチメントスコアなどの情報が含まれます。

下記は、pythonを使用してgoogle bard apiを使用するサンプルコードです。このコードは、センチメント分析の例を示しています。

```
import requests
import json

url = 'https://language.googleapis.com/v1/documents:analyzesentiment?key=your_api_key'
headers = {'content-type': 'application/json'}
document = {
    'type': 'plain_text',
    'content': '今日は素晴らしい日です！'
}
data = {
    'document': document,
    'encodingtype': 'utf8'
}
r = requests.post(url, headers=headers, json=data)
results = json.loads(r.text)
sentiment = results['documentsentiment']['score']
print(sentiment)
```

## まとめ
本記事では、google bardの基本的な情報と、google bard apiの使い方について解説しました。google bard apiを使って、自分のwebアプリやサービスに自然語生成機能を取り入れることで、モダンで使いやすいサービスを提供することができます。参考にしたいブログ記事としては、下記のものがあります。

## 初心者エンジニアを脱出するには下記もおススメです
- [TechAcademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3A%2F%2Ftechacademy.jp%2Fhtmlcss-trial%3Futm_source%3Dmoshimo%26utm_medium%3Daffiliate%26utm_campaign%3Dtextad)
- [オンラインスクール DMM WEBCAMP PRO](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=ON)

参考
- [google cloud natural language apiを徹底解剖！ドキュメント解析で文書の感情を取得する](https://qiita.com/innovator-japan/items/a04f808e53fa7a51af30)
- [【google cloud codelab】cloud natural language apiでテキストを解析する](https://www.scalajapan.com/blog/2018/09/10/google-cloud-codelab-cloud-natural-language-api/)

## AIでスキルを強化
bardやchatGPTを使ってて思うのは、まだ仕事が奪われる段階ではないってことです。
むしろAIを使ってスキルを強化していけるという思いが強くなりました。
今まで手間だった簡単なプログラミングはAIに任せて、
より高度なものをやったり、ディレクションしたりが、人間の仕事になると思います。

AIでいかに単純作業を効率化していけるかが技術力の分岐点になるので、
今のうちに基礎固めにプログラミングスクールを使ってみるのもありだと思います。
参考に載せておきます。

https://hack-note.com/programming-schools/#toc13

