---
description:  双目摄像头影像显示
---

## 功能描述

DVP 是摄像头接口模块，支持把摄像头输入图像数据转发给AI 模块或者内。

- 支持RGB565、RGB422 与单通道Y 灰度输入模式
- 支持设置帧中断
- 支持设置传输地址
- 支持同时向两个地址写数据（输出格式分别是RGB888 与RGB565）
- 支持丢弃不需要处理的帧

## API说明

### 1、dvp_init

> **描述：**初始化DVP
>
> **函数原型：**
>
> ```
> void dvp_init(uint8_t reg_len)
> ```
>
> **参数：**
>
> reg_len: sccb寄存器长度（输入）
>
> **返回值：**
>
> 无

### 2、dvp_set_image_format

> **描述：**设置图像接收模式，RGB 或YUV
>
> **函数原型：**
>
> ```
> void dvp_set_image_format(uint32_t format)
> ```
>
> **参数：**
>
> format: 图像模式DVP_CFG_RGB_FORMAT RGB 模式DVP_CFG_YUV_FORMAT YUV 模式（输入）
>
> **返回值：**
>
> 无

### 3、dvp_set_output_enable

> **描述：**设置输出模式使能或禁用
>
> **函数原型：**
>
> ```
> void dvp_set_output_enable(dvp_output_mode_t index, int enable)
> ```
>
> **参数：**
>
> index: 图像输出至内存或AI（输入）
>
> enable：0：禁用  1：使能（输入）
>
> **返回值：**
>
> 无

### 4、dvp_set_image_size

> **描述：**设置DVP 图像采集尺寸
>
> **函数原型：**
>
> ```
> void dvp_set_image_size(uint32_t width, uint32_t height)
> ```
>
> **参数：**
>
> width: 图像宽度（输入）
>
> height: 图像高度（输入）
>
> **返回值：**
>
> 无

### 5、dvp_set_ai_addr

> **描述：**设置AI 存放图像的地址，供AI 模块进行算法处理
>
> **函数原型：**
>
> ```
> void dvp_set_ai_addr(uint32_t r_addr, uint32_t g_addr, uint32_t b_addr)
> ```
>
> **参数：**
>
> r_addr: 红色分量地址（输入）
>
> g_addr: 绿色分量地址（输入）
>
> b_addr: 蓝色分量地址（输入）
>
> **返回值：**
>
> 无

### 6、dvp_set_display_addr

> **描述：**设置采集图像在内存中的存放地址，可以用来显示
>
> **函数原型：**
>
> ```
> void dvp_set_display_addr(uint32_t addr)
> ```
>
> **参数：**
>
> addr: 存放图像的内存地址（输入）
>
> **返回值：**
>
> 无

### 7、dvp_config_interrupt

> **描述：**设置图像开始和结束中断状态，使能或禁用
>
> **函数原型：**
>
> ```
> void dvp_config_interrupt(uint32_t interrupt, uint8_t enable)
> ```
>
> **参数：**
>
> interrupt: 中断类型DVP_CFG_START_INT_ENABLE 图像开
> 					始采集中断DVP_CFG_FINISH_INT_ENABLE 图像
> 					结束采集中断（输入）
>
> enable：0：禁止1：使能（输入）
>
> **返回值：**
>
> 无

### 8、dvp_get_interrupt

> **描述：**判断是否是输入的中断类型。
>
> **函数原型：**
>
> ```
> int dvp_get_interrupt(uint32_t interrupt)
> ```
>
> **参数：**
>
> interrupt: 中断类型DVP_CFG_START_INT_ENABLE 图像开
> 					始采集中断DVP_CFG_FINISH_INT_ENABLE 图像
> 					结束采集中断（输入）
>
> **返回值：**
>
> 无

### 9、dvp_clear_interrupt

> **描述：**清除中断
>
> **函数原型：**
>
> ```
> void dvp_clear_interrupt(uint32_t interrupt);
> ```
>
> **参数：**
>
> interrupt: 中断类型DVP_CFG_START_INT_ENABLE 图像开
> 				始采集中断DVP_CFG_FINISH_INT_ENABLE 图像
> 				结束采集中断（输入）
>
> **返回值：**
>
> 无

### 10、dvp_start_convert

> **描述：**开始采集图像，在确定图像采集开始中断后调用
>
> **函数原型：**
>
> ```
> void dvp_start_convert(void)
> ```
>
> **参数：**
>
> r_addr: 红色分量地址（输入）
>
> g_addr: 绿色分量地址（输入）
>
> b_addr: 蓝色分量地址（输入）
>
> **返回值：**
>
> 无

### 11、dvp_enable_burst

> **描述：**使能突发传输模式
>
> **函数原型：**
>
> ```
> void dvp_enable_burst(void)
> ```
>
> **参数：**
>
> r_addr: 红色分量地址（输入）
>
> g_addr: 绿色分量地址（输入）
>
> b_addr: 蓝色分量地址（输入）
>
> **返回值：**
>
> 无
>

### 12、dvp_disable_burst

> **描述：**禁用突发传输模式
>
> **函数原型：**
>
> ```
> void dvp_disable_burst(void)
> ```
>
> **参数：**
>
> r_addr: 红色分量地址（输入）
>
> g_addr: 绿色分量地址（输入）
>
> b_addr: 蓝色分量地址（输入）
>
> **返回值：**
>
> 无
> 

### 13、dvp_enable_auto

> **描述：**使能自动接收图像模式
>
> **函数原型：**
>
> ```
> void dvp_enable_auto(void)
> ```
>
> **参数：**
>
> 无
>
> g_addr: 绿色分量地址（输入）
>
> b_addr: 蓝色分量地址（输入）
>
> **返回值：**
>
> 无
>

### 14、dvp_disable_auto

> **描述：**禁用自动接收图像模式
>
> **函数原型：**
>
> ```
> void dvp_disable_auto(void)
> ```
>
> **参数：**
>
> 无
>
> g_addr: 绿色分量地址（输入）
>
> b_addr: 蓝色分量地址（输入）
>
> **返回值：**
>
> 无
>

### 15、dvp_sccb_send_data

> **描述：**通过sccb 发送数据
>
> **函数原型：**
>
> ```
> void dvp_sccb_send_data(uint8_t dev_addr, uint16_t reg_addr, uint8_t reg_data)
> ```
>
> **参数：**
>
> dev_addr: 外设图像传感器SCCB 地址（输入）
>
> reg_addr: 外设图像传感器寄存器（输入）
>
> reg_data: 发送的（输入）
>
> **返回值：**
>
> 无
>

### 16、dvp_sccb_receive_data

> **描述：**通过SCCB 接收数据
>
> **函数原型：**
>
> ```
> uint8_t dvp_sccb_receive_data(uint8_t dev_addr, uint16_t reg_addr)
> ```
>
> **参数：**
>
> dev_addr: 外设图像传感器SCCB 地址（输入）
>
> reg_addr: 外设图像传感器寄存器（输入）
>
> **返回值：**
>
> 读取寄存器的数据
> 
### 17、dvp_set_xclk_rate

> **描述：**设置xclk 的速率
>
> **函数原型：**
>
> ```
> uint32_t dvp_set_xclk_rate(uint32_t xclk_rate)
> ```
>
> **参数：**
>
> xclk_rate: xclk 的速率（输入）
>
> **返回值：**
>
> xclk 的实际速率
>

### 18、dvp_sccb_set_clk_rate

> **描述：**设置sccb 的速率
>
> **函数原型：**
>
> ```
> uint32_t dvp_sccb_set_clk_rate(uint32_t clk_rate)
> ```
>
> **参数：**
>
> clk_rate: clk_rate sccb 的速率（输入）
>
> **返回值：**
>
> 0：失败，设置的速率太低无法满足
>
> 非0：实际的sccb 速率
## 数据类型

### 1、dvp_output_mode_t

​	描述：DVP 输出图像的模式

​    类型：

​			DVP_OUTPUT_AI ：AI 输出

​			DVP_OUTPUT_DISPLAY ：向内存输出用于显示	

## 参考例程

​		参考/src/dvp_dual_sensor

