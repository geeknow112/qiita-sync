<!--
title: Flutter入門：初心者エンジニアが知っておくべき使い方
tags: flutter,使い方,モバイルアプリ,アプリ開発
id: 
private: false
-->

はじめに

こんにちは。今回は、Flutterについて初心者エンジニアに向けて、基本的な使い方を紹介します。

FlutterはGoogleが開発した、iOSとAndroid向けのネイティブモバイルアプリを開発するためのフレームワークです。Dartというオブジェクト指向言語で記述され、ウィジェットという概念があり、見た目や操作感がiOSとAndroidで統一された高品質のアプリを、短時間で開発することができます。

ここでは、Flutterの基本的な使い方やアプリ開発の流れを紹介します。

1. Flutterのインストール

Flutterをインストールするためには、以下の手順を実行します。

1. Flutter SDKのダウンロード

Flutter SDKをダウンロードして展開します。展開後、Flutter SDKを実行するためにパスを通します。

2. Android Studioのインストール

Flutter SDKを利用するために、Android Studioをインストールします。ダウンロードしてインストールするだけで、Android StudioにFlutterプラグインが同時にインストールされるため、簡単に使い始めることができます。

2. アプリの作成

Flutter SDKをインストールしたら、次はアプリを開発するための作業を行います。


### Flutterのプロジェクトを作成

Flutterの新プロジェクトを作成するには、以下のコマンドを実行します。プロジェクト名は、適宜変更してください。

```
$ flutter create my_project
```

プロジェクトの構成は、以下のようになります。

```
my_project/
  ├─android/
  ├─ios/
  └─lib/
    ├─main.dart
```

### Flutterプロジェクトの構成

- android: Android向けのプロジェクトファイルが格納される
- ios: iOS向けのプロジェクトファイルが格納される
- lib:  Flutterアプリのソースコードが格納される

### Flutterアプリケーションの作成

Flutterアプリを開発するために、main.dartを編集します。main.dartには、以下のようにコードを記述します。

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
    );
  }
}
```

3. Flutterアプリの開発

Flutterアプリの開発に移行する前に、留意点としては以下のようなことがあります。

 - Flutterアプリの作成は、すべてDart言語でコーディングします。
 - FlutterアプリのUIは、ウィジェットと呼ばれる部品を組み合わせて作り上げます。
 - Flutterアプリでは、Flutter SDK7に含まれる大量のウィジェットを利用できます。
 - 既存のコードを再利用することができます。


### Flutterアプリのコード例

以下のコードは、レストランのメニューを表示するFlutterアプリのコード例です。

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    title: 'Shopping App',
    home: HomePage(),
  ));
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Restaurant'),
      ),
      body: Column(
        children: [
          Text(
            '今日のメニュー',
            style: TextStyle(
              fontWeight: FontWeight.bold,
              fontSize: 40,
            ),
          ),
          SizedBox(height: 16),
          Card(
            child: Column(
              children: [
                ListTile(
                  leading: CircleAvatar(
                    backgroundImage: AssetImage('food.jpg'),
                  ),
                  title: Text('カカオ豆'),
                  subtitle: Text('300円'),
                  onTap: () {},
                ),
              ],
            ),
          ),
          Card(
            child: Column(
              children: [
                ListTile(
                  leading: CircleAvatar(
                    backgroundImage: AssetImage('food.jpg'),
                  ),
                  title: Text('カカオマス'),
                  subtitle: Text('400円'),
                  onTap: () {},
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }
}
```

まとめ

Flutterは、iOSとAndroidに対応し、ネイティブモバイルアプリの開発を高速かつ効率的に行うことができます。Flutter SDKをダウンロードしてインストールし、Android Studioを使ってアプリ開発を始めることができます。

ここでは、Flutterアプリを作成する基本的な手順とコード例を紹介しました。開発環境が整っていれば、Dart言語を使用して、高品質なモバイルアプリを開発することができます。

参考

- [Flutter Getting Started](https://flutter.dev/docs/get-started/install)
- [フラッターフレームワークとは何ですか？](https://airbnb.io/lottie/blog/what-is-flutter.html)
