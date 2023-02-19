

[TOC]



# C

## extern关键字

一般用在变量名前或函数名前，作用是用来说明“**此变量/函数是在别处定义的，要在此处引用**”





sourceinsight 怎么跳转到头文件
查找 

## 函数

### 字符串操作

#### strncpy

#### strstr

- 功能

  查找子字符串

- 格式

```c
#include <string.h>
char *strstr(const char *str1, const char *str2)
```



- 返回值

  成功：返回值为char * 类型（ 返回指向 *str1* 中第一次出现的 *str2* 的指针）；

  失败：如果 *str2* 不是 *str1* 的一部分，则返回空指针。

#### sscanf

- 功能

  sscanf通常被用来解析并转换字符串，其格式定义灵活多变，可以实现很强大的字符串解析功能。

- 格式

  ```c
  #include <stdio.h>
  int sscanf(const char *str, const char *format, ...);
  ```

  str:待解析的[字符串](https://so.csdn.net/so/search?q=字符串&spm=1001.2101.3001.7020);

  format:字符串格式描述;

  其后是一序列数目不定的指针参数，存储解析后的数据.？

- 返回值

  成功：返回公共转换的个数

- 相关链接

  [(24条消息) sscanf函数使用详解_faihung的博客-CSDN博客_sscanf](https://blog.csdn.net/faihung/article/details/119325390)

#### snprintf

- 格式

  ```c
  int snprintf(char *str, size_t size, const char *format, ...)
  ```

- 两点注意：

  (1) 如果格式化后的字符串长度 < size，则将此字符串全部复制到str中，并给其后添加一个字符串结束符('\0')；

  (2) 如果格式化后的字符串长度 >= size，则只将其中的(size-1)个字符复制到str中，并给其后添加一个字符串结束符('\0')，返回值为欲写入的字符串长度。
  不必担心缓冲区溢出

- 返回值

  返回值是欲写入的字符串长度，而不是实际写入的字符串度

  ```c
  char buf[8];
  int n = snprintf(buf, 5, "abcdefghijk");
  printf("n %d    buf %s\n", n, buf);
   
  运行结果为：
  n 10     buf abcd
  欲写入："abcdefghijk"
  ```

  

  if （ n < 0） : snprintf出错了
  if ( n >0 && n < sizeof(buf) ) : snprintf成功，并且格式了完成的字符串。
  if ( n >= sizeof(buf) ) : snprintf成功，但要格式化的字符串被截断了

#### strncpy

- 功能

  拷贝src[字符串](https://so.csdn.net/so/search?q=字符串&spm=1001.2101.3001.7020)的前n个字符至dest

- 格式

  ```c
   char *strncpy(char *dest, const char *src, int n)
  ```

  

### fopen

- 功能

  fopen() 会获取文件信息，包括文件名、文件状态、当前读写位置等，并将这些信息保存到一个 FILE 类型的结构体变量中，然后将该变量的地址返回。

- 格式

```c
FILE *fopen(char *filename, *type);
```

fopen()函数中第一个形式参数表示文件名, 可以包含路径和文件名两部分

第二个形式参数表示打开文件的类型
| "r"  | 以“只读”方式打开文件。只允许读取，不允许写入。文件必须存在，否则打开失败。 |
| ---- | ------------------------------------------------------------ |
| "w+" | 以“写入/更新”方式打开文件，相当于`w`和`r+`叠加的效果。既可以读取也可以写入，也就是随意更新文件。如果文件不存在，那么创建一个新文件；如果文件存在，那么清空文件内容（相当于删除原文件，再创建一个新文件）。 |
| "a" | 增补, 如果文件不存在则创建一个                               |



- 返回值：

打开文件不成功时，fopen() 将返回一个空指针，也就是 NULL

成功：fopen() 会获取文件信息，包括文件名、文件状态、当前读写位置等，并将这些信息保存到一个 FILE 类型的结构体变量中，然后将该变量的地址返回。

### strcmp

- 返回值

  （1）两个字符串相同，ASCII码值相同，返回值是0。

  （2）第1个字符串在第2个字符串之前，说明第1个字符串ASCII值小于第2个字符串，返回负值。

  （3）第1个字符串在第2个字符串之后。说明第1个字符串ASCII值大于第2个字符串，返回正值。

### fclose()函数

  fclose()函数用来关闭一个由fopen()函数打开的文件 , 其调用格式为:

```scss
      int fclose(FILE *stream);
```

该函数返回一个整型数。当文件关闭成功时, 返回0,　否则返回一个非零值。可以根据函数的返回值判断文件是否关闭成功。

```c
static int check_wlan()
{
    int ret = G3_ERROR;
    FILE *fp;
    char line[512] = {0};
    char *pline = NULL;

    if (NULL != (fp = fopen("/proc/net/dev", "r")))
    {
        while (NULL != fgets(line, sizeof(line), fp))
        {
            pline = strstr(line, "wlan");
            if (NULL == pline)
            {
                if (0 != feof(fp))
                    break;
                else
                    bzero(line, sizeof(line));
                continue;
            }
            else
            {
                ret = G3_SUCCEED;
                break;
            }
        }
        fclose(fp);
    }

    return ret;
}
```



### fgets

```c
# include <stdio.h>
char *fgets(char *s, int size, FILE *[stream];
```

- 功能

从 stream 流中读取 size 个字符存储到字符指针变量 s 所指向的[内存](https://so.csdn.net/so/search?q=内存&spm=1001.2101.3001.7020)空间.

其中：s 代表要保存到的内存空间的首地址，可以是字符数组名，也可以是指向字符数组的字符指针变量名。size 代表的是读取字符串的长度。stream 表示从何种流中读取，可以是标准输入流 [stdin](https://so.csdn.net/so/search?q=stdin&spm=1001.2101.3001.7020)，也可以是文件流.

- 返回值：

返回值是一个指针，指向字符串中第一个字符的地址

函数成功将返回stream，失败**或**读到文件结尾返回NULL。因此不能直接通过fgets的返回值来判断函数是否是出错而终止的，应该借助feof函数或者ferror函数来判断。



1.sizeof()作用在字符串上不记结尾\0。也就是返回除去结尾\0后的长度。

2.sizeof()作用在数组上是数组的实际长度，无论数组里面元素是否赋值，结果都是数组长度。

3.fgets()给字符数组赋值的时候，会把末尾的回车键也放入到字符数组中（前提是有地方放），字符数组最后一个字符一定是\0补充。

```c
static int check_wlan()
{
    int ret = G3_ERROR;
    FILE *fp;
    char line[512] = {0};
    char *pline = NULL;

    if (NULL != (fp = fopen("/proc/net/dev", "r")))//判断文件是否打开成功
    {
        while (NULL != fgets(line, sizeof(line), fp))
        {
            pline = strstr(line, "wlan");
            if (NULL == pline)
            {
                if (0 != feof(fp))//文件是否结束
                    break;
                else
                    bzero(line, sizeof(line));
                continue;
            }
            else
            {
                ret = G3_SUCCEED;
                break;
            }
        }
        fclose(fp);
    }

    return ret;
}
```



### feof

feof()是检测流上的文件结束符的函数，如果文件结束，则返回非0值，文件不为空，返回0

一般在文件操作，中经常使用feof()判断文件是否结束

工作原理是，站在光标所在位置，向后看看还有没有字符。

- 返回值

  如果有，返回0；如果没有，返回非0。它并不会读取相关信息，只是查看光标后是否还有内容。

### DEFUN

![image-20221010114130988](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221010114130988.png)





### memset

memset初始化是以一个字节为单位的，也即是说对[字符数组](https://so.csdn.net/so/search?q=字符数组&spm=1001.2101.3001.7020)才能初始化为任意值

### ioctlsocket() 

控制套接口的模式

 \#include <winsock.h>

 int PASCAL FAR ioctlsocket( SOCKET s, long cmd, u_long FAR* argp);

 s：一个标识套接口的描述字。
 cmd：对套接口s的操作命令。
 argp：指向cmd命令所带参数的指针

返回值：
 成功后，ioctlsocket()返回0。否则的话，返回SOCKET_ERROR错误，应用程序
可通过WSAGetLastError()获取相应错误代码。

### excel函数

exec用被执行的程序完全替换调用它的程序的影像。fork创建一个新的进程就产生了一个新的PID，exec启动一个新程序，替换原有的进程，因此这个新的被exec执行的进程的PID不会改变，和调用exec函数的进程一样。

### popen 函数

- 功能

  popen()会调用fork()生成子进程，在子进程中调用/bin/sh -c来执行参数command的指令

  利用system函数调用shell命令，只能获取到shell命令的返回值，而不能获取shell命令的输出结果，那如果想获取输出结果怎么办呢？用popen函数可以实现。

- 格式

  ```c
  #include <stdio.h>
  FILE * popen(conste char * command, const char * type);
  ```

  type:可使用“r”或者"w",分别代表读取及写入，但由于popen是以创建管道的方式创建进程连接到子进程的标准输出设备或标准输入设备，因此其带有管道的一些特性，同一时刻只能定义为写或者读。

- 返回值

  文件指针，函数执行成功返回文件指针，否则返回NULL。错误原因存于errno 中.

- 注意

  只能用pclose函数进行关闭操作，不能用fclose。

### bzero

  ```c
  #include <string.h>
  void bzero(void *s, int n);
  ```

将参数s 所指的内存区域前n 个字节全部设为零

### atol

```c
#include <stdlib.h>
long atol(const char *str);//可用于将 char 字符串转为 long 长整数类型
```

函数说明 atoi()会扫描参数nptr字符串，跳过前面的空格字符，直到遇上数字或正负符号才开始做转换，而再遇到非数字或字符串结束时('\0')才结束转换，并将结果返回

str: 字符串

成功返回转换后的长整数，如果没有执行有效的转换，则返回零。

### memset

### calloc

```c
#include <stdlib.h>
void* calloc(size_t num ,size_t size)
```

也是在堆区申请动态内存空间,size_t num为元素个数，size_t size为每个元素的字节大小

- calloc与malloc的区别

1.参数的使用方式不同
malloc(单位：字节)：malloc(10 * sizeof(int));或malloc(40)
calloc:calloc(10 , sizeof(int))
2.malloc的使用效率较高，因为calloc在返回在堆区申请的那块动态内存的起始地址之前，会将每个字节都初始化为0
（4）与malloc函数的区别：malloc 函数是动态分配一段存储空间，而calloc函数是动态分配连续的存储空间

### vfork

vfork的特点 — 创建子进程：
①子进程必定先运行，等到子进程调用exec（进程替换） 或 exit（退出进程）后，父进程才能运行
②父子进程共享空间（共享[内存](https://so.csdn.net/so/search?q=内存&spm=1001.2101.3001.7020)数据）
fork 是 创建一个子进程，并把父进程的内存数据copy到子进程中。父子进程谁先运行是随机的。

成功：子进程中返回 0，父进程中返回子进程 ID。pid_t，为无符号整型。

失败：返回 -1

用 vfork() 创建进程，子进程里一定要调用 exec（进程替换） 或 exit（退出进程），否则，程序会出问题，没有意义。

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
 
int main(int argc, char *argv[])
{
	pid_t pid;
	
	pid = vfork();	// 创建进程
	if(pid < 0){ // 出错
		perror("vfork");
	}
	
	if(0 == pid){ // 子进程
		sleep(3); // 延时 3 秒
		printf("i am son\n");
		
		_exit(0); // 退出子进程，必须
	}else if(pid > 0){ // 父进程
		
		printf("i am father\n");
	}
	
	return 0;
}
```

### **_exit()函数**

原型如下所示：

```c
#include <unistd.h>
void _exit(int status);
```

exit()函数_exit()函数都是用来终止进程的，exit()是一个标准 C 库函数，而_exit()和_Exit()是系统调用

### waitpid()

明确概念

- 进程状态

  从程序员的角度，我们可以认为进程总是处于下面三种状态之一：

  （1）运行。进程要么在CPU上执行，要么在等待被执行且最终会被内核调度。

  （2）停止。进程的执行被挂起（suspended），且不会被调度。当收到SIGSTOP、SIGTSTP、SIGTTIN或者SIGTTOU信号时，进程就停止，并且保持停止直到他收到一个SIGCONT信号，在这个时刻，进程再次开始运行。

  （3）终止。进程永远的停止了。进程会因为三种原因终止：第一、收到一个信号，信号的默认行为是终止进程。第二、从主程序返回。第三、调用exit函数

- 回收子进程

  进程终止，内核并不是立即把它从系统中清除，而是保持在已终止的状态，直到被它的父进程回收(reaped)；

  父进程回收：内核：将子进程的退出状态传递给父进程，然后抛弃已终止的进程；

  僵死进程 (zombie)：终止了但还未被回收的进程

  孤儿进程：回收前，他的父进程终止了

  - 一个进程可以通过调用 waitpid 函数来等待它的子进程终止或者停止。

- waitpid

  pid_t waitpid (pid_t pid, int* statusp, int options);
  返回 :如果成功，则为子进程的PID，如果options为WNOHANG，则返回0，如果发生其他错误，则返回-1

### **access**

**判断用户是否具有访问某个文件的权限(或判断某个文件是否存在).**

```c
#include<unistd.h>
 int access(const char *pathname,int mode)
```

pathname:表示要测试的文件的路径
         mode:表示测试的模式可能的值有:
         R_OK:是否具有读权限
         W_OK:是否具有可写权限
         X_OK:是否具有可执行权限
         F_OK:文件是否存在

返回值:若是则返回0,否则返回-1
### remove

删除文件

```c
int remove(char *filename);
```

成功则返回0，失败则返回-1，错误原因存于errno。

1 秒=1000 毫秒

1毫秒 = 1000微秒

### gettimeofday()

得到时间。它的精度可以达到微妙

```c
#include<sys/time.h>

int gettimeofday(struct  timeval*tv,struct  timezone *tz )
```

gettimeofday()会把目前的时间用tv 结构体返回，当地时区的信息则放到tz所指的结构中

```c
struct timeval
{
__time_t  tv_sec;        /* Seconds. */
__suseconds_t  tv_usec;  /* Microseconds. */
};
```

### inet_ntop 和 inet_pton()

对于IPv4地址和IPv6地址都适用，函数中p和n分别代表表达（presentation)和数值（numeric)

- **inet_ntop**

功能：将IPv4或IPv6 Internet网络地址转换为 Internet标准格式的字符串。

```c
#include <sys/types.h>
#include <sys/socket.h>
#include <arpa/inet.h>
int inet_pton(int af, const char *src, void *dst);
```

这个函数转换字符串到网络地址，第一个参数af是地址族，转换后存在dst中

返回值：
1.若无错误发生，则inet_pton()返回1，pAddrBuf参数执行的缓冲区包含按网络字节顺序的二进制数字IP地址。
2.若pAddrBuf指向的字符串不是一个有效的IPv4点分十进制字符串或者不是一个有效的IPv6点分十进制字符串，则返回0。否则返回-1。
3.可以通过WSAGetLastError()获得错误错误代码[^2]。

- **inet_pton()**

功能：将**标准文本表示形式**的IPv4或IPv6 Internet网络地址**转换为数字二进制形式**。

```
#include <sys/types.h>
#include <sys/socket.h>
#include <arpa/inet.h>
const char *inet_ntop(int af, const void *src, char *dst, socklen_t cnt);
//这个函数转换网络二进制结构到ASCII类型的地址，参数的作用和上面相同，只是多了一个参数socklen_t cnt,
//他是所指向缓存区dst的大小，避免溢出，如果缓存区太小无法存储地址的值，则返回一个空指针，并将errno置为ENOSPC
```

返回值：
1.若无错误发生，Inet_ntop()函数返回一个指向缓冲区的指针，该缓冲区包含标准格式的IP地址的字符串表示形式。
2.否则返回NULL
3.获取错误码：WSAGetLastError()

 

- struct in_addr

  ```c
  struct in_addr 
  {
    in_addr_t s_addr;
  };
  
  //表示一个32位的IPv4地址。
  //in_addr_t一般为32位的unsigned int，其字节顺序为网络字节序，即该无符号数采用大端字节序。
  ```

  

  - struct hostent

    ```c
    struct hostent
    {
        char *h_name;  //主机名，即官方域名
        char **h_aliases;  //主机所有别名构成的字符串数组，同一IP可绑定多个域名
        int h_addrtype; //主机IP地址的类型，例如IPV4（AF_INET）还是IPV6
        int h_length;  //主机IP地址长度，IPV4地址为4，IPV6地址则为16
        char **h_addr_list;  /* 主机的ip地址，以网络字节序存储。若要打印出这个IP，需要调用inet_ntoa()。*/
    };
    ```


### 类型转换函数 

#### 1. atoi

把一个[字符串](https://so.csdn.net/so/search?q=字符串&spm=1001.2101.3001.7020)转换成一个整型数据

```c
#include  < stdlib.h >  
int atoi(const char *nptr);
```

注意：**转化时跳过前面的空格字符，直到遇上数字或正负符号才开始做转换，而再遇到非数字或字符串结束时(’/0’)才结束转换，并将结果返回**。

```c
int main()
{
    char *ptr1 = "-12345.12";
    char *ptr2 = "+1234w34";
    char *ptr3 = "   456er12";
    char *ptr4 = "789 123";
    int a,b,c,d;

    a = atoi(ptr1);
    b = atoi(ptr2);
    c = atoi(ptr3);
    d = atoi(ptr4);

 printf("a = %d, b = %d, c = %d, d = %d\n", a,b,c,d);
    return 0;
}
```

> 结果： a = -12345, b = 1234, c = 456, d = 789

#### 2. itoa

把整型数字转换成字符串存储在数组中

char *itoa( int value, char *string, int radix);

itoa(整型数据，目标字符串，**进制**)

```c
	int b = 25;
	char buf[32] = {0};
	itoa(b, buf, 2);
	printf("buf = %s\n", buf);
```

结果：![image-20221022162636478](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221022162636478.png)

但无法显示有效数位前面的0

b = -25时

![image-20221022164846523](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221022164846523.png)

### getopt

命令行参数解析函数

- 命令行参数各组成部分的名称:

  ![img](https://img-blog.csdn.net/20180126161602436?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYzE1MjM0NTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

  命令行参数由Command name，Option，Option argument 以及Operands组成

```c
#include <unistd.h>  
int getopt(int argc, char * const argv[], const char *optstring);  
```

getopt函数的返回值：char类型的参数所对应的int值，比如`-b 100`，getopt函数返回的就是字符`ｂ`对应的int值

```c
void hd_show_process_version(int argc, char *argv[], char *ver)
{
    int ret = 0;

    if (!ver)
        return;
    if (argc < 2)
        return;
    ret = getopt(argc, argv, "v");//
    if (ret >= 0){
        switch(ret){
            case 'v':
                printf("%s\n", ver);
                exit(0);
                break;
            default:
                break;
        }
    }

    return;
}
```

### errno

- stdlib.h头文件

  stdlib.h[头文件](https://baike.baidu.com/item/头文件/10978258)即standard library标准[库函数](https://so.csdn.net/so/search?q=库函数&spm=1001.2101.3001.7020)头文件,包含了[C](https://baike.baidu.com/item/C/7252092)、[C++](https://baike.baidu.com/item/C++/99272)语言的最常用的[系统函数](https://baike.baidu.com/item/系统函数)，该文件中还包含了C语言标准[库函数](https://baike.baidu.com/item/库函数)的定义。

- errno宏在stdlib.h中的定义为

  ```cpp
  #define errno (*_errno())//_error()返回类型为指针  int 
  ```

  errno宏用于保存程序在运行中的错误代码（error code），以及用于显示错误信息的字符串。当程序运行时，errno宏被设置为0，一旦程序发生了系统级的错误，errno宏就会被设置为其它值。

- strerror()函数

  可以通过strerror()函数获取该错误索引号对应的错误信息。strerror()函数在string.h头文件中定义，其格式为

  char *strerror( int errnum );

  其中，参数errnum是errno宏获取的错误索引号，该函数的返回值是错误信息。

- perror()函数

  perror()函数显示标准错误输出流stderr中的错误信息，该函数的格式为：

  ```cpp
  void perror( const char *message );
  ```

### isspace函数



```c
#include <ctype.h>
extern int isspace（int c）
```

  功能：判断字符c是否为空白符

  返回值：当c为空白符时，返回非零值，否则返回零。

​				（空白符指空格、水平制表、垂直制表、换页、回车和换行符。）

char *strdup(char *str)；

```c
char * __strdup (const char *s)
{
size_t len =strlen (s) + 1;
void *new =malloc (len);
if (new == NULL)
return NULL;
return (char *)memcpy (new, s, len);
}
```

实例：

```c
//C/C++ code
#include <stdio.h>
#include <string.h>
#include <alloc.h>
int main(void)
{
char *dup_str,*string = "abcde";
dup_str =strdup(string);
      printf("%s\n", dup_str);free(dup_str); return 0;
}
```





### strdup

拷贝[字符串](https://so.csdn.net/so/search?q=字符串&spm=1001.2101.3001.7020)s的一个副本，由函数返回值返回，这个副本有自己的内存空间，和s不相干

##  静态库和动态库

- 什么是库，库(Library)说白了就是一段编译好的[二进制](https://so.csdn.net/so/search?q=二进制&spm=1001.2101.3001.7020)代码，加上头文件就可以供别人使用

- 什么时候我们会用到库：

  - 一种情况是某些代码需要给别人使用，但是我们不希望别人看到源码，就需要以库的形式进行封装，只暴露出头文件
  - 另外一种情况是，对于某些不会进行大的改动的代码，我们想减少编译的时间，就可以把它打包成库，因为库是已经编译好的二进制了，编译的时候只需要 Link 一下，不会浪费编译时间

- Link 的方式有两种，静态和动态，于是便产生了静态库和动态库

  #### 先了解可目标文件

  - 目标文件常常按照特定格式来组织，在linux下，它是**ELF**格式（Executable Linkable Format，可执行可链接格式），而在windows下是PE（Portable Executable，可移植可执行）
  - 而通常目标文件有三种形式
    - 可执行目标文件即我们通常所认识的，可直接运行的二进制文件
    - 可重定位目标文件包含了二进制的代码和数据，可以与其他可重定位目标文件合并，并创建一个可执行目标文件
    - 共享目标文件它是一种在加载或者运行时进行链接的特殊可重定位目标文件

  #### 静态库即静态链接库

  （Windows 下的 .lib，Linux 和 Mac 下的 .a）（archive）

  静态库在编译的时候会被直接拷贝一份，复制到目标程序里，这段代码在目标程序里就不会再改变了
  静态库的好处很明显，编译完成之后，库文件实际上就没有作用了目标程序没有外部依赖，直接就可以运行当然其缺点也很明显，就是会使用目标程序的体积增大

  - 静态链接构建我们的可执行文件：

    ```text
    gcc -c main.c //预处理、编译、汇编、但不连接，生成的文件叫可重定位目标文件main.o
    gcc -static -o main main.o -lm
    ```

  第二条命令的static参数，告诉链接器应该使用静态链接，-lm参数表明链接libm.a这个库（类似的，如果要链接libxxx.a,使用-lxxx即可）

  - 特别注意，必须把-lm放在后面。放在最后时它是这样的一个解析过程：
    - 链接器从左往右扫描可重定位目标文件和静态库
    - 扫描main.o时，发现一个未解析的符号exp，记住这个未解析的符号
    - 扫描libm.a，找到了前面未解析的符号，因此提取相关代码
    - 最终没有任何未解析的符号，编译链接完成

  #### 动态库即动态链接库

  （Windows 下的 .dll，Linux 下的 .so，Mac 下的 .dylib）

  与静态库相反，动态库在编译时并不会被拷贝到目标程序中，目标程序中只会存储指向动态库的引用等到程序运行时，动态库才会被真正加载进来
  动态库的优点是，不需要拷贝到目标程序中，不会影响目标程序的体积，而且同一份库可以被多个程序使用（因为这个原因，动态库也被称作共享库）同时，编译时才载入的特性，也可以让我们随时对库进行替换，而不需要重新编译代码动态库带来的问题主要是，动态载入会带来一部分性能损失，使用动态库也会使得程序依赖于外部环境如果环境缺少动态库或者库的版本不正确，就会导致程序无法运行（Linux 下喜闻乐见的 lib not found 错误）

  - 连接动态库

    ```text
    $ gcc -o main main.c -lm  #默认使用的是动态链接
    ```

​    	通过ldd命令来观察可执行文件链接了哪些动态库

```text
    $ ldd main
    linux-vdso.so.1 =>  (0x00007ffc7b5a2000)
    libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007fe9642bf000)
    libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007fe963ef5000)
    /lib64/ld-linux-x86-64.so.2 (0x00007fe9645c8000)
```

参考：[(10条消息) linux下生成静态库和动态库_枯藤闲画云的博客-CSDN博客](https://blog.csdn.net/qq_39584315/article/details/80311454)



linux为什么亦那么操作系统：redhat、ubuntu、openwrt等，有什么区别？

看懂Makefile文件。

### 函数的声明



##  多线程

线程并发，资源抢夺，

## 进程 

![image-20221010155734806](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221010155734806.png)

```text
PID：进程的ID编号
VSZ：该进程的虚拟内存的大小，单位KB（将磁盘的一部分空间转为虚拟内存使用，在物理内存使用占满后才会用到）
STAT：进程状态。R:运行、S:睡眠、T:停止、s:包含子进程、+:位于后台
```



## 枚举类型

- 定义形式为

```c
enum typeName{ valueName1, valueName2, valueName3, ...... };
```

枚举值默认从 0 开始，往后逐个加 1（递增）;或者每个名字都指定一个值;第一个名字指定值，后面从该值开始递增；

- 枚举是一种类型，通过它可以定义枚举变量：

  ```c
  enum week a, b, c;
  
  enum week{ Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun } a, b, c;
  ```

- 赋值

  ```c
  enum week{ Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun };
  enum week a = Mon, b = Wed, c = Sat;
  enum week{ Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun } a = Mon, b = Wed, c = Sat;
  ```

- 枚举和宏其实非常类似：宏在预处理阶段将名字替换成对应的值，枚举在编译阶段将名字替换成对应的值。

- 不占用数据区（常量区、全局数据区、栈区和堆区）的内存，而是直接被编译到命令里面，放到代码区，所以不能用`&`取得它们的地址。这就是枚举的本质

  

## 编译器内置宏

```text
__DATE__ 当前日期，一个以 “MMM DD YYYY” 格式表示的字符串常量。

__TIME__ 当前时间，一个以 “HH:MM:SS” 格式表示的字符串常量。

__FILE__ 这会包含当前文件名，一个字符串常量。

__LINE__ 这会包含当前行号，一个十进制常量。

__STDC__ 当编译器以 ANSI 标准编译时，则定义为 1；判断该文件是不是标准 C 程序。
```

## int/long/unsigned long 区别

整形，分类两类，一种是有符号的(正数/负数)，一种是无符号的(默认是大于等于零)；

####  char 和 unsigned char 的区别

在C中，默认的基础数据类型均为signed，如定义变量为int，long等，都为有符号的。如果要定义无符号类型，必须显式地在变量类型前加unsigned。

## 位移运算符 <<   |=

1<<４：１的二进制左移４位

左移1位：００００　０００１　＝＞　００００　０ 0 1 0   2

左移２位：００００　０００１　＝＞　００００　０１００　　４

左移４位　００００　０００１　＝＞　０００１　００００　１６



记忆： 2 4 8 16 32 分别由1左移了

​			1 2 3 4  5



### 位运算符

⼆进制规则进⾏运算

| 与             | 或   | ⾮   | 异或 |
| -------------- | ---- | ---- | ---- |
| &              | \|   | ~    | ^    |
| 对应位有0则为0 |      |      |      |

？&本身 等于本身

？&5 = 5

#### ~~~~ **1**~1 ~

0000 0**1**0**1**  含1的对应位一样，其他位置随意

=

0000 0101

- 

## 编程中

- .h文件有修改，最好清除文件make clean重新编译
- 函数参数有指针要判空，因为不能操作空指针。

## 返回值为 void *

所有void*的意思是可以被强制类型转换成任何类型的指针，例如内存分配函数 malloc 函数返回的指针就是 void * 型，用户在使用这个指针的时候，要进行强制类型转换

## 函数指针和函数指针

#### 1. 指针函数

- 什么是函数指针

  如果在程序中定义了一个函数，那么在编译时系统就会为这个函数代码分配一段存储空间，这段存储空间的首地址称为这个函数的地址。而且函数名表示的就是这个地址。既然是地址我们就可以定义一个指针变量来存放，这个指针变量就叫作函数指针变量，简称函数指针。

- 定义

  函数返回值类型 (* 指针变量名) (函数参数列表)

  ```c
  int(*p)(int, int);
  ```

  定义了一个指针变量 p，该指针变量可以指向返回值类型为 int 型，且有两个整型参数的函数。p 的类型为 int(*)(int，int)。函数参数列表”表示该指针变量可以指向具有什么参数列表的函数。这个参数列表中只需要写函数的参数类型即可。

  那么怎么判断一个指针变量是指向变量的指针变量还是指向函数的指针变量呢？首先看变量名前面有没有“*”，如果有“*”说明是指针变量；其次看变量名的后面有没有带有形参类型的圆括号，如果有就是指向函数的指针变量，即函数指针，如果没有就是指向变量的指针变量

  ```c
  # include <stdio.h>
  int Max(int, int);  //函数声明
  int main(void)
  {
      int(*p)(int, int);  //定义一个函数指针
      int a, b, c;
      p = Max;  //把函数Max赋给指针变量p, 使p指向Max函数
      printf("please enter a and b:");
      scanf("%d%d", &a, &b);
      c = (*p)(a, b);  //通过函数指针调用Max函数
      printf("a = %d\nb = %d\nmax = %d\n", a, b, c);
      return 0;
  }
  int Max(int x, int y)  //定义Max函数
  {
      int z;
      if (x > y)
      {
          z = x;
      }
      else
      {
          z = y;
      }
      return z;
  }
  ```

- **typedef函数指针**

  通常：

  ```c
  int(*p)(int, int);  //定义一个函数指针
  p = Max;  //把函数Max赋给指针变量p, 使p指向Max函数
  c = (*p)(a, b);  //通过函数指针调用Max函数
  ```

  那么，我想用函数指针p指向Max函数，另一个相同的函数指针p指向Min函数，怎么办呢，在定义一个函数指针？

  int(*p1)(int, int);  //定义一个函数指针

  p1 = Min(a,b)

  这有点麻烦，所以使用另一种方法：

  定义了一个函数指针**类型**之后，就可以通过这个函数指针**类型**来定义函数指针

  ```c
  typedef int(*p)(int,int);//定义个函数指针类型
  p a ,b ;//声明函数指针变量a，b
  a = Max;//a指向Max函数
  b = Min;//指向Min函数
  ```

  

  

  

#### 2. 指针函数

指针函数的落脚点是一个函数，这个函数的返回值是一个指针，与普通函数int function(int，int)类似，只是返回的数据类型不一样而已。

_type_ *function(int, int) 

区别看类型后面的*号有没有被括号包含进去。

## 信号

#### sigaction函数

**功能是检查或修改与指定信号相关联的处理动作（可同时两种操作）**

```C
int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact);
```

> signum参数指出要捕获的信号类型
>
> act参数指定新的信号处理方式
>
> oldact参数输出先前信号的处理方式（如果不为NULL的话）。

 返回值：0 表示成功，-1 表示有错误发生。

 **struct sigaction结构体介绍**

```c
struct sigaction {
    void (*sa_handler)(int);
    void (*sa_sigaction)(int, siginfo_t *, void *);
    sigset_t sa_mask;
    int sa_flags;
    void (*sa_restorer)(void);
}
```

>sa_handler此参数和signal()的参数handler相同，代表新的信号处理函数
>sa_mask 用来设置在处理该信号时暂时将sa_mask 指定的信号集搁置
>sa_flags 用来设置信号处理的其他相关操作，下列的数值可用。 
>	SA_RESETHAND：当调用信号处理函数时，将信号的处理函数重置为缺省值SIG_DFL
>	SA_RESTART：如果信号中断了进程的某个系统调用，则系统自动启动该系统调用
>	SA_NODEFER ：一般情况下， 当信号处理函数运行时，内核将阻塞该给定信号。但是如果设置了 SA_NODEFER标记， 那么在该信号处理函数运行时，内	核将不会阻塞该信号

#### sigemptyset（初始化信号集）
相关函数 sigaddset，sigfillset，sigdelset，sigismember
```c
 #include<signal.h>
 int sigemptyset(sigset_t *set);//struct sigaction 中的成员：sigset_t sa_mask
```


函数说明 sigemptyset()用来将参数set信号集初始化并清空。
返回值 执行成功则返回0，如果有错误则返回-1。

#### sigset_t信号集类型

```c
　#include <signal.h>
   typedef struct {
　　unsigned long sig[_NSIG_WORDS]；
　　} sigset_t
```

信号集用来描述信号的集合，linux所支持的所有信号可以全部或部分的出现在信号集中，主要与信号阻塞相关函数配合使用。

- 下面是为信号集操作定义的相关函数：

```c
int sigemptyset(sigset_t *set)//初始化由set指定的信号集，信号集里面的所有信号被清空；
int sigfillset(sigset_t *set)//调用该函数后，set指向的信号集中将包含linux支持的64种信号；
int sigaddset(sigset_t *set, int signum)//在set指向的信号集中加入signum信号；
int sigdelset(sigset_t *set, int signum)//在set指向的信号集中删除signum信号；
int sigismember(const sigset_t *set, int signum)//判定信号signum是否在set指向的信号集中。

```

SIGINT
程序终止(interrupt				)信号, 在用户键入INTR字符(通常是Ctrl-C)时发出，用于通知前台进程组终止进程

SIGQUIT
和SIGINT类似, 但由QUIT字符(通常是Ctrl-/\)来控制. 进程在因收到SIGQUIT退出时会产生core文件, 在这个意义上类似于一个程序错误信号。

程序结束(terminate)信号, 与SIGKILL不同的是该信号可以被阻塞和处理。通常用来要求程序自己正常退出，shell命令kill缺省产生这个信号。如果进程终止不了，我们才会尝试SIGKILL。

SIGSTOP
停止(stopped)进程的执行. 注意它和terminate以及interrupt的区别:该进程还未结束, 只是暂停执行. 本信号不能被阻塞, 处理或忽略.



SIG_DFL：默认信号处理程序
SIG_IGN：忽略信号的处理程序
