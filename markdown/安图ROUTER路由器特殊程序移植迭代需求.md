

#  **安图ROUTER路由器特殊程序移植迭代需求** 

http://172.16.2.8/biz/feedback-adminView-1243.html 开发[@包海欣](app://desktop.dingtalk.com/web_content/chatbox.html?isFourColumnMode=false#)  测试[@徐艳凤](app://desktop.dingtalk.com/web_content/chatbox.html?isFourColumnMode=false#) （评审时间待定

v7.2.1评审记录http://172.16.2.8/biz/testtask-view-100.html

7.2.3程序[文档-/受控软件资料库 - 禅道](http://172.16.2.8/biz/doc-browse-168-byModule-3059.html)



过滤需求[DOC #4237 安图生物H7920/H8951/H8951S/H8922SV40B、H8922V40A(H8900_APP_V7.2.1_AUTOBIO_190806123201.trx&YF190809-02) - 受控软件资料库 - 禅道](http://172.16.2.8/biz/doc-view-4237.html)

历史需求链接：http://172.16.2.4:8080/browse/PHDCUSTOMERREQ-903



1. 升级到v7.2.1升级，查看相关代码，测试相关功能，

2. 载v7.2.3程序
3. 查看历史修改记录？

转发过滤规则中，
 黑名单： 默认允许数据包转发， 符合名单中“ 丢弃” 规则的数据包不能经过路由器
转发。
 白名单： 默认拒绝数据包转发， 符合名单中“ 接受” 规则的数据包可以经过路由器
转发出去。

白名单：如果时白名单格式，默认拒绝转发，除了名单中permit规则的，只有白名单中permit规则的能拼通

黑名单：如果为黑名单格式，默认接收转发，除了名单中deny规则的，除了黑名单中deny规则的，其他都能拼通。

一个permit规则，在 白名单中：

- 1 IP过滤添加规则后的filter表

![image-20221019113240059](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019113240059.png)

OUTPUT链中的forward_ip_list, 为什么在OUTPUT链中？看错了

![image-20221019113304470](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019113304470.png)

- 2 将ip过滤切换到白名单后，日志出现：

- ![image-20221019114421425](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019114421425.png)

  ![image-20221019114447951](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019114447951.png)

  执行这行代码

  ![image-20221019114615649](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019114615649.png)

调用iptables_init地方有两处

![image-20221019114803025](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019114803025.png)

filter_exit(int signo)

filter_init



*23端口*是telnet的端口

*0端口*是为HTTP（HyperText Transport Protocol)即超文本传输协议开放的，



ip过滤：白名单和黑名单的cli.conf区别，白名单会多一条：

![image-20221019152359214](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019152359214.png)

域名过滤：为白名单时

![image-20221019152600561](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019152600561.png)

​	转为黑名单时不见了deny

![image-20221019152702881](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019152702881.png)



添加域名过滤：

黑名单：

为什么添加到链forward_ip_list了，不应该是forward_domain_list中吗？

![image-20221019153316072](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019153316072.png)

![image-20221019153308458](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019153308458.png)

![image-20221019153345957](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019153345957.png)

白名单：





![image-20221019153414019](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019153414019.png)

iptables表没有变化

iptables_init();初始化这个表  文件找不到？在cli.conf的末尾

![image-20221019164206798](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221019164206798.png)

static void filter_init(void) 过滤表的初始化：

清空表，设置默认策略，初始化上表，创建链，将链添加到相应的链中（INPUT等），初始化新建的链，信号？标志



###  自测：同时使用ip过滤和域名过滤功能

设置ip过滤白名单、域名过滤白名单，放行IP地址8.8.8.8和域名www.baidu.com.

![image-20221021093558477](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221021093558477.png)

![image-20221021093607825](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221021093607825.png)

ping 结果: 能拼通8.8.8.8和www.baidu.com，其他地址均不能拼通。

![image-20221021093742678](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221021093742678.png)



![image-20221021094000459](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221021094000459.png)



安图的这个需求 今天整理一份总结文档发我下 注意是要业务与代码实现相结合的总结文档
