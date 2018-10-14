Linux网络基础教程之网络服务  
====  
  
## 网络基础知识  
  
URL：统一资源定位  
协议+域名或IP：端口+网页路径+网页名  
eg: http://www.lampbrother.net:80 
.net  一级域名   不能申请，是域名分配组织分配不能随意更改   常见的组织一级域名、地区一级域名  
lampborther  二级域名   可以申请  
www   三级域名  
看二级域名可以判断是否是钓鱼网站  
  
  
## 网络通信协议  
  
#### OSI/ISO七层模型和TCP/IP四层模型  
  OSI七层框架  
 应用层>表示层>会话层>传输层>网络层>数据链路层>物理层  
  
>物理层：设备之间的比特流的传输、物理接口、电器特性等  
>数据链路层：成帧、用MAC地址访问媒介、错误检测与修正  
>网络层： 提供Ip地址、路由  
>传输层：可靠与不可靠的传输、传输前的错误检测、流控  
>会话层： 对应用会话的管理、同步  
>表示层：数据的表现形式  
>应用层：用户接口  
  
#### TCP/IP协议  
  应用层>              传输层>国际互联层>  网络接口层  
>国际互联层：解决主机到主机的通信问题，有三层协议：IP、互联网组管理协议（IGMP）、报文协议（ICMP）  
>TCP可靠性高  
>UDP 快速、不可靠  
查看当前计算机开的端口 ：netstat -an  
  
## Linux配置IP地址的方法  
+ ifconfig命令临时配置  
>查看与配置网络状态命令  
  
>临时设置eth0网卡的IP地址  ifconfig eth0：0 192.168.3.251  
>取消设置 ifconfig eth0：down  
  
+ setup工具永久配置  
>红帽专有图形化工具  
>网络配置》设置配置  
  service network restart  
  
  
+ 修改网络配置文件  
+ 图形界面配置IP地址  
  
## Linux网络配置文件  
#### vim /etc/sysconfig/network-scripts/ifcfg-eth0  
  
>DEVICE=eth0   网卡设备名  
>BOOTPROTO=none 是否自动获取IP（none，static，dhcp）  
>HWADDR=00：0c：29：17：c4：09   MAC地址  
>NM——CONTROLLED=yes 是否可以由Netwoek Manager图形管理工具托管  
>ONBOOT=yes 是否随网络服务启动，eth0生效  
>TYPE=Ethernet 类型为以太网  
>UUID=“55444rffa-44ffss” 唯一识别码  
>IPADDR=192.168.0.252 IP地址  
>NETMASK=255.255.255.0 子网掩码  
>GATEWAY=192.168.0.1 网关  
>DNSI=202.106.0.20 DNS  
>IPV6NIT=no IPv6没有启用  
>UESRCTL=no 不允许非root用户控制  
  
## 主机名文件  
#### vi /etc/sysconfig/network  
  
1、查看和修改主机名 永久生效  
NETWORKING=yes  网络服务是否运行  
HOSTNAME=localhost.localdomain  主机名  
  
2、查看与临时设置主机名 hostname 主机名  
  
  
## DNS配置文件  
#### vi /etc/resolv.conf  
nameserver 202.106.0.20  
search localhost  
  
  
## 常用的网络命令  
  
>ifconfig 查看与配置网络状态命令  
>hostname 查看设置主机名  
>ifdown 网卡设备名    禁用该网卡设备  
>ifup 网卡设备名  启用该网卡设备  
  
### 查询网络状态  
##### netstat[选项]  
netstat -tlun 查看监听  查看本机连接的服务  
netstat -an  所有  
netstat -an  | grep ESTABLISHED  连接的网络服务  
-t： 列出TCP协议端口  
-u： 列出UDP协议端口  
-n： 不使用域名与服务名，而使用IP地址和端口号  
-l: 仅列出在监听状态网络服务  
-a：列出所有的网络连接  
netstat -rn  查看路由表  
route -n 查看路由列表（可以看到网关）  
  
### 域名解析命令  
>nslookup 主机名或IP   进行域名与IP地址解析  
>nslookup  >server   查看本机DNS服务器
