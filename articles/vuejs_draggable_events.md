<!--
title:   【vue.js】ドラッグアンドドロップの操作イベントとハンドリング方法
tags:    JavaScript,Vue.js
id:      179aa26df323a2cca705
private: false
-->


## ドラッグアンドドロップの操作イベントとハンドリング方法

こんにちは。今回は、vue.jsについて初心者エンジニアに向けて、ドラッグアンドドロップの操作イベントとそのハンドリング方法についてご紹介します。

### ドラッグアンドドロップの基本的な操作イベントの概要

ドラッグアンドドロップは、ウェブアプリケーションで要素をマウスでドラッグして別の場所に移動する操作のことです。vue.jsでは、ドラッグアンドドロップに関連する以下のイベントが利用できます。

- dragstart: 要素をドラッグ開始した時に発生するイベントです。このイベントをキャンセルすることで、ドラッグを無効化することもできます。
- drag: 要素をドラッグ中にマウスを移動させると発生するイベントです。このイベントを利用することで、要素の位置を更新したり、他の要素に影響を与えることができます。
- dragend: 要素をドラッグ終了した時に発生するイベントです。ドラッグが正常に終了したかどうかを判定するために利用されます。
- dragenter: ドラッグ中の要素がドロップ要素に入った瞬間に発生するイベントです。このイベントを利用することで、ドロップ要素のスタイルを変更したり、他の要素との交換を行ったりすることができます。
- dragleave: ドラッグ中の要素がドロップ要素から外れた瞬間に発生するイベントです。このイベントを利用することで、ドロップ要素のスタイルを元に戻したり、他の要素との交換をやめたりすることができます。
- drop: ドラッグ中の要素をドロップした時に発生するイベントです。このイベントを利用することで、ドロップされた要素を取得したり、ドロップ時の処理を行ったりすることができます。

これらのイベントは、ドラッグ要素とドロップ要素に対してそれぞれ登録することができます。次に、各イベントのハンドリング方法と活用例をご紹介します。

## ドラッグ開始イベントのハンドリング方法と活用例

ドラッグ開始イベント（dragstart）は、要素をドラッグし始めた瞬間に発生します。このイベントをバインディングし、ドラッグ開始時の処理を行うことができます。以下に、ドラッグ開始イベントのハンドリング方法とその活用例を示します。

```javascript
<div draggable="true" @dragstart="handledragstart">
  ドラッグ対象要素
</div>

methods: {
  handledragstart(event) {
    // ドラッグ開始時の処理を記述する
  }
}
```

上記のコードでは、`div` 要素をドラッグ可能にするために `draggable` 属性を設定し、`dragstart` イベントをバインディングしています。`handledragstart` メソッドは、ドラッグ開始時に実行されるメソッドであり、ここにドラッグ開始時の処理を記述します。

ドラッグ開始時の処理として、フラグの切り替えやデータの取得・加工などを行うことができます。ドラッグ中の要素にマウスカーソルの形状を変更する場合などにも活用することができます。

## ドラッグ中の要素位置の更新と表示の反映方法

ドラッグ中の要素の位置を更新し、その表示を反映させる方法について説明します。ドラッグ中の要素の位置を更新するには、ドラッグ中イベント（drag）を利用します。以下に、ドラッグ中イベントのハンドリング方法と位置の更新・表示の反映方法を示します。

```javascript
<div draggable="true" @drag="handledrag" style="position: absolute; top: 0; left: 0;">
  ドラッグ対象要素
</div>

data() {
  return {
    dragposx: 0,
    dragposy: 0
  };
},
methods: {
  handledrag(event) {
    this.dragposx = event.clientx;
    this.dragposy = event.clienty;
  }
}
```

上記のコードでは、`div` 要素をドラッグ可能にするために `draggable` 属性を設定し、`drag` イベントをバインディングしました。また、`div` 要素の位置を指定するために `style` 属性で `position`、`top`、`left` の値を設定しています。

`handledrag` メソッドでは、`event` オブジェクトの `clientx` プロパティと `clienty` プロパティを使用して、マウスの座標を取得します。そして、取得した座標を `data` オプションで定義した `dragposx`、`dragposy` の変数に格納し、表示の反映を行います。

このようにして、ドラッグ中の要素の位置をリアルタイムに更新し、その変化を画面上に反映させることができます。

## ドロップイベントのハンドリングとドロップ時の処理手法

ドロップイベント（drop）は、要素がドロップされた瞬間に発生します。このイベントをバインディングし、ドロップ時の処理を行うことができます。以下に、ドロップイベントのハンドリングとその処理手法を示します。

```javascript
<div @drop="handledrop" @dragover="allowdrop">
  ドロップ先要素
</div>

methods: {
  handledrop(event) {
    // ドロップ時の処理を記述する
  },
  allowdrop(event) {
    event.preventdefault();
  }
}
```

上記のコードでは、`div` 要素をドロップ先として利用するために `drop` イベントと `dragover` イベントをバインディングしています。`allowdrop` メソッドは、`dragover` イベントで呼び出され、デフォルトのドロップ動作を許可するためのメソッドです。

`handledrop` メソッドは、`drop` イベントで呼び出され、ドロップ時の処理を記述します。このメソッド内で、ドロップされた要素の取得や他の要素との交換などの処理を行うことができます。

なお、`dragover` イベントにはデフォルトの処理があるため、ドロップ操作を許可するためには `event.preventdefault()` を呼び出す必要があります。

## ドラッグアンドドロップ操作のキャンセルとリセット方法

ドラッグアンドドロップ操作をキャンセルしたり、リセットする方法について説明します。ドラッグ操作をキャンセルしたい場合には、`dragstart` イベントで `event.preventdefault()` を呼び出すことで、ドラッグを無効化することができます。

```javascript
<div draggable="true" @dragstart="handledragstart">
  ドラッグ対象要素
</div>

methods: {
  handledragstart(event) {
    event.preventdefault();
  }
}
```

上記のコードでは、`div` 要素をドラッグ可能にするために `draggable` 属性を設定し、`dragstart` イベントをバインディングしています。`handledragstart` メソッド内で `event.preventdefault()` を呼び出すことで、ドラッグ操作をキャンセルしています。

また、ドラッグ操作をリセットする場合には、`dragend` イベントで `event.preventdefault()` を呼び出すことで、ドラッグを終了させることができます。

```javascript
<div draggable="true" @dragend="handledragend">
  ドラッグ対象要素
</div>

methods: {
  handledragend(event) {
    event.preventdefault();
  }
}
```

上記のコードでは、`div` 要素をドラッグ可能にするために `draggable` 属性を設定し、`dragend` イベントをバインディングしています。`handledragend` メソッド内で `event.preventdefault()` を呼び出すことで、ドラッグ操作を終了させています。

以上が、vue.jsにおけるドラッグアンドドロップの操作イベントとハンドリング方法についての説明でした。初心者エンジニアの方にとって、これからこれらのイベントを活用して、ドラッグアンドドロップの操作を実装する際の参考になれば幸いです。

参考記事：
- [vue.js公式ドキュメント - ドラッグアンドドロップ](https://jp.vuejs.org/v2/guide/events.html#%e3%83%89%e3%83%a9%e3%83%83%e3%82%b0%e3%82%a2%e3%83%b3%e3%83%89%e3%83%89%e3%83%ad%e3%83%83%e3%83%97)
- [qiita - 【vue.js】dragstartイベントでデータを持ち運ぶ](https://qiita.com/jagas/items/3860ea4e3601be20cfd0)



## 【Vue.js】関連のまとめ
https://hack-note.com/summary/vuejs-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
