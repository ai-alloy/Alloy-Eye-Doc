---
description:  实时时钟
---

## 功能描述

RTC 是用来计时的单元，设置时间后具备计时功能。RTC 模块仅当PLL0 使能, 并且CPU 频率大于30MHz 时使用。

* 获取当前日期时刻
* 设置当前日期时刻

## API说明

### 1、rtc_init

> **描述**：初始化RTC
>
> **函数原型**：
>
> ```
> int rtc_init(void)
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

### 2、rtc_timer_set

> **描述**：设置日期时间
>
> **函数原型**：
>
> ```
> int rtc_timer_set(int year, int month, int day, int hour, int minute, int second)
> ```
>
> **参数**：
>
> year：年（输入）
>
> month：月（输入）
>
> day：日（输入）
>
> hour：时（输入）
>
> minute：分（输入）
>
> second：秒（输入）
>
> **返回值**：
>
> 0	成功
>
> 非0	失败

### 3、rtc_timer_get

>**描述**：获取日期时间
>
>**函数原型**：
>
>```
>int rtc_timer_get(int *year, int *month, int *day, int *hour, int *minute, int *second)
>```
>
>**参数**：
>
>year：年（输出）
>
>month：月（输出）
>
>day：日（输出）
>
>hour：时（输出）
>
>minute：分（输出）
>
>second：秒（输出）
>
>**返回值**：
>
>0	成功
>
>非0	失败

## 参考例程

​		参考/src/rtc