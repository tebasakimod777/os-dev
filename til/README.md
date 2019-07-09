# アセンブラの前に
本当はここで2進数でOS（ぽいもの）を作ることになるが，面倒なので省略した．

# 2進数，アセンブラでのプログラムでしたこと
直接，CPUに命令を書き込んでいる．    
結局，2進数とアセンブラではやっていることに変わりはない．   
## 2進数とアセンブラの違い
2進数での最初から4つめのコード
~~~
EB 4E 90 48
~~~
アセンブラでの最初から4つ目のコード
~~~
DB  0xeb, 0x4e, 0x90, 0x48
~~~

# アセンブラの2つの命令

## DB命令

`byte data`の略．
ファイルの内容を1バイト書き込む命令．  
"アセンブラの世界における最終兵器" by OS自作本  

## RESB命令

`reserve byte`の略．
指定バイト分の空きを作成できる命令．
今回の場合，大量の`0x00`をこれで代用することができる．