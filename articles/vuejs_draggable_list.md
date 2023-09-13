<!--
title: 【vue.js】ドラッグ可能なリストを作成するためのdraggableの活用方法
tags: javascript,vue.js
id: 
private: false
-->

こんにちは。今回は、
vue.jsについて初心者エンジニアに向けて、ドラッグ可能なリストを作成するためのdraggableの活用方法についてご紹介します。

## リストの表示とデータバインディングの設定方法
vue.jsを使用してドラッグ可能なリストを作成するには、まずリストの表示とデータバインディングの設定を行う必要があります。以下のコードは、vue.jsを使用してリストとデータを表示する例です。

```javascript
<template>
  <div>
    <ul>
      <li v-for="item in list" :key="item.id">
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [
        { id: 1, name: 'item 1' },
        { id: 2, name: 'item 2' },
        { id: 3, name: 'item 3' }
      ]
    };
  }
};
</script>
```

上記のコードでは、`<ul>`要素内に`v-for`ディレクティブを使用してリストアイテムを表示しています。`v-for`ディレクティブによって、`list`配列の要素がループされてリストアイテムが生成されます。

## ドラッグ操作の有効化とリストアイテムの設定
次に、ドラッグ操作を有効にし、各リストアイテムにドラッグ可能な機能を設定する必要があります。以下のコードは、`draggable`属性を使用してドラッグ操作を有効化し、`@dragstart`イベントを使用してドラッグ開始時にデータを設定する例です。

```javascript
<template>
  <div>
    <ul>
      <li v-for="item in list" :key="item.id" draggable @dragstart="handledragstart(item)">
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [
        { id: 1, name: 'item 1' },
        { id: 2, name: 'item 2' },
        { id: 3, name: 'item 3' }
      ]
    };
  },
  methods: {
    handledragstart(item) {
      // ドラッグデータを設定
      event.datatransfer.setdata('text/plain', json.stringify(item));
    }
  }
};
</script>
```

上記のコードでは、`draggable`属性を使用してリストアイテムをドラッグ可能にし、`@dragstart`イベントを設定しています。`@dragstart`イベントハンドラ内で、ドラッグアクションが開始された際にデータを設定しています。

## ドラッグアンドドロップのソート機能の実装方法
ドラッグアンドドロップのソート機能を実装するには、ドラッグ操作のイベントハンドラ内で、ドロップ位置のデータを更新する必要があります。以下のコードは、`@dragover`イベントと`@drop`イベントを使用してドロップ位置のデータを更新する例です。

```javascript
<template>
  <div>
    <ul>
      <li v-for="item in list" :key="item.id" draggable @dragstart="handledragstart(item)" @dragover="handledragover" @drop="handledrop(item)">
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [
        { id: 1, name: 'item 1' },
        { id: 2, name: 'item 2' },
        { id: 3, name: 'item 3' }
      ]
    };
  },
  methods: {
    handledragstart(item) {
      event.datatransfer.setdata('text/plain', json.stringify(item));
    },
    handledragover(event) {
      event.preventdefault();
    },
    handledrop(item) {
      event.preventdefault();
      const draggeditem = json.parse(event.datatransfer.getdata('text/plain'));
      const dropindex = this.list.findindex(i => i.id === item.id);
      this.list.splice(dropindex, 0, draggeditem);
      this.list.splice(this.list.findindex(i => i.id === draggeditem.id), 1);
    }
  }
};
</script>
```

上記のコードでは、`@dragover`イベントを使用してドラッグオーバー時にデフォルトのドロップ操作をキャンセルし、`@drop`イベントを使用してドロップ位置におけるデータの更新を行っています。

## リスト内の要素の移動と順序の変更手法
リスト内の要素の移動と順序の変更は、ドラッグアンドドロップのソート機能を使用して実現することができます。上記のコードでは、`handledrop`メソッド内でリストの要素の移動と順序の変更が行われています。

## リストの更新と変更の監視方法
リストの更新と変更の監視は、vue.jsのリアクティブなデータの更新と監視機能を活用して行うことができます。以下のコードは、リストの更新と変更を監視する例です。

```javascript
<template>
  <div>
    <ul>
      <li v-for="item in list" :key="item.id">{{ item.name }}</li>
    </ul>
    <button @click="additem">add item</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [
        { id: 1, name: 'item 1' },
        { id: 2, name: 'item 2' },
        { id: 3, name: 'item 3' }
      ]
    };
  },
  methods: {
    additem() {
      const newitem = { id: this.list.length + 1, name: `item ${this.list.length + 1}` };
      this.list.push(newitem);
    }
  }
};
</script>
```

上記のコードでは、`<button>`要素をクリックすると新しいアイテムが追加され、リストが更新されます。vue.jsのリアクティブなデータの更新と監視機能によって、リストの変更が自動的に反映されます。

以上が、vue.jsを使用してドラッグ可能なリストを作成するためのdraggableの活用方法についての解説でした。初心者エンジニアの方にも分かりやすく、実践的な知識となっていれば幸いです。

参考ブログ記事：
- [vue.jsでドラッグ＆ドロップ可能なリスト作成](https://www.webprofessional.jp/drag-drop-vue-js/)
- [vue.draggable - レジェンダリーなドラッグ&ドロップリスト！](https://qiita.com/ryo2132/items/3e5281f6d7147f3b277c)

　

## 【Vue.js】関連のまとめ
https://hack-note.com/summary/vuejs-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

