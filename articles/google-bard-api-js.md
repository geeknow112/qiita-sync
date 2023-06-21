<!--
title: 【google】bard apiのjavascriptでの利用
tags: google,bard,api,javascript
id: 
private: false
-->

## google bard apiのjavascriptでの利用

こんにちは。今回は、google bardについて初心者エンジニアに向けて、google bard apiのjavascriptでの利用方法について説明していきます。

### google bardとは？

google bardは、機械学習モデルをトレーニングするために必要なデータセットを作成するための、先進的な注釈付けツールです。データの注釈付けを簡単に行えるようになっており、機械学習に必要なデータセット作りを効率化することができます。

### google bard api利用方法

自分でコードを書くことで、bard apiを呼び出すことができます。apiを呼び出すことで、データの注釈付けを自動化させることができます。

google cloud platformのプロジェクトを作成し、apiキーを取得する必要があります。作成したプロジェクトには、bard apiを有効にする必要があります。

google cloud sdkも使用する必要があります。sdkをインストールし、gcloudコマンドを使用してアプリケーションを作成することができます。sdkでプロジェクトを作成する際に、bard apiに関連する認証情報が生成されます。

### javascriptでのapi利用方法

以下のステップを実行することで、javascriptでbard apiを利用できるようになります。

* まずはgoogle cloud platformとbard apiを有効化する
* 次に、google cloud sdkをインストールする
* javascriptコードを書く

### サンプルコード

以下のサンプルコードを参考に、自分のプロジェクトに合わせてコードを書き換えてください。

```
// needed to handle promise rejections.
window.addeventlistener('unhandledrejection', event => {
    // suppress error output in the console.
    event.preventdefault();
});

// variables used throughout the code.
const cloud_api_endpoint = `https://us-central1-<project-id>.cloudfunctions.net/bard`;
const loader = document.getelementbyid('loader');
const form = document.getelementbyid('form');
const input_text = document.getelementbyid('input-text');
const results = document.getelementbyid('results');

// main function that sends the input text to the backend for annotation.
async function annotateinputtext() {
    try {
        const response = await fetch(cloud_api_endpoint, {
            method: 'post',
            headers: {'content-type': 'application/json'},
            body: json.stringify({inputtext: input_text.value})
        });
        if (response.ok) {
            const data = await response.json();
            results.textcontent = data.annotatedtext;
            form.reset();
        } else {
            results.textcontent = 'failed to annotate input text.';
            console.error('error response:', response);
        }
    } catch (error) {
        results.textcontent = 'failed to annotate input text.';
        console.error('error occurred during annotation request', error);
    }
    loader.style.display = 'none';
}
```

### javascriptでgoogle bardを呼び出す

javascriptでは、以下のようにbard apiを呼び出すことができます。

```
function httppost(theurl, data) {
    var xmlhttp = new xmlhttprequest();
    xmlhttp.open("post", theurl, false);
    xmlhttp.setrequestheader("content-type", "application/json;charset=utf-8");
    xmlhttp.send(json.stringify(data));
    return json.parse(xmlhttp.responsetext);
}

var request_data = {
    "annotation_request" : {
        "inputs": {
            "text": [
                "apple is looking at buying u.k. startup for $1 billion",
                "the iphone maker is discussing a potential acquisition of the british company behind some of the world’s best-known music festivals"
            ]
        },
        "feature_settings": [
            {
                "name": "text_entity_extraction_annotation",
                "settings": {}
            }
        ],
        "extract_document_level_sentiment": false,
        "extract_entities": true
    }
}

var api_key = "your_api_key";
var api_url = "https://inference.googleapis.com/v1/projects/your_project_id/models/bert_ner:predict?key=";
var entities;

var request_uri = api_url + api_key;
var raw_response = httppost(request_uri, request_data);
console.log(raw_response);
```

### 使えるjavascriptのライブラリ

以下のjavascriptのライブラリがあります。

* axios - api呼び出しに使用されるjavascriptのライブラリです
* google api client - googleのapiを使用するために必要なjavascriptのライブラリです。

### サンプルコード

axiosを使ったサンプルコードです。

```
import axios from 'axios';

const cloud_api_endpoint = `https://us-central1-<project-id>.cloudfunctions.net/bard`;
const loader = document.getelementbyid('loader');
const form = document.getelementbyid('form');
const input_text = document.getelementbyid('input-text');
const results = document.getelementbyid('results');

async function annotateinputtext() {
    try {
        loader.style.display = 'block';
        const response = await axios.post(cloud_api_endpoint, {
            inputtext: input_text.value,
        }, {
            headers: {
                'content-type': 'application/json',
            },

        });
        console.log(response.data);
        results.textcontent = response.data.annotatedtext;
        form.reset();
    } catch (error) {
        results.textcontent = 'failed to annotate input text.';
        console.error('error occurred during annotation request', error);
    }
    loader.style.display = 'none';
}
```

google api clientを使ったサンプルコードです。

```
// load the google api client using the module loader.
google.load('client', onclientload);

function onclientload() {
    // loads the client library and authenticates the user. 
    gapi.client.load('prediction', 'v1.6', dorequest);
}

function dorequest() {
    // creates the prediction api request.
    var request = gapi.client.prediction.trainedmodels.annotate({
        'id': '<model-id>',
        'storagedatalocation': 'gs://<bucket-name>/data.csv',
        'input': {
            'csvinstance': ['<message-1>', '<message-2>', '<message-3>', '<message-4>']
        }
    });

    // executes the request and handles the result.
    request.execute(function (response) {
        if (response.error) {
            console.log(response.error.message);
        } else {
            console.log(response.outputmulti.csvinstance);
        }
    });
}
```

### まとめ

この記事では、初心者でもbard apiをjavascriptで呼び出す方法について解説してきました。google cloud platformのプロジェクトを作成し、apiキーを取得し、sdkをインストールして、コードを書くことでapiを利用できます。javascriptのaxiosやgoogle api clientを使ってapiを呼び出すことができるので、ぜひ取り組んでみてください。

　

## Google Bard 関連まとめ
https://hack-note.com/summary/google-bard-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)

