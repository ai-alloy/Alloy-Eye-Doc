# Linux 下Jtag 调试样例

通过jtag可以很方便的调试k210芯片，提高工作效率，要通过Jtag调试硬件，需要用到的软硬件如下：

## 硬件准备

1. k210开发板
2. jtag调试器



## 软件准备

1. openocd，[下载地址](https://github.com/kendryte/openocd-kendryte/releases/tag/v0.2.3) ，根据自己的电脑系统选择对应的版本下载，这里以linux版本进行讲解，win下面请参照讲解自行调试，不另外讲解。

   

2. gdb，一般linux系统会自带

## 下载依赖

1. first in Debian/Ubuntu,Install the following libraries if you do not have:

   ```
   sudo apt install libusb-dev libftdi-dev libhidapi-dev -y
   ```

2. then download the JLink driver (DEB installer) 

     https://www.segger.com/downloads/jlink/#J-LinkSoftwareAndDocumentationPack

   and install it:

   ```shell
   sudo dpkg -i JLink_Linux_xxx_xxx.deb
   ```



## 文件讲解

openocd 文件夹内容如下

![](images/openocd.png)

bin文件夹为openocd执行文件

tcl文件夹下存放调试配置文件



## 开始调试

官方针对J-Link制作了一份调试模板，我们这里直接按照官方的模板来设置我们的J-Link设备。模板路径：`/tcl/kendryte.cfg`



启动openocd 调试服务器，命令如下：

`sudo ./bin/openocd -f ./tcl/kendryte.cfg -m0`

`-m`选项来指定要调试的是哪一个内核，可选数字为0或1

`kendryte.cfg`为J-Link调试配置文件。



可以通过下列命令来查看更多的openocd命令

`./bin/openocd -h



openocd启动之后，可以通过gdb连接进行调试，连接命令：

`(gdb) target remote localhost:3333`

连接成功后即可开始调试工作。

```
(gdb) target remote localhost:3333
Remote debugging using localhost:3333
...
(gdb) load
Loading section .vectors, size 0x100 lma 0x20000000
Loading section .text, size 0x5a0 lma 0x20000100
Loading section .data, size 0x18 lma 0x200006a0
Start address 0x2000061c, load size 1720
Transfer rate: 22 KB/sec, 573 bytes/write.
(gdb) c
Continuing.
...
```

更多详细内容参考：https://github.com/kendryte/openocd-kendryte/wiki