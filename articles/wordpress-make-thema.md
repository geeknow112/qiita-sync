<!--
title:   【初心者向け】wordpressテーマを爆速で作る方法
tags:    WordPress,thema,作り方
id:      a403a07b6bda4225c1e3
private: false
-->


---

こんにちは。今回は、wordpressについて初心者エンジニアに向けて、themaの作り方について解説します。

## はじめに

wordpressは、多くのウェブサイトやブログで利用されているcms(content management system)です。wordpressには、themaと呼ばれるテンプレートがあり、これを使うことで簡単に独自のウェブサイトを作ることができます。

themaを作成するときには、初期設定が必要です。下記の設定コードを記事の先頭に入れ、それぞれの値を設定します。


## wordpressテーマの作り方

themaを作成するには、下記の手順を順に進めます。

1. テーマファイルの作成
2. ディレクトリの作成
3. テンプレートファイルの作成
4. スタイルシートの作成

### 1.テーマファイルの作成

最初に、テーマファイルを作成します。テーマファイルは、`style.css`と呼ばれるファイル名である必要があります。

```css
/*
theme name: your theme name
author: your name
author uri: your site
version: 1.0
*/

```

`style.css`には、テーマの基本情報を設定します。themaの名称、作者、作者サイト、バージョンなどを指定します。

### 2.ディレクトリの作成

次に、テーマが使用するディレクトリを作成します。themaは、下記のディレクトリ名を使用します。

- wp-content/themes/yourtheme/
- wp-content/themes/yourtheme/css/
- wp-content/themes/yourtheme/js/
- wp-content/themes/yourtheme/images/

themaのファイルは、これらのディレクトリ内に配置されます。

### 3.テンプレートファイルの作成

テンプレートファイルは、themaの見た目を構成するファイルです。代表的なテンプレートファイルは、下記のとおりです。

- index.php
- header.php
- footer.php
- single.php
- page.php
- archive.php
- functions.php

これらのファイルをテーマフォルダに作成します。各ファイルには、下記のように基本的なコードを挿入します。

```php
<?php get_header(); ?>

<!-- themaの内容 -->

<?php get_footer(); ?>
```

`get_header()`と`get_footer()`は、wordpressが用意する関数で、themaのheader.phpとfooter.phpを読み込むために使用されます。

### 4.スタイルシートの作成

最後に、スタイルシートを作成します。スタイルシートは、themaのデザインを指定するために使用されます。

デフォルトのスタイルシートは、`style.css`の中に記述します。下記は、基本的なスタイルシートの例です。

```css
body {
    background-color: #fff;
    color: #333;
    font-family: sans-serif;
}

h1 {
    font-size: 36px;
}

a {
    color: #009;
    text-decoration: none;
}
```

スタイルシートをカスタマイズする場合は、`functions.php`に新しいスタイルシートを追加することもできます。例えば、下記のようなコードを追加することで、新しいスタイルシートを読み込めます。

```php
function my_theme_scripts() {
    wp_enqueue_style( 'my-theme-style', get_template_directory_uri() . '/css/my-theme-style.css' );
}

add_action( 'wp_enqueue_scripts', 'my_theme_scripts' );
```

このコードでは、`my-theme-style.css`という新しいスタイルシートを読み込んでいます。

## サンプルコード

### ヘッダー部分のカスタマイズ

```php
<?php get_header(); ?>

<header>
    <h1><?php echo get_bloginfo( 'name' ); ?></h1>
    <nav>
        <ul>
            <li><a href="#">home</a></li>
            <li><a href="#">about</a></li>
            <li><a href="#">blog</a></li>
            <li><a href="#">contact</a></li>
        </ul>
    </nav>
</header>

<?php get_footer(); ?>
```

### タイトル部分のカスタマイズ

```php
<?php get_header(); ?>

<main>
    <?php if ( have_posts() ) : ?>
        <h2><?php single_post_title(); ?></h2>

        <?php while ( have_posts() ) : the_post(); ?>
            <article>
                <h3><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h3>
                <p><?php the_content(); ?></p>
            </article>
        <?php endwhile; ?>

    <?php else : ?>
        <p>投稿がありません</p>
    <?php endif; ?>
</main>

<?php get_footer(); ?>
```

## まとめ

今回は、wordpress初心者エンジニア向けにthemaの作り方について解説しました。

themaを作成するためには、テーマファイルの作成、ディレクトリの作成、テンプレートファイルの作成、スタイルシートの作成が必要です。また、`functions.php`を使うことで、スタイルシートの読み込みや新しいショートコードの定義などを行うことができます。

themaの作成には、htmlやcss、phpの知識が必要ですが、wordpress初心者エンジニアにとっては、themaのカスタマイズが手軽にできるメリットがあります。

参考url:
- https://qiita.com/erikokido/items/11ace72cf51d3cec4d9d
- https://www.wpbeginner.com/wp-themes/
- https://www.noteschool.jp/wordpress/2961
- https://manablog.org/short-code/