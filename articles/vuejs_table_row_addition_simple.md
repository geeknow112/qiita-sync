<!--
title: 【vue.js】シンプルな方法でテーブルに行を追加する手順
tags: javascript,vue.js
id: 
private: false
-->

## vue.jsでの基本的なテーブルコンポーネントの作成

vue.jsは、javascriptのフレームワークであり、uiを構築するための強力なツールです。vue.jsを使用すると、データのバインディングやコンポーネントの再利用など、効率的な開発が可能となります。

まずはじめに、vue.jsで基本的なテーブルコンポーネントを作成する手順について説明します。

まず、htmlファイルにvue.jsを読み込むためのスクリプトタグを追加します。

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

次に、htmlファイル内に`<table>`要素を定義します。テーブルの見出し行には`<th>`要素、データ行には`<td>`要素を使用します。

```html
<table>
  <tr>
    <th>名前</th>
    <th>年齢</th>
  </tr>
  <tr>
    <td>山田太郎</td>
    <td>25</td>
  </tr>
  <tr>
    <td>佐藤花子</td>
    <td>30</td>
  </tr>
</table>
```

次に、vue.jsのコンポーネントを定義します。このコンポーネントでは、テーブルのデータを扱い、表示するためのロジックを記述します。

```javascript
vue.component('my-table', {
  data: function () {
    return {
      users: [
        { name: '山田太郎', age: 25 },
        { name: '佐藤花子', age: 30 }
      ]
    }
  },
  template: `
    <table>
      <tr>
        <th>名前</th>
        <th>年齢</th>
      </tr>
      <tr v-for="user in users">
        <td>{{ user.name }}</td>
        <td>{{ user.age }}</td>
      </tr>
    </table>
  `
})
```

最後に、vue.jsのインスタンスを生成し、先ほど定義したコンポーネントをマウントします。

```javascript
new vue({
  el: '#app'
})
```

これで、vue.jsで基本的なテーブルコンポーネントが完成しました。テーブルに表示するデータは、定義したコンポーネントのdataオプション内に記述されており、v-forディレクティブを使用してループ処理を行い、データを表示しています。

## テーブルデータの初期化と表示方法の設定

vue.jsでは、テーブルデータを初期化するためのオプションや、データの表示方法を設定するためのディレクティブが提供されています。

テーブルデータの初期化は、vue.jsのdataオプションを使用します。dataオプション内には、テーブルに表示するデータをオブジェクトとして記述します。

```javascript
data: function() {
  return {
    users: [
      { name: '山田太郎', age: 25 },
      { name: '佐藤花子', age: 30 }
    ]
  }
}
```

上記の例では、`users`という配列にテーブルデータを格納しています。このデータは、テーブルの表示に使用されます。

表示方法の設定は、ディレクティブを使用します。ディレクティブは、html要素に対して特定の動作を行うための指示です。

vue.jsでテーブルデータを表示するためには、v-forディレクティブを使用します。このディレクティブは、配列やオブジェクトに対して繰り返し処理を行うためのものです。

```html
<tr v-for="user in users">
  <td>{{ user.name }}</td>
  <td>{{ user.age }}</td>
</tr>
```

上記の例では、`users`配列の要素数だけテーブルの行を繰り返し生成しています。v-forディレクティブの`user in users`の部分では、`users`配列の要素を`user`という変数に代入しています。そのため、`user.name`や`user.age`のようにして各要素のプロパティにアクセスすることができます。

## ボタンクリックイベントのリスナー登録と行追加処理の実装

テーブルに行を追加するためには、ボタンクリックイベントのリスナーを登録し、行追加処理を実装する必要があります。

まず、ボタンをhtmlに追加します。

```html
<button v-on:click="addrow">行追加</button>
```

上記の例では、`v-on:click`ディレクティブを使用して、ボタンがクリックされた際に`addrow`というメソッドを呼び出すようにしています。

次に、vue.jsのmethodsオプションに`addrow`メソッドを追加します。

```javascript
methods: {
  addrow: function() {
    this.users.push({ name: '', age: 0 });
  }
}
```

addrowメソッドでは、`users`配列に新しい要素を追加しています。この新しい要素は、名前と年齢のプロパティを持ち、初期値は空文字列と数値0です。

ボタンをクリックすると、addrowメソッドが実行され、新しい行がテーブルに追加されます。

## データのバインディングと新しい行の表示方法

vue.jsでは、データとui要素をバインディングすることができます。これにより、データの変更がuiに反映されるようになります。

テーブルの新しい行にデータを入力するために、テキストフィールドを追加し、データとバインドします。

```html
<tr v-for="user in users">
  <td><input type="text" v-model="user.name"></td>
  <td><input type="text" v-model="user.age"></td>
</tr>
```

上記の例では、`v-model`ディレクティブを使用して、テキストフィールドの入力値を`user.name`と`user.age`にバインドしています。つまり、テキストフィールドの値が変更されると、`users`配列の対応する要素のプロパティに反映されます。

また、vue.jsでは、データの値が変更されると、自動的にuiが更新されます。そのため、テキストフィールドに入力された値が即座にテーブルに反映されるようになります。

## シンプルなテーブル行追加の手順のまとめと応用例

以上で、vue.jsを使用してシンプルなテーブルに行を追加する手順が完了しました。

まずはじめに、htmlファイルにvue.jsを読み込むためのスクリプトタグを追加します。次に、htmlファイル内にテーブルの基本的な構造を作成します。

vue.jsのコンポーネントを定義し、テーブルデータを初期化します。データの表示方法やバインディングを設定し、新しい行を追加するボタンを実装します。

最後に、vue.jsのインスタンスを生成し、コンポーネントをマウントします。これで、シンプルなテーブルに行を追加する機能が実現されます。

この手順を応用することで、さまざまなテーブルコンポーネントを作成することができます。例えば、ユーザーがダイナミックに行を追加できるtodoリストやスケジュール管理システムなどが考えられます。

vue.jsの強力なデータバインディング機能やコンポーネントの再利用性により、テーブルの行追加などの機能を簡単に実装することができます。

## 参考記事

1. [vue.js documentation](https://vuejs.org/)
2. [vue.js guide](https://vuejs.org/v2/guide/)

以上で、vue.jsを使用してテーブルに行を追加する手順を解説しました。初心者の方でもわかりやすいように、基本的な手順から事例まで詳しく説明しています。vue.jsを使用したテーブルコンポーネントの作成に挑戦してみてください。

　

## 【Vue.js】関連のまとめ
https://hack-note.com/summary/vuejs-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

