---
layout: default_en
title: mac_intel_en
permalink: /mac_intel_en
---

# Build with Intel compiler on Mac

## Environment Construction
The installation by the intel compiler is omitted here. First, install brew on a terminal. 
```
% /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
At the end of the installation, "====> Next steps:" appears, indicating the work to be done after the installation. If it indicates that you need to add a description to the .zprofile, follow the instructions. After that, update the package as follows. 
```
% brew update
% brew upgrade
```
Then, install gnuplot.
```
% brew install gnuplot
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
