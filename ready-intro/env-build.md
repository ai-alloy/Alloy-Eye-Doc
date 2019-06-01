# 开发环境搭建

## 1、安装linux环境

可在windows上安装workstation虚拟机，然后在虚拟机上安装ubuntu系统（建议使用16.04）

关于虚拟机上安装ubuntu系统可以自行百度，资料还是比较详细的。

* [ ] [workstation+ubuntu-16.04下载](http://www.ai-alloy.com/)

## 2、安装依赖库

在linux下，需要下载linux版本固件烧录脚本Kflash.py，可在github下载：

git clone [https://github.com/kendryte/kflash.py.git](https://github.com/kendryte/kflash.py.git)

Kflash.py是基于python3编写的，需要安装python3相关库，如下：

sudo apt update

sudo apt install python3 python3-pip

sudo pip3 install pyserial

## 3、获取SDK代码

完整的SDK代码需通过以下方式获取。

* [ ] [获取SDK](http://www.ai-alloy.com/)

github会有提供相关样例，包括src目录和build目录，但不是完整的SDK，build目录的是已经根据src对应目录编译的最终文件，直接下载对应的bin文件到开发板可直接跑。

* [ ] [github克隆（非完整）](https://github.com/ai-alloy/scrapy-cookbook)

## 4、获取编译工具链

编译工具链需通过以下方式获取。

* [ ] [编译工具链获取](http://www.ai-alloy.com/)

编译器工具可解压到/opt/my-kendryte-toolchain这个默认路径，编译脚本使用的是这个默认路径，也可自行修改。

## 5、下载Kflash烧录工具

此Kflash工具是windows版本（Kflash支持windows和linux两种方式），用于windows下下载固件到开发板

* [ ] [windows版本Kflash下载](https://s3.cn-north-1.amazonaws.com.cn/dl.kendryte.com/documents/K-Flash.zip)

## 6、Tpye-C连接线

主要用于供电，烧录以及调试。

