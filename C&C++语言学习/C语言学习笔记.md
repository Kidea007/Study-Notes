# C语言学习笔记

（知识源：B站鹏哥，大约500个小时）



C 语言文档通常包括以下内容：

1. **语法规则**：介绍 C 语言的基本语法规则，包括关键字、标识符、数据类型、运算符、控制语句等。

2. **标准库函数**：介绍 C 语言标准库提供的各种函数，如输入输出函数（printf、scanf）、字符串处理函数（strcpy、strlen）、内存管理函数（malloc、free）等。

3. **数据类型**：介绍 C 语言中的基本数据类型（int、float、char）以及复合数据类型（数组、结构体、指针）的定义和用法。

4. **程序结构**：介绍 C 语言程序的基本结构，包括函数定义、函数调用、变量作用域、程序流程控制等。

5. **指针和内存管理**：介绍指针的概念和用法，以及内存分配和释放的方法。

6. **文件操作**：介绍如何在 C 语言中进行文件的读写操作，包括打开文件、读取文件、写入文件等。

7. **预处理器指令**：介绍 C 语言中的预处理器指令，如宏定义、条件编译等。

8. **错误处理**：介绍如何处理在程序运行过程中可能出现的错误和异常情况。

这些内容涵盖了 C 语言的基本知识和常用技术，对于初学者来说是入门学习的基础，对于有经验的开发人员来说是解决问题和优化代码的重要参考。

## C语言初阶视频的笔记

### 启蒙程序

```c
#include<stdio.h> /*C语言的标准输入输出函数库 表示引用这个库里面的函数，比如printf()用来打印数据*/
int main() /*int表示主程序main()的返回的数据类型是整型int 括号（）内是main函数的参数()=（void）*/
{
 	printf("hello dog!"); //打印输出：hello dog
 	return 0; //代码正常运行返回写0，用别的int类型数据也可以
}
/*C语言规定main()是最先编译的程序,一个程序只能有一个主程序，默认情况下代码从上到下依次执行*/
```

### 数据类型

- 整型

  - int   整型

  - short 短整型

  - long   长整型

  - long long  更长的整型

- 浮点型 //就是小数啊

  - float   单精度浮点型（就是小数）

  - double 双精度浮点型

- char 字符型

不同类型的数据存储空间大小不一样

### 存储单位（与寄存器有关）

bit 比特位 b	一位二进制数字占用一个bit，即0或者1

byte 字节 B	一个byte等于8个bit，即8位二进制数字

KB 千字节	1KB=1024B       

MB 兆字节	1MB=1024KB

GB		1GB=1024MB

TB		 1TB=1024GB

PB		 1PB=1024TB



```c
#include <stdio.h>//引用库和函数后面不用带分号；
int main() /*函数sizeof()可以用来打印指定的数据类型占用的内存，%zu表示sizof()的返回值的数据类型是无符号整型*/
{
    printf("%zu\n",sizeof(int)); //一般int占4个字节
    printf("%zu\n",sizeof(float));//一般也是4字节
    printf("%zu\n",sizeof(char)); //一般char占1个字节
    
    return 0;
}
```



### 常量和变量

```c
#include <stdio.h>	/*全局变量和局部变量名字一样时，程序会优先使用局部变量的值，在同一个局部的局部变量不能重名。
局部变量的作用范围只能在局部使用，而全局变量可以在整个程序中使用*/

int high = 180；//在主函数main()外的就是全局变量

int main()
{
    int age = 18;	//自定义一个名称为age的整型的局部变量
    float weight =125.5; //定义一个体重的变量
    //等号表示将右边的数据存放到左边的变量申请的内存中
    int mun1 = 0;//将mun1初始化为0
    int mun2 ; //mun2没有进行初始化，程序会进行随机初始化赋值
}
```

### 输入函数

```c
#include <stdio.h>
int main()
{
    int mun1 = 0;//声明两个局部变量并初始化
    int mun2 = 0;
    
    scanf("%d %d",&mun1,&mun2);//在键盘上输入这2个数（赋值）
    
    int sum = mun1 + mun2;//求和后赋值给sum
    
    printf("%d\n",sum);//把结果sum的值打印出来
    
    return 0;
}
```

### 全局变量和局部变量的作用范围

```c
int a = 666;	 //声明一个整型的全局变量并初始化
/*如果是在另外的文件中定义的变量，想要在这个文件中使用，需要用关键字extern来声明后才能正常调用。例如：
extern int a;
*/
extern int b; 	//表示声明这个变量b是在外部定义的

void test()	//声明一个返回类型为空类型的函数，用来打印变量a
{
    print("test:%d\n",a);
}

int main()
{
	test();		//在主程序中调用函数test()
    
    {
        int a = 555;
        print("%d\n",a);  //局部变量只能在花括号内使用
    }
    
    print("%d\n",a);
    
    return 0;
}
```

### 常量

- 字面常量

- const修饰的常变量

- #define定义的标识符常量

- 枚举常量

  
  
  ```c
  int main()
  {
      666;
      3.1415926;
      'a';//用单引号的是字符，双引号叫字符串
      "abc";//以上都是字面常量
      
      const int r = 10 ;//在const后的变量不能直接被修改（不能使用=来给r赋值），但是也不能当成常量用 ，因为r占据的是int申请的内存，与字面常量占用的内存不一样，r在本质上还是变量，或者说常变量。
  }
  ```
  
  ```c
  #define MAX 100 
  //宏定义，用MAX替代100
  //相当于起了名字的全局字面常量，这个名字称为标识符，通过标识符可以引用数据，但是不能使用=给MAX赋值。
  #define NAME "张三"
  int main()
  {
      printf("%d\n",MAX);
      int b = MAX;
      printf("%s\n",NAME);
  }
  ```
  
  ```c
  //enum为枚举关键字,枚举就是一一列举的意思
  //习惯上会把枚举常量和define的标识符写成大写
  enum Color
  {
      RED,//在这里面的就是枚举常量，代表的就是Color的未来可能取值
      GREEN,//声明枚举常量是不占用内存的
      BLUE，
      BLACK
  }
  int main()
  {
     enum Color a = RED;//变量a向内存申请空间，将Color中的枚举常量RED赋值给a
  }
  ```

### 

### 字符串

```c
#include <stdio.h> //复习：一个char类型的字符占用的内存空间是1个字节，一个字节是内存的最小单位
int main()
{
char arr1[] = "abcdef";	//用一个数组向内存申请空间存放字符串,即7个字节。
//arr[]是数组函数，[]内可以填内存的大小(等于ASCII码的个数+1，因为字符串后面会自动添加一个转义字符'\0'作为结束标志（规定）)，如果不填会自动计算需要的内存空间
 char arr2[] = {'a','b','c','d','e','f','\0'};
    printf("%s\n",arr1);
    printf("%s\n",arr2);
    //在arr2中如果没有'\0'printf在打印的时会顺着内存空间一直打印下去直到遇见'\0',导致占用过大的内存。
    return 0;
}
```



### 转义字符

即用来 转变字符原来的意思 的字符，这类字符在C语言中具有特定的意义

  \n 表示换行

\\ \   	防止打印path的时候斜杠\被识别为转义字符

\0 表示字符串的结束，在ASCII码中\0的值为0，所有字符串后用0也可以

\? 现在用不到了，古老符号

%d  打印整型

%c   打印字符    在打印字符单引号需要用转义字符

%s   打印字符串  也要用转义字符

%f    打印float

%lf    打印double

\t  相当于tab

\r  相当于回车，与换行不太一样

\ddd     其中ddd代表用8进制表示的ASCII码中的字符

\xdd    其中dd代表用16进制表示的ASCII码中的字符

注意：

这个dd的值不能超出ASCII码的值（即十进制下的0~127）

一个转义字符占用一个字节的内存空间



### 注释

//注释一行代码，不参与编译

/*

注释

一段字符串

注意不支持嵌套注释

*/

注释快捷键 ctrl+k+c ，ctrl+k+u

### 选择语句

- if else

- switch

### 循环语句

- while

- for

- do while

```c
int main()
{
    int line = 0;
    printf("在B站大学看鹏哥的C语言")；
        while(line<20000)
        {
            printf("写代码：%d",line);
            line++;
        }
    if(line>=20000)
    {
        printf("秃了，也变强了")；
    }
    else
    {
        printf("秃了还是菜，继续肝")；
            
            return 0;
    }
    
}
```





C语言的结构化是指

- 顺序结构
- 选择结构
- 循环结构

### 函数

在 C 语言中，函数参数的传递分为两种：值传递（By Value）和指针传递（By Reference）。

1. 值传递（By Value）

值传递是指函数调用时，将实参的值复制到函数栈区，然后在函数内部对这份复制的内容进行操作。当函数调用结束时，这份复制的内容被销毁。实参本身的数据不会受到影响。值传递有三种情况：

- 基本数据类型（如 int、float、double 等）：此时，函数栈区分配一块内存存储实参的值，函数内部对这块内存中的数据进行操作。
- 数组：当数组作为参数传递时，函数栈区分配一块内存，将数组的第一个元素的值复制到这块内存中。然后，函数内部通过索引访问这个数组元素。需要注意的是，此时传递的只是数组的第一个元素的值，而不是整个数组的所有元素。
- 指针：指针作为参数传递时，实际上传递的是指针所指向的内存地址。函数内部通过这个地址访问指针所指向的内存区域。

2. 指针传递（By Reference）

指针传递是指函数调用时，将实参的内存地址（即指针）传递给函数。在函数内部，通过这个指针访问实参的内存区域，对实参的数据进行操作。由于传递的是内存地址，而不是值，因此函数内部的操作会影响实参的数据。需要注意的是，指针传递只能用于指针类型的参数。

在 C 语言中，指针传递通常用于以下情况：

- 修改指针指向的内存区域：例如，在函数中分配一块内存，并将指针指向这块内存，然后返回。此时，函数内部的操作会影响实参指向的内存区域。
- 遍历数组：当数组作为参数传递时，可以使用指针传递。这样，函数内部可以直接通过指针访问数组的元素，而无需使用索引。

总之，C 语言中函数参数的传递分为值传递和指针传递。在实际编程过程中，可以根据实际需求选择合适的传递方式。值传递适用于基本数据类型和数组，而指针传递适用于指针类型的参数。

可以引用库函数

也可以自定义函数

```c
#include<stdio.h>//包含stdio.h这个库，下面调用的scanf()和printf()都是这个库内提供的函数。

int Add(int x,int y)//自定义一个函数名为add的函数，小括号内的是函数的参数，大括号的是函数体，前面的int是函数类型。
{
    int z = 0;
    z = x + y;
    return z;//也可以这样: return x + y;
}
int main()
{
    int n1;
    int n2;
    scanf("在键盘上键入2个整数:%d %d",&n1,&n2);
    
    int sum = Add(n1,n2);//将参数传入Add()
    printf("计算结果：%d\n",sum);
    
    return 0;
}
    
```

### 数组

定义：一组相同类型的数据的集合

```c
int main()   
{	//这个10不写也可以，arr不是关键字也可以起别的函数名
int arr[10] = {5,2,0,1,3,1,4,1,5,9};
//如果[]内的值大于实际数据个数，称为不完全初始化，剩余的内存会默认初始化为0
//也可以创建别的类型的数组: 
    char ch[10] ="hello!"; double [8]; 
//arr内的10代表数组中的数据个数是10个，其中每个元素都有对应的序号，序号规定从0开始从左到右增加，arr()中序号为0~9（也叫下标），通过序号可以准确的访问每一个数据。
printf("第三个数是：%d\n"，arr[2]);
    
    int i;//用循环语句把arr[]的所有数据打印出来
    while (i<10)
    {
    printf("%d "，arr[i]);
        i++;
    }
    return 0;
}
```

### 操作符

- 算术操作符	+ - * / %
- 移位操作符        >>   <<
- 位操作符         &  ^  |
- 赋值操作符  =  +=  -=  *=  /=  &=  ^=  |=  >>=  <<=
- 单目操作符  
  - ! 逻辑反操作
  - -负值
  - +正值
  - &取地址
  - sizeof 操作数的类型长度（以字节为单位）
  - ～ 对一个数的二进制按位取反
  - --前置，后置--
  - ++前置，后置++
  - *间接访问操作符（解引用操作符）
  - （类型）强制类型转换



单目是指操作数只有一个

+加号可以操作2个操作数相加，称为双目操作符

```c
int a = (int)3.14;	//把浮点数强制转换为整数
```

- 关系操作符 > >= < <= != ==
- 逻辑操作符  &&   ｜｜
- 条件操作符 exp1 ? Exp2 : exp3

这个条件操作符是三目操作符，有3个操作数

当exp1为真的时候返回exp2

当exp1为假的时候返回exp3



- 逗号表达式 exp1,exp2,exp3, ...expN
- 下标引用、函数调用和结构成员 [ ] ( ) . ->



### 关键字



![image-20240131172203823](/Users/huangchunlong/Library/Application Support/typora-user-images/image-20240131172203823.png)

关键字不能自己创建，是C语言本身规定的具有固定的意义的词。

变量的命名

- 要有意义，方便阅读
- 名字必须字母、数字、下划线组成，且不能以数字开头。
- 不能是关键字
- 可以用中文起名字，但不建议，容易出错，显得不够专业

enum 枚举

struct 结构体

union 联合体

#### register 寄存器

```c
int main()
{
    //寄存器变量
    register int num =3; //存放在寄存器中获得更快的访问速度,是否存放在寄存器，最终决定权在于编译器
    return 0;
}
```



static 静态的

extern 声明外部变量

signed 有符号的

unsigned 无符号的

sizeof 计算占用内存的字节数 

#### void 表示无（函数的返回类型，函数的参数）

#### typedef 数据类型重命名

//只能对数据类型重命名

```c
//将过长的不方便使用的名字重命名。
//这里unsigned int等价于unit_32,也可以用来创建无符号整型变量。
typedef unsigned int uint_32;

//也可以给结构体重命名。
typedef struct Node
{
    int data;
    struct Node* next;
}Node;

int main()
{
    unsigned int num1 = 0;
    unit_32 num2 = 0;  //num1与num2的数据类型是一样的
    
    struct Node n1;
    Node n2;	//这里n1和n2数据类型也是一样的
    
    return 0；
}

```

#### static  静态的 

（用来修饰变量和函数）只进行一次初始化，再次调用会使用上一次的值

- 修饰局部变量，称为静态局部变量
- 修饰全局变量，称为静态全局变量
- 修饰函数， 称为静态函数

static 修饰局部变量的时候，局部变量出了作用域，不会销毁，本质上，只是改变了变量的存储位置

```c
#include<stdio.h>

void test1()//有了void就不用return了
{
int a = 0;//在内存的栈区创建局部变量，使用后会销毁，再次进入局部时会重新初始化。
a++;
    printf("test1:a=%d",a);
}

void test2()
{
static int b = 0;//在内存的静态区创建局部变量，使用后不会销毁，会保留原来的值，再次进入局部时不会初始化。    
b++;
    printf("test2:b=%d",b);
}

int main()
{
    int i = 0
    while (i<10)
    {
        test1();//结果：1 1 1 1 1 1 1 1 1 1
        //test2();//结果：1 2 3 4 5 6 7 8 9 10
        i++;
    }
    return 0;
}

```



#### 内存分区：栈区、堆区、静态区

```c
int g_val = 2020;//外部全局变量具有外部链接属性
//如果使用 static int g_val=2020; 会把g_val的外部链接属性变成内部链接属性
//则外部文件无法调用这个全局变量
```

```c
extern int g_val;//声明外部全局变量，然后可以在主程序中调用
int main()
{
    printf("%d\n",g_val);
    return 0;
}
```





静态全局变量相当于作用域变小了

全局变量和静态全局变量和静态局部变量都在内存静态区创建

extern可以调用外部文件中的全局变量和函数

但是不能调用被static修饰的静态全局变量和静态函数

```c
static int Add(int x,int y) //静态全局函数无法被外部文件调用
{
    return x + y ;
}
```

```c
extern int Add(int x,int y);
int main()
{
    int a=10;
    int b=20;
    
    int z=Add(a,b);
    printf("%d\n",z);
    return 0;
}
```

#### ==宏定义==

在 C 语言中，`#define` 是一个预处理器指令，用于定义宏（macro）。宏是一种在程序中用来表示某个值或代码片段的符号常量，通过宏定义可以简化代码编写、提高代码的可读性和维护性。

`#define` 的基本语法如下：
```
#define 宏名 值或代码片段
```

其中，`宏名` 是定义的宏的名称，可以是任意有效的标识符；`值或代码片段` 则是宏的取值或代码片段。

宏定义可以用来 定义常量、简单函数、条件编译 等。例如：
```c
#define PI 3.14159
#define MAX(a, b) ((a) > (b) ? (a) : (b))

int main() {
    double radius = 5.0;
    double area = PI * radius * radius;

    int x = 10, y = 20;
    int max_num = MAX(x, y);

    return 0;
}
```

在上面的例子中，

`#define PI 3.14159` 定义了一个表示圆周率的宏，

`#define MAX(a, b) ((a) > (b) ? (a) : (b))` 定义了一个比较两个数大小的宏。

==在程序中使用这些宏可以直接替换成对应的值或代码片段==，从而简化代码编写。

需要注意的是，宏定义是在预处理阶段展开的，不会进行类型检查，因此在使用宏时要确保参数和返回值的类型匹配，以避免潜在的问题。

```c
#define ADD(x,y)  ((x)+(y)) //ADD为宏名，x，y为宏的无类型参数，（（X）+（y））为宏体
int Add(int x,int y)
{
    return 0;
}

int main()
{
    int a=10;
    int b=20;
    int c=ADD(a,b); //调用宏ADD进行加法运算
    printf("%d\n",c);
    
    return 0;
}
```





### 指针

定义格式

- 数据类型（空格）*变量名
  - 在 int *p 中 *表示p是一个指针变量 
  - 在 *p 中 * 表示通过指针变量p存储的地址，访问这个地址对应的对象
  - 所以 *p 相当于指向的对象本身

#### 内存

内存由一个一个内存单元组成，每个内存单元大小一个字节，

一个字节8bit，内存的每个内存单元都有对应的地址编号

地址总线通电后产生地址编号

32位的电脑的地址总线位宽32bit，最大寻址4G的内存单元

 char类型是内存占用最小的变量，

一个char类型的变量占用一个字节

占用多个字节的数据，以第一个字节的地址作为数据的地址，

用&寻址就是找这个地址

地址转成16进制看起来方便一点

```c
int main()
{
    int a = 10;//int a表示向内存申请4个字节的空间
    //10是存放在该内存空间内的数据
    peintf("%p",&a);//%p表达的是以地址的格式打印数据
    //&是取址符
    //&a表示要取a所在的内存空间第一个字节的地址
int* p1 = &a;//&表示取变量的地址
    //创建一个变量p1用来存放a的地址
    //用来存放地址的变量称为指针变量
    //int表示的不是p1的类型，是p指向的对象a的数据类型
    //*说明p1是一个指针变量
    //p1也可以用别的名字表示
    
    char ch = 'hhh';
    char* p2 = &ch;//32bit系统中，任何类型指针变量都是占用4个字节
    
    *p1 = 20 ;//*表示解引用操作符，*p1=a,这里相当于直接给a赋值
    //*p1表示通过p中存放的地址，找到p1指向的对象的地址
    //*p相当于a
return 0;
}
```



### 结构体

访问结构体对象的数组成员时，不能直接用 对象名.成员名 来访问



自定义类型的一种

```c
#include <stdio.h>
//这段代码定义了一个 Person 结构体，包含姓名、年龄和身高三个成员变量。
//然后在 main 函数中实例化了一个 person1 结构体变量，并给成员变量赋值，最后输出了这些成员变量的值。
// 定义一个结构体
struct Person {
    char name[50];
    int age;
    float height;
};

int main() {
    // 实例化一个结构体变量
    struct Person person1;

    // 给结构体成员赋值
    strcpy(person1.name, "Alice");
    person1.age = 25;
    person1.height = 165.5;

    // 输出结构体成员的值
    printf("Name: %s
", person1.name);
    printf("Age: %d
", person1.age);
    printf("Height: %.1f
", person1.height);

    return 0;
}
```



把一些单一的类型组合在一起

```c
#include <stdio.h>

struct Stu //创建一个学生的结构体，具有名字、年龄、性别、电话等属性。
{
    char name;
        int age;
    char sex;
    int tel;
}
int main()
{
    struct stu s ={"kidea",18,"boy","10086"};
    //struct stu相当于类型，s是用该类型创建的变量，{}大括号内是s初始化参数的值
    printf("%s %d %s %d",s.name,s.age,s.tel);
    //打印结构体s内的参数，.这个点是一个操作符
    
    return 0;
}

```

用结构体指针找到结构体内的成员的地址，然后打印其中的内容

```c
void print(struct Stu* ps)
{
    printf("%s %d %s %s\n",(*ps).name,(*ps).age,(*ps).sex,(*ps).tele);
    printf("%s %d %s %s\n",ps->name,ps->age,ps->sex,ps->tele);
    //这是两种等效表示指针寻址的方法
}
int main()
{
    struct Stu s = {"kidea",18,"boy","10086666666"};//创建结构体成员s并赋值
    
    print(&s);//打印结构体成员s的地址
    //等价于
    //结构体.成员名 寻址格式
    printf("%s %d %s %s\n",s.name,s.age,s.sex,s.tele);
    
    return 0;
}
```



#include #define 都是预编译指令



## 分支语句和循环语句

C语言的结构化

- 顺序结构
- 选择结构 if、switch
- 循环结构 for、while、do while



### 分支语句

```c
int age =10;
if(age<18)
    printf("青少年\n");
else if(age>=18 && age<28)
    printf("青年\n");
else if(age>28 && age<40)
    printf("中年\n")
    else
        printf("老了")；
return 0;
```

```c
int main()
{
    int day =0;
    switch (day)
    {
      case 1:
            printf("星期一\n");
            break;
        case 2:
            printf("星期二\n");
            break;
        case 3:
            printf("星期三\n");
        case 4:
            printf("星期四\n");      
    }
   
}
```



switch后面（）必须是整型变量

case后面（）必须是整型常量，字符也可以，因为对应的ASCII码值是整型

```c
switch (day)
{
    case 1:
    case 2:
    case 3:
    case 4:
    case 5: 
        printf("weekday\n");
        break;
    case 6: 
    case 7: 
      printf("weekend\n");
        break;
        
    default:
        printf("选择错误\n");
        break;
}

return 0;
```

可以实现多个条件匹配一个结果

case 1 ：	后面的冒号后的内容在case为真时执行

default ：	表示输入的case都不符合时的默认输出

break ;	会在当前为真的case执行完后跳出switch，即使后面的case为真也无法输出。

### 循环语句

用break可以直接跳出while循环

```c
int main()
{
    int i=1;
    while (i<=10)
    {
        printf("%d",i);
        i++;
    }
    return 0;
}
```

```c
int main()
{
    int i=1;
    while (i<=10)
    {
        if (5==i)
            break;
        printf("%d",i);
        i++;
    }
    return 0;
}
```





continue;  可以跳过while循环内位于continue后的语句，但是不会跳出循环。

```c
int main()
{
    int i=1;
    while (i<=10)
    {
        if (5==i)
            continue;
        printf("%d",i);
        i++;
    }
    return 0;
}
```



```c
int main()
{
    int ch = getchar(); //函数getchar()可以从获取键盘输入的一个字符的ASCII值，然后存储到变量ch中
int ch = 0;
    while ((ch = getchar())!= EOF)
    {
        putchar(ch);
    }

}
```







-----

-----

# 项目常用知识点汇总



## 文件结构模块化

在C++中，通常将函数的声明和定义分别放在头文件（.h文件）和源文件（.cpp文件）中，以便提高代码的可维护性和可重用性。下面通过一个具体的例子来说明.h文件和.cpp文件之间的关系，以及它们在一个类的实现中的作用。

### 1. 头文件（.h文件）

头文件通常包含类的声明、函数的声明和全局变量的声明，以及必要的头文件引用。头文件中不包含具体的实现代码，只包含函数的原型和数据成员的声明。例如：

**Calculator.h**
```cpp
#ifndef CALCULATOR_H
#define CALCULATOR_H

class Calculator {
public:
    Calculator();
    int add(int a, int b);
    int subtract(int a, int b);

private:
    int memory;
};

#endif
```

### 2. 源文件（.cpp文件）

源文件通常包含类的具体实现代码和函数的定义。源文件中包含了头文件，并实现了头文件中声明的函数。例如：

**Calculator.cpp**
```cpp
#include "Calculator.h"

Calculator::Calculator() {
    memory = 0;
}

int Calculator::add(int a, int b) {
    return a + b;
}

int Calculator::subtract(int a, int b) {
    return a - b;
}
```

### 3. 主程序文件

主程序文件（例如main.cpp）通常包含程序的入口点main函数和对类的实例化和使用。主程序文件需要包含头文件以访问类的声明和函数的声明。例如：

**main.cpp**
```cpp
#include <iostream>
#include "Calculator.h"

int main() {
    Calculator calc;
    int result = calc.add(5, 3);
    std::cout << "Result: " << result << std::endl;

    return 0;
}
```

### 总结

- 头文件用于声明类、函数和变量，提供接口给其他文件使用。
- 源文件用于实现头文件中声明的函数和类的具体功能。
- 主程序文件包含程序的入口点和对类的实例化和使用，需要包含头文件以访问声明。

通过将声明和定义分离到不同的文件中，可以提高代码的可维护性和可读性，同时也方便代码的重用和组织。

## 编译器查找规则

常用编译器（如GCC、Clang等）在查找和链接函数定义时遗留的规则通常如下：

查找规则：

当编译器遇到函数调用时，首先会在当前文件中查找函数的声明。
如果在当前文件中找不到函数声明，则会查找已经包含的头文件中是否包含了函数声明。
如果还是找不到，则会继续查找库文件（标准库或用户自定义的库）中是否包含了函数定义。

链接规则：

如果函数的定义位于单独的源文件中，编译器会在编译阶段生成==目标文件== （.o/.obj）。
在链接阶段，链接器会将所有的目标文件和必要的库文件链接在一起，生成最终==可执行文件==。
==链接器== 会解析函数调用，==将函数调用与实际的函数定义进行关联== ，以便生成完整的可执行文件。

库文件的搜索顺序：

链接器在查找库文件时会按照一定的搜索路径顺序进行搜索，通常包括系统默认的库路径和用户自定义的库路径。
搜索路径顺序可能包括当前目录、系统默认库目录、==环境变量== 指定的路径等。

静态库和动态库：

对于静态库（.a/.lib），链接器会将库文件的代码直接复制到可执行文件中。
对于动态库（.so/.dll），链接器会在运行时加载库文件，需要确保库文件在运行时可以找到。

这些规则是常用编译器在查找和链接函数定义时遵循的基本原则。在实际开发中，遵循这些规则可以确保函数调用能够正确地链接到相应的函数定义，从而生成可执行文件或库文件。



## 预处理指令

编译之前对代码进行文本替换、条件编译等操作。

以下是一些常见的C语言预处理指令：

#define: 用于定义宏

定义常量：`#define PI 3.14159`

定义函数宏：`#define SQUARE(x) ((x) * (x))`

#include: 用于包含头文件

`#include <stdio.h>`: 包含系统头文件
`#include "myheader.h"`: 包含用户==自定义的头文件==

条件编译相关的指令：

`#if, #ifdef, #ifndef, #elif, #else, #endif`: 用于条件编译，根据条件判断是否编译某段代码。

`#undef`: 用于取消已定义的宏。

`#pragma`: 用于向编译器发出特定的指令。

`#error` 和 `#warning`: 用于生成编译错误或警告信息。

`#line`: 用于修改行号和文件名信息。

`#ifdef` 和 `#ifndef`: 用于检查一个宏是否已经被定义，

`#ifdef `检查宏是否==已经定义==，

`#ifndef` 检查宏是==否未被定义==。

这些预处理指令在编译之前由预处理器处理，对源代码进行相应的处理，例如宏替换、条件编译等。

这些指令可以使得代码更具有灵活性和可移植性，能够根据不同的条件选择性地包含或排除代码段，以满足不同平台和需求的编译。

#ifndef 是C/C++预处理器中的条件编译指令，用于检查某个标识符是否已经被定义。如果这个标识符已经被定义过，那么条件为假，对应的代码段将被跳过；否则条件为真，对应的代码段将被编译。

具体来说，#ifndef 的使用形式如下：

```c
#ifndef identifier
    // 如果 identifier 未被定义，则执行这部分代码
#endif
```

解释一下上面的代码：

如果 identifier 没有被定义过（即未包含在之前的代码中），那么 #ifndef identifier 判断为真，下面的代码段将被编译。
如果 identifier 已经被定义过，那么 #ifndef identifier 判断为假，下面的代码段将被跳过，不会被编译。

这种机制通常用于==防止同一个头文件被多次包含==。

在头文件中使用 #ifndef 可以避免在多个地方重复包含同一个头文件，从而避免由此引发的重复定义错误。

通常与 #ifndef 一起使用的还有 #define 和 #endif：

```c
#ifndef MY_HEADER_H
#define MY_HEADER_H

// 头文件内容，一般是函数、结构体、类的声明

#endif
```

这是一种常见的防卫式声明（header guard）的写法，==确保同一个头文件在同一编译单元中只被包含一次==。

---

在C/C++中，宏定义的形式包括简单宏定义、带参数的宏定义和条件编译。

1. 简单宏定义：
   简单宏定义是最基本的宏定义形式，使用`#define`关键字来定义一个标识符代表一个常量值或者一段代码。例如：
   
   ```c
   #define PI 3.14159
   #define MAX(a, b) ((a) > (b) ? (a) : (b))
   ```
   上面的例子中，`PI`被定义为3.14159，`MAX`被定义为一个带参数的宏，用于返回两个数中的较大值。
   
2. 带参数的宏定义：
   带参数的宏定义允许在宏定义中使用参数，类似于函数的宏定义形式。例如：
   
   ```c
   #define SQUARE(x) ((x) * (x))
   ```
   上面的例子中，`SQUARE`是一个带有参数的宏，用于计算参数的平方。
   
3. 条件编译：
   条件编译是通过预处理指令来控制源代码的编译过程，常用的预处理指令包括`#if`、`#ifdef`、`#ifndef`、`#elif`、`#else`和`#endif`等。例如：
   
   ```c
   #define DEBUG 1
   #ifdef DEBUG
       // 只有在DEBUG被定义时才会编译这部分代码
       printf("Debug mode\n");
   #else
       // 在DEBUG未被定义时编译这部分代码
       printf("Release mode\n");
   #endif
   ```
   上面的例子中，`#ifdef`指令用于判断`DEBUG`是否被定义，根据条件进行编译。

总之，宏定义在C/C++中有多种形式，包括简单宏定义、带参数的宏定义和条件编译。条件编译在实际编程中非常有用，可以根据不同的条件选择性地编译不同的代码，从而实现更灵活的程序控制。



当编写C/C++程序时，有时候需要根据不同的条件选择性地编译特定的代码，这时就需要使用条件编译。条件编译是通过预处理指令来控制源代码的编译过程的一种技术。

##  ==条件编译==

1. `#if`：
   `#if`指令用于判断一个常量表达式的值是否为真，如果为真则编译后面的代码，否则忽略。例如：
   ```c
   #if DEBUG == 1
       // 只有当DEBUG的 值为1 时才会编译中间这部分代码
       printf("Debug mode\n");
   #endif
   ```

2. `#ifdef`：
   `#ifdef`指令用于判断一个标识符是否已经被定义，如果已经被定义则编译后面的代码，否则忽略。例如：

   ```c
   #ifdef DEBUG
       // 只有当DEBUG 被定义 时才会编译中间这部分代码
       printf("Debug mode\n");
   #endif
   ```

3. `#ifndef`：
   `#ifndef`指令与`#ifdef`相反，用于判断一个标识符是否未被定义，如果未被定义则编译后面的代码，否则忽略。例如：

   ```c
   #ifndef RELEASE
       // 只有当RELEASE 未被定义 时才会编译中间这部分代码
       printf("Not in release mode\n");
   #endif
   ```

4. `#elif`：
   `#elif`指令用于在 多个条件 之间进行选择，类似于`else if`语句。例如：

   ```c
   #if defined(DEBUG)
       printf("Debug mode\n");
   #elif defined(RELEASE)
       printf("Release mode\n");
   #else
       printf("Unknown mode\n");
   #endif
   ```

5. `#else`：
   `#else`指令用于在条件不成立时执行另外的代码块，类似于`else`语句。例如：

   ```c
   #ifdef DEBUG
       printf("Debug mode\n");
   #else
       printf("Not in debug mode\n");
   #endif
   ```

6. `#endif`：
   `#endif`指令用于==结束条件==编译块，==与`#if`、`#ifdef`、`#ifndef`等配对使用==

   例如：

   ```c
   #ifdef DEBUG
       printf("Debug mode\n");
   #endif
   ```

通过使用以上的==条件编译==指令，可以根据不同的条件选择性地编译特定的代码，从而实现更灵活的程序控制。



```c
h
```





## ==函数==

### 函数的声明

函数的声明指的是在程序中提供函数的原型，告诉编译器函数的名称、返回类型和参数列表。函数的声明通常在函数的调用之前，以便编译器知道函数的存在并能够对函数进行正确的调用。函数的声明通常包括函数的返回类型、函数名和参数列表，形式如下：

```c
return_type function_name(parameters);
```

例如，下面是一个函数的声明：

```c
int sum(int a, int b);
```

### 函数的定义

函数的定义指的是实现函数的具体代码块，即函数的功能实现部分。函数的定义通常包括函数的返回类型、函数名、参数列表和函数体，形式如下：

- 函数名在符合标识符规定下可自定义
- 参数最好指定数据类型

```c
return_type function_name(parameters) {
    // 函数体
    // 实现函数的具体功能
}
```

例如，下面是一个函数的定义：

```c
int sum(int a, int b) {
    return a + b;
}
```

### 函数的调用

- 先定义后调用的函数不用声明

- 先调用后定义的函数，要在调用前声明

函数的调用指的是 在程序中使用函数来执行特定的功能。

函数调用时使用函数的名称和参数列表，通过传递参数来调用函数。函数的调用可以在程序的任何地方进行，只要函数的==声明在调用之前== 。函数的调用形式如下：

```c
return_value = function_name(arguments);
```

例如，调用上面定义的`sum`函数：

```c
int result = sum(3, 5);
//将实参(3,5)传递给形参(a,b)，然后用变量result来接收sum的返回值
```

总结来说，函数的声明告诉编译器函数的原型，函数的定义实现函数的具体功能，函数的调用使用函数执行特定的功能。在C/C++中，合理的函数声明、定义和调用是程序正确运行的关键。

----

## LVGL API的调用

相关知识点

- 结构体类型的指针变量
- 结构体类型的指针函数
- 接收参数和返回类型也可以是 结构体类型的指针函数

在接受参数（父对象的结构体指针类型函数）的基础上创建一个子对象（结构体类型的指针变量）

 在LVGL中，当您使用`lv_obj_create`创建对象时，可以自定义对象的名称。这个名称在内部用于唯一标识对象，以便在后续的编程中方便地引用。自定义对象名称的方法是在创建对象时使用`lv_obj_t`结构体的成员变量`name`。

以下是自定义对象名称的示例：

```c
lv_obj_t   *label     =     lv_obj_create(NULL,   LV_OBJ_ATTR_FLAG_EXPAND);
lv_obj_t   *label2   =     lv_obj_create(NULL,   LV_OBJ_ATTR_FLAG_EXPAND);

//  设置对象名称
lv_obj_set_name(label,  "my_label");
lv_obj_set_name(label2,  "my_label2");

//  后续编程中，可以使用名称来引用对象
lv_obj_t  *active_label   =  lv_obj_get_name_active("my_label");
```

在这个例子中，我们创建了两个标签对象`label`和`label2`，并为它们分别设置了自定义名称"my_label"和"my_label2"。在后续的编程中，我们可以使用这些名称来引用相应的对象。

需要注意的是，自定义对象名称仅仅是一个方便编程的标识符，它不会影响对象的性能和功能。在实际应用中，您可以根据需要为对象设置名称，以便在代码中更好地管理和维护。
