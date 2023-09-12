<!--
title: 【vue.js】draggableコンポーネントの基本的な使い方と導入方法
tags: javascript,vue.js
id: 
private: false
-->

## draggableコンポーネントの導入と依存関係の設定

vue.jsについて初心者エンジニアに向けて、今回はdraggableコンポーネントの基本的な使い方と導入方法について解説します。draggableコンポーネントは、要素をドラッグして移動させることができる機能を持つコンポーネントです。これを利用することで、ユーザーが要素をドラッグして自由に配置することができるようなインタラクティブなアプリケーションを作ることができます。

まず、draggableコンポーネントを導入するためには、vue.jsのプロジェクトに以下のように必要な依存関係を設定する必要があります。

```javascript
// package.json
{
  // ...

  "dependencies": {
    // ...
    "vue-draggable-resizable": "^2.2.1"
  }
}
```

上記の依存関係を設定した後、以下のコマンドで必要なパッケージをインストールします。

```bash
$ npm install
```

または

```bash
$ yarn install
```

これによって、draggableコンポーネントを利用するために必要なパッケージがプロジェクトに追加されます。

## 基本的なドラッグ操作と要素の移動方法

draggableコンポーネントでは、要素をドラッグして移動させることができます。これを実現するために、以下のような基本的な操作方法が用意されています。

1. ドラッグする要素を指定する: ドラッグ可能な要素を指定するために、`draggable`属性を要素に追加します。

```html
<template>
  <div>
    <div class="draggable-element" draggable>ドラッグ可能な要素</div>
  </div>
</template>
```

2. 要素をドラッグして移動する: ドラッグ可能な要素をマウスでドラッグすると、要素が移動します。

```html
<template>
  <div>
    <div class="draggable-element" draggable>ドラッグ可能な要素</div>
    <div class="drop-zone">ドロップゾーン</div>
  </div>
</template>

<script>
export default {
  mounted() {
    const draggableelement = this.$el.queryselector('.draggable-element');
    draggableelement.addeventlistener('dragstart', (event) => {
      event.datatransfer.setdata('text/plain', event.target.id);
    });
  },
};
</script>

```

上記のように、`dragstart`イベントを利用して要素の移動を開始することができます。

## ドラッグ可能な要素のカスタマイズとスタイリングの方法

draggableコンポーネントを利用する際には、要素のカスタマイズやスタイリングを行うことができます。以下のような方法があります。

1. ドラッグ可能な要素のスタイルを設定する: ドラッグ可能な要素のスタイルをcssで設定することで、見た目をカスタマイズすることができます。

```css
.draggable-element {
  cursor: grab;
  border: 1px solid #ccc;
  background-color: #fff;
  padding: 10px;
}

.draggable-element:active {
  cursor: grabbing;
  border-color: #000;
}
```

2. カスタムハンドルを作成する: ドラッグ操作用のカスタムハンドルを作成し、要素の一部分だけをドラッグ操作の対象とすることもできます。

```html
<template>
  <div>
    <div class="draggable-element">
      <div class="handle">ドラッグハンドル</div>
      <div>要素の内容</div>
    </div>
    <div class="drop-zone">ドロップゾーン</div>
  </div>
</template>

<script>
export default {
  mounted() {
    const draggableelement = this.$el.queryselector('.draggable-element');
    const handleelement = this.$el.queryselector('.handle');
    handleelement.addeventlistener('mousedown', (event) => {
      event.preventdefault();
      draggableelement.draggable = true;
    });
    draggableelement.addeventlistener('dragstart', (event) => {
      event.datatransfer.setdata('text/plain', event.target.id);
    });
    draggableelement.addeventlistener('dragend', () => {
      draggableelement.draggable = false;
    });
  },
};
</script>
```

上記の例では、`.handle`クラスが付与された要素(`ドラッグハンドル`)をクリックしてドラッグ操作を開始し、要素全体ではなくハンドル部分だけがドラッグ操作の対象となるようになります。

## ドラッグアンドドロップのイベントとハンドリング方法

draggableコンポーネントでは、ドラッグアンドドロップに関連するイベントが提供されており、それらのイベントをハンドリングすることで、さまざまな操作や処理を実装することができます。

以下に、よく利用されるドラッグアンドドロップのイベントとそのハンドリング方法を示します。

1. `dragstart`: ドラッグ操作が開始されたときに発火します。このイベントハンドラ内では、ドラッグする要素にデータを設定することができます。

```javascript
draggableelement.addeventlistener('dragstart', (event) => {
  event.datatransfer.setdata('text/plain', event.target.id);
});
```

2. `dragover`: ドラッグ中の要素がドロップゾーン上に移動しているときに発火します。このイベントのデフォルトの動作は、ドロップが無効であるため、イベントをキャンセルする必要があります。

```javascript
dropzoneelement.addeventlistener('dragover', (event) => {
  event.preventdefault();
});
```

3. `drop`: ドラッグ中の要素がドロップゾーンにドロップされたときに発火します。このイベントハンドラ内では、ドラッグしている要素にセットされているデータを取得することができます。

```javascript
dropzoneelement.addeventlistener('drop', (event) => {
  event.preventdefault();
  const data = event.datatransfer.getdata('text/plain');
  const draggableelement = document.getelementbyid(data);
  dropzoneelement.appendchild(draggableelement);
});
```

## ドラッグ操作の制約とドロップゾーンの設定方法

draggableコンポーネントでは、ドラッグ操作の制約やドロップゾーンの設定を行うことができます。

1. ドラッグ可能な要素の制約を設定する: ドラッグ可能な要素の制約を設定することで、ドラッグ操作を一部の範囲内に制限することができます。

```html
<template>
  <div>
    <div class="drag-area">
      <div class="draggable-element" draggable>ドラッグ可能な要素</div>
    </div>
    <div class="drop-zone">ドロップゾーン</div>
  </div>
</template>

<script>
export default {
  mounted() {
    const dragareaelement = this.$el.queryselector('.drag-area');
    const draggableelement = this.$el.queryselector('.draggable-element');
    draggableelement.addeventlistener('dragstart', (event) => {
      event.datatransfer.setdata('text/plain', event.target.id);
    });
    draggableelement.addeventlistener('dragenter', (event) => {
      event.preventdefault();
    });
    dragareaelement.addeventlistener('dragover', (event) => {
      event.preventdefault();
    });
    dragareaelement.addeventlistener('drop', () => {
      dragareaelement.appendchild(draggableelement);
    });
  },
};
</script>
```

上記の例では、`.drag-area`クラスが付与された要素がドラッグ操作の範囲となり、ドロップゾーン以外の場所へのドラッグを禁止しています。

2. ドロップゾーンの設定を行う: ドラッグ操作で要素をドロップする場合、対象の要素にドロップを許可するためのドロップゾーンを設定することができます。

```html
<template>
  <div>
    <div class="draggable-element" draggable>ドラッグ可能な要素</div>
    <div class="drop-zone" droppable>ドロップゾーン</div>
  </div>
</template>

<script>
export default {
  mounted() {
    const draggableelement = this.$el.queryselector('.draggable-element');
    draggableelement.addeventlistener('dragstart', (event) => {
      event.datatransfer.setdata('text/plain', event.target.id);
    });
    const dropzoneelement = this.$el.queryselector('.drop-zone');
    dropzoneelement.addeventlistener('dragover', (event) => {
      event.preventdefault();
    });
    dropzoneelement.addeventlistener('drop', (event) => {
      event.preventdefault();
      const data = event.datatransfer.getdata('text/plain');
      const draggableelement = document.getelementbyid(data);
      dropzoneelement.appendchild(draggableelement);
    });
  },
};
</script>
```

上記の例では、`.drop-zone`クラスが付与された要素がドロップゾーンとなり、ドラッグ可能な要素をこのゾーン内にドロップすることができます。

以上が、vue.jsのdraggableコンポーネントの基本的な使い方と導入方法の解説です。これを活用して、ユーザーに自由な配置を可能にするインタラクティブなアプリケーションを開発してみてください。

参考記事：
- [vuedraggableresizable - vue.js component for draggable and resizable elements](https://github.com/mauricius/vue-draggable-resizable)
- [drag and drop in vue.js using the vue-draggable directive](https://medium.com/@hamidv/how-to-drag-drop-using-vue-js-d58ab099a9c1)

　

## 【Vue.js】関連のまとめ
https://hack-note.com/summary/vuejs-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)


