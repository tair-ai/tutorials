# Env Trouble shoot

## 安装ubuntu

1. 检查bios设置 是否开启security boot模式，如果开启需要禁用

> 否则将会出现Nvidia显卡驱动不能正确安装的情况 (sign kernel)问题

2. ubuntu-16.04 / centos 需要检查 bios 的硬盘将 SATA 换为 AHCI模式

3. 如果为SSD + 机械硬盘，SSD原有windows系统情形时，建议压缩ssd 1G出来为linux安装boot

4. 安装linux时，尽量将boot安装在ssd的磁盘上

5. cuda-9.0提供的显卡驱动，可以提供给cuda-8.0

## Grub修复

1. grub支持部分bash命令，如ls等，ls时列出全部磁盘逻辑分区，支持reboot

2. grub修复方法
```
    grub rescue>ls
    (hd0) (hd0,msdos9) (hd0,msdos8) (hd0,msdos7) (hd0,msdos6) (hd0,msdos5) (hd0,msdos2) (hd0,msdos1)
    # 依次查看分区设备，确认安装引导的分区
    grub rescue>ls (hd0,msdos1)
    # 若出现unknown filesystem字样，则尝试下一个，若为目录则该分区为引导分区
    # 将该区设置为root, 如机器安装的引导(hd0,msdos8)，则
    grub rescue>set root=(hd0,msdos8)
    # 查找grub.cfg所在的路径，该路径为prefix, 如位于/boot/grub下面，则
    grub rescue>set prefix=(hd0,msdos8)/boot/grub
    # 查看引导目录，查找.mod文件所在的文件路径，找到normal.mod文件,启动normal启动
    grub rescue>insmod i386-pc/normal.mod
    # 启动
    grub rescue>normal
    # 进入ubuntu引导界面
```
## cuda安装

1. nvidia官方下载cuda-xxx-xxxx.run文件

2. 禁用默认的显卡驱动
```
$sudo apt-get update
$sudo apt-get -y install git openssh-server g++ vim
$sudo echo "blacklist nouveau" >>  /etc/modprobe.d/blacklist.conf
$sudo update-initramfs -u
$reboot
```

3. 按组合键进入并登陆terminal，CTRL+ALT+F2Explosion 
```
$sudo service lightdm stop
$ps -ef |grep Xorg  # 如果还有Xorg进程，kill掉
$sudo sh cuda-xxx-xxxx.run --extract=`pwd`
# 会得到 cuda-linux-xxx.run / cuda-samples-xxx.run / Nvidia-xx-driver.run 三个新文件
$sudo sh Nvidia-xx-driver.run --no-opengl-libs  # 安装显卡驱动, 笔记本上避免循环login问题
# 如果不报错则安装成功，如果报错 `$cat /var/log/nvidia-install.log` 查看原因
# 笔记本问题(记录)，联想拯救者1060，16.04安装cuda的驱动以后，执行 apt-get install nvidia-375 
# 再取消禁用nouveau，更新kernel然后reboot既可以(这个问题比较奇怪), 安装后nvidia-smi 是384.90版本(2017.11)
$nvidia-smi    # 查看显卡驱动安装情况
$sudo sh cuda-linux-xxx.run  # 安装cuda
$sudo sh cuda-samples-xxx.run  # 安装cuda-samples，记住安装路径
$sudo lightdm start
$nvidia-smi
$cd /usr/local/cuda/samples/1_Utilities/deviceQuery
$make
$./deviceQuery    # 如果输出正常则安装成功
$sudo su   # 进入 root
$echo "export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}" >> /etc/profile
$echo "export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}"
$echo "/usr/local/cuda/lib64" >> /etc/ld.so.conf.d/cuda.conf
$ldconfig
$source /etc/profile
```
