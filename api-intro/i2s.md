---
description:  音频总线
---

## 功能描述

I2S 标准总线定义了三种信号：时钟信号BCK、声道选择信号WS 和串行数据信号SD。一个基本的I2S 数据总线有一个主机和一个从机。主机和从机的角色在通信过程中保持不变。I2S 模块包含独立的发送和接收声道，能够保证优良的通信性能。

- 根据音频格式自动配置设备（支持16、24、32 位深，44100 采样率，1 - 4 声道）
- 可配置为播放或录音模式
- 自动管理音频缓冲区

## API说明

### 1、i2s_init

> **描述**：初始化I2S
>
> **函数原型**：
>
> ```
> void i2s_init(i2s_device_number_t device_num, i2s_transmit_t rxtx_mode, uint32_t channel_mask)
> ```
>
> **参数**：
>
> device_num： I2S 号（输入）
>
> rxtx_mode： 接收或发送模式（输入）
>
> channel_mask： 通道掩码（输入）
>
> **返回值**：
>
> 无

### 2、i2s_send_data_dma

>**描述**：I2S 发送数据
>
>**函数原型**：
>
>```
>void i2s_send_data_dma(i2s_device_number_t device_num, const void *buf, size_t buf_len, dmac_channel_number_t channel_num)
>```
>
>**参数**：
>
>device_num： I2S 号（输入）
>
>buf： 发送数据地址（输入）
>
>buf_len： 数据长度（输入）
>
>channel_num： DMA 通道号（输入）
>
>**返回值**：
>
>无
>
>小于0： 失败

### 3、i2s_receive_data_dma

>**描述**：I2S 接收数据
>
>**函数原型**：
>
>```
>void i2s_receive_data_dma(i2s_device_number_t device_num, uint32_t *buf, size_t buf_len, dmac_channel_number_t channel_num)
>```
>
>**参数**：
>
>device_num： I2S 号（输入）
>
>buf： 接收数据地址（输出）
>
>buf_len： 数据长度（输入）
>
>channel_num： DMA 通道号（输入）
>
>**返回值**：
>
>0： 成功
>
>非0：失败

### 4、i2s_rx_channel_config

>**描述：**设置接收通道参数。
>
>**函数原型：**
>
>```
>void i2s_rx_channel_config(i2s_device_number_t device_num,
>    i2s_channel_num_t channel_num,
>    i2s_word_length_t word_length,
>    i2s_word_select_cycles_t word_select_size,
>    i2s_fifo_threshold_t trigger_level,
>    i2s_work_mode_t word_mode)
>```
>
>**参数：**
>
>device_num： I2S 号（输入）
>
>channel_num： 通道号（输入）
>
>word_length： 接收数据位数（输出）
>
>word_select_size： 单个数据时钟数（输入）
>
>trigger_level： DMA触发时FIFO 深度（输入）
>
>word_mode： 工作模式（输入）
>
>**返回值：**
>
>无
>
>非0：失败

### 5、i2s_tx_channel_config

>**描述：**设置发送通道参数
>
>**函数原型：**
>
>```
>void i2s_tx_channel_config(i2s_device_number_t device_num,
>    i2s_channel_num_t channel_num,
>    i2s_word_length_t word_length,
>    i2s_word_select_cycles_t word_select_size,
>    i2s_fifo_threshold_t trigger_level,
>    i2s_work_mode_t word_mode)
>```
>
>**参数：**
>
>device_num： I2S 号（输入）
>
>channel_num： 通道号（输入）
>
>word_length： 接收数据位数（输出）
>
>word_select_size： 单个数据时钟数（输入）
>
>trigger_level： DMA 触发时FIFO 深度（输入）
>
>word_mode： 工作模式（输入）
>
>**返回值：**
>
>无
>
>非0：失败

### 6、i2s_play

>**描述：**发送PCM 数据, 比如播放音乐
>
>**函数原型：**
>
>```
>void i2s_play(i2s_device_number_t device_num, dmac_channel_number_t channel_num,
>const uint8_t *buf, size_t buf_len, size_t frame, size_t bits_per_sample, uint8_t track_num);
>```
>
>**参数：**
>
>device_num： I2S 号（输入）
>
>channel_num： 通道号（输入）
>
>buf： PCM 数据（输入）
>
>buf_len： PCM 数据长度（输入）
>
>frame： 单次发送数量（输入）
>
>bits_per_sample： 单次采样位宽（输入）
>
>track_num： 声道数（输入）
>
>**返回值：**
>
>无
>

### 7、i2s_set_sample_rate

>**描述：**设置采样率
>
>**函数原型：**
>
>```
>uint32_t i2s_set_sample_rate(i2s_device_number_t device_num, uint32_t sample_rate)
>```
>
>**参数：**
>
>device_num： I2S 号（输入）
>
>sample_rate：采样率号（输入）
>
>**返回值：**
>
>实际的采样率

### 8、i2s_set_dma_divide_16

>**描述：**设置dma_divide_16，16 位数据时设置dma_divide_16，DMA 传输时自动将32 比特INT32 数据分
>			成两个16 比特的左右声道数
>
>**函数原型：**
>
>```
>int i2s_set_dma_divide_16(i2s_device_number_t device_num, uint32_t enable)
>```
>
>**参数：**
>
>device_num： I2S 号（输入）
>
>enable：（输入） 0：禁用 1：使能
>
>**返回值：**
>
>0： 成功
>
>非0：失败

### 9、i2s_get_dma_divide_16

>**描述：**获取dma_divide_16 值。用于判断是否需要设置dma_divide_16
>
>**函数原型：**
>
>```
>int i2s_get_dma_divide_16(i2s_device_number_t device_num)
>```
>
>**参数：**
>
>device_num： I2S 号（输入）
>
>**返回值：**
>
>1： 使能
>0： 禁用
><0： 失败

### 10、fpioa_get_io_driving

## 数据类型

### 1、i2s_device_number_t

​	描述：I2S 编号

​    类型：

​			I2S_DEVICE_0： I2S 0

​			I2S_DEVICE_1： I2S 1

​			I2S_DEVICE_2： I2S 2

### 2、i2s_channel_num_t

​	描述：I2S 通道号

​	类型：

​			I2S_CHANNEL_0： I2S 通道0	

​			I2S_CHANNEL_1： I2S 通道1

​			I2S_CHANNEL_2： I2S 通道2

​			I2S_CHANNEL_3： I2S 通道3

### 3、i2s_transmit_t

​	描述：I2S 传输模式

​	类型：

​			I2S_TRANSMITTER： 发送模式

​			I2S_RECEIVER： 接收模式

### 4、i2s_work_mode_t

​	描述：I2S 工作模式

​	类型：

​			STANDARD_MODE：标准模式

​			RIGHT_JUSTIFYING_MODE： 右对齐模式		

​			LEFT_JUSTIFYING_MODE： 左对齐模式	

### 5、i2s_word_select_cycles_t

​		描述：I2S 单次传输时钟数

​		类型：

​				SCLK_CYCLES_16： 16 个时钟

​				SCLK_CYCLES_24： 24 个时钟

​				SCLK_CYCLES_32： 32 个时钟

### 6、i2s_word_length_t

​		描述：2S 传输数据位

​		类型：

​				IGNORE_WORD_LENGTH： 忽略长度

​				RESOLUTION_12_BIT：  12 位数据长度			

​				RESOLUTION_16_BIT：  16 位数据长度

​				RESOLUTION_20_BIT：  20 位数据长度

​				RESOLUTION_24_BIT：  24 位数据长度

​				RESOLUTION_32_BIT：  32 位数据长度

### 7、i2s_fifo_threshold_t

​		描述：I2S FIFO 深度

​		类型：

​				TRIGGER_LEVEL_1： 1 字节FIFO 深度

​				TRIGGER_LEVEL_2： 2 字节FIFO 深度

​				TRIGGER_LEVEL_3： 3 字节FIFO 深度

​				TRIGGER_LEVEL_4：4 字节FIFO 深度

​				TRIGGER_LEVEL_5： 5 字节FIFO 深度

​				TRIGGER_LEVEL_6： 6 字节FIFO 深度

​				TRIGGER_LEVEL_7： 7 字节FIFO 深度

​				TRIGGER_LEVEL_8： 8 字节FIFO 深度

​				TRIGGER_LEVEL_9： 9 字节FIFO 深度

​				TRIGGER_LEVEL_10： 10 字节FIFO 深度

​				TRIGGER_LEVEL_11： 11 字节FIFO 深度

​				TRIGGER_LEVEL_12： 12 字节FIFO 深度

​				TRIGGER_LEVEL_13： 13 字节FIFO 深度

​				TRIGGER_LEVEL_14： 14 字节FIFO 深度

​				TRIGGER_LEVEL_15： 15 字节FIFO 深度

​				TRIGGER_LEVEL_16： 16 字节FIFO 深度

## 参考例程

​		参考/src/mic_play、/src/play_pcm