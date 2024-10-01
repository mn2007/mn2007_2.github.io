---
layout: default
title: linux_gfortran
permalink: /linux_gfortran
---

# LinuxでのgfortranによるAkaiKKRのビルド

## 環境構築
make, gfortran, gnuplotのインストールを行う。CentOS等のRedHat系のディストリビューションであれば、
```
$ sudo yum install "Developer Tools"
$ sudo yum install gcc-gfortran libgfortran
$ sudo yum install gnuplot
```
Debien, Ubuntu等のDebian系ディストリビューションであれば
```
$ sudo apt install build-essential
$ sudo apt install gfortran
$ sudo apt install gnuplot
```
のようにコマンドを実行する。


## AkaiKKRのビルド
AkaiKKRの作業フォルダを作成し、cdで移動する。
```
% mkdir AkaiKKR
% cd AkaiKKR
```
ダウンロードした最新版のAkaiKKRを作成したAkaiKKRディレクトリに入れる。その後、ファイルを展開した後cdで移動する。
```
% tar zxvf cpa2021v01.tgz
% cd cpa2021
```
そして、makefileをvi, emacs, nano等の好みのエディタで編集する。15行目、16行目の
```
fort = ifort
#fort = gfortran
```
について、15行目の行頭に「#」を追加し、16行目の行頭の「#」を削除する。
```
#fort = ifort
fort = gfortran
```
この操作によりコンパイラをifortからgfortranに切り替える。編集が終わったら保存して終了する。そしてビルドを行う。
```
% make
% make gpd
% make spc
```
実行ファイル"specx", "gpd", "spc"があれば成功している。

## 動作確認

ビルドを行ったディレクトリで以下のコマンドを実行することで動作確認ができる。
```
$ ./specx < in/fe
```

