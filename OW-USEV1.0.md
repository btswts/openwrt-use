# openwrt-use
openwrt使用过程中记录笔记

VBOX安装openwrtlede
先于官方下载IMG文件
https://downloads.openwrt.org/
使用qume-img 转换成虚拟机硬盘文件
   ubuntu 下安装需要的部件apt-get install qemu-utils
    然后使用命令 qemu-img convert -f raw -O vmdk *.img **.vmdk
    其中：-f 的参数值为源镜像文件的格式。-O（必须是大写）的参数值为目标镜像格式 、源镜像文件名称
和目标文件名称。

生成VMDK 后。进入VBOX安装。
要点
   注册生成的VMDK ，直接使用VMDK当硬盘。网络部分要设置两个网卡
   第一个仅主机网络 用来给宿主机连接用，第二个 桥接网卡
然后启动进入系统
   回车 ifconfig 看是否连上路由。
vi /etc/config/network
   重点要于eth0 eth1 分配
    config interface 'lan'
    option ifname 'eth0'
    option type 'bridge'
    option proto 'static'
     option ipaddr '192.168.16.2' 看VBOX网卡属性如何配置
    option netmask '255.255.255.0'

config interface 'wan'
   option ifname 'eth1'
   option proto 'dhcp'
：wq 保存退出
/etc/init.d/network restart
宿主机测试看看行不行用。
