---
description:  Fat文件系统
---

## 功能描述

使用文件系统，可以方便的操作flash或外置TF卡，需要做持久化的信息或配置信息，将其保存为文件写入flash或TF卡即可。调用文件系统的api，把数据发送到文件系统，文件系统会决定擦除哪个分区以及存储到哪个分区。

文件系统操作flash时，注意可操作的空间大小（目前使用的16Mflash，后8M可用来供用户操作文件系统，前8M为系统使用）。

## API说明

### 1、spi_init

> **描述**：设置SPI 工作模式、多线模式和位宽
>
> **函数原型**：
>
> ```
> void spi_init(spi_device_num_t spi_num, spi_work_mode_t work_mode, spi_frame_format_t frame_format, size_t data_bit_length, uint32_t endian);
> ```
>
> **参数**：
>
> spi_num： SPI 号（输入）
> work_mode：  极性相位的四种模式（输入）
> frame_format：  多线模式（输入）
> data_bit_length：  单次传输的数据的位宽（输入）
> endian：  大小端（输入）0：小端 1：大端
>
> **返回值**：
>
> 无
>


### 2、spi_init_non_standard

>**描述**：多线模式下设置指令长度、地址长度、等待时钟数、指令地址传输模式
>
>**函数原型**：
>
>```
>void spi_init_non_standard(spi_device_num_t spi_num, uint32_t instruction_length, uint32_t address_length, uint32_t wait_cycles, spi_instruction_address_trans_mode_t instruction_address_trans_mode)
>```
>
>**参数**：
>
>spi_num： SPI 号（输入）
>
>instruction_length： 发送指令的位数（输入）
>
>address_length： 发送地址的位数（输入）
>
>wait_cycles： 等待时钟个数（输入）
>
>instruction_address_trans_mode： 指令地址传输的方式（输入）
>
>**返回值**：
>
>无
>


### 3、spi_send_data_standard

>**描述**：SPI 标准模式通过CPU传输数据
>
>**函数原型**：
>
>```
>void spi_send_data_standard(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff,size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
>```
>
>**参数**：
>
>spi_num： SPI 号（输入）
>
>chip_select： 片选信号（输入）
>
>cmd_buff： 外设指令地址数据（输入），没有则设为NULL 
>
>cmd_len： 外设指令地址数据长度（输入），没有则设为0 
>
>tx_buff： 发送的数据（输入）
>
>tx_len： 发送数据的长度（输入）
>
>**返回值**：
>
>无
>

### 4、spi_send_data_standard_dma

>**描述：**SPI 标准模式下使用DMA 传输数据
>
>**函数原型：**
>
>```
>void spi_send_data_standard_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num,spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len);
>```
>
>**参数：**
>
>channel_num： DMA 通道号（输入）
>
>spi_num： SPI 号（输入）
>
>chip_select： 片选信号（输入）
>
>cmd_buff： 外设指令地址数据，没有则设为NULL （输入）
>
>cmd_len： 外设指令地址数据长度，没有则设为0 （输入）
>
>tx_buff： 发送的数据（输入）
>
>tx_len： 发送数据的长度（输入）
>
>**返回值：**
>
>无
>


### 5、spi_receive_data_standard

>**描述：**标准模式下通过CPU接收数据。
>
>**函数原型：**
>
>```
>void spi_receive_data_standard(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff,size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
>```
>
>**参数：**
>
>spi_num： SPI 号（输入）
>
>chip_select： 片选信号（输入）
>
>cmd_buff： 外设指令地址数据（输入），没有则设为NULL 
>
>cmd_len： 外设指令地址数据长度（输入），没有则设为0 
>
>rx_buff： 接收的数据（输出）
>
>rx_len： 接收数据的长度（输入）
>
>**返回值：**
>
>无
>


### 6、spi_receive_data_standard_dma

>**描述：**标准模式下通过DMA 接收数据
>
>**函数原型：**
>
>```
>void spi_receive_data_standard_dma(dmac_channel_number_t dma_send_channel_num,
>	dmac_channel_number_t dma_receive_channel_num,spi_device_num_t spi_num, 		
>	spi_chip_select_t chip_select, const uint8_t *cmd_buff,
>	size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
>```
>
>**参数：**
>
>dma_send_channel_num： 发送指令地址使用的DMA 通道号（输入）
>
>dma_receive_channel_num： 接收数据使用的DMA 通道号（输入）
>
>spi_num： SPI 号（输入）
>
>chip_select： 片选信号（输入）
>
>cmd_buff： 外设指令地址数据（输入），没有则设为NULL 
>
>cmd_len： 外设指令地址数据长度（输入），没有则设为0 
>
>rx_buff： 接收的数据（输出）
>
>rx_len： 接收数据的长度（输入）
>
>**返回值：**
>
>无
>


### 7、spi_send_data_multiple

>**描述：**多线模式发送数据
>
>**函数原型：**
>
>```
>void spi_send_data_multiple(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff,size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
>```
>
>**参数：**
>
>spi_num： SPI 号（输入）
>
>chip_select： 片选信号（输入）
>
>cmd_buff： 外设指令地址数据（输入），没有则设为NULL
>
>cmd_len： 外设指令地址数据长度（输入），没有则设为0 
>
>tx_buff： 发送的数据（输入）
>
>tx_len： 发送数据的长度（输入）
>
>**返回值：**
>
>无
>


### 8、spi_send_data_multiple_dma

>**描述：**多线模式使用DMA 发送数据
>
>**函数原型：**
>
>```
>void spi_send_data_multiple_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num,spi_chip_select_t chip_select,const uint32_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
>```
>
>**参数：**
>
>channel_num： DMA 通道号（输入）
>
>spi_num： SPI 号（输入）
>
>chip_selec：t 片选信号（输入）
>
>cmd_buff： 外设指令地址数据（输入），没有则设为NULL 
>
>cmd_len： 外设指令地址数据长度（输入），没有则设为0 
>
>tx_buff： 发送的数据（输入）
>
>tx_len： 发送数据的长度（输入）
>
>**返回值：**
>
>无
>

### 9、spi_receive_data_multiple

>**描述：**多线模式接收数据
>
>**函数原型：**
>
>```
>void spi_receive_data_multiple(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff,size_t cmd_len, uint8_t *rx_buff, size_t rx_len);
>```
>
>**参数：**
>
>spi_num：  SPI 号（输入）
>
>chip_select：  片选信号（输入）
>
>cmd_buff：  外设指令地址数据（输入），没有则设为NULL 
>
>cmd_len：  外设指令地址数据长度（输入），没有则设为0 
>
>rx_buff：  接收的数据（输出）
>
>rx_len：  接收数据的长度（输入）
>
>**返回值：**
>
>无
>


### 10、spi_receive_data_multiple_dma

>**描述：**多线模式通过DMA 接收
>
>**函数原型：**
>
>```
>void spi_receive_data_multiple_dma(dmac_channel_number_t dma_send_channel_num,
>                                   dmac_channel_number_t dma_receive_channel_num,
>                                   spi_device_num_t spi_num, spi_chip_select_t 	
>                                   chip_select, const uint32_t *cmd_buff,
>                                   size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
>```
>
>**参数：**
>
>dma_send_channel_num：  发送指令地址使用的DMA 通道号（输入）
>
>dma_receive_channel_num：  接收数据使用的DMA 通道号（输入）
>
>spi_num：  SPI 号（输入）
>
>chip_select：  片选信号（输入）
>
>cmd_buff：  外设指令地址数据（输入），没有则设为NULL 
>
>cmd_len：  外设指令地址数据长度（输入），没有则设为0 
>
>rx_buff：  接收的数据（输出）
>
>rx_len：  接收数据的长度（输入）
>
>**返回值：**
>
>无
>

### 11、spi_fill_data_dma

>**描述**：多线模式通过DMA 接收
>
>**函数原型：**
>
>```
>void spi_fill_data_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num, 
>spi_chip_select_t chip_select, const uint32_t *tx_buff, size_t tx_len)
>```
>
>**参数**：
>
>channel_num：  DMA 通道号（输入）
>
>spi_num：  SPI 号（输入）
>
>chip_select：  片选信号（输入）
>
>tx_buff：  发送的数据, 仅发送tx_buff 这一个数据，不会自动增加（输入）
>
>tx_len：  发送数据的长度（输入）
>
>**返回值：**
>
>无

### 12、spi_send_data_normal_dma

>**描述**：通过DMA 发送数据。不用设置指令地址。
>
>**函数原型：**
>
>```
>void spi_send_data_normal_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num,spi_chip_select_t chip_select,const void *tx_buff, size_t tx_len, spi_transfer_width_t spi_transfer_width)
>```
>
>**参数**：
>
>channel_num：  DMA 通道号（输入）
>
>spi_num：  SPI 号（输入）
>
>chip_select：  片选信号（输入）
>
>tx_buff：  发送的数据, 仅发送tx_buff 这一个数据，不会自动增加（输入）
>
>tx_len：  发送数据的长度（输入）
>
>spi_transfer_width：  发送数据的位宽（输入）
>
>**返回值：**
>
>无

### 13、spi_set_clk_rate

>**描述**：设置SPI 的时钟频率
>
>**函数原型：**
>
>```
>uint32_t spi_set_clk_rate(spi_device_num_t spi_num, uint32_t spi_clk)
>```
>
>**参数**：
>
>spi_num： SPI 号（输入）
>
>spi_clk： 目标SPI 设备的时钟频率（输入）
>
>**返回值**：
>
>设置完后的SPI 设备的时钟频率

## 数据类型

## 参考例程

​		参考/src/fs