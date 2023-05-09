<!--
title:   JsonデータをPythonで扱う方法
tags:    JSON,Python,使い方
id:      80fed6448c7a8bfed9da
private: false
-->


こんにちは。今回は、PythonでJSONを使う方法について説明します。

はじめに
JSONは、JavaScript Object Notationの略で、文字列を使ってデータを格納するための軽量なデータ交換フォーマットです。PythonでもJSONを扱うことができ、辞書やリストなどのPythonのオブジェクトをJSONに変換したり、JSONをPythonのオブジェクトに変換したりすることができます。

PythonでJSONを扱うには、jsonモジュールを使用します。jsonモジュールは、JSONのエンコード、デコード、および検証を提供します。

JSONのエンコード
PythonのオブジェクトをJSONに変換するには、json.dumps()メソッドを使用します。以下のように使用します。

```python
import json

data = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

json_string = json.dumps(data)

print(json_string)
```

上記のプログラムでは、dataという辞書オブジェクトをJSON文字列に変換しています。json.dumps()メソッドはオブジェクトをJSON文字列に変換し、変換された文字列を返します。

実行結果：
```
{"name": "John", "age": 30, "city": "New York"}
```

JSONのデコード
JSONデータをPythonのオブジェクトに変換するには、json.loads()メソッドを使用します。以下のように使用します。

```python
import json

json_string = '{"name": "John", "age": 30, "city": "New York"}'

data = json.loads(json_string)

print(data)
```

上記のプログラムでは、json_stringというJSON文字列を辞書オブジェクトに変換しています。json.loads()メソッドはJSON形式の文字列をPython形式のオブジェクトに変換します。変換されたデータは変数dataに代入されます。

実行結果：
```
{'name': 'John', 'age': 30, 'city': 'New York'}
```

データの書き込みと読み込み
Pythonでは、JSON形式のデータをファイルに書き込むことができます。書き込みには、json.dump()メソッドを使用し、読み込みには、json.load()メソッドを使用します。

以下は、JSONデータをファイルに書き込む例です。

```python
import json

data = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

with open('data.json', 'w') as f:
    json.dump(data, f)
```

上記のプログラムでは、dataという辞書オブジェクトをdata.jsonファイルに書き込んでいます。with open() as文を使用して、ファイルを開き、json.dump()メソッドでdataをdata.jsonファイルに書き込んでいます。

以下は、JSONデータをファイルから読み込む例です。

```python
import json

with open('data.json', 'r') as f:
    data = json.load(f)

print(data)
```

上記のプログラムでは、data.jsonファイルからデータを読み込み、dataに代入しています。with open() as文を使用して、ファイルを開き、json.load()メソッドでdata.jsonファイルからデータを読み込んでいます。

まとめ
Pythonでは、jsonモジュールを使用することでJSONデータを扱うことができます。PythonのオブジェクトをJSONデータに変換するには、json.dumps()メソッドを使用し、JSONデータをPythonのオブジェクトに変換するには、json.loads()メソッドを使用します。また、JSONデータをファイルに書き込むには、json.dump()メソッドを使用し、ファイルからJSONデータを読み込むには、json.load()メソッドを使用します。

参考:
- [PythonでJSONを扱う方法](https://techacademy.jp/magazine/34829)
- [PythonでJSONを扱う方法](https://www.atmarkit.co.jp/ait/articles/1912/13/news024.html)