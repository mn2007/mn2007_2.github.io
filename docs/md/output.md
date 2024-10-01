---
layout: default
title: output
permalink: /output
---

# AkaiKKR Outputファイルの解説

ここでは、計算モードを"go"と指定したときのOutputについて解説する。

## Outputファイルの構成
### Part1 計算パラメータ及び読み込まれたデータ

画面上あるいは保存先のファイルにOutputが表示される。
```start
  6-Nov-2022
    22:59:50
    meshr   mse    ng   mxl
      400    35    21     3
```
まず、日付と時刻が表示される。これは計算開始時刻である。
続くそれぞれの意味は、次のようになる。
* meshr : 動径方向の座標のメッシュ数
* mse : 複素積分のエネルギーメッシュ数
* ng : チェビシェフ展開の次数
* mxl : 考慮される最大の散乱角運動量で、単位は$\hbar$

続けて、Inputとして与えたデータが表示される。このデータやキーワードの意味はInputファイルの解説で詳細に記述しているので、参照されたい。
[Inputファイルの解説ページ](../input/input.md)

```start
   data read in
   go=go   file=data/fe                                                         
   brvtyp=bcc     a=  5.27000  c/a= 0.00000  b/a= 0.00000
   alpha=  0.0  beta=  0.0  gamma=  0.0
   edelt= 1.0E-03  ewidth=  1.000  reltyp=nrl    sdftyp=mjw      
   magtyp=mag     record=2nd   outtyp=update  bzqlty=4       
   maxitr= 50  pmix= 0.02300  mixtyp=tchb-brydn
   ntyp=  1  natm=  1  ncmpx=  1
```

### part2 複素エネルギー経路
その後、複素エネルギー経路がn(ewidth,edelt)の組で表示される。[Inputファイルの解説ページ](../input/input.md)で述べたように、この2つの値が適切かどうかが計算の成功に密接に関わる。

積分範囲が妥当かどうかチェックするには、ewidthの値とコア状態のエネルギー(のちに出力されるcore level  (spin up  )core level  (spin down)の値)を比べてみるのがよい。具体的には、出力されているフェルミエネルギーの値と浅いコア状態のエネルギーの差を計算してそれがewidthの値より十分（0.1Ry以上）大きいか、または十分小さいか（0.1Ry以上）を確認をする。これが危なそう、あるいは収束がおかしいとなった場合はDOSをプロットして確かめる。

```start
   complex energy mesh
   1( -1.0000, 0.0000)   2( -0.9998, 0.0027)   3( -0.9990, 0.0062) 
   4( -0.9971, 0.0107)   5( -0.9933, 0.0163)   6( -0.9862, 0.0234) 
   7( -0.9738, 0.0319)   8( -0.9535, 0.0421)   9( -0.9220, 0.0536) 
  10( -0.8757, 0.0660)  11( -0.8117, 0.0782)  12( -0.7292, 0.0889) 
  13( -0.6307, 0.0965)  14( -0.5224, 0.0999)  15( -0.4130, 0.0985) 
  16( -0.3115, 0.0926)  17( -0.2245, 0.0835)  18( -0.1553, 0.0724) 
  19( -0.1037, 0.0610)  20( -0.0671, 0.0500)  21( -0.0424, 0.0403) 
  22( -0.0262, 0.0320)  23( -0.0160, 0.0251)  24( -0.0096, 0.0195) 
  25( -0.0057, 0.0151)  26( -0.0034, 0.0116)  27( -0.0020, 0.0089) 
  28( -0.0012, 0.0069)  29( -0.0007, 0.0052)  30( -0.0004, 0.0040) 
  31( -0.0002, 0.0031)  32( -0.0001, 0.0023)  33( -0.0001, 0.0018) 
  34( -0.0000, 0.0014)  35( -0.0000, 0.0010) 
```

### Part3 ポテンシャルデータを保存するファイルと格子の情報

今回の計算では、指定されたファイルがなかったので、新しいファイルが作成された。

```start
   file to be accessed=data/fe                  
   created
```

次の段落では結晶の情報がまとめられている。

```start
   lattice constant
   bravais=bcc   a=  5.27000   c/a= 1.0000   b/a= 1.0000
   alpha=  90.00   beta=  90.00   gamma=  90.00
```
ユニットセルの体積と、マフィン・ティン球(MT球)によって埋められるその体積(volume filling)が68%であることを示している。

```start
   unit cell volume=    73.18159(a.u.)
   volume filling=  68.0%
```

基本並進ベクトルを示す。単位はa。

```start
   primitive translation vectors (in units of a)
   a=( -0.50000  0.50000  0.50000)
   b=(  0.50000 -0.50000  0.50000)
   c=(  0.50000  0.50000 -0.50000)
```

ga、gb、gcは逆格子ベクトルを示す。単位は2π/aとなる。

```start
   reciprocal lattice vectors (in units of 2*pi/a)
   ga=(  0.00000  1.00000  1.00000)
   gb=(  1.00000  0.00000  1.00000)
   gc=(  1.00000  1.00000  0.00000)
```

### Part4 各サイトを占める原子の情報、格子の対称性、k点の数

まず、サイトの「タイプ」を作る。以下のタイプの位置は鉄によって100%占められている。詳しいことはInputの解説に記載されている。

[Inputファイルの解説ページ](../input/input.md)

```start
type of site
   type=Fe        rmt= 0.43301 field=  0.000   lmxtyp=  2
                  component= 1  anclr=  26.00  conc= 1.0000
```

続いて、そのタイプの位置情報、つまり原子の位置を示す。

```start
   atoms in the unit cell
   position=   0.00000000   0.00000000   0.00000000  type=Fe
```
チェビシェフ展開をする際のエネルギーウィンドウの情報が与えられる。
* ew : エネルギーウィンドウの中心
* ez : エネルギーウィンドウの幅

```start
 ***wrn in spmain...eof detected; data generated
 ***msg in spmain...new ew, ez generated
   ew=   0.19997  ez=   1.25000

   preta= 0.35542  eta= 0.35542
```

#### 対称操作について

与えられた原子の配置で許される対称操作**symop**について記述がある。許される操作に対しては1、なければ0と表示される。
* g : 直接 gerade
* u : 反転 ungerade
  
**nk**が既約ゾーン内でのk点数を示す。
```start
   symop   E  C4*3   C2*3  C4^3*3   C3*4    C3^2*4      C2'*6
     g     1  1 1 1  1 1 1  1 1 1  1 1 1 1  1 1 1 1  1 1 1 1 1 1
     u     1  1 1 1  1 1 1  1 1 1  1 1 1 1  1 1 1 1  1 1 1 1 1 1

   last=  243   np=  19   ngpt= 273   nrpt= 169   nk=     29   nd=    1
```

### part5 原子の計算

今回の計算はポテンシャルエネルギーの値があらかじめ与えられていなかったので、原子のLDA/GGA計算が行われる。反復計算の回数が記述される。以下の記述では15回で収束したことがわかる。

```start
 atomic potential generated

   itr=  1      rms error =  0.245
   itr=  2      rms error = -0.412

　　　　　　．．．（途中省略） ．．．

   itr= 15      rms error = -6.237
   interval= 15     cpu time=      0.00 sec
   nuclear charge=26.00
```
**energy**に求まった原子のエネルギー準位が書かれる。単位はRyになる。

```start
         nl      cnf         energy
    -----------------------------------
         1s     2.000       -508.5203
         2s     2.000        -59.2074
         2p     6.000        -51.1807
         3s     2.000         -6.8027
         3p     6.000         -4.4563
         3d     6.000         -0.6696
         4s     2.000         -0.4930
```

### part6 その他の情報

```start
   record 1 will be overlaied by input and
   record 2 will be replaced by new output.

   core configuration for Z= 26
   state  1s 2s 2p 3s 3p 3d 4s 4p 4d 5s 5p 4f 5d 6s 6p 5f 6d 7s
    up     1  1  3  1  3  0  0  0  0  0  0  0  0  0  0  0  0  0
   down  1  1  3  1  3  0  0  0  0  0  0  0  0  0  0  0  0  0
```
**record1**でレコードはインプットポテンシャルに置き換わる。2番目のレコードは計算で得られた新しいポテンシャルになる。
ポテンシャルファイルの構造は、バイナリデータからなる2個のレコードを含む。
* record1 ： 一つ前の計算で得られたデータ
* record2 ： 最新の計算で得られたデータ

Inputファイルにおけるrecordキーワードと対応しているので、Inputファイルの解説を以下に引用する。
> **record**はポテンシャルデータの利用に関するキーワードである。異常終了などで計算結果が失われてしまわないように、最新の計算結果と、その一つ前のバックアップの、二組のデータが常に保存されている。
> * init : 新規ポテンシャルデータ（与えられた原子配置からポテンシャルを計算して利用する）
> * 2nd : 最新のポテンシャルデータから計算を続ける
> * 1st : 一つ前のデータから計算を続ける

**core configuration**以下は、コア準位の占拠数である。

### part7 反復計算開始
```start
 ***** self-consistent iteration starts *****
       Fe
   itr=  1 neu=   -2.5047  moment=  4.0909  te=  -2523.19969054  err=  0.502
   itr=  2 neu=   -1.6328  moment=  2.5475  te=  -2522.86071488  err= -0.371
   itr=  3 neu=   -0.3261  moment=  2.6308  te=  -2522.80866273  err= -0.443
   itr=  4 neu=    0.0541  moment=  2.5226  te=  -2522.80177581  err= -0.367
   itr=  5 neu=    0.0943  moment=  2.5160  te=  -2522.80050661  err= -0.335
   itr=  6 neu=    0.0459  moment=  2.4553  te=  -2522.80806361  err= -0.454
   itr=  7 neu=   -0.1653  moment=  2.2229  te=  -2522.81662663  err= -0.640
   itr=  8 neu=   -0.3538  moment=  1.9560  te=  -2522.82374971  err= -1.132
```

* itr : 反復数
* neu : 系内の全電荷数。ゼロなら電気的中性が保たれている。
* moment : 系の磁気モーメント（$µ_B$）
* te : 全エネルギー(Ry)
* err : インプットとアウトプットポテンシャルの差のノルムの最大値。対数。マイナスに大きくなっていくとエラーは小さくなっていくことになる。

### part8 反復計算収束

```start
　 itr= 46 neu=   -0.0001  moment=  2.1598  te=  -2522.81762151  err= -5.193
   itr= 47 neu=   -0.0001  moment=  2.1598  te=  -2522.81762150  err= -5.557
   itr= 48 neu=   -0.0001  moment=  2.1598  te=  -2522.81762150  err= -6.104
   interval= 48     cpu time=      0.31 sec
   sdftyp=mjw     reltyp=nrl     dmpc= 0.10000
       Fe
   itr= 48  neu -0.0001  chr,spn   8.0000   2.1598  intc,ints  1.0307 -0.0270
   rms err= -6.140 -6.104
   ef=   0.7686596   0.7779665  def=     5.0213887    17.8605662
   band energy=    4.763028241   total energy=  -2522.817621496
   magnetization=   2.3210 T
```
今回は**interval**にもあるように48回の反復計算で収束した。設定したerrorよりerrの値が小さくなったとき、反復計算は正常に終了する。設定したmaxitrの回数反復してもerrが十分小さくならない場合は、計算が打ち切られる。

* intc, ints : 格子間隙に溜まった電子数とスピンモーメント
* ef : フェルミレベル(up、down)
* def : フェルミエネルギーでの状態密度
* total energy : 全エネルギー(Ry)

**ef**が2つの値を持つのは、これがスピンの向きによって異なるからである。マフィン・ティンの平らな部分を原点と取っているため、エネルギー原点がアップとダウンで差が出る。

### part9 各サイトのローカルな情報
```start
　                                      *** type-Fe     Fe (z= 26.0) ***
   core charge in the muffin-tin sphere =17.9774112
   valence charge in the cell (spin up  ) =     0.19393(s)   0.19656(p)   4.19816(d)
   valence charge in the cell (spin down) =     0.20117(s)   0.22849(p)   1.97357(d)
   total charge=  24.96929   valence charge (up/down)=   4.58865   2.40323
   spin moment=   2.18542  orbital moment=   0.00000
   orbital current (up/down)=   0.00000   0.00000
   core level  (spin up  )
      -507.0825055 Ry(1s)       -57.8242188 Ry(2s)       -49.7860958 Ry(2p) 
        -5.4714121 Ry(3s)        -3.1285211 Ry(3p) 
   core level  (spin down)
      -507.0728003 Ry(1s)       -57.7222519 Ry(2s)       -49.7063113 Ry(2p) 
        -5.2798012 Ry(3s)        -2.9425195 Ry(3p) 
```
**valence charge in the cell**はマフィン・ティン球内の価電子の角運動量成分を示す。

**total charge**がFeの総電子数26と一致していない。これは、格子間隙位置にも電子が溜まっているためである。

**valence charge**はマフィン・ティン球内の全価電子数を示す。

**spin moment**はマフィン・ティン球内のスピンモーメントを表す。

### part10 各サイトのローカルな情報　超微細構造
```start
hyperfine field of Fe
     -274.068 kG (core=  -219.153 kG  valence=   -54.915 kG  orbital=     0.000 kG )
   core contribution
      -18.434 kG(1s)     -491.698 kG(2s)      290.979 kG(3s)
   charge density at the nucleus
       11820.4209 (core=    11814.6730  valence=        5.7479 )
   core contribution
       10701.4235(1s)         972.7172(2s)         140.5324(3s)
```
**hyperfine field**は、原子核位置で電子によって作られる磁場を指す。NMR等の共鳴周波数やメスバウアースペクトルに対応する超微細磁場のこと。

**charge density at the nucleus**は、原子核位置での電子密度を表す。NMR等でのアイソマーシフトに対応している。

### part11 計算に関する情報
```start
  sbtime report
  routine           1         2         3         4
  count           864       864       864        96
  cpu(sec)       3.60      1.19      1.32      0.13
```
sbtime reportにおける**routine**は特定のルーチンに関する情報である。時間は実時間×スレッド数となっている。

```start
 OS: Linux
 Host: ru
 Machine: x86_64
 numcor: 36
 elapsed time         0.38 sec (  9 threads)
```
OSや用いられたマシンの情報が掲載されたのち、**elapsed time**に計算にかかった実時間と用いられたスレッド数が記載される。
