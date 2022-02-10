# J1900软路由安装ESXi 6.7u3

## Reference document

-  https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.esxi.install.doc/GUID-C3F32E0F-297B-4B75-8B3E-C28BD08680C8.html

# Prerequisites

- Download **VMware-VMvisor-Installer-201912001-15160138.x86_64.iso**
- Download rufus  https://rufus.ie/en_US/
- Prepare an installation USB flash disk
  - 找一个速度还可以的，容量大于1G的优盘；
  - Rufus里选择VMware-VMvisor-Installer-201912001-15160138.x86_64.iso，和FAT32分区制作启动优盘；
  - 在我的电脑里，打开优盘，新建一个文本文件起名ks.cfg（记得在文件夹选项里取消隐藏扩展名）；
  - ks.cfg文件中可修改默认密码，**rootpw** 为其他；

## Installation

1. 配置BIOS启动菜单，选择UEFI或者BIOS模式启动安装优盘；
2. ESXi安装引导倒计时，迅速按下 **Shift+O**（字母O）；
3. 在命令行里输入 **ignoreHeadless=TRUE ks=file://etc/vmware/weasel/ks.cfg** 回车；
4. 静等安装结束后，弹出一个黑色背景显示成功的消息框；
5. 拔掉优盘，重启软路由机器；

## Fix Headless Mode for ESXi boot

1. 重启进入倒计时，迅速按下 Shift+O（字母O）；
2. 在命令行里输入 **ignoreHeadless=TRUE** 回车；
3. 静等ESXi系统启动完成；
4. 在ESXi Web管理界面中，打开 ESXi SSH；
5. 用SSH进入ESXi；
6. 输入 **esxcfg-advcfg -k TRUE ignoreHeadless**
7. 退出SSH，在Web UI里关闭ESXi SSH；
