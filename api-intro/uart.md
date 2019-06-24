---
description:  通用异步收发传输器
---

## 功能描述

嵌入式应用通常要求一个简单的并且占用系统资源少的方法来传输数据。通用异步收发传输器(UART)
即可以满足这些要求，它能够灵活地与外部设备进行全双工数据交换。

- 配置UART 参数
- 自动收取数据到缓冲区

## API说明

### 1、uart_init

> **描述**：初始化uart
>
> **函数原型**：
>
> ```
> void uart_init(uart_device_number_t channel)
> ```
>
> **参数**：
>
> channel： UART 号（输入）
>
> **返回值**：
>
> 无
>

### 2、uart_config

>**描述**：设置UART 相关参数
>
>**函数原型**：
>
>```
>void uart_config(uart_device_number_t channel, uint32_t baud_rate, uart_bitwidth_t data_width, uart_stopbit_t stopbit, uart_parity_t parity)
>```
>
>**参数**：
>
>channel： UART 号（输入）
>
>baud_rate： 波特率（输入）
>
>data_width： 数据位(5-8)（输入）
>
>stopbit： 停止位（输入）
>
>parity： 校验位（输入）
>
>**返回值**：
>
>无
>

### 3、uart_send_data

>**描述**：通过UART 发送数据
>
>**函数原型**：
>
>```
>int uart_send_data(uart_device_number_t channel, const char *buffer, size_t buf_len)
>```
>
>**参数**：
>
>channel： UART 编号（输入）
>
>buffer： 待发送数据（输入）
>
>buf_len： 待发送数据的长度（输入）
>
>**返回值**：
>
>已发送数据的长度

### 4、uart_send_data_dma

>**描述：**UART 通过DMA 发送数据，数据全部发送完毕后返回。
>
>**函数原型：**
>
>```
>void uart_send_data_dma(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel, const uint8_t *buffer, size_t buf_len)
>```
>
>**参数：**
>
>channel： UART 编号（输入）
>
>dmac_channel： DMA 通道输入（输入）
>
>buffer： 待发送数据（输入）
>
>buf_len： 待发送数据的长度（输入）
>
>**返回值：**
>
>无
>

### 5、uart_send_data_dma_irq

>**描述：**UART 通过DMA 发送数据，并设置DMA 发送完成中断函数，仅单次中断
>
>**函数原型：**
>
>```
>void uart_send_data_dma_irq(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel, const uint8_t *buffer, size_t buf_len, plic_irq_callback_t， uart_callback, void *ctx, uint32_t priority)
>```
>
>**参数：**
>
>channel： UART 编号（输入）
>
>dmac_channel： DMA 通道输入（输入）
>
>buffer： 待发送数据（输入）
>
>buf_len： 待发送数据的长度（输入）
>
>uart_callback： DMA 中断回调（输入）
>
>ctx： 中断函数参数（输入）
>
>priority:  中断优先级（输入）
>
>**返回值：**
>
>无

### 6、uart_receive_data

>**描述：**通过UART 读取数据
>
>**函数原型：**
>
>```
>int uart_receive_data(uart_device_number_t channel, char *buffer, size_t buf_len)
>```
>
>**参数：**
>
>channel： UART 编号（输入）
>
>buffer： 接收数据输（输出）
>
>buf_len： 接收数据的长度（输入）
>
>**返回值：**
>
>已接收到的数据长度

### 7、uart_receive_data_dma

>**描述：**UART 通过DMA 接收数据
>
>**函数原型：**
>
>```
>void uart_receive_data_dma(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel, uint8_t *buffer, size_t buf_len);
>
>```
>
>**参数：**
>
>channel： UART 编号（输入）
>
>dmac_channel： DMA 通道输入（输入）
>
>buffer：接收数据（输出）
>
>buf_len： 接收数据的长度（输入）
>
>**返回值：**
>
>0： 成功
>
>非0：失败

### 8、uart_receive_data_dma_irq

>**描述：**UART 通过DMA 接收数据，并注册DMA 接收完成中断函数，仅单次中断
>
>**函数原型：**
>
>```
>void uart_receive_data_dma_irq(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel,uint8_t *buffer, size_t buf_len, plic_irq_callback_t uart_callback, void *ctx, uint32_t priority)
>```
>
>**参数：**
>
>channel： UART 编号（输入）
>
>dmac_channel： DMA 通道输入（输入）
>
>buffer：接收数据（输出）
>
>buf_len： 接收数据的长度（输入）
>
>uart_callback： DMA 中断回调（输入）
>
>ctx： 中断函数参数（输入）
>
>priority:  中断优先级（输入）
>
>**返回值：**
>
>无 
>

### 9、uart_irq_register

>**描述：**注销UART 中断函数
>
>**函数原型：**
>
>```
>void uart_irq_register(uart_device_number_t channel, uart_interrupt_mode_t interrupt_mode, plic_irq_callback_t uart_callback, void *ctx, uint32_t priority)
>```
>
>**参数：**
>
>channel： UART编号（输入）
>
>interrupt_mode： 中断类型（输入）
>
>uart_callback： 中断回调（输入）
>
>ctx： 中断函数参数（输入）
>
>priority： 中断优先级（输入）
>
>**返回值：**
>
>无
>

### 10、uart_irq_unregister

>**描述：**注销UART 中断函数
>
>**函数原型：**
>
>```
>void uart_irq_unregister(uart_device_number_t channel, uart_interrupt_mode_t interrupt_mode)
>```
>
>**参数：**
>
>channel： UART编号（输入）
>
>interrupt_mode： 中断类型（输入）
>
>**返回值：**
>
>无
>

## 数据类型

### 1、uart_device_number_t

​	描述：UART 编号

​    类型：

​			UART_DEVICE_1：UART 1

​			UART_DEVICE_2： UART 2

​			UART_DEVICE_3： UART 3

### 2、uart_bitwidth_t

​	描述：UART 数据位宽

​	类型：

​			UARTBITWIDTH5BIT：5比特

​			UARTBITWIDTH6BIT：6比特

​			UARTBITWIDTH7BIT：7比特

​			UARTBITWIDTH8BIT：8比特

### 3、uart_stopbits_t

​	描述：UART 停止位

​	类型：

​			UART_PARITY_NONE： 无校验位

​			UART_PARITY_ODD： 奇校验

​			UART_PARITY_EVEN： 偶校验

### 4、uart_parity_t

​		描述：UART 校验位

​		类型：

​			UART_STOP_1： 1 个停止位

​			UART_STOP_1_5： 1.5 个停止位

​			UART_STOP_2： 2个停止位

### 5、uart_interrupt_mode_t

​		描述：UART 中断类型，接收或发送

​		类型：

​			UART_SEND： UART 发送

​			UART_RECEIVE： UART 接收

### 6、uart_send_trigger_t

​		描述：发送中断或DMA 触发FIFO 深度。当FIFO 中的数据小于等于该值时触发中断或DMA 传输。FIFO的深度					为16字节。

​		类型：

​			UART_SEND_FIFO_0： FIFO 为空

​			UART_SEND_FIFO_2： FIFO 剩余2 字节

​			UART_SEND_FIFO_4： FIFO 剩余4字节

​			UART_SEND_FIFO_8： FIFO 剩余8字节

### 7、uart_receive_trigger_t

​		描述：接收中断或DMA 触发FIFO 深度。当FIFO 中的数据小于等于该值时触发中断或DMA 传输。FIFO的深度					为16字节。

​		类型：

​			UART_RECEIVE_FIFO_0：FIFO 剩余1 字节

​			UART_RECEIVE_FIFO_2： FIFO 剩余2 字节

​			UART_RECEIVE_FIFO_4： FIFO 剩余4字节

​			UART_RECEIVE_FIFO_8： FIFO 剩余8字节

## 参考例程

​		参考/src/uart