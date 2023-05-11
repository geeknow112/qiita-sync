<!--
title:   Github CLIリファレンス
tags:    GitHub,cli,リファレンス
id:      b02d3b5301c2cac67452
private: false
-->


---

こんにちは。今回は、GitHubについて初心者エンジニアに向けて、GitHub CLIのリファレンスについて解説していきたいと思います。

GitHub CLIは、GitとGithubをより使いやすくするCLI(Command Line Interface)ツールです。コマンドラインからGithubリポジトリやIssue、Pull Requestなどの操作を行えるようになり、GitとGithubをより便利に利用することができます。リポジトリの作成やクローン、コミットやプッシュなどの基本的なGit操作はもちろん、Github固有の操作もCLIで行えます。

まず、Github CLIをインストールする前に、以下のものが必要です。

- Gitバージョン2.14.1以降
- Githubアカウント

導入方法は、Github CLI公式サイトからOSに応じたインストーラーをダウンロードし、インストールするだけです。インストールが完了したら、コマンドラインで`gh`を実行して、Github CLIが正しくインストールされたか確認してください。

以下では、Github CLIの主要なコマンドについて解説していきます。

## gh repo

`gh repo`コマンドは、Githubリポジトリの作成、クローン、削除、ブラウズなどの操作ができます。例えば、リポジトリを新規作成する場合は以下のようにコマンドを実行します。

```
$ gh repo create
```

このコマンドを実行すると、リポジトリの作成に必要なパラメータ(リポジトリ名、説明、公開/非公開など)を入力するプロンプトが表示されます。また、リポジトリをクローンする場合は`gh repo clone`、削除する場合は`gh repo delete`といったコマンドでも操作できます。

## gh issue

`gh issue`コマンドは、GithubのIssueの作成、閲覧、編集、削除などの操作ができます。例えば、Issueを新規作成する場合は以下のようにコマンドを実行します。

```
$ gh issue create
```

Issueを閲覧する場合は、Issue番号を指定して以下のように実行します。

```
$ gh issue view 1
```

また、`gh issue list`コマンドを実行すると、現在のリポジトリに紐づく全てのIssueを一覧表示することもできます。

## gh pr

`gh pr`コマンドは、GithubのPull Requestの作成、閲覧、編集、マージなどの操作ができます。例えば、Pull Requestを新規作成する場合は以下のようにコマンドを実行します。

```
$ gh pr create
```

Pull Requestを閲覧する場合は、Pull Request番号を指定して以下のように実行します。

```
$ gh pr view 1
```

また、`gh pr merge`コマンドを実行すると、指定されたPull Requestをマージすることができます。

以上が、Github CLIの主要なコマンドについての解説です。他にも様々なコマンドが存在するため、Github CLI公式サイトのドキュメントもあわせて参照することをおすすめします。

## まとめ

今回は、Github CLIのリファレンスについて解説してきました。Github CLIを使うことで、より手軽にGithub上での開発作業ができるようになります。是非、Github CLIを活用して、GitとGithubをよりスムーズに使いこなしてください！

参考記事：
- [Github CLI v1.0.0がリリースされました！](https://github.blog/jp/2020-09-17-github-cli-1-0-is-now-available/)
- [GitHub CLIを使ってみた！](https://qiita.com/HeRo/items/4f48e6447cfed4bfa1e3)