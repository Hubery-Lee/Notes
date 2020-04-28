# Oracle vbox 安装macOS Mojave 

## :pencil: 安装包准备

1. oracle virtualbox
2. [mac 安装包]( https://www.professionaltutorial.com/macos-mojave-image-download/ )
3. [安装教程]( https://www.professionaltutorial.com/install-macos-mojave-virtualbox-windows/#Step_1_Configure_System )
4. [安装教程视频]( https://www.youtube.com/watch?v=v_hENCR6nEw )

## :fire: orcale 虚拟机识别vmdk虚拟硬盘

1.首先根据视频教程，新建并配置mac虚拟机，关闭oracle
2.以管理身份打开window命令终端，并如下设置使oracle能够找到并启动mac

```
cd "C:\Program Files\Oracle\VirtualBox\"
VBoxManage.exe modifyvm "Your VM Name" --cpuidset 00000001 000106e5 00100800 0098e3fd bfebfbff
VBoxManage setextradata "Your VM Name" "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "iMac11,3"
VBoxManage setextradata "Your VM Name" "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"
VBoxManage setextradata "Your VM Name" "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Iloveapple"
VBoxManage setextradata "Your VM Name" "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"
VBoxManage setextradata "Your VM Name" "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1

```
3.打开Oracle，启动mac虚拟机

## :question: 键盘鼠标不识别的解决办法

1.安装虚拟机拓展包

2.使用USB3.0接口

## :o: 全屏显示模式

常用显示器尺寸

`1920×1080
1280×720
2048×1080
2560×1440
3840×2160
1280×800
1280×1024
1440×900
1600×900`

以管理身份打开window命令终端，并如下设置虚拟机显示器大小

```
cd "C:\Program Files\Oracle\Virtualbox"
VBoxManage setextradata “Your Virtual Machine Name” VBoxInternal2/EfiGraphicsResolution X
```

## :memo:给个赞吧 :thumbsup:

Copyright :copyright:2019 [Hubery-Lee](https://github.com/Hubery-Lee)

