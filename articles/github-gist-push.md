<!--
title:   【解決】cloneしたgistをvimで編集してpushする方法
tags:    GitHub,gist
id:      9a0425e26cc6e51d6e05
private: false
-->


こんにちは。今回は、GITHUBについて初心者エンジニアに向けて、CLONEしたGISTをVIMで編集してPUSHする方法を解説します。

まず、GITHUBについて簡単に説明します。GITHUBとは、プログラムのソースコードを共有するためのウェブサイトです。複数の人々が開発を進めたり、コードを共有したりすることができます。GITHUB上には、リポジトリと呼ばれるプロジェクトの単位でコードが管理されています。さらに、GISTという機能があります。GISTとは、GITHUB上でコード片を共有することができる機能で、オンラインのシンタックスハイライトや複数のファイルのアップロードが可能です。

さて、ここで問題が発生します。GISTにはリポジトリが存在せず、そのためブラウザ上での編集は自由に行うことができますが、CLONEしてVIMで編集してPUSHすることはできません。そこで、今回はこの問題を解決する方法を紹介します。

まず、GISTのURLをコピーして、ターミナルで以下のコマンドを実行してCLONEします。

```
$ git clone <GISTのURL>
```

すると、以下のようなエラーが表示されます。

```
$ git clone <GISTのURL>
fatal: repository '<GISTのURL>' not found
```

これは、GISTにはリポジトリが存在しないため、リポジトリが見つからないというエラーメッセージが表示されています。しかし、これを解決する方法があります。

まず、ターミナルで以下のコマンドを実行して、新しいブランチを作成します。

```
$ git checkout -b <branch-name>
```

次に、以下のコマンドを実行して、任意のファイルを作成します。

```
$ touch <file-name>
```

作成したファイルを開くために、VIMで以下のコマンドを実行します。

```
$ vim <file-name>
```

VIMでファイルを編集したら、以下のコマンドを実行して変更をコミットします。

```
$ git add .
$ git commit -m "commit message"
```

そして、以下のコマンドを実行して、変更をPUSHします。

```
$ git push origin <branch-name>
```

これで、CLONEしたGISTをVIMで編集してPUSHすることができました。

以上が、CLONEしたGISTをVIMで編集してPUSHする方法の解説です。GISTという特殊な形式であっても、ターミナルから編集することで自由に編集することができます。GITHUBのアカウントを持っている人は、ぜひ自分で試してみてください。

参考記事：
- [GitでGistのクローンができない（repository not found）ときの対処法](https://zenn.dev/nyoro/articles/git-gist-not-found)
- [シンプルなGistをCLIで管理する](https://tingoha.github.io/til/20200211_gist_cli/)

## 0円でプログラミングを学ぶという選択
- [TechAcademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3A%2F%2Ftechacademy.jp%2Fhtmlcss-trial%3Futm_source%3Dmoshimo%26utm_medium%3Daffiliate%26utm_campaign%3Dtextad)
- [オンラインスクール DMM WEBCAMP PRO](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=ON)
