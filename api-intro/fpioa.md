---
description:  现场可编程IO阵列
---

## 功能描述

FPIOA(现场可编程IO阵列)允许用户将255 个内部功能映射到芯片外围的48个自由IO上。

- 支持IO 的可编程功能选择
- 支持IO 输出的8 种驱动能力选择
- 支持IO 的内部上拉电阻选择
- 支持IO 的内部下拉电阻选择
- 支持IO 输入的内部施密特触发器设置
- 支持IO 输出的斜率控制
- 支持内部输入逻辑的电平设置

## API说明

### 1、fpioa_set_function

> **描述**：设置IO0-IO47 管脚复用功能
>
> **函数原型**：
>
> ```
> int fpioa_set_function(int number, fpioa_function_t function)
> ```
>
> **参数**：
>
> number： IO 管脚号
>
> function： FPIOA 功能号
>
> **返回值**：
>
> 0： 成功
>
> 非0： 失败

### 2、fpioa_get_io_by_function

>**描述**：根据功能号获取IO 管脚号
>
>**函数原型**：
>
>```
>int fpioa_get_io_by_function(fpioa_function_t function)
>```
>
>**参数**：
>
>function： FPIOA 功能号
>
>**返回值**：
>
>大于等于0： IO 管脚号
>
>小于0： 失败

### 3、fpioa_get_io

>**描述**：获得IO 管脚的配置
>
>**函数原型**：
>
>```
>int fpioa_get_io(int number, fpioa_io_config_t *cfg)
>```
>
>**参数**：
>
>number： IO 管脚号（输入）
>
>cfg： 管脚功能结构体（输出）
>
>**返回值**：
>
>0： 成功
>
>非0：失败

### 4、fpioa_set_io

>**描述：**设置IO 管脚的配置
>
>**函数原型：**
>
>```
>int fpioa_set_io(int number, fpioa_io_config_t *cfg)
>```
>
>**参数：**
>
>number： IO 管脚号（输入）
>
>cfg： 管脚功能结构体（输入）
>
>**返回值：**
>
>0： 成功
>
>非0：失败

### 5、fpioa_set_tie_enable

>**描述：**使能或禁用FPIOA 功能输入信号的强制输入电平功能
>
>**函数原型：**
>
>```
>int fpioa_set_tie_enable(fpioa_function_t function, int enable)
>```
>
>**参数：**
>
>function： FPIOA 功能号（输入）
>
>enable： 强制输入电平使能位（输入） 0：禁用 1：使能
>
>**返回值：**
>
>0： 成功
>
>非0：失败

### 6、fpioa_set_tie_value

>**描述：**设置FPIOA 功能输入信号的强制输入电平高或者低，仅在强制输入电平功能启用时生效
>
>**函数原型：**
>
>```
>int fpioa_set_tie_value(fpioa_function_t function, int value)
>```
>
>**参数：**
>
>function： FPIOA 功能号（输入）
>
>value： 强制输入电平值（输入）0：低 1：高
>
>**返回值：**
>
>0： 成功
>
>非0：失败

### 7、fpioa_set_io_pull

>**描述：**设置IO 的上拉下拉
>
>**函数原型：**
>
>```
>int fpioa_set_io_pull(int number, fpioa_pull_t pull)
>```
>
>**参数：**
>
>number： IO编号（输入）
>
>pull： 上下拉值（输入）
>
>**返回值：**
>
>0： 成功
>
>非0：失败

### 8、fpioa_get_io_pull

>**描述：**获取IO 管脚上下拉值
>
>**函数原型：**
>
>```
>int fpioa_get_io_pull(int number)
>```
>
>**参数：**
>
>number： IO编号（输入）
>
>**返回值：**
>
>0 ：无上下拉
>1： 下拉
>2 ：上拉

### 9、fpioa_set_io_driving

>**描述：**设置IO 管脚的驱动能力
>
>**函数原型：**
>
>```
>int fpioa_set_io_driving(int number, fpioa_driving_t driving)
>```
>
>**参数：**
>
>number： IO编号（输入）
>
>driving:	 驱动能力（输入）
>
>**返回值：**
>
>0： 成功
>
>非0：失败

### 10、fpioa_get_io_driving

>**描述：**获取IO 管脚的驱动能力
>
>**函数原型：**
>
>```
>int fpioa_get_io_driving(int number)
>```
>
>**参数：**
>
>number： IO编号（输入）
>
>**返回值：**
>
>大于等于0： 驱动能力
>
>小于0：失败

## 数据类型

### 1、fpioa_function_t

​	描述：管脚的功能编号

​    类型：

​			

### 2、fpioa_io_config_t

​	描述：FPIOA 的配置

​	类型：

​			

### 3、fpioa_pull_t

​	描述：FPIOA 上拉或者下拉特性

​	类型：

​			

### 4、fpioa_driving_t

​	描述：FPIOA 驱动能力编号

​	类型：

​			FPIOA_DRIVING_0 	驱动能力0

​			FPIOA_DRIVING_1 	驱动能力1

​			FPIOA_DRIVING_2 	驱动能力2

​			FPIOA_DRIVING_3 	驱动能力3

​			FPIOA_DRIVING_4 	驱动能力4

​			FPIOA_DRIVING_5 	驱动能力5

​			FPIOA_DRIVING_6 	驱动能力6

​			FPIOA_DRIVING_7 	驱动能力7		

驱动能力表：

A、低电平输入电流

| ds   | Min(mA) | Typ(mA) | Max(mA) |
| ---- | ------- | ------- | ------- |
| 0    | 3.2     | 5.4     | 8.3     |
| 1    | 4.7     | 8.0     | 12.3    |
| 2    | 6.3     | 10.7    | 16.4    |
| 3    | 7.8     | 13.2    | 20.2    |
| 4    | 9.4     | 15.9    | 24.2    |
| 5    | 10.9    | 18.4    | 28.1    |
| 6    | 12.4    | 20.9    | 31.8    |
| 7    | 13.9    | 23.4    | 35.5    |



## 参考例程

​		