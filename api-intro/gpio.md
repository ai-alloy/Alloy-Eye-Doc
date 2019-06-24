---
description:  通用输入/输出(GPIO)
---

## 功能说明

系统支持8个通用GPIO，均支持FPOTA方式将外设管脚映射到GPIO上。

* 可配置上下拉驱动模式
* 可配置输入输出信号
* 支持FPOTA映射功能

要使用GPIO功能，首先要FPOTA方式映射GPIO口，比如映射IO13（物理外设管脚）作为普通FUNC\_GPIO0普通GPIO口，可以

```text
fpioa_set_function(13, FUNC_GPIO0);
```

## API说明

### 1、gpio\_init

> **描述**：初始化 GPIO
>
> **函数原型**：
>
> ```
> int gpio_init(void)
> ```
>
> **参数**：
>
> 无
>
> **返回值**：
>
> 0	成功
>
> 非0	失败

### 2、gpio_set_drive_mode

> **描述**：设置GPIO驱动模式
>
> **函数原型**：
>
> ```
> void gpio_set_drive_mode(uint8_t pin, gpio_drive_mode_t mode)
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

### 3、gpio_set_pin

>**描述**：设置GPIO的管脚值
>
>**函数原型**：
>
>```
>void gpio_set_pin(uint8_t pin, gpio_pin_value_t value)
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

### 4、gpio_get_pin

>**描述**：获取GPIO的管脚值
>
>**函数原型**：
>
>```
>gpio_pin_value_t gpio_get_pin(uint8_t pin)
>```
>
>**参数**：
>
>无
>
>**返回值**：
>
>获取的GPIO管脚值

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

## 参考例程

​		参考/src/gpio_led