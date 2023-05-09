<!--
title:   【初心者向け】Twitterのツイートをダウンロードする方法
tags:    Twitter,使い方
id:      84a01c767ff69d90466a
private: false
-->


---

はじめに

こんにちは。今回は、Twitterについて初心者エンジニアに向けて、ツイートのダウンロード方法について解説します。

Twitterは日々更新される情報の宝庫であるため、気になるツイートを保存しておきたいことがあります。そのためには、ツイートをダウンロードすることが必要になります。そこで、この記事ではTwitterのツイートを簡単にダウンロードする方法を紹介します。

まずは、ツイートをダウンロードする方法の概要を説明します。

1. ダウンロードしたいツイートのURLをコピーする。
2. プラットフォームによって違うダウンロードサイトにアクセスする。
3. URLをペーストし、ダウンロードする。

実際に手順を詳しく解説していきます。

---

ツイートをダウンロードする方法

### 1. ダウンロードしたいツイートのURLをコピーする

まずはダウンロードしたいツイートのURLをコピーします。以下の手順で行います。

1. ブラウザでTwitterにログインする。
2. ダウンロードしたいツイートを表示する。
3. ツイートの時間欄を右クリックし、「リンクアドレスをコピー」を選択する。

### 2. プラットフォームによって違うダウンロードサイトにアクセスする

次に、使用するプラットフォームに合わせたダウンロードサイトにアクセスします。以下が主要なプラットフォームごとに使用するサイトの例です。

- **Windows:** [twdownload.com](https://twdownload.com/)
- **MacOS:** [getmytweet.com](https://getmytweet.com/)
- **Android/iOS:** [twittervideodownloader.com](https://twittervideodownloader.com/)

### 3. URLをペーストし、ダウンロードする

ダウンロードサイトにアクセスしたら、先ほどコピーしたURLをペーストします。その後、「Download」ボタンをクリックすると、ツイートがダウンロードされます。

この方法で、Twitterのツイートを簡単にダウンロードすることができます。

---

まとめ

以上で、Twitterのツイートをダウンロードする方法について解説しました。

ツイートをダウンロードすることで、資料や情報収集などに役立てることができます。ぜひ、この方法を活用してTwitterをより効率的に活用しましょう。

- サンプルコード1
```javascript
// Node.jsを使用したツイートダウンロードの例

const fs = require("fs");
const request = require("request");

// ダウンロードするツイートのURL
const tweetUrl = "https://twitter.com/Twitter/status/1011802053146026498";

// ダウンロード先ファイルのパス
const output = "./downloaded_tweet.mp4";

// ダウンロード
request.get(tweetUrl).pipe(fs.createWriteStream(output));
```

- サンプルコード2
```html
<!-- HTML/JavaScriptを使用したツイートダウンロードの例 -->

<!-- ダウンロードするツイートのURL -->
<input type="text" id="tweet-url" value="https://twitter.com/Twitter/status/1011802053146026498">

<!-- ダウンロードボタン -->
<button onclick="downloadTweet()">Download</button>

<script>
function downloadTweet(){
  // 入力したURLを取得
  const tweetUrl = document.getElementById("tweet-url").value;

  // ダウンロード用のリンクを作成し、自動的にクリックする
  const downloadLink = document.createElement("a");
  downloadLink.href = tweetUrl + "/video/1";
  downloadLink.download = "tweet.mp4";
  document.body.appendChild(downloadLink);
  downloadLink.click();
}
</script>
```

参考記事：
- [【Twitter】ダウンロードサイト一覧＆方法【Twitter全ツイート画像動画】](https://gw5.jp/twitter-download-tweet.html)
- [Twitterのツイートをダウンロードする方法【2022年最新版】](https://c-old.xyz/twitter-download/)
