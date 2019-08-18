# マウスカーソルの作成

フォントを作成するときと同じ原理でマウスカーソル（見た目のみ）を作ることができる．
ただし，このマウスカーソルを動かすことはできない，そのためにPICの設定や割り込みの作成等をする必要がある．

# マウスカーソルを動かすには

マウスカーソルを動かすにはGDTとIDTの設定をしないといけない，いかにその説明を示す．

## GDT

`Global (Segment) Table`の略，これを説明するためにセグメンテーションの説明をする．

### セグメンテーション

メモリ（32Bitなので4GB？）を好きなように切り分けてその切り分けたものを0番地として扱うことができる機能．
この機能によって，プログラムはメモリの番地を逐一計算せずに`ORG 0`として作ればよくなる．  

この切り分けられた1つ1つのメモリはセグメントと呼ばれる．

セグメントは以下の情報を持つ

- セグメントの大きさ
- セグメントの開始番地
- セグメントの管理属性

CPUではこれらの情報を64ビットで表すが，セグメントレジスタは16ビットしかない．
ではどのようにセグメントレジスタを表すかというと，セグメントレジスタで直接セグメントを持つのではなく，セグメントの情報を別のところに保存しておき，その情報をセグメントレジスタで呼び出せるようにしておくのである．

CPUの仕様上セグメントレジスタの下位3ビットが使用できないので，13ビットで表すことになり，0~8191を表すことができる．
つまり，8191個のセグメントを定義できる．
このセグメントの設定を保存しておくレジスタがGDTRというレジスタである．

## IDT

割り込みに関する記述を保存してあるテーブルである．

### 割り込み

キーボードやマウスはCPUの速度（2GHz=）からすると人間のキーボードやマウスを動かすのは遅すぎる（せいぜい一秒間に50～60回程度），その他にネットワークやディスクドライブなどの動作を確認しないといけない．
そのため，CPUがいちいちそれらのデバイスの動作状況を確認するのはあまりにも非効率的すぎる．

そこで割り込みという仕組みを用いる．
外部の装置に変化があったとき，一旦CPUのすべて動作を中止し，あらかじめ決められた動作を行う．
例えば，マウスが変化したときマウスカーソルの再描画を行う関数を，キーボード変化したときには入力された文字をプログラムに送信する関数など．
外部機器とそれが変化したときに動作する関数の対応表をIDTと呼び，GDTと同じような動作をする．

また，このIDTを使用するためにはGDTの設定をきっちりしないといけない．

# ファイル分割（分割コンパイル）

ヘッダファイル（.h）とMakefileを使いこなせば行数が圧倒的に減って，コードが見やすくなるよ！