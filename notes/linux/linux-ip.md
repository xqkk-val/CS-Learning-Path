默认情况下，我们linux操作系统ip获取的方式是自动获取的方式，我们可以查看自己linux操作系统，看看ip的获取方式：

![image-20260516115301698](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20260516115301698.png)

linux的IP地址是自动匹配的,最好让他固定

etc/sysconfig/network-scripts/ifcfg-ens33

该文件描述linux网络配置的文件

```
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=dhcp		//dhcp:自动获取--static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=a72f7457-e49f-4b89-b6ab-4240b1281c67
DEVICE=ens33
ONBOOT=yes
//额外编辑
IPADDR=192.168.16.135	//IPADDR需要在同一网段192.168.16.xx规定在128~254之间
//子网掩码
NETMARSK=255.255.255.0
//网关
GETWAY=192.168.16.2

DNS1=114.11.114.114
DNS2=1.2.4.8
```

> ![image-20260516000445555](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20260516000445555.png)

IPADDR需要在同一网段192.168.16.xx

规定在128~254之间

- 最后重启网络服务

```
systemctl restart network
```

- 或者重启系统

```
reboot
```

