<!--
title:   AWS関連
tags:    AWS,EC2,EIP,vpc
id:      271c632d571a4052bb91
private: false
-->
- [EIPとEC2はアカウントが異なっても利用できるのかどうか](#EIPとEC2はアカウントが異なっても利用できるのかどうか)
- [ALBを使って301リダイレクトができる。SSL証明書設定がAWSだけで完結する件](#ALBを使って301リダイレクトができる。SSL証明書設定がAWSだけで完結する件)
- [AWS図,クラウドサービス利用図](#AWS図,クラウドサービス利用図)
- [AWS_Direct_Connectの使用状況確認](#AWS_Direct_Connectの使用状況確認)
- [Amazon_Connect_SalesForce](#Amazon_Connect_SalesForce)
- [Radius_監視＋AWS_DLM](#Radius_監視＋AWS_DLM)
- [AWS_サポートチャットシステム_appsync](#AWS_サポートチャットシステム_appsync)
- [AWS_限定したVPCのみで有効なIAM]
- [AWS_AMIをローカルに移す方法(料金がかかるため)]

#EIPとEC2はアカウントが異なっても利用できるのかどうか
###EIPとEC2は分けれるのか？
EIPを管理するアカウントと、EC2が動作しているアカウントを分ける必要ができたので調べました。

###なぜ必要か
外部APIとの連携でEIPだけ別のアカウントで管理したい。

###具体的にできるかどうか

###結論
無理そう。。。
EIPの関連付けインスタンスに同じアカウント内のものしか出てこない。。。
Peeringしたらいいのか？

`end
`

#ALBを使って301リダイレクトができる。SSL証明書設定がAWSだけで完結する件
https://dev.classmethod.jp/cloud/aws/alb-redirects/

#AWS図,クラウドサービス利用図

#AWS_Direct_Connectの使用状況確認

#Amazon_Connect_SalesForce
#Radius_監視＋AWS_DLM
#AWS_サポートチャットシステム_appsync
