<!--
title: 【aws cli】iamユーザーの作成と権限設定
tags: aws,cli
id: 
private: false
-->

## aws cliを使用したiamユーザーの作成手順

こんにちは。今回は、aws cliについて初心者エンジニアに向けて、iamユーザーの作成と権限設定についてご説明します。aws cliは、コマンドラインインターフェースを通じてawsリソースを管理するためのツールであり、効率的に操作することができます。

aws cliを使用してiamユーザーを作成する手順は以下の通りです。

### 1. aws cliのインストール
まずは、aws cliを導入しましょう。以下の公式ドキュメントを参考に、適切な環境にaws cliをインストールしてください。

- [aws cliのインストールガイド](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-configure-files.html)

### 2. aws cliの設定
aws cliをインストールしたら、設定を行います。以下のコマンドを実行し、awsのアクセスキーidとシークレットアクセスキーを設定してください。

```bash
$ aws configure
aws access key id [none]: <アクセスキーidを入力>
aws secret access key [none]: <シークレットアクセスキーを入力>
default region name [none]: <使用するリージョンを入力>
default output format [none]: <出力形式を入力（json, textなど）>
```

### 3. iamユーザーの作成
aws cliを設定したら、iamユーザーを作成します。以下のコマンドを実行し、必要な情報を入力してください。

```bash
$ aws iam create-user --user-name <ユーザー名>
```

上記コマンドを実行することで、指定した名前のiamユーザーが作成されます。

### 4. アクセスキーとシークレットアクセスキーの設定
次に、作成したiamユーザーに対してアクセスキーとシークレットアクセスキーを設定します。以下のコマンドを実行し、アクセスキーとシークレットアクセスキーを作成し、出力された情報を忘れずに保管してください。

```bash
$ aws iam create-access-key --user-name <ユーザー名>
```

### 5. iamユーザーのグループへの所属とポリシーの割り当て
次は、iamユーザーをグループに所属させ、必要なポリシーを割り当てます。以下のコマンドを実行してください。

```bash
$ aws iam add-user-to-group --user-name <ユーザー名> --group-name <グループ名>
```

また、ポリシーを割り当てる場合は以下のコマンドを実行します。

```bash
$ aws iam attach-user-policy --user-name <ユーザー名> --policy-arn <ポリシーarn>
```

### 6. パスワードポリシーとmfaの設定
パスワードポリシーやmfa(multi-factor authentication)を設定することで、iamユーザーのセキュリティを強化することができます。以下のコマンドを実行して設定してください。

```bash
$ aws iam update-account-password-policy --minimum-password-length <パスワードの最小長さ> --require-symbols <シンボルの必要性(true/false)> --require-uppercase-characters <大文字の必要性(true/false)> --require-lowercase-characters <小文字の必要性(true/false)> --require-numbers<数字の必要性(true/false)> --allow-users-to-change-password <パスワード変更の許可(true/false)>
```

```bash
$ aws iam enable-mfa-device --user-name <ユーザー名> --serial-number <デバイスのシリアル番号> --authentication-code1 <mfaデバイスが出力する1つ目の認証コード> --authentication-code2 <mfaデバイスが出力する2つ目の認証コード>
```

### 7. iamユーザーの一時的な認証情報の取得と管理
iamユーザーの一時的な認証情報を取得するには、以下のコマンドを実行します。

```bash
$ aws sts assume-role --role-arn <ロールのarn> --role-session-name <セッション名>
```

一時的な認証情報は、一定時間で無効になるため、再度取得する必要があります。また、不要になった認証情報は適切に削除してください。

以上が、aws cliを使用したiamユーザーの作成と権限設定の手順です。初心者エンジニアの方でも迷うことなく、効率的にiamユーザーを管理することができるでしょう。

参考記事：
- [awsのiamユーザーを追加してみる](https://qiita.com/chripell/items/85be0350cb2007d877d3)
- [aws cliでiamユーザーを作ってみる](https://qiita.com/nakohdo/items/cb0d6800800fa549d012)

　

## 【aws cli】関連のまとめ
https://hack-note.com/summary/aws-cli-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

