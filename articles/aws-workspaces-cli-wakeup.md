<!--
title: 【簡単】awsの作業をcliで効率化する - workspaces編
tags: aws,workspaces,cli,効率化
id: 
private: false
-->

こんにちは。今回は、awsについて初心者エンジニアに向けて、workspacesをcliで起動する方法について解説します。

awsには様々なサービスがありますが、その中でも特に仮想デスクトップサービスであるworkspacesは、リモートからの作業に対応したクラウドデスクトップサービスとして利用されています。しかし、workspacesを起動するためにはawsコンソールにログインして手動で起動する必要があり、手間がかかってしまいます。そこで、cliを使ってworkspacesを起動し、作業効率を上げる方法を紹介します。

### aws cliの準備

まずは、aws cliをインストールする必要があります。インストール方法については以下のブログ記事を参考にしてください。

- [aws cli のインストールとセットアップ](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/install-cliv2.html)

### iamユーザーの設定

次に、iamユーザーを作成し、aws cliで使用するアクセスキーとシークレットアクセスキーを取得します。iamユーザーの作成方法については以下のブログ記事を参考にしてください。

- [iamユーザーの作成とアクセスキーの取得](https://aws-blog.info/857/)

アクセスキーとシークレットアクセスキーを取得したら、以下のコマンドを実行してaws cliにログインします。

```
aws configure
```

コマンドを実行すると、以下の入力が求められます。

- aws access key id
- aws secret access key
- default region name
- default output format

アクセスキーとシークレットアクセスキーを入力し、残りの項目はデフォルトのままでokです。

これで準備は完了です。次に、cliでworkspacesを起動する方法について説明します。

### workspacesをcliで起動する方法

workspacesをcliで起動するには、以下の2つのコマンドを実行する必要があります。

```
create-workspaces
```

```
start-workspaces
```

まずは、`create-workspaces`コマンドを実行し、workspacesを作成します。以下は、workspacesを1つ作成する場合の例です。

```
aws workspaces create-workspaces --workspaces-directory-id d-0123456789 --bundle-id wsab-0123456789 --user-name example.user --workspace-properties '{"runningmode": "auto_stop","runningmodeautostoptimeoutinminutes": 60}' --tags 'key=name,value=example-workspace'
```

- `--workspaces-directory-id`：workspacesを作成するディレクトリid
- `--bundle-id`：workspacesのバンドルid
- `--user-name`：workspacesを作成するユーザー名
- `--workspace-properties`：workspacesのプロパティを設定
- `--tags`：workspacesにタグを付ける

作成したworkspacesを起動するには、`start-workspaces`コマンドを実行します。以下は、先ほど作成したworkspacesを起動する場合の例です。

```
aws workspaces start-workspaces --start-workspace-requests "workspaceid=ws-0123456789"
```

- `--start-workspace-requests`：起動するworkspacesの情報を設定

これで、workspacesをcliで起動することができます。また、`stop-workspaces`コマンドを使用することで、起動中のworkspacesを停止することもできます。

### まとめ

今回は、awsのworkspacesをcliで効率的に起動する方法について紹介しました。手動で起動する場合よりも時間が短縮でき、作業効率が向上します。初めての方でも簡単に導入することができるので、ぜひ試してみてください。

【参考記事】
- [aws cliを使ってawsのec2を効率化する](https://blog.takanakahiko.me/2020/02/07/aws-cli%e3%82%92%e4%bd%bf%e3%81%a3%e3%81%a6aws%e3%81%aeec2%e3%82%92%e5%8a%b9%e7%8e%87%e5%8c%96%e3%81%99%e3%82%8b/)
- [aws cli リファレンス](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html)

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)

