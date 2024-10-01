---
layout: default
title: mac_gfortran
permalink: /mac_gfortran
---

# MacでのgfortranによるAkaiKKRのビルド

## 環境構築
ターミナルにて、まずはbrewのインストールを行う。
```
% /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
installの最後には「===> Next steps:」が表示され、install後に行う作業が示される。ここに.zprofileへの記述の追加をする旨が現れたらその指示に従う。その後、パッケージを更新する。
```
% brew update
% brew upgrade
```
そして、gfortran, gnuplotをインストールする。
```
% brew install gfortran
% brew install gnuplot
```

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
そして、makefileをvi, nano等の好みのエディタで編集する。15行目、16行目の
```
fort = ifort
#fort = gfortran
```
について、15行目の行頭に「#」を追加し、16行目の行頭の「#」を削除する。
```
#fort = ifort
fort = gfortran
```
この操作によりコンパイラをifortからgfortranに切り替える。そしてビルドを行う。
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

