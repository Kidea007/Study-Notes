#  C++学习

> 学习目标：用于QT开发GUI界面

#  day01 从C到C++及类与对象

## 编译流程

```bash
kidea@ubuntu:~$ vim test.cpp
kidea@ubuntu:~$ g++ test.cpp
kidea@ubuntu:~$ ./a.out

kidea@ubuntu:~$ cat test.c #把目标文件的内容打印到标准输出（终端）
```

## 引用

**引用示例：**

```cpp
#include <stdio.h>

int main()
{
	int a = 100; // a申请了一块内存空间
	int &b = a;  // b引用了a的内存空间，相当于a的别名

	printf("a = %d\n", a);
	printf("b = %d\n", b); //这里输出两者的内容一样

	printf("addr: a = %p\n", &a);
	printf("addr: b = %p\n", &b); //这里输出两者的地址一样
}
//相当于2个变量共用了同一块内存
```

> 既然变量名称已经知道，取别名还有什么意义，直接用这个变量名操作不可以吗？

- 对比在C和CPP下进行**两个变量的数据交换**来说明这个问题
-   c语言交换数据的错误示范：

```c
  /*
  c语言的错误示范：
      不同函数内的同名变量的地址不一样
      对swap内的a进行任何操作都不会影响到main内的a
      因为每个函数在调用时都会在其自己的栈帧（stack frame）或调用栈（call stack）上分配局部变量空间。栈帧是函数调用时分配的内存区域，用于存储该函数的参数、局部变量以及返回地址等信息。当函数被调用时，一个新的栈帧被创建，并在该栈帧上分配局部变量；当函数返回时，该栈帧被销毁，其上的局部变量也随之消失。
  
  因此，即使两个函数使用了相同名称的局部变量，这些变量也会位于不同的栈帧上，因此它们的地址是不同的。这种机制保证了函数调用的独立性和局部变量的隔离性，即一个函数中的变量修改不会影响到另一个函数中同名变量的值（除非这些变量是通过某种方式（如指针、全局变量或静态变量）在函数之间共享的）。
  
  需要注意的是，虽然局部变量通常位于栈上，但并非所有类型的变量都如此。例如，全局变量和静态变量通常位于程序的数据段（data segment）或BSS段（Block Started by Symbol，用于未初始化的全局变量和静态变量），而不是栈上。此外，某些编译器优化可能会改变变量的存储位置或行为，但这些优化通常不会改变不同函数内同名变量地址不同的基本原则。
  */
  #include <stdio.h>
  
  int swap(int a, int b)
  {
  	a ^= b;
  	b ^= a;
  	a ^= b;
      return a=b,b=a;
  }
  int main()
  {
  	int a = 100;
  	int b = 10;
  
  	printf("a = %d, b = %d\n", a, b);
      
  	swap(a, b);
      
  	printf("a = %d, b = %d\n", a, b);
  }
```

- c语言交换数据的正确示范：

```c
#include <stdio.h>

//&a,&b被传到p,q的内存空间，这里的操作符*表示去到p,q内存放的地址
//即跳到a,b地址下执行数据交换
void swap(int *p, int *q)
{
	*p ^= *q;
	*q ^= *p;
	*p ^= *q;
}

int main()
{
	int a = 100;
	int b = 10;

	printf("a = %d, b = %d\n", a, b);
    
	swap(&a, &b);//取a，b的地址传过去

	printf("a = %d, b = %d\n", a, b);
}
```

- 用cpp进行数据交换

```cpp
#include <stdio.h>
//这里接收到a和b的时候进行了引用，和进行指针操作是一样的作用
int swap(int &a, int &b)
{
	a ^= b;
	b ^= a;
	a ^= b;
}
int main()
{
	int a = 100;
	int b = 10;

	printf("a = %d, b = %d\n", a, b);

	swap(a, b);
    
	printf("a = %d, b = %d\n", a, b);
}
```

## 函数的默认参数

> 调用函数时不传入实际参数
>
> 目标函数就会使用默认参数初始化值
>
> 同时存在默认参数和一般形式参数的时候，默认参数需要放在最右边

作用：需要多次调用同一函数的时候不用频繁的写入口参数

```cpp
#include <stdio.h>

//void sortarr(int *arr, int len, int flag=UP);
void debug(const char *ptr = "---------------")
{
	printf("%s\n", ptr);
}

int main()
{
	debug();
	debug();
	debug();
	debug();
	debug();
	debug();
	debug("hello");
	debug("world");
}

```

## 函数的重载

> 字符串：string 
>
> 比较：compare

- 在C中比较2个数据类型的数据大小

```c
#include <stdio.h>
#include <string.h>
//比较不同的数据类型的数据需要调用不同的函数
int intcmp(int a, int b)
{
	return a-b;
}

int scmp(const char *str1, const char *str2)
{
	return strcmp(str1, str2);
}

int main()
{
	printf("%d\n", cmp(1, 2));
	printf("%d\n", cmp("aaaaaa", "bbbb"));
}
```

- 在cpp中同一个函数名可以写出不同的函数，称为函数的重载

```cpp
#include <stdio.h>
#include <string.h>
/*比较不同类型的数据都可以用同一个函数名称
通过区分传入的参数来进行区分
所以同名的函数的入口参数不能一样*/
int cmp(int a, int b)
{
	return a-b;
}

int cmp(const char *str1, const char *str2)
{
	return strcmp(str1, str2);
}

int main()
{
	printf("%d\n", cmp(1, 2));
	printf("%d\n", cmp("aaaaaa", "bbbb"));
}

```

## 堆内存的分配

malloc = "memory allocation" = “内存 分配”

- 在C中分配内存

```c
#include <stdio.h>
#include <malloc.h>
#include <string.h>

int main()
{
	char *p = (char *)malloc(10);	//在堆中申请10个byte内存
	strcpy(p, "hello");		//往内存写入内容

	printf("p: %s\n", p);

	free(p);	//释放内存，防止泄漏
}
```

- 在CPP中申请内存

```cpp
include <stdio.h>
#include <malloc.h>
#include <string.h>

int main()
{
    //分配一块内存
	int *intp = new int;//相当于C中的(int*)malloc(sizeof(int));

	*intp = 100;

	printf("*intp = %d\n", *intp);

	delete intp;	//释放一块内存
//分配一堆内存//////////////////////////////////////////////////
	char *p = new char[10];

	strcpy(p, "hello");

	printf("p: %s\n", p);

	delete [] p;	//释放一堆内存
	
}
```



## 类class与对象

- 方法和数据应该要有绑带关系，不应该独立，这就是面向对象

- 虽然C主要是面向过程，但是在C中可以利用结构体模仿面向对象
- 虽然可以模仿，但是存在很多弊端
- 所以cpp引入了类的概念实现真正的面向对象

## 构造函数

- 类class创建实例后会==自动==调用构造函数来对自己的成员进行==初始化==

- 如果没有指定构造函数会默认调用一个空类型的空函数

- 在创建实例的时候还可以给构造函数传入参数，实现初始化，不用直接操作类的成员

## 析构函数

当构造函数的生命周期结束后（被销毁后）会自动调用析构函数

例如在构造函数中申请了内存，就需要在析构函数中实现释放内存
