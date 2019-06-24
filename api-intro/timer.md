---
description:  硬件定时器
---

## 功能描述

芯片有3 个定时器，每个定时器有4 路通道，可以配置为PWM。

- 启用或禁用定时器
- 配置定时器触发间隔
- 配置定时器触发处理程序

## API说明

### 1、timer_init

> **描述**：初始化定时器
>
> **函数原型**：
>
> ```
> void timer_init(timer_device_number_t timer_number)
> ```
>
> **参数**：
>
> timer_number： 定时器号（输入）
>
> **返回值**：
>
> 无
>
> 非0： 失败

### 2、timer_set_interval

>**描述**：设置定时间隔
>
>**函数原型**：
>
>```
>size_t timer_set_interval(timer_device_number_t timer_number, timer_channel_number_t channel, size_t nanoseconds)
>```
>
>**参数**：
>
>timer_number： 定时器号（输入）
>
>channel： 定时器通道号（输入）
>
>nanoseconds：时间间隔（纳秒）（输入）
>
>**返回值**：
>
>实际的触发间隔（纳秒）

### 3、timer_set_enable

>**描述**：使能禁用定时器
>
>**函数原型**：
>
>```
>void timer_set_enable(timer_device_number_t timer_number, timer_channel_number_t channel, uint32_t enable)
>```
>
>**参数**：
>
>timer_number： 定时器号（输入）
>
>channel： 定时器通道号（输入）
>
>enable： 使能禁用定时器（输入）0：禁用 1：使能
>
>**返回值**：
>
>0： 成功
>
>非0：失败

### 4、timer_irq_register

>**描述：**注册定时器触发中断回调函数
>
>**函数原型：**
>
>```
>int timer_irq_register(timer_device_number_t device, timer_channel_number_t channel, int is_single_shot, uint32_t priority, timer_callback_t callback, void *ctx);
>```
>
>**参数：**
>
>timer_number： 定时器号（输入）
>
>channel： 定时器通道号（输入）
>
>is_single_shot： 是否单次中断（输入）
>
>priority： 中断优先级（输入）
>
>callback：中断回调函数（输入）
>
>ctx： 回调函数参数（输入）
>
>**返回值：**
>
>0： 成功
>
>非0：失败

### 5、timer_irq_unregister

>**描述：**注销定时器中断函数
>
>**函数原型：**
>
>```
>int timer_irq_unregister(timer_device_number_t device, timer_channel_number_t channel);
>```
>
>**参数：**
>
>timer_number： 定时器号（输入）
>
>channel： 定时器通道号（输入）
>
>**返回值：**
>
>0： 成功
>
>非0：失败

## 数据类型

### 1、timer_device_number_t

​	描述：定时器编号

​    类型：

​			TIMER_DEVICE_0 	定时器 0

​			TIMER_DEVICE_1 	定时器 1

​			TIMER_DEVICE_2 	定时器 2

### 2、timer_channel_number_t

​	描述：定时器通道号

​	类型：

​			TIMER_CHANNEL_0 	定时器通道 0

​			TIMER_CHANNEL_1 	定时器通道 1

​			TIMER_CHANNEL_2 	定时器通道 2

​			TIMER_CHANNEL_3 	定时器通道 3

### 3、timer_callback_t

​	描述：定时器回调函数

​	定义：

```
typedef int (*timer_callback_t)(void *ctx)
```

## 参考例程

​		参考/src/timer

