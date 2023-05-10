<!--
title:   Github Actionsでpushをトリガとして実行する方法
tags:    GitHub,Python,使い方
id:      1ab7dd60f7c1fdf9a715
private: false
-->


こんにちは。今回は、githubについて初心者エンジニアに向けて、pythonを利用してgithub actionsのpush時に自動で処理を実行する方法について解説します。

## はじめに

github actionsは、開発プロセスを自動化することができる便利なツールです。push時に自動で処理を実行することで、開発効率を大幅に改善することができます。本記事では、pythonを利用したgithub actionsの設定方法について説明します。

## github actions設定

まず、リポジトリに移動して「actions」をクリックします。その後、「new workflow」をクリックして新しいワークフローファイルを作成します。

```yaml
name: github actions on push

on:
  push:
    branches:
      - master

jobs:
  action:
    runs-on: ubuntu-latest
    steps:
      - name: checkout the code
        uses: actions/checkout@v2
      - name: set up python
        uses: actions/setup-python@v2
        with:
          python-version: "3.x"
      - name: install packages
        run: |
          python -m pip install --upgrade pip
          pip install pandas
      - name: run the python script
        run: |
          python myscript.py
```

この設定ファイルでは、マスターブランチにpushされた場合にpythonのコードを実行するように設定しています。また、上記の例ではpandasを利用するためにpipインストールしています。なお、この設定ファイルでは、実行するpythonファイルをmyscript.pyと仮定しています。ご自身の環境に合わせて変更してください。

## pythonサンプルコード

以下は、pythonでgithub actionsを利用するサンプルコードです。この例では、コミットしたファイルの数を出力する処理を実行しています。ご自身の目的に合わせて変更してください。

```python
import os

def main():
    repo_dir = os.getenv("github_workspace")
    os.chdir(repo_dir)
    os.system('git fetch origin "+refs/heads/*:refs/remotes/origin/*"')
    os.system('git rev-parse --abbrev-ref head > branch.txt')
    os.system('git diff --numstat origin/$(<$deploybranch) > changes.txt')
    with open("changes.txt") as file:
        print(len(file.readlines()))

if __name__ == "__main__":
    main()
```

## まとめ

今回は、pythonを利用してgithub actionsのpush時に自動で処理を実行する方法について解説しました。github actionsを利用することで、開発プロセスを自動化することができます。ぜひ、この記事を参考にして、github actionsを活用して開発効率を上げていきましょう。

参考記事:
- [公式ドキュメント - github actions](https://docs.github.com/en/actions)
- [初心者にもわかる！github actionsの使い方](https://qiita.com/ataruohto/items/b4651d75408cae9f947b)