<!--
title:   Github Actionsでsecretsを使って認証情報をセキュアに管理する方法
tags:    GitHub,Python,actions
id:      e8d0680846b8008ce995
private: false
-->


こんにちは。今回は、githubについて初心者エンジニアに向けて、github actionsのsecretsの使い方についてご紹介します。

はじめに
---

github actionsは、リポジトリ内でアクションを自動化するためのプラットフォームです。このプラットホームを利用することで、自分で指定したタイミングで、指定した条件を満たした場合、指定したアクションを自動で実行できるようになります。

github actionsの中でも、github secretsを使うことで、apiキーやパスワードなどの機密情報をgithubに保存することができます。この記事では、pythonを使ってgithub actionsのsecretsを設定し、使う方法について解説します。

まずはsecretsの登録から始めましょう。

secretsの登録方法
---

githubのリポジトリを開き、settingsタブをクリックし、左メニューの"secrets"を選択します。

![secrets1](https://user-images.githubusercontent.com/12345678/1234567890/secrets1.png)

「new repository secret」をクリックします。

![secrets2](https://user-images.githubusercontent.com/12345678/1234567890/secrets2.png)

secretsの名前を入力し、secretsの値を入力し、[add secret]をクリックして保存します。

![secrets3](https://user-images.githubusercontent.com/12345678/1234567890/secrets3.png)

secretsを使う方法
---

1. actionsの設定を作成します。

```yml
name: deploy

on:
  push:
    branches:
      - master

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: checkout
        uses: actions/checkout@v2

      # secretsの使い方（例）
      - name: setup python
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'
          architecture: 'x64'
          # secretsの認証情報の利用
          # ${{}}を使って、リポジトリのsecretsから認証情報にアクセスします。
          #  ※"my_secret_token"は自分で作ったsecretsの名前です。必ず自分で作成したsecretsの名前に変更してください。
          #  ※認証情報の使い方によって入力値が異なるので、自分で入力値を調べてください。
          #  ※認証情報を使う場合、公開リポジトリ内にhiddenリポジトリを作ることをおすすめします。
          env:
            my_secret_token: '${{ secrets.my_secret_token }}'
```

2. pythonコードからsecretsを使う方法を紹介します。以下のように記述します。

```python
import os

# secretsの認証情報の利用
#  ※"my_secret_token"は自分で作ったsecretsの名前です。必ず自分で作成したsecretsの名前に変更してください。
#  ※認証情報の使い方によって入力値が異なるので、自分で入力値を調べてください。
secret_token = os.environ['my_secret_token']
```

以上でgithub actionsのsecretsの使い方を解説しました。

まとめ
---

github actionsを利用することで、リポジトリ内でアクションを自動化することができます。その中でも、機密情報をgithub secretsに保存することで安全に利用することができます。pythonのコードからsecretsを使う場合について詳しく解説しました。ぜひ実際に試してみてください。

参考：
- [github actions公式ドキュメント- secrets](https://docs.github.com/ja/actions/reference/encrypted-secrets#creating-encrypted-secrets-for-a-repository)
- [actionsの設定例(actionのワークフロー)](https://github.com/actions/starter-workflows/blob/master/ci/python-app.yml)