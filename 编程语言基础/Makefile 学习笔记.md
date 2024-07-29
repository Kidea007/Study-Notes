# Makefile 学习笔记





# day14 Makefile

## make工具的作用

项目文件少的时候可以手动编译

但是对于项目文件非常多的项目编译起来工作量非常大

这时候就需要make这类工具来编译项目文件

## make工具的特点

- Make工具可以根据文件时间戳自动发现更新过的文件而减少编译的工作量

- make通过读取唯一的配置文件Makefile的内容来执行编译 

- Make将只编译改动后的代码文件，未改动的代码不会重复编译。



# Makefile作用

- makefile关系到了整个工程的编译规则。

- 一个工程中的源文件不计数，其按类型、功能、模块分别放在若干个目录中

- makefile定义了一系列的规则来指定，哪些文件需要先编译，哪些文件需要后编译，哪些文件需要重新编译

- 甚至于进行更复杂的功能操作，因为makefile就像一个Shell脚本一样，其中也可以执行操作系统的命令。



# Makefile配置文件

> Makefile是Make的==唯一配置文件==

- 由make工具创建的目标体（target），通常是目标文件或可执行文件

- 要创建的目标体所依赖的文件（dependency_file）

- 创建每个目标体时需要运行的命令（command）

- 命令行前面必须是用 ” Tab ”  缩进
- 使用‘’ space ‘’ 来缩进，会编译错误提示: missing separator. Stop.

```makefile
Makefile格式
target : dependency_files
	command
例子
hello.o : hello.c hello.h
	gcc  –c  hello.c  –o  hello.o
```



# 变量

```makefile
关于变量的例子
sunq : kang.o yul.o
	gcc kang.o yul.o -o sunq
kang.o : kang.c kang.h 
	gcc –Wall –O -g –c kang.c -o kang.o
yul.o : yul.c 
	gcc - Wall –O -g –c yul.c -o yul.o
注释:-Wall:表示允许发出gcc所有有用的报警信息.
     -c:只是编译不链接,生成目标文件”.o”
     -o file:表示把输出文件输出到file里
关于更多的用man工具

```

## 创建变量的目的:

**用来代替一个文本字符串**:

- 替换系列文件的名字 
- 替换传递给编译器的参数 
- 替换需要运行的程序 
- 替换需要查找源代码的目录 
- 替换你需要输出信息的目录 
- 替换你想做的其它事情。