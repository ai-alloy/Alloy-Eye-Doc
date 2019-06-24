---
description:  看门狗定时器
---

## 功能描述

WDT 提供系统出错或无响应时的恢复功能。

- 配置超时时间
- 手动重启计时

## API说明

### 1、wdt_init

> **描述**：配置参数，启动看门狗。不使用中断的话，将on_irq 设置为NULL
>
> **函数原型**：
>
> ```
> uint32_t wdt_init(wdt_device_number_t id, uint64_t time_out_ms, plic_irq_callback_t on_irq, void *ctx)
> ```
>
> **参数**：
>
> id： 看门狗编号（输入）
>
> time_out_ms： 超时时间（毫秒）（输入）
>
> on_irq： 中断回调函数输入（输入）
>
> ctx： 回调函数参数输入（输入）
>
> **返回值**：
>
> 看门狗超时重启的实际时间（毫秒）。与time_out_ms 有差异，一般情况会大于这个时间。在外部晶
> 振26M 的情况下，最大超时时间为330 毫秒

### 2、wdt_stop

>**描述**：设置定时间隔
>
>**函数原型**：
>
>```
>void wdt_stop(wdt_device_number_t id)
>```
>
>**参数**：
>
>id： 看门狗编号（输入）
>
>**返回值**：
>
>无

### 3、wdt_feed

>**描述**：喂狗
>
>**函数原型**：
>
>```
>void wdt_feed(wdt_device_number_t id)
>```
>
>**参数**：
>
>id： 看门狗编号（输入）
>
>**返回值**：
>
>无

### 4、wdt_clear_interrupt

>**描述：**清除中断。如果在中断函数中清除中断，则看门狗不会重启
>
>**函数原型：**
>
>```
>void wdt_clear_interrupt(wdt_device_number_t id)
>```
>
>**参数：**
>
>id： 看门狗编号（输入）
>
>**返回值：**
>
>无
>
>非0：失败

## 数据类型

###   wdt_device_number_t

​	描述：看门狗编号

​    类型：

​			WDT_DEVICE_0	看门狗0

​			WDT_DEVICE_1	看门狗1

## 参考例程

​		参考/src/watchdog

