<!--
title: 【基礎】Wordpressの記事データだけ、dumpファイルで移行するには
tags: wordpress,mysql,dump
id: 
private: false
-->

こんにちは。今回は、Wordpressについて初心者エンジニアに向けて、Wordpressの記事データだけをdumpファイルで移行する方法について解説していきます。

## WordpressのDBテーブル定義

WordpressのDBには、以下のようなテーブルが存在します。

| テーブル名 | 内容 |
| --- | --- |
| wp_posts | 記事の本文やタイトル、投稿者などの情報を格納する。 |
| wp_postmeta | 記事のメタ情報（例：タグ、カテゴリー、投稿日時など）を格納する。 |
| wp_terms | 記事のタグやカテゴリーの情報を格納する。 |
| wp_term_relationships | 記事とタグ、カテゴリーの関係性を格納する。 |
| wp_term_taxonomy | タグやカテゴリーの分類情報を格納する。 |

それぞれのテーブルの役割は、以下の通りです。

- wp_posts: 記事の本文やタイトル、投稿者などの情報を格納する。
- wp_postmeta: 記事のメタ情報（例：タグ、カテゴリー、投稿日時など）を格納する。
- wp_terms: 記事のタグやカテゴリーの情報を格納する。
- wp_term_relationships: 記事とタグ、カテゴリーの関係性を格納する。
- wp_term_taxonomy: タグやカテゴリーの分類情報を格納する。

## Wordpressの記事データの格納先

Wordpressの記事データは、テーブルwp_postsに格納されています。各記事には、以下のような情報が格納されています。

| カラム名 | 内容 |
| --- | --- |
| ID | 記事のID |
| post_author | 記事の投稿者 |
| post_date | 記事の投稿日時 |
| post_content | 記事の本文 |
| post_title | 記事のタイトル |
| post_excerpt | 記事の抜粋 |
| post_status | 記事のステータス（公開、下書き、削除など） |
| comment_status | コメントのステータス（許可、禁止など） |
| ping_status | トラックバックのステータス（許可、禁止など） |
| post_password | 記事のパスワード（設定されている場合） |
| post_name | 記事のURLスラッグ |
| to_ping | トラックバックの送信先URL |
| pinged | トラックバックが送信されたURL |
| post_modified | 記事の更新日時 |
| post_content_filtered | フィルタされた記事本文 |

## Wordpressの記事データだけdumpで移行するには

Wordpressの記事データだけをdumpファイルで移行するには、以下の手順を実行します。

1. MySQLのデータベースにログインする。

```
mysql -u ユーザ名 -p パスワード データベース名
```

2. データベース内のwp_postsテーブルをdumpする。

```
mysqldump -u ユーザ名 -p パスワード データベース名 wp_posts > wp_posts.sql
```

上記のコマンドを実行することで、wp_postsテーブルのデータがdumpファイルに出力されます。

3. 出力されたdumpファイルを移行先の環境にコピーする。

4. 移行先のMySQLのデータベースにログインする。

```
mysql -u ユーザ名 -p パスワード データベース名
```

5. wp_postsテーブルを削除する。

```
DROP TABLE wp_posts;
```

6. dumpファイルをインポートする。

```
source wp_posts.sql
```

上記の手順を実行することで、移行元のWordpressの記事データだけをdumpファイルで移行することができます。

## 注意点

- wp_postsテーブルには、記事の本文以外にも、画像などのメディアファイルのパスなどが格納されているため、移行先の環境にメディアファイルをコピーする必要があります。
- また、移行元と移行先の環境のWordpressのバージョンが異なる場合、データベースのテーブル定義が異なる可能性があるため、移行先の環境でエラーが発生することがあります。


## Wordpressを学ぶには下記もおススメ
- [TechAcademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3A%2F%2Ftechacademy.jp%2Fhtmlcss-trial%3Futm_source%3Dmoshimo%26utm_medium%3Daffiliate%26utm_campaign%3Dtextad)
- [オンラインスクール DMM WEBCAMP PRO](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=ON)


参考記事：
- [WordPressデータベースのテーブル一覧とその役割 - スマートウェブ制作事例集](https://smart-web.co.jp/blog/wordpress-database/)
- [WordPressのデータベースをmysqldumpで出力して別環境に移行する方法 - Qiita](https://qiita.com/kyosuke5_20/items/2a2cf2d8b2e6b55f8d1e)
