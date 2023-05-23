<!--
title:   pythonで株を分析し、有利な売買局面を探す
tags:    Python,Quantx,VisualStudio,matplotlib,株
id:      7c984dc1b06474fc642a
private: false
-->
#要望
- [ ] python matplotlib 株価の前年比をグラフ表示したい。
- [ ] python matplotlib ローソク足非表示機能を作って移動平均線を強調し、トレンドの可視化を強めたい。
- [ ] visual studioでzip化、
- [ ] python matplotlib グラフを再描画
- [ ] 毎日PPPを探索、QuantXでゾーンを自動表示
- [ ] python matplotlib上で建玉操作練習できるようにする
- [ ] pythonでQuantX的バックテスト、まず下半身シグナルを捉える、高値警戒圏を捉える、ボラティリティ計算、日柄値幅計算
- [ ] pythonでログみたいに建玉操作したタイミングの自分の投資戦略を表示、記録する
- [ ] 10分足のデータを集めて、日中株価変動を見る。変動タイミングがわかる。寄りでつけた株価が引けでどう変動してるか。AM9:30までに形成した安値高値圏をAM:11:30で脱している率。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/68348/98aa6a5b-d3f7-25aa-88ac-159b3c3bdce8.png)

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/68348/4de6a837-acda-5dec-0bf3-4ff8d4ec162d.png)

- 読みが外れて大きく損失を出のは、銘柄選択時の局面の読み間違いにある。上昇トレンドなのにLowポジションを建ててしまったりとか。これを無くしたい。そのためには、チャートでトレンドを確認するべきだが、これをシステマチックにやるには。。

## データサイエンティストスクール 無料部分あります
PythonやRなどのプログラミングを学ぶなら、
さらに統計分野を学習してデータサイエンティストを目指すのがおすすめ！

ディープラーニングやビックデータ分析などの高額システム案件の受注にも有利になります。

システム開発より、分析がやりたい方向けですが、下記載せておきます。

https://hack-note.com/programming-schools/#toc17
 
