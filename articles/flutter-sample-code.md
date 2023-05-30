<!--
title: 【基礎】flutterのサンプルコードまとめ
tags: flutter,サンプルコード
id: 
private: false
-->

こんにちは。今回は、flutterについて初心者エンジニアに向けて、flutterのサンプルコードまとめについて紹介したいと思います。flutterは、googleが開発したモバイルアプリ開発フレームワークであり、開発者に多くの便利な機能を提供しています。flutterを学ぶためには、サンプルコードを実際に試してみることが大切です。そこで、今回はflutterのサンプルコードをまとめて紹介します。

## flutterのサンプルコード集

### ウィジェットのサンプルコード

flutterでは、ウィジェットを使用して様々なコンポーネントを作成します。以下は、flutterのウィジェットのサンプルコードです。

```
import 'package:flutter/material.dart';

void main() {
  runapp(myapp());
}

class myapp extends statelesswidget {
  @override
  widget build(buildcontext context) {
    return materialapp(
      title: 'flutter widget',
      theme: themedata(
        primaryswatch: colors.blue,
        visualdensity: visualdensity.adaptiveplatformdensity,
      ),
      home: scaffold(
        appbar: appbar(
          title: text('flutter widget'),
        ),
        body: center(
          child: text(
            'hello, world!',
            style: textstyle(fontsize: 30),
          ),
        ),
      ),
    );
  }
}
```

上記のサンプルコードでは、materialapp ウィジェットを使用してアプリのテーマを設定し、scaffold ウィジェットを使用してアプリの構造を定義しています。また、appbar ウィジェットを使用してアプリの上部にバーを作成し、text ウィジェットを使用して画面の中央にテキストを表示しています。

### flutterの状態管理

flutterでは、アプリの状態を管理するために状態管理ライブラリを提供しています。以下は、flutterの状態管理のサンプルコードです。

```
import 'package:flutter/material.dart';

void main() {
  runapp(myapp());
}

class myapp extends statefulwidget {
  @override
  _myappstate createstate() => _myappstate();
}

class _myappstate extends state<myapp> {
  string _text = 'hello, world!';

  void _changetext() {
    setstate(() {
      _text = 'hello, flutter!';
    });
  }

  @override
  widget build(buildcontext context) {
    return materialapp(
      title: 'flutter state management',
      theme: themedata(
        primaryswatch: colors.blue,
        visualdensity: visualdensity.adaptiveplatformdensity,
      ),
      home: scaffold(
        appbar: appbar(
          title: text('flutter state management'),
        ),
        body: center(
          child: column(
            mainaxisalignment: mainaxisalignment.center,
            children: [
              text(
                _text,
                style: textstyle(fontsize: 30),
              ),
              sizedbox(height: 10),
              raisedbutton(
                child: text('change text'),
                onpressed: _changetext,
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

上記のサンプルコードでは、statefulwidget ウィジェットを使用してアプリの状態を管理し、setstate() メソッドを使用して状態が変更されたときに再レンダリングします。また、raisedbutton ウィジェットを使用して、ボタンがクリックされたときに状態を変更します。

### flutterのアニメーション

flutterでは、アニメーションを作成するための豊富な機能を提供しています。以下は、flutterのアニメーションのサンプルコードです。

```
import 'package:flutter/material.dart';

void main() {
  runapp(myapp());
}

class myapp extends statefulwidget {
  @override
  _myappstate createstate() => _myappstate();
}

class _myappstate extends state<myapp> with singletickerproviderstatemixin {
  animationcontroller _controller;
  animation<offset> _animation;

  @override
  void initstate() {
    super.initstate();
    _controller = animationcontroller(
      vsync: this,
      duration: duration(seconds: 1),
    );
    _animation = tween<offset>(
      begin: offset(0, 1),
      end: offset.zero,
    ).animate(_controller);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  widget build(buildcontext context) {
    return materialapp(
      title: 'flutter animation',
      theme: themedata(
        primaryswatch: colors.blue,
        visualdensity: visualdensity.adaptiveplatformdensity,
      ),
      home: scaffold(
        appbar: appbar(
          title: text('flutter animation'),
        ),
        body: center(
          child: slidetransition(
            position: _animation,
            child: text(
              'hello, flutter!',
              style: textstyle(fontsize: 30),
            ),
          ),
        ),
        floatingactionbutton: floatingactionbutton(
          child: icon(icons.play_arrow),
          onpressed: () {
            if (_controller.status == animationstatus.completed) {
              _controller.reverse();
            } else {
              _controller.forward();
            }
          },
        ),
      ),
    );
  }
}
```

上記のサンプルコードでは、singletickerproviderstatemixin を使用してアニメーションのステータスを設定し、animationcontroller を使用してアニメーションを制御します。また、tween クラスを使用して、アニメーションの開始位置と終了位置を定義し、slidetransition ウィジェットを使用して、テキストがアニメーションするようにします。

### flutterのhttpリクエスト

flutterでは、httpリクエストを簡単に実行できます。以下は、flutterのhttpリクエストのサンプルコードです。

```
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() {
  runapp(myapp());
}

class myapp extends statefulwidget {
  @override
  _myappstate createstate() => _myappstate();
}

class _myappstate extends state<myapp> {
  string _text = '';

  void _fetchdata() async {
    final response =
        await http.get('https://jsonplaceholder.typicode.com/todos/1');
    if (response.statuscode == 200) {
      final data = jsondecode(response.body);
      setstate(() {
        _text = data['title'];
      });
    } else {
      setstate(() {
        _text = 'error: ${response.statuscode}';
      });
    }
  }

  @override
  widget build(buildcontext context) {
    return materialapp(
      title: 'flutter http request',
      theme: themedata(
        primaryswatch: colors.blue,
        visualdensity: visualdensity.adaptiveplatformdensity,
      ),
      home: scaffold(
        appbar: appbar(
          title: text('flutter http request'),
        ),
        body: center(
          child: text(
            _text,
            style: textstyle(fontsize: 30),
          ),
        ),
        floatingactionbutton: floatingactionbutton(
          child: icon(icons.cloud_download),
          onpressed: _fetchdata,
        ),
      ),
    );
  }
}
```

上記のサンプルコードでは、http パッケージを使用して、httpリクエストを実行します。また、jsondecode() メソッドを使用して、jsonデータを解析し、状態が変更されたときに再レンダリングします。また、floatingactionbutton ウィジェットを使用して、ボタンがクリックされたときにhttpリクエストを実行します。

### flutterのローカルストレージ

flutterでは、ローカルストレージを簡単に実装できます。以下は、flutterのローカルストレージのサンプルコードです。

```
import 'dart:convert';
import 'dart:io';

import 'package:flutter/material.dart';
import 'package:path_provider/path_provider.dart';

void main() {
  runapp(myapp());
}

class myapp extends statefulwidget {
  @override
  _myappstate createstate() => _myappstate();
}

class _myappstate extends state<myapp> {
  string _text = '';

  @override
  void initstate() {
    super.initstate();
    _loaddata();
  }

  void _loaddata() async {
    final directory = await getapplicationdocumentsdirectory();
    final file = file('${directory.path}/data.txt');
    if (await file.exists()) {
      final data = jsondecode(await file.readasstring());
      setstate(() {
        _text = data['text'];
      });
    } else {
      setstate(() {
        _text = 'no data';
      });
    }
  }

  void _savedata() async {
    final directory = await getapplicationdocumentsdirectory();
    final file = file('${directory.path}/data.txt');
    await file.writeasstring(jsonencode({'text': _text}));
  }

  @override
  widget build(buildcontext context) {
    return materialapp(
      title: 'flutter local storage',
      theme: themedata(
        primaryswatch: colors.blue,
        visualdensity: visualdensity.adaptiveplatformdensity,
      ),
      home: scaffold(
        appbar: appbar(
          title: text('flutter local storage'),
        ),
        body: center(
          child: textfield(
            decoration: inputdecoration(hinttext: 'enter text'),
            onchanged: (text) {
              setstate(() {
                _text = text;
              });
            },
          ),
        ),
        floatingactionbutton: floatingactionbutton(
          child: icon(icons.save),
          onpressed: _savedata,
        ),
      ),
    );
  }
}
```

上記のサンプルコードでは、path_providerパッケージを使用して、デバイスのファイルシステムにアクセスします。また、fileクラスを使用して、ファイルを操作します。また、jsonencode()メソッドを使用して、データをjson形式に変換します。また、textfied ウィジェットを使用して、ユーザーにデータを入力してもらい、状態が変更されたときに再レンダリングします。

## まとめ

flutterのサンプルコードについて紹介しました。flutterを学ぶためには、サンプルコードを実際に試してみることが大切です。今回紹介したflutterのサンプルコードを参考に、自分なりのアプリを作成してみてください。

参考情報：
- [flutter公式ドキュメント(日本語)](https://flutter.dev/docs/get-started/flutter-for/ios-android-devs)
- [フロントエンドエンジニア初心者がflutterを使ってアプリを作ってみた話](https://benoitpatra.com/2020/04/15/flutter/)
- [flutterでfirebase authenticationとfirestoreを使ってみた](https://qiita.com/amfuku/items/edb0201e2a0bca9754b4)

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)

