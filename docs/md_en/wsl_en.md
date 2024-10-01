---
layout: default_en
title: wsl_en
permalink: /wsl_en
---

# Build with WSL on Windows

## WSL Launch
Right click on the Windows button on the bottom bar of the desktop (taskbar). Then click on "Windows Terminal" to launch PowerShell.

Then, check to verify that WSL is included by using the following command. 
```
> wsl -l -v

  NAME                   STATE           VERSION
* Ubuntu                 Running         2
  Ubuntu-20.04           Stopped         1
```

If WSL is not installed, install it. It cannot be installed without administrator rights. If you have launched PowerShell without it, close PowerShell, right click the Windows button on the taskbar, and choose "Windows Terminal (Administrator)". Then use the following command to install WSL.
```
> wsl --install
```
Then, exit "Windows Terminal (Administrator)" and launch "Windows Terminal". 

If there is no * on Ubuntu when you run "wsl -l -v", use the following command.
```
> wslconfig /s Ubuntu
```

After confirming that WSL is installed, start WSL by the following command. 
```
> wsl
```

## Environment Construction
Execute the following commands in order to install the execution commands required to build AkaiKKR, such as make and gfortran. Finally, check if make and gfortran are installed.
```
# sudo apt update
# sudo apt upgrade
# sudo apt install build-essential
# sudo apt install gfortran
# make -v
# gfortran -v
```

## Build for AkaiKKR
After creating a working directory for AkaiKKR, use "cd" to move there.
```
# mkdir AkaiKKR
# cd AkaiKKR
```

Leave PowerShell for a moment and put the latest version of AkaiKKR that you downloaded into "C:\Users\username\AkaiKKR" using the Explore function of Windows, etc. Then return to PowerShell, extract the file, and use "cd" to move to the extracted directory.
```
# tar zxvf cpa2021v01.tgz
# cd cpa2021
```

Open the makefile with your favorite editor such as "vi", "emacs", "nano", etc. If you use "nano", you can open the makefile with the following command.
```
# nano makefile
```

Followings are lines 15 and 16.
```
fort = ifort
#fort = gfortran
```
Add "#" to the beginning of line 15 and delete "#" from the beginning of line 16.
```
#fort = ifort
fort = gfortran
```
This operation switches the compiler from ifort to gfortran. After editing, save (If using nano, press Ctrl-O, then Enter.) and exit (If using nano, press Ctrl-X). Then, build with the following commands. 
```
# make
# make gpd
# make spc
```

If executables "specx", "gpd", and "spc" are present, the build has succeeded.

## Operation Check

The operation can be checked by executing the following command in the directory where the build was performed.
```
$ ./specx < in/fe
```
When all work has been completed, WSL and PowerShell can be terminated with the "exit" command.

## About gnuplot
gnuplot must be installed in order to use "gpd" or "spc" to plot results. The installation of gnuplot itself can be done with the following command.

```
# sudo apt install gnuplot
```

Setting up the results to be displayed on a separate screen is a bit time-consuming. The procedure is described in the "Using GUI" section of [an external site (Japanese)](https://utphys-comp.github.io/wsl2.html). The following is a translated description of the contents of this site.

### Preparation on Windows side
On the Windows side, it is necessary to prepare a server to receive the screen that Linux is trying to display. Here, "VcXsrv" is used. You can download VcXsrv from [https://sourceforge.net/projects/vcxsrv/](https://sourceforge.net/projects/vcxsrv/). After downloading, follow the instructions to install the software. If you want to display the GUI, follow the procedure below to start the X server.

1. run xlaunch.exe (you can open it from the Start menu)
2. follow the on-screen instructions
3. Select "multiple window" and go to the next step.
4. Select "start no client" and go to the next step.
5. Check the box if you want to use "clipboard" (so-called "copy and paste")
6. Enter "-ac" in the "Additional parameters for VcXsrv" field before continuing.

It is troublesome to start up every time. The following procedure can be used to automatically start the X server when the PC starts up.

1. Do steps 1-6 described above.
2. Press "Save configuration" button and save "config.xlaunch" to a convenient location (e.g. desktop).
3. Press "Finish" button.
4. Press "Win "+"R" and type shell:startup.
5. A folder named "startup" will open. Move "config.xlaunch" to the startup folder.

### Preparation on Ubuntu side
On the Ubuntu side, the display destination must be set to the DISPLAY environment variable in advance.

1. "cat /etc/resolv.conf" to display the contents of the file /etc/resolv.conf.
2. Note down the number (IP address) of the line starting with "nameserver" such as nameserver 123.45.67.89 (the number is different each time you run Ubuntu).
3. Execute the following command. Note that the 123.45.67.89 part should be the value of the IP address in step 2.
```
export DISPLAY=123.45.67.89:0
```
With these settings, for example, if you run gnuplot from a terminal and type plot sin(x), a window should open and the sin function should be plotted.

It is tedious to repeat the above steps every time you open the Ubuntu terminal. If you add the following line to the end of the $HOME/.bashrc file, the environment variable will be set automatically.
```
export DISPLAY=$(grep nameserver /etc/resolv.conf | cut -d " " -f 2):0
```