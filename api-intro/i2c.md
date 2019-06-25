---
description:  I2C总线集成
---

## 功能描述

I2C 总线用于和多个外部设备进行通信。多个外部设备可以共用一个I2C 总线。

- 独立的I2C 设备封装外设相关参数
- 自动处理多设备总线争用

## API说明

### 1、i2s_init

> **描述**：配置I²C 器件从地址、寄存器位宽度和I²C 速率
>
> **函数原型**：
>
> ```
> void i2c_init(i2c_device_number_t i2c_num, uint32_t slave_address, uint32_t address_width, uint32_t i2c_clk)
> ```
>
> **参数**：
>
> i2c_num： I²C 号（输入）
>
> slave_address： I²C 器件从地址（输入）
>
> address_width： I²C 器件寄存器宽度(7 或10) （输入）
>
> i2c_clk： I²C 速率(Hz) （输入）
>
> **返回值**：
>
> 无

### 2、i2c_init_as_slave

>**描述**：配置I²C 为从模式
>
>**函数原型**：
>
>```
>void i2c_init_as_slave(i2c_device_number_t i2c_num, uint32_t slave_address, uint32_t address_width, const i2c_slave_handler_t *handler)
>```
>
>**参数**：
>
>i2c_num： I²C 号（输入）
>
>slave_address： I²C 从模式的地址（输入）
>
>address_width： I²C 器件寄存器宽度(7 或10) （输入）
>
>handler： I²C 从模式的中断处理函数（输入）
>
>**返回值**：
>
>无
>

### 3、i2c_send_data

>**描述**：通过CPU 写数据
>
>**函数原型**：
>
>```
>int i2c_send_data(i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len)
>```
>
>**参数**：
>
>i2c_num： I²C 号（输入）
>
>send_buf： 待传输数据（输入）
>
>send_buf_len： 待传输数据长度（输入）
>
>**返回值**：
>
>0： 成功
>
>非0： 失败

### 4、i2c_send_data_dma

>**描述：**通过DMA 写数据
>
>**函数原型：**
>
>```
>void i2c_send_data_dma(dmac_channel_number_t dma_channel_num, i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len)
>    ```
>    
>    **参数：**
>    
>    dma_channel_num： 使用的dma 通道号（输入）
>
>i2c_num： I²C 号（输入）
>
>send_buf： 待传输数据（输入）
>
>send_buf_len： 待传输数据长度（输入）
>
>**返回值：**
>
>无
>

### 5、i2c_recv_data

>**描述：**通过CPU 读数据
>
>**函数原型：**
>
>```
>int i2c_recv_data(i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len, uint8_t *receive_buf, size_t receive_buf_len);
>    ```
>    
>    **参数：**
>    
>    i2c_num： I²C 总线号（输入）
>
>send_buf： 待传输数据（输入），一般情况是i2c 外设的寄存器，如果没有设置为NULL 
>
>send_buf_len： 待传输数据长度，如果没有则写0 （输入）
>
>receive_buf： 接收数据内存(输出)
>
>receive_buf_len： 接收数据的长度（输入）
>
>**返回值：**
>
>0： 成功
>
>非0： 失败

### 6、i2c_recv_data_dma

>**描述：**通过dma 读数据
>
>**函数原型：**
>
>```
>void i2c_recv_data_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num,i2c_device_number_t i2c_num, 
>const uint8_t *send_buf, size_t send_buf_len,uint8_t *receive_buf, size_t receive_buf_len);
>```
>
>**参数：**
>
>dma_send_channel_num： 发送数据使用的dma 通道（输入）
>
>dma_receive_channel_num： 接收数据使用的dma 通道（输入）
>
>i2c_num： I²C 总线号（输入）
>
>send_buf： 待传输数据（输入），一般情况是i2c 外设的寄存器，如果没有设置为NULL 
>
>send_buf_len： 待传输数据长度（输入），如果没有则写0 
>
>receive_buf： 接收数据内存（输出）
>
>receive_buf_len： 接收数据的长度（输入）
>
>**返回值**：
>
>无
>

## 数据类型

### 1、i2c_device_number_t

​	描述：i2c 编号

​    类型：

​			I2C_DEVICE_0： I2C 0

​			I2C _DEVICE_1： I2C 1

​			I2C _DEVICE_2： I2C 2

### 2、i2c_slave_handler_t

​	描述：i2c 从模式的中断处理函数句柄。根据不同的中断状态执行相应的函数操作

​	定义：

```
typedef struct _i2c_slave_handler
{
    void(*on_receive)(uint32_t data);
    uint32_t(*on_transmit)();
    void(*on_event)(i2c_event_t event);
} i2c_slave_handler_t;
```

## 参考例程

​		参考/src/lcd_ctp

