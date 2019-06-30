---
description:  ST7789 SPI LCD Display
---

## 功能描述

DEMO使用ST7789作为LCD的驱动IC，通过SPI方式驱动LCD点屏，主控使用的I80接口8BIT MCU方式。

I80接口连线通常为：CS/，RS/(数据/指令选择），RD/，WR/，RST/，再就是数据线D0-D7了，ST7789的驱动可

以参考st7789.h。



## 主要函数

### 1、lcd_init

> **描述：**初始化lcd屏，主要是lcd的复位和屏寄存器的的初始化
>
> **函数原型：**
>
> ```
> void lcd_init(void)
> ```
>
> **参数：**
>
> 无
>
> **返回值：**
>
> 无

## **2、**lcd_set_direction

>**描述：**设置屏显方向
>
>**函数原型：**
>
>```
>void lcd_set_direction(lcd_dir_t dir)
>```
>
>**参数：**
>
>dir：屏显扫描方式（输入）
>
>**返回值：**
>
>无

### **3、**lcd_set_area

>**描述：**设置屏显区域
>
>**函数原型：**
>
>```
>void lcd_set_area(uint16_t x1, uint16_t y1, uint16_t x2, uint16_t y2)
>```
>
>**参数：**
>
>x1：屏显区域的起点x坐标（输入）
>
>y1：屏显区域的起点y坐标（输入）
>
>x2：屏显区域的终点x坐标（输入）
>
>y2：屏显区域的终点y坐标（输入）
>
>**返回值：**
>
>无

### **4、**lcd_draw_point

>**描述：**画点
>
>**函数原型：**
>
>```
>void lcd_draw_point(uint16_t x, uint16_t y, uint16_t color)
>```
>
>**参数：**
>
>x1：所画点的x坐标（输入）
>
>y1：所画点的要y坐标（输入）
>
>color：点的颜色（输入）
>
>**返回值：**
>
>无

### **5、**lcd_draw_char

>**描述：**显示字符
>
>**函数原型：**
>
>```
>void lcd_draw_char(uint16_t x, uint16_t y, char c, uint16_t color)
>```
>
>**参数：**
>
>x：字符的x坐标（输入）
>
>y：字符y坐标（输入）
>
>c：要显示的字符（输入）
>
>color：字符颜色（输入）
>
>**返回值：**
>
>无

### **6、**lcd_draw_string

>**描述：**显示字符串
>
>**函数原型：**
>
>```
>void lcd_draw_string(uint16_t x, uint16_t y, char *str, uint16_t color)
>```
>
>**参数：**
>
>x：字符串的x坐标（输入）
>
>y：字符串的y坐标（输入）
>
>str：要显示的字符串（输入）
>
>color：字符串的颜色（输入）
>
>**返回值：**
>
>无

### 7、lcd_clear

>**描述：**清屏
>
>**函数原型：**
>
>```
>void lcd_clear(uint16_t color)
>```
>
>**参数：**
>
>color：清屏显示的背景颜色（输入）
>
>**返回值：**
>
>无

### 8、lcd_draw_rectangle

>**描述：**画矩形框
>
>**函数原型：**
>
>```
>void lcd_draw_rectangle(uint16_t x1, uint16_t y1, uint16_t x2, uint16_t y2, uint16_t width, uint16_t color)
>```
>
>**参数：**
>
>x1：矩形框的起点x坐标（输入）
>
>y1：矩形框的起点y坐标（输入）
>
>x2：矩形框的终点x坐标（输入）
>
>y2：矩形框的终点y坐标（输入）
>
>width：矩形框的宽度（输入）
>
>color：矩形框的颜色（输入）
>
>**返回值：**
>
>无

### 9、lcd_draw_picture

>**描述：**填充指定区域
>
>**函数原型：**
>
>```
>void lcd_draw_picture(uint16_t x1, uint16_t y1, uint16_t width, uint16_t height, uint32_t *ptr)
>```
>
>**参数：**
>
>x1：填充区域的起点x坐标（输入）
>
>y1：填充区域的起点y坐标（输入）
>
>x2：填充区域的终点x坐标（输入）
>
>y2：填充区域的终点y坐标（输入）
>
>ptr：填充的数据指向的指针（输入）
>
>**返回值：**
>
>无

### 10、lcd_drawline

>**描述：**画线
>
>**函数原型：**
>
>```
>void lcd_drawline(uint16_t x1, uint16_t y1, uint16_t x2, uint16_t y2, uint16_t color)
>```
>
>**参数：**
>
>x1：线的起点x坐标（输入）
>
>y1：线的起点y坐标（输入）
>
>x2：线的终点x坐标（输入）
>
>y2：线的终点y坐标（输入）
>
>color：线的颜色（输入）
>
>**返回值：**
>
>无

### 11、lcd_draw_circle

>**描述：**画圆
>
>**函数原型：**
>
>```
>void lcd_draw_circle(uint16_t x0,uint16_t y0,uint8_t r,uint16_t color)
>```
>
>**参数：**
>
>x0：圆中心点的x坐标（输入）
>
>y0：圆中心点的y坐标（输入）
>
>r：半径（输入）
>
>color：线的颜色（输入）
>
>**返回值：**
>
>无

## 数据类型

### 1、lcd_dir_t

​	描述：屏显扫描方式

​	类型：

​			DIR_XY_RLUD = 0x00

​    		DIR_YX_RLUD = 0x20

   		 DIR_XY_LRUD = 0x40

​    		DIR_YX_LRUD = 0x60

   		 DIR_XY_RLDU = 0x80

  		  DIR_YX_RLDU = 0xA0

  		  DIR_XY_LRDU = 0xC0

 		   DIR_YX_LRDU = 0xE0

## 参考例程

​		参考/src/lcd