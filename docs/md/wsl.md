---
layout: default
title: wsl
permalink: /wsl
---

# WindowsでのWSLによるAkaiKKRのビルド

## WSLの起動
デスクトップの下のバー(タスクバー)のWindowsボタンを右クリックする。そして「Windows ターミナル」をクリックするとPowerShellが立ち上がる。

PowerShellが実行できるようになったら、下記コマンドにてWSLが入っているかを確認する。
```
> wsl -l -v

  NAME                   STATE           VERSION
* Ubuntu                 Running         2
  Ubuntu-20.04           Stopped         1
```

WSLが入っていないのであればインストールをする。ただし管理者権限がないとインストールできないため、一旦PowerShellを終了し、タスクバーのWindowsボタンを右クリックして「Windows ターミナル(管理者)」を選ぶ。その後
```
> wsl --install
```
を実行してインストールした後、「Windows ターミナル(管理者)」を終了して「Windows ターミナル」を立ち上げる。

なお「wsl -l -v」を実行した際にUbuntuに*がついていないのであれば、
```
> wslconfig /s Ubuntu
```
を実行する。

WSLが入っていることが確認出来たら、下記コマンドによりwslを起動する。
```
> wsl
```

## 環境構築
以下のコマンドを順に実行し、make、gfortran等のAkaiKKRのビルドに必要な実行コマンドをインストールする。最後にmake、gfortranが入ったかどうかを確認する。
```
# sudo apt update
# sudo apt upgrade
# sudo apt install build-essential
# sudo apt install gfortran
# make -v
# gfortran -v
```

## AkaiKKRのビルド
AkaiKKRの作業フォルダを作成し、cdで移動する。
```
# mkdir AkaiKKR
# cd AkaiKKR
```

PowerShellからは一旦離れ、WindowsのExploreの機能等を用いて、ダウンロードした最新版のAkaiKKRを「C:\Users\ユーザー名\AkaiKKR」に入れる。その後PowerShellに戻り、ファイルを展開した後cdで移動する。
```
# tar zxvf cpa2021v01.tgz
# cd cpa2021
```

makefileをvi, emacs, nano等の好みのエディタで編集する。
nanoを使う場合は
```
# nano makefile
```
でファイルを開ける。

15行目、16行目の
```
fort = ifort
#fort = gfortran
```
について、15行目の行頭に「#」を追加し、16行目の行頭の「#」を削除する。
```
#fort = ifort
fort = gfortran
```
この操作によりコンパイラをifortからgfortranに切り替える。編集が終わったら保存する(nanoを使っている場合は Ctrl-O、Enterを順に押す。)。そして終了する(nanoを使っている場合はCtrl-X)。


編集を終えたらビルドを行う。
```
# make
# make gpd
# make spc
```

実行ファイル"specx", "gpd", "spc"があれば成功している。

## 動作確認

ビルドを行ったフォルダで以下のコマンドを実行することで動作確認ができる。
```
$ ./specx < in/fe
```
なお、作業が全て終わったら「exit」コマンドによりWSLおよびPowerShellを終了できる。

## gnuplotについて
結果を描画する際にgpdやspcを用いるためにはgnuplotがインストールされている必要がある。gnuplotのインストール自体は

```
# sudo apt install gnuplot
```

で行えるが、別画面で結果を表示するための設定は少々手間がかかる。[外部サイト](https://utphys-comp.github.io/wsl2.html) の「GUIの利用」に手順が書かれているため、以下そのサイトに書かれている内容をそのまま記述する。

### Windows側の準備
Windows側では、Linuxが表示しようとしている画面を受け取るサーバーを用意する必要がある。ここでは”VcXsrv”を利用する。 VcXsrvのダウンロードは[https://sourceforge.net/projects/vcxsrv/](https://sourceforge.net/projects/vcxsrv/) から出来る。ダウンロードしたら案内に従ってインストールすればよい。 GUIを表示したい時は以下のような手順でX serverの起動を行えば良い。

1. xlaunch.exeを実行する(スタートメニューから開けばよい)
2. 画面の案内に従って設定する
3. “multiple window”を選び次に進む
4. “start no client”を選び次に進む
5. “clipboard”(いわゆるコピペ)を使用したければチェックを入れる
6. “Adittional parameters for VcXsrv”の欄に-acと入力してから次に進む

毎回起動するのは面倒である。以下のような操作でパソコン起動時に自動でX serverも起動することが出来る

1. 上述の操作1-6をする
2. “Save configuration”ボタンを押し、”config.xlaunch”を移動させやすい場所(例えばデスクトップ)に保存する
3. 完了を押す
4. “Winキー”+”R”を押してshell:startupと入力する
5. “スタートアップ”という名前のフォルダが開くので、”config.xlaunch”をスタートアップフォルダ内に移動する

### Ubuntu側の準備
Ubuntu側では、表示先をあらかじめ環境変数DISPLAYに設定する必要がある

1. cat /etc/resolv.conf でファイル/etc/resolv.confの中身を表示する
2. 先頭がnameserverで始まるnameserver 123.45.67.89のような行(数字はUbuntuを実行するたびに異なる)があるのでこの数字(IPアドレス)を控えておく
3. 以下のコマンドを実行する。なお123.45.67.89の部分は手順2のIPアドレスの値を入れる
```
export DISPLAY=123.45.67.89:0
```
以上の設定により、例えばターミナルからgnuplotを実行し、plot sin(x)と入力するとウインドウが開きsin関数がプロットされるはずである

Ubuntuターミナルを開くたびに、上記の手順を繰り返すのは面倒である。$HOME/.bashrcファイルの最後に、以下の1行を追加しておけば自動的に環境変数が設定される
```
export DISPLAY=$(grep nameserver /etc/resolv.conf | cut -d " " -f 2):0
```