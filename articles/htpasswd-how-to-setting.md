<!--
title:   .htpasswdへのユーザー追加
tags:    htpasswd
id:      3fb233167a9514467876
private: false
-->
#.htpasswdへのユーザー追加

https://qiita.com/kimihito_/items/3fb0788f28e5b51bcaa9


## 1. 初回ユーザー登録
`
$ sudo htpasswd -c ./.htpasswd username
New password:
Re-type new password:
Adding password for user username
`
## 2. ユーザー追加
`
$ sudo htpasswd ./.htpasswd addUser
New password:
Re-type new password:
Adding password for user addUser
