<!--
title:   Windows7サポート終了に伴いOSバックアップとWindows10へのアップグレードを試みた件
tags:    Windows10,windows7
id:      f4d52d01cdcfe21c4cde
private: false
-->
#Windows7からWindows10へのアップグレードに必要な作業
事前に以下の手順で動作検証と復元まで実施して、元に戻せない状況を回避する。

1. [Windows7をHDDにbackup](#windows7をhddにbackup)
2. [Window7リカバリメディアを用意する](#window7リカバリメディアを用意する)
3. [Windows10にupgrade](#windows10にupgrade)
4. [Windows10上でアプリの動作検証](#windows10上でアプリの動作検証)
5. [backupからWindows7へ復元](#backupからwindows7へ復元)
6. [関連事項](#関連事項)
 1. [SSDクローン](#関連事項)

#windows7をhddにbackup
https://www.techdevicetv.com/ch_windows10/09/
https://arutora.com/archives/20190420112038/

##window7リカバリメディアを用意する
一度Windows10にして期限を過ぎてしまうと、Windows7で用意したリカバリメディアが使えなかった。
どうやらOSがWindows7じゃないとリカバリメディアは意味がないようです。
なので、Windows10にして戻せなくなったら仕方ないので、Windows10のリカバリメディアを用意する。

##Windows10の回復ドライブ作成
https://solution.fielding.co.jp/column/it/itcol04/201905_05/
https://www.pasoble.jp/windows/10/kaifuku-drive.html

#windows10にupgrade
https://hackers-high.com/windows/upgrade-windows10-for-free/

#windows10上でアプリの動作検証

#backupからwindows7へ復元
復元できない。。。
下記参考
http://yakudate.com/windows10-1month-over/
http://yakudate.com/ends-without-charge/

事前にリカバリディスクを用意しておくべきだった。
https://www.pc-koubou.jp/kaitori/re/recovery-win7.html

#関連事項
- SSDクローン
https://pssection9.com/archives/19749854.html

- Windows10リカバリディスクの作成

- Windows10からWindows7へのダウングレード
https://pc-karuma.net/windows-10-downgrade-windows-7-8-1/
現状はWindows10にアップグレードしてから10日間のみ「Windows7に戻す」処理を利用可能のようです。
下記が表示される。
>「以前のバージョンに復元すことができません
以前のバージョンのWindowsに戻すために必要なファイルが、このPCから削除されています。」

- DELL製PC RecoveryDiscからのWindows7への戻し
https://www.dell.com/community/Windows-10/Windows10-%E5%88%9D%E6%9C%9F%E5%8C%96%E6%96%B9%E6%B3%95-DELL%E8%A3%BD%E3%83%A1%E3%83%87%E3%82%A3%E3%82%A2-DELL-OS-Recovery-Tool%E3%81%A7%E4%BD%9C%E6%88%90%E3%83%A1%E3%83%87%E3%82%A3%E3%82%A2/td-p/6126304

- DELL製PC DVDからのWindowns7への戻し
https://www.dell.com/community/Microsoft/Windows-7%E3%82%92%E5%88%9D%E6%9C%9F%E5%8C%96%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95/td-p/6186049

- HDDからのWindows7への戻し
https://www.pc-koubou.jp/kaitori/re/recovery-win7.html

- 通常のPCをシンクライアント化
