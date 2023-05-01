<!--
title:   AWS S3に置いているMovableTypeで作ったサイトをhttps化した件
tags:    AWS,CloudFront,MovableType,S3,route53
id:      6f042d2cac7272776d6c
private: false
-->
## 概要
MobableTypeで作ったサイト(静的コンテンツのみで生成されたサイト)をAWS S3に置いて公開していたところ、
https化が求められたので対応した内容を残しておく。
EC2+ロードバランサー+AWS Certificate Managerでのhttps化は何度かやってたが、
cloudFront + Route53 + S3で静的コンテンツのみでhttps化できるとは知らなかった。
むしろこちらの方が用途が広そう。

## 利用技術
- AWS S3 (MTで作った静的コンテンツを配置)
- AWS CM (無料SSL証明書の取得)
- AWS CloudFront (CDNをRoute53でエンドポイントに設定するという使い方)
- AWS Route53

[参考: https://test.com ](https://test.com)

```php:filename.php
code
```