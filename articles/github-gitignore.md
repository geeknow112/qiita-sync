<!--
title: Githubの.gitignoreファイルの使い方
tags: Github,gitignore,使い方
id:
private: false
-->

---

はじめに

こんにちは。今回は、Githubについて初心者エンジニアに向けて、`.gitignore`ファイルの使い方について解説します。

`.gitignore`ファイルは、リポジトリの管理対象外とするファイルやディレクトリを指定することができます。例えば、デバッグ時に生成されるログファイルや、開発環境ごとの設定ファイルなどが該当します。

このファイルを利用することにより、管理対象としないファイルの数を減らし、リポジトリのサイズを縮小することができます。

また、不用意に管理対象としないと、コラボレーター間で管理するファイルやディレクトリが異なってしまい、混乱が生じることがあります。 `.gitignore`ファイルを用意し、全員が同じ管理対象外とするファイルを設定することで、管理しやすいリポジトリを作成することができます。

まずは、 `.gitignore`ファイルの作成方法について見ていきましょう。

---

## `.gitignore`ファイルの作成方法

`.gitignore`ファイルの作成には、以下の2つの方法があります。

### 手動作成

`.gitignore`ファイルは、リポジトリのルートディレクトリに設置します。`touch`コマンドやファイルマネージャーなど、手動で作成する方法があります。

手動で作成する際には、`.gitignore`ファイルをルートディレクトリに置き、対象外とするファイルやディレクトリを記述します。

例えば以下のように、`test.log`ファイルや`/vendor`ディレクトリを管理対象外とする場合、`.gitignore`ファイルに以下のように記述します。

```git
#指定のファイルを非管理対象とする
test.log
# 指定のディレクトリを非管理対象とする
/vendor
```

### GitIgnore.ioを利用する

[GitIgnore.io](https://www.gitignore.io/)は、利用する言語やフレームワーク、IDE等から、`.gitignore`ファイルを自動生成するツールです。 複数の言語やIDEを利用している場合には、自分で記述するよりも便利に利用することができます。

サイト上で必要な設定を行い、作成した`.gitignore`の内容を、手動でルートディレクトリに設置してください。

---

## `.gitignore`ファイルの記述方法

`.gitignore`ファイルには、以下のように記載することができます。

1. ファイルパス
   - ファイル名にマッチ
   - ディレクトリ名にマッチ"> 
1. ファイルパスとパターンを組み合わせる
1. `#`でコメントを書くことができます
1. `!`を先頭記号に書くことで、管理対象にすることができます

### ファイルパス

`.gitignore`ファイルを用いる際には、下記のようなパターンで指定することができます。

```python
test.log  # 特定のファイルを指定する
temp   # 特定のファイルやディレクトリを指定する
*.log # 拡張子が指定したもののファイルを指定する
secret_??.txt # ワイルドカードを利用し、指定したパターンのファイルを指定する
```

### ファイルパスとパターンを組み合わせる

`.gitignore`ファイルを用いる際には、下記のような方法で、ファイル名やディレクトリを指定することができます。

```python
temp/* # temp/ディレクトリ下の全ファイル、ディレクトリを指定
temp/** # temp/ディレクトリ下の全階層に渡るファイル、ディレクトリを指定(applicable starting Git 2.8.0)
!temp/log/log.txt # log.txtファイルは、管理対象とする
temp/*/data/data.csv # fooディレクトリ含むその下階層のdata.csvファイル
```

### `#`でコメントを書くことができます

`.gitignore`ファイルを明確にするために、 `#`でコメントを書くことができます。

```python
*.log   # *.logを指定
# Secret Configファイル
config_secret.py    # config_secret.pyを指定
```

### `!`を先頭記号に書くことで、管理対象にすることができます。

`.gitignore`ファイルで除外しているディレクトリに対して、特定のファイルだけ管理対象にすることができます。

```python
/composer.lock    # composer.lockのみ除外し、他は管理対象
!/web/app/themes/customtheme/composer.lock    # /web/app/themes/customtheme/composer.lockを管理対象にする
```

---

## まとめ

今回は、`.gitignore`ファイルの使い方について解説しました。

リポジトリを開発環境で共有する際には、`.gitignore`ファイルを設定することで、管理対象にしないファイル数を減らし、管理しやすいリポジトリを作成することができます。

環境依存の設定ファイルを管理対象から除外することで、誤った設定ファイルを共有することを防ぎます。

サンプルコードとして、以下にGitIgnore.ioを利用して自動生成した`.gitignore`ファイルを載せます。

```python
# Created by https://www.gitignore.io/api/python,emacs,linux,macos
# Edit at https://www.gitignore.io/?templates=python,emacs,linux,macos

### Python ###
# Byte-compiled / optimized / DLL files
__pycache__/
*.py[cod]
*$py.class

# C extensions
*.so

# Distribution / packaging
.Python
env/
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# PyInstaller
#  Usually these files are written by a python script from a template
#  before PyInstaller builds the exe, so as to inject date/other infos into it.
*.manifest
*.spec

# Installer logs
pip-log.txt
pip-delete-this-directory.txt

# Virtual environments
venv/
ENV/
env.bak/
env/
pythonenv*
.Python36*

# IDE files
.project
.pydevproject
workspace.xml
.vscode/
.idea
dist/
build/
target/
.venv/
.idea_modules/
django_debug.log
pytest_cache/
pytest.ini

# Sphinx documentation
docs/_build/

# PyBuilder
target/

# Jupyter Notebook
.ipynb_checkpoints

# File-type config:
*.log

# mypy: https://github.com/python/mypy.git
.mypy_cache/

# asyncio debug
*.sock

# standard python ignore
*~




### Emacs ###
#-*- mode: gitignore; -*-
*~
.#*
.#*#
*.elc
*.pyc



### Linux ###
*~
.cache/
logs/
*.log
*.log.*
*.swp
*.swo
rotatelogs*
local_settings.py
media/aperr_params.json
generated/


### macOS ###
*.DS_Store
.AppleDouble
.LSOverride
Icon
._*
.thumbnail/
.metadata
.svn/
.docdata
.idea/
.project
.pydevproject
.settings/
*.xcworkspace
*.iml
xcuserdata/
.DS_Store?
profile
robomongo.json
.DS_Store.?
.Debug/
.Release/

# End of https://www.gitignore.io/api/python,emacs,linux,macos
```
