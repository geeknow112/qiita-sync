<!--
title:   【javascript】フィードフィルタリングとソート：rssデータを操作する方法
tags:    JavaScript,RSS
id:      dbd7d1a46f48367e276f
private: false
-->


## フィードデータのフィルタリングと絞り込み方法

rssフィードデータを操作する際に、特定の条件にマッチするデータのみ表示したい場合があります。javascriptを使用して、フィードデータのフィルタリングと絞り込みを行う方法を解説します。

フィルタリングと絞り込みには、arrayオブジェクトの`filter()`メソッドを活用します。このメソッドは、指定した条件にマッチする要素だけを抽出して新たな配列を作成します。

以下のサンプルコードでは、`filter()`メソッドを使って、`title`プロパティが指定したキーワードに含まれている記事だけを抽出する例を示します。

```javascript
const keyword = "javascript";
const filtereddata = feeddata.filter((item) => {
  return item.title.includes(keyword);
});
console.log(filtereddata);
```

このコードは、`feeddata`という配列に格納されたフィードデータから、`title`プロパティがキーワードに含まれている記事だけを抽出しています。抽出されたデータは、`filtereddata`という新たな配列に格納されます。

## ソート機能の実装とデータの並び替え手法

rssフィードデータを表示する際に、特定の基準でデータを並び替えたい場合があります。javascriptを使用して、ソート機能を実装し、データを並び替える手法を解説します。

並び替えには、arrayオブジェクトの`sort()`メソッドを活用します。このメソッドは、指定した基準に従って要素を並び替えます。

以下のサンプルコードでは、`sort()`メソッドを使って、`publishedat`プロパティを基準に降順で並び替える例を示します。

```javascript
feeddata.sort((a, b) => {
  const datea = new date(a.publishedat);
  const dateb = new date(b.publishedat);
  return dateb - datea;
});
console.log(filtereddata);
```

このコードは、`feeddata`という配列に格納されたフィードデータを、`publishedat`プロパティを基準に降順で並び替えています。並び替え結果は、`feeddata`自体が変更されます。

## キーワード検索と正規表現を使ったフィードの絞り込み

特定のキーワードにマッチする記事だけを抽出するだけでなく、正規表現を使ってより柔軟にフィードを絞り込むこともできます。javascriptを使用して、キーワード検索と正規表現を組み合わせたフィードの絞り込み方法を解説します。

正規表現を使ってフィードの絞り込みを行うには、`test()`メソッドを活用します。このメソッドは、指定した正規表現パターンにマッチするかどうかを判定します。

以下のサンプルコードでは、`test()`メソッドを使って、`title`または`description`プロパティに指定したキーワードにマッチする記事だけを抽出する例を示します。

```javascript
const keyword = "javascript";
const regex = new regexp(keyword, "i");
const filtereddata = feeddata.filter((item) => {
  return regex.test(item.title) || regex.test(item.description);
});
console.log(filtereddata);
```

このコードは、`feeddata`という配列に格納されたフィードデータから、`title`または`description`プロパティに指定したキーワードにマッチする記事だけを抽出しています。

## カテゴリー別フィルタリングとタグの活用方法

一つのフィードには、複数のカテゴリーやタグが付与されている場合があります。そのため、特定のカテゴリーに属する記事だけを表示したい、あるいは特定のタグを活用してフィードを絞り込みたい場合があります。javascriptを使用して、カテゴリー別フィルタリングやタグの活用方法を解説します。

以下のサンプルコードでは、`filter()`メソッドを使って、`categories`プロパティが指定したカテゴリーに一致する記事だけを抽出する例を示します。

```javascript
const category = "javascript";
const filtereddata = feeddata.filter((item) => {
  return item.categories.includes(category);
});
console.log(filtereddata);
```

このコードは、`feeddata`という配列に格納されたフィードデータから、`categories`プロパティが指定したカテゴリーに一致する記事だけを抽出しています。

## ユーザー設定の保存とフィルタリングオプションのカスタマイズ

ユーザーが特定のフィルタリング条件やソート順を設定した場合、その設定を保存し、次回ウェブページを開いた際にも適用させることができれば便利です。javascriptを使用して、ユーザー設定の保存とフィルタリングオプションのカスタマイズ方法を解説します。

ユーザーの設定は通常、ブラウザのローカルストレージやクッキーに保存されます。下記のコードでは、ブラウザのローカルストレージを使用してユーザーの設定を保存し、次回ページを表示した時に反映させる例を示します。

```javascript
const filteroptions = {
  keyword: "javascript",
  category: "programming",
  sortoption: "date"
};

// ユーザー設定の保存
localstorage.setitem("filteroptions", json.stringify(filteroptions));

// ユーザー設定の取得
const savedfilteroptions = json.parse(localstorage.getitem("filteroptions"));
console.log(savedfilteroptions);
```

このコードは、`filteroptions`というオブジェクトにユーザーの設定を保存し、`localstorage`オブジェクトを使ってブラウザのローカルストレージに保存します。次回ページを表示する時には、保存された設定を取得し、反映させることができます。

以上の方法を活用することで、javascriptについて初心者エンジニアでもフィードデータのフィルタリングやソート、キーワード検索、カテゴリー別フィルタリング、ユーザー設定の保存といった操作をスムーズに行うことができるようになります。

参考文献:
- [mdn web docs: array.filter()](https://developer.mozilla.org/en-us/docs/web/javascript/reference/global_objects/array/filter)
- [mdn web docs: array.sort()](https://developer.mozilla.org/en-us/docs/web/javascript/reference/global_objects/array/sort)
- [mdn web docs: regexp.test()](https://developer.mozilla.org/en-us/docs/web/javascript/reference/global_objects/regexp/test)
- [mdn web docs: array.includes()](https://developer.mozilla.org/en-us/docs/web/javascript/reference/global_objects/array/includes)
- [mdn web docs: localstorage](https://developer.mozilla.org/en-us/docs/web/api/window/localstorage)



## 【Javascript】関連のまとめ
https://hack-note.com/summary/javascript-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
