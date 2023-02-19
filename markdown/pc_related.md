

[TOC]

# pc操作相关

## 1 同时连接内网和外网

PC网线连接内网，网线连接路由器

查看目前路由：当前有两条默认路由

![image-20220930163531434](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220930163531434.png)

```c
C:\Users\Administrator>route delete 0.0.0.0//删除所有默认路由
C:\Users\Administrator>route add -p 0.0.0.0 mask 0.0.0.0 192.168.8.1//将其中一个设置为默认路由
C:\Users\Administrator>route add -p 172.16.0.0 mask 255.255.0.0 172.16.6.1//添加另一个路由
```

查看修改后的路由表

![image-20220930164052875](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220930164052875.png)

此时可以同时访问外网和内网。

## 2 映射网络驱动器

- 1 打开电脑文件夹

![image-20221011111257555](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011111257555.png)

- 2  选择任意一个空的驱动器，注意文件夹的格式

  ![image-20221011112233951](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011112233951.png)
