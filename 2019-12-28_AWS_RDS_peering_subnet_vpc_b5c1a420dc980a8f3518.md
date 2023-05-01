<!--
title:   AWSのアカウントが分かれたVPC間をPeeringしてRDSからデータを抽出した件
tags:    AWS,RDS,peering,subnet,vpc
id:      b5c1a420dc980a8f3518
private: false
-->
## 概要
ある一方のアカウント内で作成しているVPC内のRDSのデータを、
別アカウント内のEC2から参照してデータを抽出する必要があり、
できるかやってみた。

なぜ必要だったかというと、
同じデータを使いたいが、別サービスだったため、
AWS利用料の請求を分けたかったから。
あと、参照するだけのサービスのため、
RDSのコピーとか面倒なことはしたくなかったから。

## 利用技術
- AWS VPC
- AWS Subnet
- AWS Peering
- AWS RDS
- AWS EC2

[参考: https://test.com](https://test.com)

```php:filename.php
code
```