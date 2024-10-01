---
layout: default_en
title: linux_intel_en
permalink: /linux_intel_en
---

# Build with Intel compiler on Linux

## Environment Construction
The installation of the intel compiler is omitted here. First, we install make and gnuplot. if you are using a RedHat distribution such as CentOS, execute commands as follows.
```
$ sudo yum install "Developer Tools"
$ sudo yum install gnuplot
```
If you are using a Debian distribution such as Debien and Ubuntu, execute commands as follows.
```
$ sudo apt install build-essential
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
Build is done with the following commands.
```
% make
% make gpd
% make spc
```
If executables "specx", "gpd", and "spc" are present, the build has succeeded.

## Operation Check

The operation can be checked by executing the following command in the directory where the build was performed.
```
$ ./specx < in/fe
```
