<!--
title:   matomoマニュアル
tags:    Matomo
id:      33ef6875c7780c9993b4
private: false
-->
Matomoマニュアル

#accesslogのimport方法

#accesslogの保存先(DBスキーマ)
dbname.mtm_log_visit

#問題
一つのサイトのログを複数人で閲覧するための権限管理があるが、
複数サイトのログに対して閲覧権限を割り当てる管理ができないように見える。

#現段階の解決方法
* プラグインを開発する
* ドメインをユーザー単位にする。

#プラグイン開発する場合
ログインするユーザーによってDBが切替るようにする。

#ドメインをユーザー単位にする方法
1. AWSでサブドメインを増やす。
report-01.domain.com
report-02.domain.com
report-03.domain.com ...

2. EC2上でバーチャルホスト設定をする。
3. RDS上に別DBをユーザー単位で作成する。
4. 各サイトにそれぞれのユーザーのサイトのログをインポートする。
