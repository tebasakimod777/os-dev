# static

大量の配列を少ないコード数で宣言しようと思ったら，普通に`char foor[]`よりも`static char foo[]`の方がより少ないコード（アセンブラ的に）で宣言できる．

# パレットの設定をする前にすること

パレットの設定をしている最中に割り込みがくると困るのでこれが来ないようにする．(`io_cli()`)

また，割り込みを再開させるには`io_store_eflags(eflags)`をする．

# ポップとプッシュとスタック

スタックを間に挟むことでデータの受け渡しをすることができる．

## ポップ

スタックからデータを取り出すこと

## プッシュ

スタックにデータを入れること

# 画面の番地の指定

画面の1番左上を`0xa0000`とし，1番右下を`0xaffff`とする．
左からx，上からyの画素の番地は以下の式で導き出せる．

> 0xa0000 + x + y * 320

