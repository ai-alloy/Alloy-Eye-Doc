---
description:  现场可编程IO阵列（FPIOA）
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

### 1、gpiohs_set_drive_mode

> **描述**：设置高速GPIO驱动模式
>
> **函数原型**：
>
> ```
> void gpiohs_set_drive_mode(uint8_t pin, gpio_drive_mode_t mode)
> ```
>
> **参数**：
>
> pin：GPIO管脚（IN）
>
> mode： GPIO驱动模式（IN）
>
> **返回值**：
>
> 无
>

### 2、gpiohs_get_pin

>**描述**：设置GPIO的管脚值
>
>**函数原型**：
>
>```
>void gpiohs_set_pin(uint8_t pin, gpio_pin_value_t value)
>```
>
>**参数**：
>
>pin：GPIO 管脚值(IN)
>
>value：GPIO值(IN)
>
>**返回值**：
>
>无

### 3、gpiohs_get_pin

>**描述**：获取GPIO的管脚值
>
>**函数原型**：
>
>```
>gpio_pin_value_t gpiohs_get_pin(uint8_t pin)
>```
>
>**参数**：
>
>无
>
>**返回值**：
>
>获取的GPIO管脚值

### 4、gpiohs_set_pin_edge

>**描述：**设置高速GPIO 中断触发模式
>
>**函数原型：**
>
>```
>void gpiohs_set_pin_edge(uint8_t pin, gpio_pin_edge_t edge)
>```
>
>**参数：**
>
>pin： GPIO 管脚 
>
>edge： 中断触发方式
>
>**返回值：**
>
>无

### 5、gpiohs_irq_register

>**描述：**设置高速GPIO 的中断回调函数
>
>**函数原型：**
>
>```
>void gpiohs_irq_register(uint8_t pin, uint32_t priority, plic_irq_callback_t callback, void *ctx);
>```
>
>**参数：**
>
>pin： GPIO 管脚
>
>priority： 中断优先级
>
>plic_irq_callback_t： 中断回调函数
>
>ctx: 	回调函数参数
>
>**返回值：**
>
>无

### 6、gpiohs_irq_unregister

>**描述：**注销GPIOHS 中断
>
>**函数原型：**
>
>```
>void gpiohs_irq_unregister(uint8_t pin)
>```
>
>**参数：**
>
>pin： GPIO 管脚
>
>**返回值：**
>
>无

## 数据类型

### 1、gpio_drive_mode_t

​	描述：GPIO的驱动模式

​    类型：

​			GPIO_DM_INPUT 	输入

​			GPIO_DM_INPUT_PULL_DOWN	输入下拉

​			GPIO_DM_INPUT_PULL_UP	输入上拉

​			GPIO_DM_OUTPUT	输出

### 2、gpio_pin_value_t

​	描述：GPIO值

​	类型：

​			GPIO_PV_LOW	低

​			GPIO_PV_HIGH	高

### 3、gpio_pin_edge_t

​	描述：高速GPIO 边沿触发模式

​	类型：

​			GPIO_PE_NONE 	不触发

​			GPIO_PE_FALLING 	下降沿触发

​			GPIO_PE_RISING 	上升沿触发

​			GPIO_PE_BOTH 	双沿触发

​			GPIO_PE_LOW 	低电平触发

​			GPIO_PE_HIGH	 高电平触发

## 参考例程

​		参考/src/gpiohs_io_key