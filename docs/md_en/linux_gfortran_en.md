---
layout: default_en
title: linux_gfortran_en
permalink: /linux_gfortran_en
---

# Build with gfortran on Linux

## Environment Construction
First, we install make and gnuplot. If you are using a RedHat distribution such as CentOS, execute commands as follows.
```
$ sudo yum install "Developer Tools"
$ sudo yum install gcc-gfortran libgfortran
$ sudo yum install gnuplot
```
If you are using a Debian distribution such as Debien and Ubuntu, execute commands as follows.
```
$ sudo apt install build-essential
$ sudo apt install gfortran
$ sudo apt install gnuplot
```

## Build for AkaiKKR
After creating a working directory for AkaiKKR, use "cd" to move there.
```
% mkdir AkaiKKR
% cd AkaiKKR
```
Put the latest version of AkaiKKR you downloaded into the AkaiKKR directory you created. After extracting the file, use "cd" to move to the extracted directory.
```
% tar zxvf cpa2021v01.tgz
% cd cpa2021
```
Then, open the makefile with your favorite editor such as "vi", "emacs", "nano", etc. Followings are lines 15 and 16.
```
fort = ifort
#fort = gfortran
```
Add "#" to the beginning of line 15 and delete "#" from the beginning of line 16.
```
#fort = ifort
fort = gfortran
```
This operation switches the compiler from ifort to gfortran. After editing, save and exit. Then, build.
```
% make
% make gpd
% make spc
```
Build is done with the following commands.

## Operation Check

The operation can be checked by executing the following command in the directory where the build was performed.
```
$ ./specx < in/fe
```