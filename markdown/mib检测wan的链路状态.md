[TOC]



# 巴西Primetel-mib检测wan的链路状态

巴西Primetel-mib检测wan的链路状态 -- 10.14
http://172.16.2.8/biz/feedback-adminView-1086.html



> 客户名称：Primetel
>
> 基线程序：H8922V40_APP_V7.2.2_SE_IPSEC_2206011315.trx（修复ipsec无法长期保持连接问题）
>
> \1. 客户使用wan，modem主备模式，需要在linkbackup切换链路时，触发ipsec进程重启。
>
> \2. 当前IPSec脚本是openswan，相对于Strongswan连接速度更慢，客户期望优化缩短ipsec建立连接的时间
>
> 新增需求评估：目前客户用的是有线无线备份，有线上端出问题时，我们路由器是会切换到modem通讯，但是有个情况： 客户用的是mib来监控wan口的状态，发现这种方法无法正确判断，因为wan口上端出问题时，我们设备上的wan状态是正常的。客户想要解决这个问题。用mib检测wan的链路状态.
>
> ftp://172.16.2.5/Router/Primetel/22-07-22_14-17-15/

链路备份的知识点 8-12/8_15

MIB --- SNMP

需求评估：确认客户问题：其中WAN口上端出现问题，具体是什么问题，网线拔插？还是链路切换，网络连接状态



需求评估主要是确认客户问题，开发确认能不能实现，实现的周期，

主链路是WAN，备份链路是modem，链路切换就是有问题的？

- 1 目前WAN status 情况是：只要WAN口是UP，情况都是connected，就是只要检测到WAN，就能查询WAN口信息，状态都是connected，

​          链路只有规则名是*好，检测IP或域名为空白的，是怎么工作的？无效的

- 2 说的是有线上端出问题时，路由器是会切换到modem通讯，那么，此时WAN的status应为disconnected ？ ，即网络连接状态 是不是能拼通链路备份中相应的地址就是connect，否则就是disconnectd。

  拼通 用icmp检测吗

实现初步：

获取cli.conf 中链路备份 wan的检测地址，使用ping命令



## 1 获取版本，升级版本

### 法1

- 1 登录路径：ftp://172.16.2.5/Router/Primetel/22-07-22_14-17-15/

     登录：m2m ,m2m

![image-20221011110657116](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011110657116.png)

![image-20221011110754162](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011110754162.png)

- 2 升级到相应版本，8922v40和8951一样的，只是大小问题，所以可以用8951板子验证。

![image-20221011110856090](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011110856090.png)

- 3 升级

  ![image-20221011115520216](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011115520216.png)

### 法2

登录：172.16.2.5:8080

选择Router

![image-20221011141021227](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011141021227.png)

选择对应版本

![image-20221011141134178](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011141134178.png)

![image-20221011141210768](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011141210768.png)

找到对应时间

![image-20221011141243842](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011141243842.png)

控制台输出

![image-20221011141314165](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011141314165.png)

拉倒底，获取版本链接

![image-20221011141339770](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011141339770.png)

## 2 获取程序代码

下载代码，建立source insight 工程

gitlab地址: http://172.16.8.42/oversea/mtk7628_openwrt/tree/odm-primetel-mqtt

命令下载 ：git clone git@172.16.8.42:oversea/mtk7628_openwrt.git  

此时我下载到的是develop分支的，应切换到odm-primetel-mqtt分支

切换到对应的远程分支

```c
 git checkout odm-primetel-mqtt
```

查看当前分支

![image-20221011154532191](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011154532191.png)

git clone 下载到服务器的文件夹最好用客户名称，source insight建立工程，文件夹里有一个project名字的，建在那里；

source insight建立的工程显示的是当前分支的代码，所以分支切换时，代码也随之切换。

![image-20221011154921489](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011154921489.png)

```text
git log
```

![image-20221011155503658](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011155503658.png)

- 当找不到函数定义时

```text
 cd hongdian_release/ #切换目录
 grep "DMO" -nr # grep可以查找文件的内容，再在source insight中添加相应的文件
```

### 编译

执行./build.sh d v7.2.2出现的问题

![img](https://static.dingtalk.com/media/lQLPJxbFTB2A8xjNAaXNB2WwnGQDNZxYfHEDRFF31gBMAA_1893_421.png?auth_bizType='IM')



- 先编all，再编single

  >编译all：
  >在工程根目录下：
  >清理
  >make clean;cd hongdian_release;make clean;cd ..;
  >编译
  >./build.sh d V7.2.2_SE-SC all
  >
  >编译single：
  >在工程根目录下：
  >清理
  >cd hongdian_release;make clean;
  >编译
  >make Version=V7.2.2_SE-SC
  >
  >

- 编译文件目录：/home/baohaixin2218/8922_v40/mtk7628_openwrt/hongdian_release/build/image







```text

```

## 3 学习snnp功能

- SNMP（简单网络管理协议）
  - SNMP可以使网络管理员通过**一台工作站**完成对计算机、路由器和其他网络设备的**远程管理和监视**。管理工作站可以远程管理所有支持该协议的网络设备，如监控网络状态、修改网络设备配置、接收网络事件警告等。
  - 背景：设备种类繁多，用于管理设备，服务、管理、协议 
  - SNMP是管理进程（ NMS）和代理进程（ Agent）之间的通信协议。
  - 网络管理员使用SNMP功能可以查询设备信息、修改设备的参数值、监控设备状态、自动发现网络故障、生成报告等。
  - 。

mib 管理信息库

- SNMP网络架构由三部分组成： NMS、 Agent和MIB。

  - NMS

    >NMS是网络中的管理者，是一个利用SNMP协议对网络设备进行管理和监视的系
    >统。 NMS既可以指一台专门用来进行网络管理的服务器，也可以指某个设备中执
    >行管理功能的一个应用程序。
    >NMS可以向Agent发出请求，查询或修改一个或多个具体的参数值。同时， NMS可
    >以接收Agent主动发送的Trap信息，以获知被管理设备当前的状态。

  - Agent

    >Agent是网络设备中的一个应用模块，用于维护被管理设备的信息数据并响应NMS
    >的请求，把管理数据汇报给发送请求的NMS。
    >Agent接收到NMS的请求信息后，完成查询或修改操作，并把操作结果发送给
    >NMS，完成响应。同时，当设备发生故障或者其他事件的时候， Agent会主动发送
    >Trap信息给NMS，通知设备当前的状态变化

  - MIB

    >MIB是被管理对象的集合。它定义了被管理对象的一系列属性：对象的名称、对象的访问权限和对象
    >的数据类型等。每个Agent都有自己的MIB

![image-20221011163224513](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011163224513.png)

- 版本

  SNMPv1、 SNMPV2c、 SNMPv3种最常用的版本

 	  SNMPv3 版本提供了认证和加密安全机制，以及基于用户和视图的访问控制功能，增强了安全性

### 使用

- router的snmp配置

  ![image-20221011191859996](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011191859996.png)

  源接口：用于指定和SNMP工具通信时消息报文带的源地址

  共同体：SNMP客户端连接路由器SNMP服务的共同体密码，用于身份识别。

- MIB Browser工具

  - 下载MIB Browser工具安装，登录

  Read community 、Write Community 和snmp共同体配的一样，版本号也要一样。

  ![image-20221011192646793](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011192646793.png)

  - 将下列压缩包中的文件导入工具中 File -> load MIBs

  ![image-20221011192450327](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011192450327.png)

  - 查看信息，选中文件夹，在Router上右键，选择Get Subtree，即打印信息

  ![image-20221011193130365](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011193130365.png)

  ![image-20221011193255696](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011193255696.png)
  
  ## 记录
  
  ![image-20221012145558908](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221012145558908.png)
  
  ![image-20221012145803115](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221012145803115.png)
  
  ![image-20221012150002952](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221012150002952.png)
  
  strcmp 匹配成功，返回0
  
  
  
  ret |= (1<<WORK_MODE_V4_BIT);  ？
  
## 4 链路备份

链路备份为空时, linkbackup 进程停止，有规则时运行。

  ![image-20221014115456760](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221014115456760.png)

为一条链路

2条链路



如果WAN连接另一端，那么查询信息会不会完整。

![image-20221014135520284](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221014135520284.png)



![image-20221017155624203](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221017155624203.png)



用链路备份的话，wan模式为DHCP，地址不能确定，

字符数组的操作，

函数不带长度的最好不用。

strncpy

snprintf

 