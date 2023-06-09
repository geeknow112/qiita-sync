<!--
title:   【bootstrap】グリッドシステムを使いこなす：初心者向けガイド
tags:    Bootstrap,Webデザイン
id:      817ac6166e829a223af4
private: false
-->


## bootstrapのグリッドシステムとは？初心者向けの解説

### bootstrapとは
こんにちは。今回は、bootstrapについて初心者エンジニアに向けて、グリッドシステムの使い方やカスタマイズ方法、レイアウトの作り方などを詳しく解説していきます。

まず、bootstrapとは、オープンソースのフレームワークで、html、css、javascriptのコードを再利用して、効率的にウェブサイトやウェブアプリケーションを構築することができます。bootstrapは、twitter社の開発者たちによって作成され、その軽量さ、使いやすさ、カスタマイズ性の高さから、多くのウェブデザイナーやエンジニアに支持されています。

bootstrapの特徴の一つに、グリッドシステムがあります。グリッドシステムは、ウェブデザインで頻繁に使用されるレイアウトの基本となるもので、ページを均等に分割し、コンポーネントを配置するための規則となります。このグリッドシステムを使うことで、ウェブページのレスポンシブデザインを簡単に実現することができます。

### bootstrapのグリッドシステムとは？
bootstrapのグリッドシステムは、12列のレイアウトをベースにしています。これにより、ウェブページを12等分して配置することができます。各列の幅は、コンテンツを一つの列に均等に配置するための単位となります。

bootstrapのグリッドシステムは、行（row）と列（column）の組み合わせで構成されます。行は、ページの水平方向の領域を定義し、列はその中に配置されるコンテンツを表します。各列は、指定した列数に応じて自動的に均等に配置され、レスポンシブデザインを実現することができます。

### 基本的な使い方と注意点
bootstrapのグリッドシステムを使うためには、以下のような基本的な使い方と注意点があります。

#### グリッドシステムの基本的な構造
bootstrapのグリッドシステムは、htmlの`<div>`要素を使用して構成されます。以下は、グリッドシステムの基本的な構造の例です。

```html
<div class="container">
  <div class="row">
    <div class="col-md-6">内容a</div>
    <div class="col-md-6">内容b</div>
  </div>
</div>
```

まず、`container`クラスで囲まれた領域が行（row）を表し、その中に`row`クラスで囲まれた領域が列（column）を表します。その中に配置される実際のコンテンツには、`col-*-*`のクラスが指定されます。`col-md-6`の場合、列のサイズを表し、`col-md-*`の場合は、画面の幅が中サイズ以上の場合に有効になります。

#### オフセットとネスト
bootstrapのグリッドシステムでは、オフセットとネストという機能も利用することができます。オフセットは、列を水平方向にずらすことができる機能で、ネストは、列の中にさらに列を配置することができる機能です。

```html
<div class="container">
  <div class="row">
    <div class="col-md-4">内容a</div>
    <div class="col-md-4 offset-md-4">内容b</div>
  </div>
  <div class="row">
    <div class="col-md-6">
      <div class="row">
        <div class="col-md-6">ネスト内容a</div>
        <div class="col-md-6">ネスト内容b</div>
      </div>
    </div>
    <div class="col-md-6">内容c</div>
  </div>
</div>
```

#### レスポンシブブレイクポイント
bootstrapのグリッドシステムでは、レスポンシブブレイクポイントという概念も重要です。これは、デバイスの幅に応じて、表示する列の数や配置方法を変更するためのものです。以下に、bootstrapのデフォルトのレスポンシブブレイクポイントを示します。

- extra small (<576px)
- small (≥576px)
- medium (≥768px)
- large (≥992px)
- extra large (≥1200px)

### グリッドシステムのカスタマイズ方法とは？
bootstrapのグリッドシステムは、デフォルトで12列のレイアウトが用意されていますが、独自のレイアウトを作成する場合には、カスタマイズする必要があります。ここでは、グリッドシステムのカスタマイズ方法について解説します。

#### カスタム変数の設定
bootstrapのグリッドシステムをカスタマイズするためには、まずカスタム変数を設定する必要があります。カスタム変数は、`_variables.scss`というファイルに定義されており、ここで変数を上書きすることで、カスタマイズを行うことができます。

#### グリッドクラスのカスタマイズ
次に、グリッドクラスをカスタマイズします。グリッドクラスは、`grid.scss`というファイルに定義されており、ここで列の幅やオフセット、ネストなどを定義することができます。

#### グリッドレイアウトのスタイルの変更
最後に、グリッドレイアウトのスタイルを変更する方法も紹介します。これにより、背景色やボーダーなどのスタイルを自由に変更することができます。

### グリッドシステムを使ったレイアウトの作り方と例
bootstrapのグリッドシステムを使ったレイアウトの作り方を紹介します。以下は、グリッドシステムを使った2列のレイアウトの例です。

```html
<div class="container">
  <div class="row">
    <div class="col-md-6">コンテンツa</div>
    <div class="col-md-6">コンテンツb</div>
  </div>
</div>
```

上記のコードでは、`col-md-6`というクラスが指定されており、列の幅を半分にしています。これにより、コンテンツaとコンテンツbを均等に配置することができます。

### グリッドシステムを使ったレスポンシブデザインの実現方法
bootstrapのグリッドシステムを使うことで、レスポンシブデザインを簡単に実現することができます。具体的な実現方法を以下に解説します。

#### デフォルトのレイアウト
bootstrapのデフォルトのレイアウトは、画面の幅が大きい場合には4列を表示し、中サイズの場合は2列を表示します。これにより、異なるデバイスの画面サイズに応じたレイアウトを自動的に適用することができます。

#### カスタムブレイクポイントの設定
カスタムブレイクポイントを設定することで、デバイスの幅に応じたレイアウトの切り替えが可能です。

#### 列の表示／非表示を制御する
また、`d-*-*`のクラスを使うことで、特定のデバイスサイズでのみ列を表示または非表示にすることができます。

### グリッドシステムでの要素の配置方法と、美しいデザインの実現法
最後に、グリッドシステムを使った要素の配置方法と、美しいデザインの実現法について解説します。以下に、要素の配置の例と美しいデザインの実現法を示します。

#### 要素の配置方法
- 水平方向の配置：`justify-content-*`クラスを使用して、要素を水平方向に配置することができます。
- 垂直方向の配置：`align-items-*`クラスを使用して、要素を垂直方向に配置することができます。

#### 美しいデザインの実現法
- コンテンツの枠線のスタイル：`border-*`クラスを使用して、コンテンツの枠線のスタイルを変更することができます。
- コンテンツの背景色：`bg-*`クラスを使用して、コンテンツの背景色を変更することができます。

以上が、bootstrapのグリッドシステムを使いこなすための初心者向けガイドの内容でした。bootstrapのグリッドシステムは、ウェブデザインを効率的かつ美しく作成するための重要なツールであるため、ぜひマスターして活用してみてください。

参考記事：
- [bootstrap grid system - an ultimate guide for a web designer and developer](https://www.codexworld.com/bootstrap-grid-system-web-designer-developer-guide/)
- [a complete breakdown of the bootstrap grid system](https://www.freecodecamp.org/news/complete-breakdown-of-the-twitter-bootstrap-4-grid-system-5a29dd54840c/)



## Bootstrap 関連のまとめ
https://hack-note.com/summary/bootstrap-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
