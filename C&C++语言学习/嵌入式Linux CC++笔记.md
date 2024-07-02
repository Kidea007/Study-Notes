# 嵌入式Linux C/C++笔记

form：华清远见

---



# 环境搭建：

参考技术博客，虚拟机VMwa Workstation最新版 安装Ubuntu最新版

下面的配置是基于华清远见的课程，安装14.4版本ubuntu

### 虚拟配置:

1个1核处理器

1G内存

20G硬盘

### 硬盘分区：

/ 根目录 5G

/boot 引导程序 200M

Swap 虚拟内存（交换区） 2G

/home 用户文件 剩下的空间

---





# termina的基础命令

## Ubuntu系统teminal的常用命令

命令严格区分大小写 

ctrl+alt+t快速打开teminal

ls 打开文件夹的目录

cd 进入文件夹

cd .. 退回到上一个文件夹

ls -l 打开目录并显示文件详细信息

Cat -s -b 其中，Cat表示在teminal中查看文件内容，-s 表示合并空行，-b 表示加行序号

cp test.c test1.c 在同一文件夹把文件test.c复制为test1.c

programe 程序

---



# 数据类型

所有数据（数字、字母、字符&字符串、特殊符号）最后都会变成2进制（机器语言）

---



## 数值数据

| 十六进制 HEX | 十进制 DEC | 二进制 BIN |
| :----------: | :--------: | :--------: |
|     0x0      |    000     |    000     |
|     0x1      |    001     |    001     |
|     0x2      |    002     |    010     |
|     0x3      |    003     |    011     |
|     0x4      |    004     |    100     |
|     0x5      |    005     |    101     |
|     0x6      |    006     |    110     |
|     0x7      |    007     |    111     |
|     0x8      |    008     |    1000    |
|     0x9      |    009     |    1001    |
|     0xA      |    010     |    1010    |
|     0xB      |    011     |    1011    |
|     0xC      |    012     |    1100    |
|     0xD      |    013     |    1101    |
|     0xE      |    014     |    1110    |
|     0xF      |    015     |    1111    |
|     0x10     |    016     | 0001 0000  |
|     0x11     |    017     | 0001 0001  |
|     0x12     |    018     | 0001 0010  |
|     0x13     |    019     | 0001 0011  |
|     0x14     |    020     | 0001 0100  |
|     0x15     |    021     | 0001 0101  |
|     0x16     |    022     | 0001 0110  |
|     0x17     |    023     | 0001 0111  |
|     0x18     |    024     | 0001 1000  |
|     0x19     |    025     | 0001 1001  |
|     0x1A     |    026     | 0001 1010  |
|     0x1B     |    027     | 0001 1011  |
|              |            |            |

---



## 非数值数据

根据编码标准转化为二进制

如：ASCII码表

---





# 编译器

gcc（GNU Compiler）

调用gcc的相关SHELL指令

gcc hello.c 最基础的编译命令 生成 a.out

gcc hello.c -o hello.exe 自定义编译后的文件名

gcc hello.c -wall表示编译hello.c并生成详细的错误提示

cat hello.c 把程序打印到teminal

# shell的使用

shell工具是对操作系统的指令的封装，用于实现用户与linux内核的交互

若干shell命令行+控制语句=shell脚本

linux内核接受到shell工具转译后的指令，可以控制相关硬件执行操作

硬件执行操作后会给shell提供反馈

相当于用户通过shell工具，间接的控制了硬件

shell工具简化了linux内核指令，使操作硬件更方便快捷

## shell的类型

bash shell

zshell





# 标准IO

控制高端的硬件必须通过操作系统内核来实现

不同操作系统内核提供了不同的API接口

用库函数将常用的一些操作系统的API接口封装成统一标准的新API接口

这个新的API接口就是标准IO，如:  <stdio.h>在所有主流操作系统上使用C语言

标准IO方便了程序在不同操作系统间的移植

---

# C语言

## 01数据类型

![image-20240616112236200](../AppData/Roaming/Typora/typora-user-images/image-20240616112236200.png)

### bool类型

bool不是基本数据类型，需要调用<stdbool.h>中的宏定义bool

```c
#include <stdio.h>
#include <stdbool.h>
bool = not_zero = true;//非零的任何数据都识别为1
bool = zero =false;

```

不同硬件平台下相同的数据类型占用的内存大小不一样

### 基本数据类型

下面是32bit的ubuntu下的数据长度

![image-20240616114340320](../AppData/Roaming/Typora/typora-user-images/image-20240616114340320.png)

![image-20240616114901604](../AppData/Roaming/Typora/typora-user-images/image-20240616114901604.png)

![image-20240616114910197](../AppData/Roaming/Typora/typora-user-images/image-20240616114910197.png)

对于不同硬件平台可以调用sizeof(datetype)查看不同数据类型的长度(不是变量)

直接打开 /usr/include/limits.h也可以查看各种数据类型的长度

数据范围溢出会乱码，但是编译器不一定会报错，需要人工检查

![image-20240616115554108](../AppData/Roaming/Typora/typora-user-images/image-20240616115554108.png)

![image-20240616115641086](../AppData/Roaming/Typora/typora-user-images/image-20240616115641086.png)

### 常量



char  本质上还是int 转换的规则就是ASCII

例如：A=65 a=65+32=97

SHELL 指令 man ASCII可以查看具体转换规则

---

宏定义 常量

方便代码维护

#define A B    把A替换为B，可修改B的值，相当于复制粘贴

预处理不会占用资源

存入寄存器的变量不能取地址&，即指针不能控制

static 静态类型 

正常情况下每次循环都会销毁局部变量

static修饰的变量默认初始化为0，并且不入轮回（值不被销毁）

调用其他文件中的全局变量，需要用extern修饰这个变量

如果全局变量被static修饰，无法被extern调用

---



## 02运算符号

### 算数运算符

按照小学数学来就行

![image-20240616155454376](../AppData/Roaming/Typora/typora-user-images/image-20240616155454376.png)

### 关系运算符

判断0和1，即假和真，false or true

可以在括号外加 ！取反

![image-20240616154622623](../AppData/Roaming/Typora/typora-user-images/image-20240616154622623.png)

### ==逻辑运算符==

![image-20240616154906737](../AppData/Roaming/Typora/typora-user-images/image-20240616154906737.png)

逻辑与 相当于串联开关

逻辑或 相当于并联开关 

### ==位运算符号==

进行位运算时候一定要把数据转换为==二进制==

在操作寄存器配置时经常用到位操作

![image-20240616161609129](../AppData/Roaming/Typora/typora-user-images/image-20240616161609129.png)

位逻辑反 ：在~后的二进制数每一位都分别取反

位逻辑与：在&两侧的二进制数对应的每一位都分别进行逻辑与

位逻辑或：在|两侧的二进制数对应的每一位都分别进行逻辑或

---



==位逻辑异或==：（==异或==表示相同位0，不同为1）

对^两侧对应的每一位二进制数分别进行异或

左移位：在<<左侧是被操作的变量，右侧是操作变量向左移动的位数

```c
uchar a=0xe4, b;
b=a<<3;//a转化为二进制：1110 0100
//左移3位相当于：去掉左边3位，然后在末尾补上3位0，
//b=0010 0000
```

右移位：>>原理同上。

---

### ==赋值复合运算符==

将右边的表达式的运算结果赋值给左边的变量

![image-20240616165235551](../AppData/Roaming/Typora/typora-user-images/image-20240616165235551.png)

---

---



### 条件运算符

if<表达式1>为真，则执行<表达式2>，else执行<表达式3>

注意：只有表达式1是布尔型的判断

![image-20240616170100989](../AppData/Roaming/Typora/typora-user-images/image-20240616170100989.png)

### 逗号运算符

在括号内的表达式从左往右依次执行，将最右边的结果赋值给最左边的变量

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240616201857238.png" alt="image-20240616201857238" style="zoom:50%;" />

### ==内存运算符号==

```c
int a = 0;
int b = 0;
int c = 0;
b = sizeof(int);//括号内填变量和数据类型，都等同数据类型
c = sizeof(a);//b=c,内存占用的大小和变量的值无关，只和数据类型有关

```

### 运算符的==优先级==

记不住的，用到再来查

![image-20240616203223348](../AppData/Roaming/Typora/typora-user-images/image-20240616203223348.png)

## 03输入和输出函数

来自<stdio.h>的输入输出函数

---

常量、变量、表达式从本质上都可以归纳为数据

在理解代码框架的过程中只需要关注数据的结果

得到结果的过程可以战略性忽略

### 格式输出函数：

printf(" 被打印的变量是：%格式符1，%格式符2 "，变量名1，变量名2)

不同数据类型的变量打印需要不同的格式符

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240616205639231.png" alt="image-20240616205639231" style="zoom: 50%;" />

![image-20240616210248669](../AppData/Roaming/Typora/typora-user-images/image-20240616210248669.png)

![image-20240616210300084](../AppData/Roaming/Typora/typora-user-images/image-20240616210300084.png)

![image-20240616210434410](../AppData/Roaming/Typora/typora-user-images/image-20240616210434410.png)

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240616210509771.png" alt="image-20240616210509771" style="zoom: 33%;" />





![image-20240616214552947](../AppData/Roaming/Typora/typora-user-images/image-20240616214552947.png)
