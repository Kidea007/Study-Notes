# ESP32学习笔记

MCU：ESP32

开发环境：ESP-IDF 4.3

idf使用方式：powerShell

代码编辑器：SourceInsight 4.0

串口工具：友善串口调试工具

串口芯片：CH340 

---

编译程序：

```shell
PS D:\Espressif\frameworks\esp-idf-v5.1.2> cd .\examples\get-started\hello_world
#cd到项目文件夹下
PS D:\Espressif\frameworks\esp-idf-v5.1.2\examples\get-started\hello_world> idf.py build
#第一次编译有点久
```

下载程序：

先一直按住boot，再按一下reset松开

然后执行下载命令

```shell
PS D:\Espressif\frameworks\esp-idf-v5.1.2\examples\get-started\hello_world>idf.py -p (PORT) flash
#PORT填自己的串口号，（在设备管理器中查看）
```

出现Connecting……..松开boot即可

串口打印的信息可以在串口助手查看

> 华清远见的这套开发环境有点老了，还是在vscode里用idf插件开发方便
>
> SourceInsight的主题实在太丑，远不如vscode

