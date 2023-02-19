[TOC]



# Source Insight

Source Insight：
向左缩进				: F9
向右缩进				: F10
替换				: Ctrl+H
剪切一行（删除一行）		: Ctrl+U
选择一个单词			: Shift+F5
选择一行				: ctrl + k  /  Shift+F6
光标跳到当前行的结束		: End
选中多行 				：ctrl +k ，一直按k

在文件内搜索 ：ctrl + H ,F3、F4跳转



在多个文件中替换			: Ctrl+Shift+H
从光标起，向右剪切一个字		: Ctrl+,
从光标起，右边剪切至行尾		: Ctrl+;
复制一行				: Ctrl+K
复制光标到行尾的内容		: Ctrl+Shift+K
插入一新行			: Ctrl+I
光标跳到当前行的开始		: Home

选择左边单词			: Ctrl+Shift+Left
选择右边单词			: Ctrl+Shift+Right
从当前位置选择到文件结束		: Ctrl+Shift+End
从当前位置选择到行结束		: Shift+End
从当前位置选择到行的开始		: Shift+Home
从当前位置选择到文件顶部		: Ctrl+Shift+Home
重复输入				: Ctrl+\
选中文本时，鼠标回到选择的开始	: Ctrl+Alt+[
到选择部分的尾部			: Ctrl+Alt+]
到代码块的起始位置			: Ctrl+Shift+[
到代码块的结束位置			: Ctrl+Shift+]
完成语法				: Ctrl+E

搜索：
在当前文件搜索			: Ctrl+F
在多个文件搜索			: Ctrl+Shift+F
向后查找选中的内容			: Shift+F3
向前查找选中的内容			: Shift+F4
转到下一个匹配，配合Ctrl+F使用	: F3 或 F12
转到上一个匹配，配合Ctrl+F使用	: F4
跳转到指定行			: F5 或 Ctrl+G
查找符号				: F7

文件操作：
关闭文件				: Ctrl+W
关闭所有文件			: Ctrl+Shift+W
新建				:Ctrl+N
打开				: Ctrl+O
重新装载文件			: Ctrl+Shift+O
另存为				: Ctrl+Shift+S
显示文件状态			: Shift+F10
移除文件				: Alt+Shift+R
同步文件				: Alt+Shift+S
跳转到下一个文件			: Alt+,
跳转到上一个文件			: Alt+.

窗口操作：
全屏（Full Screen）			: F11
关闭窗口				: Alt+F6, Ctrl+F4
新窗口				: Alt+F5
选择下一个窗口			: F2,Ctrl+F6
选择前一个窗口			: Shift+F1
层叠窗口				: F6
放大缩小窗口			: Alt+F10, Ctrl+F10
排列语法窗口			: Alt+F7
激活语法窗口			: Alt+L
全屏（Full Screen）			: F11
关闭窗口				: Alt+F6, Ctrl+F4
新窗口				: Alt+F5
选择下一个窗口			: F2,Ctrl+F6
选择前一个窗口			: Shift+F1
层叠窗口				: F6
放大缩小窗口			: Alt+F10, Ctrl+F10
排列语法窗口			: Alt+F7
激活语法窗口			: Alt+L

退出程序				: Alt+F4

单词高亮：选中词，F8，取消高亮同理

### 打开文件窗口

不小心把文件窗口关了，打开方式

![image-20221011195419355](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011195419355.png)

这个也不小心叉掉了

![image-20221011195454548](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011195454548.png)

不要怕

![image-20221011195609066](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011195609066.png)



# 虚拟机

Ctrl + Alt  进入windows
Ctrl + G 进入虚拟机



# 命令行

root@Router:~# cat /etc/version 
H8922V40_APP_V7.2.2_SE_2104211653
root@Router:~# telnet 127.0.0.1

## 把代码编入工程：
1 新建文件夹，把.c放进去，从其他目录拷贝Makefile，修改Makefile 的头头，
2 修改/trunk/package/expand/hongdian/app路径下的Makefile ：添加目录
3 在trunk目录下执行命令：make hongdian

## 查看进程状态

```
ps  | grep snmp
cd /proc/26417
cat status 
9 ps | grep 1518
```

ps  | grep snmp

 cd /proc/26417
 cat status 
 ps | grep 1518

- 1 开启snmp服务

![image-20220929113837969](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220929113837969.png)

- 2 查看它的进程 ps | grep snmp

![image-20220929114104295](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220929114104295.png)

- 3 cd /proc/26417  cat status 

![image-20220929114330355](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220929114330355.png)

- 4 ps | grep 151

![image-20220929114436801](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220929114436801.png)

父进程是mp进程。

![image-20220929133505933](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220929133505933.png)

router(config)# service snmp
trap port 1231 

cat /tmp/hdconfig/cli.conf

## 编译整个文件

全部 编译./build.sh d V7.2.3
编译生成的app和boot在bin目录下

## 查看版本

后台：nvram show 
cli: show version

## RouterMP/QCTool获取注册码，将后面一段替换
http://172.16.8.57:5000/reg/a7a46d1e14b06f9289474541d8dbf308

- MP机器码为：262d3590765c5f76a3bad5ea6e132002

  cJb84cL4ZGb7ezW0 Y0zfDbb5a8J14XYw

- QC 
  aJe88cB0DCy3ebW0 F2cdFbb8f4B78GDc

## 端口开关

- 国内版本：

  swconfig dev switch0 port xxx set link disable on
   swconfig dev switch0 port xxx set link disable off

- 海外版本

  swconfig dev switch0 port 0 set disable 0
  swconfig dev switch0 port 0 set disable 1 
  swconfig dev switch0 set apply

- 查看网口

   swconfig dev switch0 show

- 修改网口速率

  swconfig dev switch0 port %d set link speed 10 duplex full

- 进入CLI修改端口

  service port
lan port %d on/off

## ## cli

### 登录**cli**方法 192.168.8.1

- 1 

  ```text
  root@router:~# telnet 127.0.0.1
  Entering character mode
  Escape character is '^]'.
  Router CLI
  User Access Verification
  Password: super
  router> en
  router# conf t 
  router(config)# 
  router# 
  ```

  2

- ```
  root@router:~# log_cli
  Entering character mode
  Escape character is '^]'.
  Router CLI
  User Access Verification
  Password: 
  router> en
  router# conf t
  router(config)# exit
  router# exit
  Connection closed by foreign host
  root@router:~#
  ```

  ### 操作
  
  conf t 进入全局
  
  ？：提示信息
  
  TAB ：操作提示
  
  ![image-20221010103213399](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221010103213399.png)

## 文件升级

boot、app

- 1 页面升级

- 2 TF卡升级

- 3 CFE升级

  - 断电时长按复位键，不要松开，插电，灯不停的闪烁，说明进入状态
  - 登录192.168.1.1升级文件

## 进程是否重新拉起

查看进程PID，看有没有变化

## 跳转到不同的终端

ALT + 数字键

![image-20221010101843227](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221010101843227.png)


- 
- 
- 
- 

  - 


#### ln命令

连接文件或目录。这里有两点要注意：第一，ln命令会保持每一处链接文件的同步性，也就是说，不论你改动了哪一处，其它的文件都会发生相同的变化；第二，ln的链接有[软链接](https://baike.baidu.com/item/软链接?fromModule=lemma_inlink)和[硬链接](https://baike.baidu.com/item/硬链接?fromModule=lemma_inlink)两种，软链接就是ln –s ** **，它只会在你选定的位置上生成一个文件的[镜像](https://baike.baidu.com/item/镜像?fromModule=lemma_inlink)，不会占用磁盘空间，硬链接ln ** **，没有参数-s， 它会在你选定的位置上生成一个和源文件大小相同的文件，无论是软链接还是硬链接，文件都保持同步变化。如果你用ls察看一个目录时，发现有的文件后面有一个@的符号，那就是一个用ln命令生成的文件，用ls –l命令去察看，就可以看到显示的link的路径了。

# 电脑快捷键

win+i 打开设置
win+l 快速锁屏
win+v打开剪贴板
win+m 最小化所有窗口
win+shift+s 局部截图 保存到剪贴板中

屏幕截图    Fn + windos + PrtSc   文件夹在图片
录屏	 Ctrl+Alt+s QQ快捷键   /E/录屏
定位到文档开头 ctrl + home  同理 结尾 ctrl + end

清除缓存 ctrl+F5

输入法半角/全角切换：shift + space 



### 输入法快速打印当前时间

打印首字母

- rq 日期

![image-20221013135801617](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221013135801617.png

![image-20221013135817852](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221013135817852.png)

- sj 时间

![image-20221013135948063](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221013135948063.png)

- xq 星期

  ![image-20221013140059446](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221013140059446.png)

# GIT

 vim test.txt 
  990  git diff .
  991  git add test.txt 
  992  git commit -m "更新test.txt"
  993  git branch
  994  git checkout -b feature-updateTest
  995  git branch
  996  git push origin feature-updateTest



命令行：

```
svn diff -  # 对比文件
svn updata - #更新文件
```

查看配置 git config -l
查看系统配置 git config --system --list
用户配置 git config --global --list

设置用户名邮箱
git config --global user.name "bhx"
$ git config --global user.email "2391712646@qq.com"



git branch 查看分支
git branch branch_name 创建分支
git checkout branch_name  切换分支
git branch -b branch_name 创建并切换到分支
git merge branch_name 把指定分支合并到当前分支上

删除分支命令

```
git branch -d (branchname)
```

 1114  git add .
 1115  git commit -m 'add 456'
 1116  git branch
 1117  git push origin feature-updateTest

- 查看远程分支

  ```text
  git branch -r
  ```

  

![image-20221011151113986](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221011151113986.png)

查看本地分支

```text
git branch
```

查看所有分支:本地和远程分支

```text
git branch -a 
```

拉取远程分支

 git branch -a
 git checkout odm-primetel-mqtt





### 新建分支

#### 1 复制链接

![image-20221024135123457](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221024135123457.png)

#### 2 选择分支，新建分支

![image-20221024135211788](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221024135211788.png)



选择框框位置，右击粘贴,回车

![image-20221024135632636](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221024135632636.png)

![image-20221024135833726](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221024135833726.png)

### 拉取某个分支

如果直接使用克隆的链接，下载的只能是develop分支的内容

```text
git clone git@172.16.8.42:router/H8922V65.git
```

 ![image-20221024141957588](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221024141957588.png)![image-20221024141845720](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221024141845720.png)





如果下载某个分支，使用以下命令: -b  指定分支

![image-20221024142101067](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221024142101067.png)

```c
git clone http://172.16.8.42/router/H8922V65.git -b  ODM-ZYWL
```

## 提交代码流程

### 1 命令行 

切到文件修改的目录

```
cd package/hongdian/
```



```c
git status .    //查看当前目录的文件状态
```

![image-20221026192337608](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221026192337608.png)

```c
git diff . //查看修改的地方
```

```c
git add .  //将当前目录下修改的文件上传，如果单个文件 git add .config
```

```c
git commit -m "中移平台对接功能OneCyberClient代码提交"
```

![image-20221026192827793](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221026192827793.png)

```c
git log //查看提交
```

![image-20221026192900180](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221026192900180.png)

```c
git checkout -b ODNM-ZY-commit  //新建一个分支上传
```

![image-20221026193043556](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221026193043556.png)

```c
 git push origin ODM-ZY-commit //上传到新建的分支
```

### 2 git 网页操作

![image-20221026193806622](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221026193806622.png)

![image-20221026193734093](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221026193734093.png)

记得勾选合并后删除该分支

![image-20221026193548954](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221026193548954.png)

 到这部后，就等待合并请求通过。



### 3 jenkins编版本

找到对应的分支

![image-20221026194003366](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221026194003366.png)



![image-20221026194037152](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221026194037152.png



![image-20221026194224939](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221026194224939.png)

2027  git diff .config
 2028  git branch
 2029  git status .
 2030  git diff warehouse/root/etc/init.d/done
 2031  git add .config 
 2032  cd package/hongdian/
 2033  git status .
 2034  git diff .
 2035  git status .
 2036  git add .
 2037  git commit -m "中移平台对接功能OneCyberClient代码提交"
 2038  git checkout -b ODM-ZY-commit
 2039  git log
 2040  git push origin ODM-ZY-commit

# SVN

## 提交代码流程

### 1 创建分支

找到基线程序，创建分支

![image-20221020140628688](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020140628688.png)

创建分支：

![image-20221020141515536](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020141515536.png)

创建好之后刷新，在目录下找到刚创建的分支

![image-20221020141645342](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020141645342.png)

show log:

![image-20221020141731388](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020141731388.png)

### 2 下载代码到本地

- 创建目录，目录名称：客户名称+版本号

  ![image-20221020142054323](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020142054323.png)

- 进入目录，下载代码

  ![image-20221020142140539](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020142140539.png)

- 在source insight建立工程

  ![image-20221020142510809](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020142510809.png)

  

### 3 提交前确认文件修改的地方

  

随机打开文件，随便写点啥

![image-20221020143938407](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020143938407.png)

打开本地目录，右键

![image-20221020144116341](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020144116341.png)

  

  ![image-20221020144151001](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020144151001.png)

  ![image-20221020144226906](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020144226906.png)

### 4  提交分支：

打开所在目录，右键

![image-20221020144802845](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020144802845.png)

![image-20221020144637456](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020144637456.png)

### 5 Jenkins编译

进入到相应目录

![image-20221020145118028](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020145118028.png)

![image-20221020145459626](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020145459626.png)

![image-20221020193830562](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020193830562.png)

版本V7.2.3_ANTUV1

##  命令

### 1 svn checkout(co)下载代码

命令行：

```c
svn checkout svn地址
```

查看代码：修改日志等

申请开通读的权限
http://172.16.8.9/Agile-Router/trunk/MTK7628/06_SRC/trunk
开启读写权限
http://172.16.8.9/Agile-Router/trunk/MTK7628/06_SRC/branches

![image-20221010151225158](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221010151225158.png)

### 2 svn status(st)

在提交你的文件到服务器之前，可以查看下有哪些文件变更。提交前查看本地文本和版本库里面的文件的区别

![image-20221020115238429](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221020115238429.png)

- 第一列的显示的是本地文件与版本库文件的差异状态。

```c
[url=]  L    abc.c               # svn已经在.svn目录锁定了abc.c
M      bar.c               # bar.c的内容已经在本地修改过了
X      3rd_party           # 这个目录是外部定义的一部分
?      foo.o               # svn并没有管理foo.o
!      some_dir            # svn管理这个，但它可能丢失或者不完整
~      qux                 # 作为file/dir/link进行了版本控制，但类型已经改变
I      .screenrc           # svn不管理这个，配置确定要忽略它
A  +   moved_dir           # 包含历史的添加，历史记录了它的来历
M  +   moved_dir/README    # 包含历史的添加，并有了本地修改
D      stuff/fish.c        # 这个文件预定要删除
A      stuff/loot/bloo.h   # 这个文件预定要添加
C      stuff/loot/lump.c   # 这个文件在更新时发生冲突
R      xyz.c               # 这个文件预定要被替换
S  stuff/squawk        # 这个文件已经跳转到了分
```

#### 4 svn命令行提交

svn status

svn add 文件

svn commit -m 'review:678 修改链接文件' 

 ln -s ifup ifdown

### 编译权限

每个版本的编译方法不一样，查找方法：

jenkins -> 控制台输出

代码下载完成后面

![image-20221025083906402](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221025083906402.png)

make -j1 V=s

H8922V65的代码是在另一个平台，编译时才从其他地方拷贝过来。

#### 查看版本号

 /etc/version 

![image-20221025091249391](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221025091249391.png)

# other

### tcp笔记

tcpserver实现的功能：多个客户端连接；客户端连接后，服务端向客户端发送连接成功信息；服务端返回客户端发送的信息；接收客户端断开的信息；

client：可以向服务端发送信息；接收服务端断开的信息。

- 1 在app目录下新建文件夹：tcp_server ：

```c
~/trunk/package/expand/hongdian/app/tcp_server
    server1.c  Makefile
```

在Make file文件中注意这句CFLAGS += -DBIN_VERSION=\"$(COMPILE_PATCH_VERSION)\"，与server1.c中hd_show_process_version(argc, argv, BIN_VERSION);有关，提示找不到文件。

- 2 app目录下的Make file文件中加入路径：subdir_common += tcp_server

- 3 增加cli字段

  参考：

  ![image-20221010150913844](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221010150913844.png)

  *_conf.c /.h文件用于命令定义

  hd_cli.c :hong dian cli init interface 声明

  command.c 基础命令

  增加mp配置，参考

  ![image-20221010150946130](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221010150946130.png)

- tcpserver 进程由1号进程拉起，应该为mp进程拉起才对，解决由1号进程拉起：在tcpserver文件中加入：main函数的第一个位置加上hd_show_process_version(argc, argv, BIN_VERSION);

  mp拉起程序，process_manage.h中mp结构体加入

  ![image-20221012194542213](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221012194542213.png)

  去.c 文件中

  ![image-20221012194631181](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221012194631181.png)

  处理mp_options.c

![image-20221008164407373](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221008164407373.png)

![image-20221008164429263](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221008164429263.png)

- 升级出现不断重启的现象，先升级boot.

- 查看进程拉起状态

``` 
cat /var/log/kernel
```

![image-20221008165047359](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221008165047359.png)

0 说明进程关闭，1进程开启，-1表示没从cli中识别到相关字样（mp/mp_option.c）

![image-20221008171642965](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221008171642965.png)

0：检查配置文件，有返回0 ，无返回-1

1：检查到有server字符

2：检查到shutdown字符

- tcp 端口号改变，mp重新拉起进程

  cli检查配置文件的port修改（通过命令），然后告诉mp重启tcpserver进程，进程读取配置的port、监听客户端的连接。

  ![image-20221010110532667](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221010110532667.png)
  
  ![image-20221010110447751](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221010110447751.png)

#### 10.9 添加的tcp修改端口代码

- cli_api.h

  ![image-20221009111603346](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221009111603346.png)

  ![image-20221009104923346](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221009104923346.png)

- cli_api.c

  ![image-20221009105228969](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221009105228969.png)

- 打印print问题

## 9月份的测试笔记

1、升级版本：
国内：廖显锋：H8922V40/H8951/H7920/  H8850/H8922V60  http://172.16.2.8/biz/doc-view-5909.html
国外：包海欣：H8922V40//H8951/  H7960/H8953    http://172.16.2.8/biz/doc-view-4957.html
2、陪测设备程序V65升级，升级时要勾选恢复出厂按钮：http://172.16.8.9/version-router/test/Router/OPENSDT-H8922V65/V7.8.0-T1_netPortTest/2022-09-14_09-41-34/
3、搭建环境：将待测设备网线接入陪测设备（陪测端从最左边WAN口开始依次接入）
4、生产工具测试
5、验收工具测试
6、编写测试报告

需要注意的点：
1、重点测试网口速率，初始化等基础功能过一遍
2、遍历WAN/LAN口基本功能（DHCP、静态）；端口全获取和端口部分获取
3、异常场景测试



nvram show

![image-20221013153838244](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221013153838244.png)

swconfig dev switch0 show

查看端口状态

![image-20221013173246238](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221013173246238.png)

设置wan设置消失

nvram set wan_lice 0

![image-20221013153941066](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221013153941066.png)

## 阅读笔记

- 1  匹配配置文件中的字符串

fopen打开文件，获取文件指针，判断指针是否为空
fgets 循环读取一行：判断文件结尾、判断是否为空行或“！”、判断是否有匹配的字符串

- 2 

  从配置文件中查找相关的字符

  先找到某个service对应的信息，再从信息里找到匹配的字符。

  ![image-20221010173009509](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221010173009509.png)