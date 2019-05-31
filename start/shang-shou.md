# 上手

本文主要说明如何编写、编译代码以及固件的烧录，请先获取完整SDK和编译工具链，并已搭建好开发环境。

#### SDK代码结构

![](/images/sdk-tree.png)

build:编译中间件、固件、编译脚本存放处；

cmake：编译构建系统；

face-module-sdk:人脸识别支持库；

fat-fs-module：文件系统支持库；

lds:编译连接文件；

lib:官方原代码；

src:项目代码存放处；

通常情况下，只需要在build和src处操作。

#### 开始第一份代码

在src目录下新建项目文件夹，比如新建hello_world，在此文件下放置源代码

cd src && mkdir hello_world

![](/images/first-code.png)

添加源代码入口文件是main.c，入口函数为main()

```
int core1_function(void *ctx)
{
    uint64_t core = current_coreid();
    printf("Core %ld Hello world\n", core);
    while(1);
}

int main()
{
    uint64_t core = current_coreid();
    printf("Core %ld Hello world\n", core);
    register_core1(core1_function, NULL);
    while(1);
}
```

#### 编译

进入build目录下执行./getbin.sh xxx；xxx指代src下的项目名称，比如项目名称是hello_world

执行./getbin.sh hello_world

![](/images/complier-start.png)

在build目录会生成hello_world目录，包含最终生成的hello_world.bin固件，此固件是最终下载到开发板上的。

![](/images/complier-end.png)

注意：getbin.sh脚本第7行/opt/my-kendryte-toolchain是编译工具默认路径，此路径必须和编译工具实际放置的位置一致。

![](/images/get-sh.png)

#### 下载固件

支持linux和windows下下载固件到开发板。

**A、linux环境下：**

1、用Type-C连接开发板和电脑；

2、按开发板上的住boot按键；

3、执行以下固件下载命令：

​	python3 kflash.py -b 200000 -p ttyUSB0 firmware.bin 

​	说明：kflash.py 下载脚本

​				-b 波特率设置

​				-p 选择串口

​				firmware.bin 要烧录的固件

例如：

​	执行下载命令：

​	![](/images/linux-flash-2.png)

​	当出现如下图时放开boot按键，进入下载模式

​	![](/images/linux-flash-3.png)

整个过程如下图所示：

​	![](/images/linux-flash-1.png)

**B、windows环境下：**

1、用Type-C连接开发板和电脑

2、打开k-flash.exe下载工具，选择对应串口，导入固件

​	![](/images/windows-flash-1.png)

3、先按住开发板的boot按键，点击K-Flash的烧录按钮Flash,出现downloading时可松开boot按键，   

​      等待烧录完成。

​	![](/images/windows-flash-2.png)

4、按复位键重新上电，可连接串口调试。

#### 调试

在window上使用串口助手或SecureCRT可方便进行调试。

​	![](/images/windows-debug.png)

说明：

- 实际使用中可方便的把ubuntu下的固件共享到windows方便在windows下用K-Flash工具烧录。
- 或者直接在ubuntu上安装samba网络服务器共享文件，且可在windows下用sourceinsight方便查看代码。