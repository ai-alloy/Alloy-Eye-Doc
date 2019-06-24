---
description:  脉冲宽度调制器
---

## 功能描述

PWM 用于控制脉冲输出的占空比。本质是一个硬件定时器，设置PWM 号与通道时不能与TIMER
定时器冲突。

* 配置PWM 输出频率
* 配置PWM 每个管脚的输出占空比

## API说明

### 1、pwm_init

> **描述**：初始化PWM
>
> **函数原型**：
>
> ```
> void pwm_init(pwm_device_number_t pwm_number)
> ```
>
> **参数**：
>
> pwm_number： PWM 号（输入）
>
> **返回值**：
>
> 无
>
> 非0	失败

### 2、pwm_set_enable

> **描述**：使能禁用PWM
>
> **函数原型**：
>
> ```
> void pwm_set_enable(pwm_device_number_t pwm_number, pwm_channel_number_t channel, int enable)
> ```
>
> **参数**：
>
> pwm_number： PWM 号（输入）
>
> channel： PWM 通道号（输入）
>
> enable：使能禁用PWM（输入）0：禁用 1：使能
>
> **返回值**：
>
> 无

### 3、pwm_set_frequency

>**描述**：设置频率及占空比
>
>**函数原型**：
>
>```
>double pwm_set_frequency(pwm_device_number_t pwm_number, pwm_channel_number_t channel, double frequency, double duty)
>```
>
>**参数**：
>
>pwm_number： PWM 号（输入）
>
>channel： PWM 通道号（输入）
>
>frequency： PWM 输出频率（输入）
>
>duty： 占空比输（输入）
>
>**返回值**：
>
>实际输出频率

## 数据类型

### 1、pwm_device_number_t

​	描述：PWM 号

​    类型：

​			PWM_DEVICE_0	PWM0

​			PWM_DEVICE_1	PWM1

​			PWM_DEVICE_2	PWM2

### 2、pwm_channel_number_t

​	描述：PWM 通道号

​	类型：

​			PWM_CHANNEL_0	PWM通道0

​			PWM_CHANNEL_1	PWM通道1

​			PWM_CHANNEL_2	PWM通道2

​			PWM_CHANNEL_3	PWM通道3

## 参考例程

​		参考/src/pwm