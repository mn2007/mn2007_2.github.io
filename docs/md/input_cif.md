---
layout: default
title: input_cif
permalink: /input_cif
---

# cifファイルから作成したインプットの確認方法

## 概要

cifファイルから作成したInputファイルの確認方法を示す。確認方法としてはAkaiKKRPythonUtilを用いる。これはAkaiKKRをPythonから利用するためのユーティリティを提供するライブラリであり、AkaiKKRの出力を解析したり、AkaiKKRの機能をPythonスクリプト内で直接使用するための機能をサポートしている。AkaiKKRPythonUtilはcifからInputファイルを生成することが可能であるため、ここではその手順を示す。

## サンプル

この記事で用いるサンプルは"[FeRh0.5Pt0.5.cif](https://github.com/AkaiKKRteam/AkaiKKRPythonUtil/blob/master/tests/structure/FeRh0.5Pt0.5.cif)"である。この物質は、プリミティブセル内にサイトが2箇所あり、1個所はFeの割合が100%、もう一か所はRhの割合が50%、Ptの割合が50%であるような合金である。

## AkaiKKRPythonUtil実行手順

まず、以下の内容が書かれたファイルを"run_akaikkr.py"という名前で保存する。
```
import pyakaikkr

akjob = pyakaikkr.AkaikkrJob("./")
structure = akjob.read_structure("FeRh0.5Pt0.5.cif")
print("## read structure")
print("structure dict: ", structure)
print("AkaiKKRJob default dict: ", akjob.default)
input_dic = akjob.default.copy()
input_dic.update(structure)
print("input dict: ", input_dic)

print("## make inputcard")
akjob.make_inputcard(input_dic, "inputcard")
```

次に、AkaiKKRPythonUtilをダウンロードする。
```
$ git clone https://github.com/AkaiKKRteam/AkaiKKRPythonUtil
```

先ほど作成したrun_akaikkr.pyではAkaiKKRPythonUtil内のpyakaikkrディレクトリ内のコードを使用するため、そのディレクトリへのリンクを作成する。
```
$ ln -s AkaiKKRPythonUtil/library/PyAkaiKKR/src/pyakaikkr .
```

また、今回サンプルとして使用するcifファイルをカレントディレクトリにコピーする。
```
$ cp AkaiKKRPythonUtil/tests/structure/FeRh0.5Pt0.5.cif .
```

さらに、run_akaikkr.pyを実行するために必要となるライブラリをインストールする。
```
$ pip install pymatgen
$ pip install seaborn
```

最後にrun_akaikkr.pyを実行する。
```
$ python run_akaikkr.py
```

実行が終了すると、以下の"inputcard"ファイルが出力される。
```
#--- go potentialfile
go pot.dat
#--- brvtyp a c/a b/a alpha beta gamma
st 5.204307821390574 1.2817719680464779 1.0 90.0 90.0 90.0
#--- edelt ewidth reltyp sdftyp magtyp record
0.001 1.0 sra mjw nmag 2nd
#--- outtyp bzqlty maxitr pmix
update 6 200 0.02
#--- ntyp
2
#--- type ncmp
  Fe_1a_0 1
#- rmt field mxl
0.0 0.0 2
#- anclr conc
26 100.0
#--- type ncmp
  Rh0.5Pt0.5_1d_1 2
#- rmt field mxl
0.0 0.0 2
#- anclr conc
45 50.0
78 50.0
#--- natm
2
#--- atmicx atmtyp
0.00000000a 0.00000000b 0.00000000c Fe_1a_0
0.50000000a 0.50000000b 0.50000000c Rh0.5Pt0.5_1d_1
```

## 得られたインプットの説明

inputcardの上から3,4行目にセルの形状の情報がある。
```
#--- brvtyp a c/a b/a alpha beta gamma
st 5.204307821390574 1.2817719680464779 1.0 90.0 90.0 90.0
```
brvtypはst(単純正方格子)で、一つ目の格子ベクトルの長さが5.204307821390574 Bohrである。残りの格子ベクトルについては、1つ目の格子ベクトルの長さとの比で1.2817719680464779, 1.0となっている。格子ベクトル同士のなす角は全て90度である。

上から9,10行目に異なったtypeの位置の数、つまり結晶学的に同等でない位置の数が示されている。
```
#--- ntyp
2
```
ここでは、FeのみであるFe_1a_0と、Rhが50%、Ptが50%であるRh0.5Pt0.5_1d_1の2種類のサイトがあるため、ntypは2である。

上から11行目から22行目に、各typeに対する入力パラメータが書かれている。
```
#--- type ncmp
  Fe_1a_0 1
#- rmt field mxl
0.0 0.0 2
#- anclr conc
26 100.0
#--- type ncmp
  Rh0.5Pt0.5_1d_1 2
#- rmt field mxl
0.0 0.0 2
#- anclr conc
45 50.0
78 50.0
```
まず1種類目のtypeであるFe_1a_0の入力パラメータが書かれている。ncmpはそのサイトに占める原子の種類の数であり、ここでは1である。anclr(原子番号)は26で、conc(サイトに原子が占める確率もしくは濃度)は100%である。続いて、2種類目のtypeであるRh0.5Pt0.5_1d_1の入力パラメータが書かれている。RhとPtがあるためncmpは2である。一つ目のRhについてはanclr(原子番号)は45でconcは50%、二つ目のPtについてはanclrは78でconcは50%である。

上から23行目から27行目に、セル内のサイトについての記述がある。
```
#--- natm
2
#--- atmicx atmtyp
0.00000000a 0.00000000b 0.00000000c Fe_1a_0
0.50000000a 0.50000000b 0.50000000c Rh0.5Pt0.5_1d_1
```
上から23,24行目はセル内のサイトの数でありここでは2である。また、上から25行目から27行目には原子の位置とtype名が書かれている。

以上の情報を基にして、手元にあるインプットをチェックすることが可能である。