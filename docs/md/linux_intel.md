---
layout: default
title: linux_intel
permalink: /linux_intel
---

# LinuxでのintelコンパイラによるAkaiKKRのビルド

## 環境構築
intelコンパイラのインストールについてはここでは省略する。まずmake, gnuplotのインストールを行う。CentOS等のRedHat系のディストリビューションであれば、
```
$ sudo yum install "Developer Tools"
$ sudo yum install gnuplot
```
Debien, Ubuntu等のDebian系ディストリビューションであれば
```
$ sudo apt install build-essential
$ sudo apt install gnuplot
```
のようにコマンドを実行する。


## AkaiKKRのビルド
AkaiKKRの作業ディレクトリを作成し、cdで移動する。
```
% mkdir AkaiKKR
% cd AkaiKKR
```
ダウンロードした最新版のAkaiKKRを作成したAkaiKKRディレクトリに入れる。その後、ファイルを展開した後cdで移動する。
```
% tar zxvf cpa2021v01.tgz
% cd cpa2021
```
そしてビルドを行う。
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

