---
description:  触摸屏驱动显示
---

## 功能描述

DEMO 板提供了电容屏和电阻屏的驱动方式，电阻屏采用spi的方式（样例中使用IO口模拟SPI的方式），电容屏使用I2C通讯方式，电阻屏需要校正，电容屏不需要，具体参考样例。

board_config.h文件中USE_RTP_PANEL和USE_CAP_PANEL这个两个宏分别对应电阻屏和电容屏的代码编译开关；

基本原理是TP中断触发了，CPU是通过SPI或I2C方式读取触摸的坐标位置。



## 参考例程

​		参考/src/tp

