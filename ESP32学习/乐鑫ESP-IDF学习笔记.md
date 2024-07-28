# 乐鑫ESP-IDF学习笔记

- B站-孤独的二进制

## 开发环境搭建



### Windows 10搭建   CMD  IDF：



#### IDF程序下载与安装

查找乐鑫官方文档：docs.espressif.com

![image-20240506094609418](../AppData/Roaming/Typora/typora-user-images/image-20240506094609418.png)

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506095031530.png" alt="image-20240506095031530" style="zoom:30%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506095515633.png" alt="image-20240506095515633" style="zoom:30%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506095902473.png" alt="image-20240506095902473" style="zoom: 50%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506103914262.png" alt="image-20240506103914262" style="zoom:50%;" />

不同时期的常用版本不一样，可以在 www.github.com/espressif 上随便打开几个项目看一下用什么版本



下载完成后双击exe文件安装

安装步骤：

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506104028826.png" alt="image-20240506104028826" style="zoom:50%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506104113030.png" alt="image-20240506104113030" style="zoom:50%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506104122517.png" alt="image-20240506104122517" style="zoom:50%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506104147525.png" alt="image-20240506104147525" style="zoom:50%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506104222712.png" alt="image-20240506104222712" style="zoom:50%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506104308814.png" alt="image-20240506104308814" style="zoom: 40%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506105133108.png" alt="image-20240506105133108" style="zoom:50%;" />

![image-20240506105156292](../AppData/Roaming/Typora/typora-user-images/image-20240506105156292.png)

![image-20240506105806214](../AppData/Roaming/Typora/typora-user-images/image-20240506105806214.png)

安装结束



#### IDF运行验证

编译例程验证IDF是否安装完成

打开 CMD

![image-20240506110209833](../AppData/Roaming/Typora/typora-user-images/image-20240506110209833.png)

![image-20240506110606889](../AppData/Roaming/Typora/typora-user-images/image-20240506110606889.png)

打开IDF的安装文件夹，找到hello_world然后复制一份

![image-20240506111129571](../AppData/Roaming/Typora/typora-user-images/image-20240506111129571.png)

然后回到 根目录 下新建一个文件夹并命名为 projects，把hello_world粘贴进去

![image-20240506111425051](../AppData/Roaming/Typora/typora-user-images/image-20240506111425051.png)

##### 编译程序

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506111847844.png" alt="image-20240506111847844" style="zoom:50%;" />



![image-20240506113741218](../AppData/Roaming/Typora/typora-user-images/image-20240506113741218.png)

![image-20240506111829772](../AppData/Roaming/Typora/typora-user-images/image-20240506111829772.png)

![image-20240506111808715](../AppData/Roaming/Typora/typora-user-images/image-20240506111808715.png)

![image-20240506113334716](../AppData/Roaming/Typora/typora-user-images/image-20240506113334716.png)

![image-20240506113342402](../AppData/Roaming/Typora/typora-user-images/image-20240506113342402.png)

![image-20240506113349191](../AppData/Roaming/Typora/typora-user-images/image-20240506113349191.png)

##### 上传程序

插上esp32板子，在设备管理器里面查看是否安装对应驱动，也可以看到对应的端口号

![image-20240506114224021](../AppData/Roaming/Typora/typora-user-images/image-20240506114224021.png)

![image-20240506114302400](../AppData/Roaming/Typora/typora-user-images/image-20240506114302400.png)

上传完成后打开串口监视器

![image-20240506114424689](../AppData/Roaming/Typora/typora-user-images/image-20240506114424689.png)

![image-20240506114747597](../AppData/Roaming/Typora/typora-user-images/image-20240506114747597.png)

如果想要上传程序后自动打开串口监视器  idf.py flash monitor -p COM3

退出串口监视器 快捷键ctrl+]

练习：可以再到例程里复制一份blink来玩一下





##### 误操作：

不小心删除了桌面的快捷方式，然后打开了windows的CMD发现根本找不到idf.py

![image-20240506115631199](../AppData/Roaming/Typora/typora-user-images/image-20240506115631199.png)

其实IDF的CMD和windows的CMD是不一样的，把IDF的CMD找回来就行了

![image-20240506120031836](../AppData/Roaming/Typora/typora-user-images/image-20240506120031836.png)

关于环境变量的问题

![image-20240506171841453](../AppData/Roaming/Typora/typora-user-images/image-20240506171841453.png)

![image-20240506171904126](../AppData/Roaming/Typora/typora-user-images/image-20240506171904126.png)

可以通过配置环境变量来解决第一个问题

#### 环境变量的配置

打开windows的cmd

![image-20240506173106330](../AppData/Roaming/Typora/typora-user-images/image-20240506173106330.png)

使用 cd 命令打开对应的文件夹

![image-20240506173543812](../AppData/Roaming/Typora/typora-user-images/image-20240506173543812.png)

根据目录提示一步步打开文件夹

![image-20240506173759274](../AppData/Roaming/Typora/typora-user-images/image-20240506173759274.png)

![image-20240506174126126](../AppData/Roaming/Typora/typora-user-images/image-20240506174126126.png)

最终找到 ==export.bat== 这个文件，这个是用来自动配置环境变量的程序

![image-20240506174356566](../AppData/Roaming/Typora/typora-user-images/image-20240506174356566.png)

因为再==path==中缺少python和git的路径导致不能执行export.bat这个文件（需要下载python和git）

![image-20240506174856893](../AppData/Roaming/Typora/typora-user-images/image-20240506174856893.png)

再IDF的PowerShell中使用 echo $env:path 命令提取环境变量的path

![image-20240506175058363](../AppData/Roaming/Typora/typora-user-images/image-20240506175058363.png)

复制这个path，然后打开windows的cmd，把这个path粘贴到 path=后面

![image-20240506175553420](../AppData/Roaming/Typora/typora-user-images/image-20240506175553420.png)

然后就可以正常运行 export.bat 然后打开 idf.py 了

![image-20240506175749651](../AppData/Roaming/Typora/typora-user-images/image-20240506175749651.png)

但是这里配置的path是一次性的，想要永久配置需要在系统中进行配置

windows环境变量path配置

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506180549059.png" alt="image-20240506180549059" style="zoom:80%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506180627389.png" alt="image-20240506180627389" style="zoom: 67%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506180735128.png" alt="image-20240506180735128" style="zoom: 67%;" />

<img src="../AppData/Roaming/Typora/typora-user-images/image-20240506180753834.png" alt="image-20240506180753834" style="zoom:67%;" />

到这里已经完全完成命令行版的IDF开发环境搭建



### Mac环境搭建

先用win开发吧，后面有空了再搞mac的环境





### Windows利用 VScode搭建IDE

在官网下载　ＶＳｃｏｄｅ

顺便检查一下ｃｍｄ中ｉｄｆ．ｐｙ是否正常

在VScode中打开extensions安装 esp-IDF 和 C/C++ (一般默认安装)

![image-20240512182710680](../AppData/Roaming/Typora/typora-user-images/image-20240512182710680.png)



![image-20240512182822706](../AppData/Roaming/Typora/typora-user-images/image-20240512182822706.png)

然后打开这个命令 >ESP-IDF:configure ESP-IDF extension

![image-20240512183303933](../AppData/Roaming/Typora/typora-user-images/image-20240512183303933.png)

![image-20240512183310335](../AppData/Roaming/Typora/typora-user-images/image-20240512183310335.png)

![image-20240512183738483](../AppData/Roaming/Typora/typora-user-images/image-20240512183738483.png)

![image-20240512184108712](../AppData/Roaming/Typora/typora-user-images/image-20240512184108712.png)

![image-20240512184200236](../AppData/Roaming/Typora/typora-user-images/image-20240512184200236.png)

![image-20240512184348684](../AppData/Roaming/Typora/typora-user-images/image-20240512184348684.png)

![image-20240512184453423](../AppData/Roaming/Typora/typora-user-images/image-20240512184453423.png)

![image-20240512184557040](../AppData/Roaming/Typora/typora-user-images/image-20240512184557040.png)

运行menuconfig

![image-20240512184843313](../AppData/Roaming/Typora/typora-user-images/image-20240512184843313.png)

![image-20240512185256905](../AppData/Roaming/Typora/typora-user-images/image-20240512185256905.png)

 在menuconfig中的配置会自动同步到sdkconfig里面,如图所示

![image-20240512185627599](../AppData/Roaming/Typora/typora-user-images/image-20240512185627599.png)

![image-20240512185848686](../AppData/Roaming/Typora/typora-user-images/image-20240512185848686.png)

![image-20240512190408982](../AppData/Roaming/Typora/typora-user-images/image-20240512190408982.png)

![image-20240512190534838](../AppData/Roaming/Typora/typora-user-images/image-20240512190534838.png)

收工



#### 错误案例

![image-20240512191329755](../AppData/Roaming/Typora/typora-user-images/image-20240512191329755.png)

![image-20240512191429257](../AppData/Roaming/Typora/typora-user-images/image-20240512191429257.png)

![image-20240512191547409](../AppData/Roaming/Typora/typora-user-images/image-20240512191547409.png)

![image-20240512191648541](../AppData/Roaming/Typora/typora-user-images/image-20240512191648541.png)

打开命令 >esp-idf: add vscode configuration folder

![image-20240512191951668](../AppData/Roaming/Typora/typora-user-images/image-20240512191951668.png)

![image-20240512192226868](../AppData/Roaming/Typora/typora-user-images/image-20240512192226868.png)

还不行就再编译一下,然后关闭VScode重新打开就可以了



## 构建项目

一个发音很水，但是乐于助人的up

关于cmakelist的介绍：

[ESP32-IDF中cmake文件管理(添加头文件 C文件 组件的方法)_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1w14y1s7oy/?spm_id_from=333.337.search-card.all.click&vd_source=168cfdeaa638dd4ee22415c821287ce1)

在高版本中出现的问题解决方法如下图：

![image-20240623213835358](../AppData/Roaming/Typora/typora-user-images/image-20240623213835358.png)
