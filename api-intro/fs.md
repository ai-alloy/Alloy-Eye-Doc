---
description:  Fat文件系统
---

## 功能描述

使用文件系统，可以方便的操作flash或外置TF卡，需要做持久化的信息或配置信息，将其保存为文件写入flash或TF卡即可。调用文件系统的api，把数据发送到文件系统，文件系统会决定擦除哪个分区以及存储到哪个分区。

文件系统操作flash时，注意可操作的空间大小（目前使用的16Mflash，后8M可用来供用户操作文件系统，前8M为系统使用）。

## API说明

### 1、f_mount

> **描述**：
>
> **函数原型**：
>
> ```
> FRESULT f_mount (FATFS* fs, const TCHAR* path, BYTE opt)
> ```
>
> **参数**：
>
> fs： Pointer to the file system object (NULL:unmount)
>
> path：  Logical drive number to be mounted/unmounted
>
> opt：  Mode option 0:Do not mount (delayed mount), 1:Mount immediately 
>
> **返回值**：
>
> 无
>


### 2、f_open

>**描述**：
>
>**函数原型**：
>
>```
>FRESULT f_open (FIL* fp, const TCHAR* path, BYTE mode);
>```
>
>**参数**：
>
>**返回值**：
>
>无
>


### 3、f_close

>**描述**：
>
>**函数原型**：
>
>```
>FRESULT f_close (FIL* fp)
>```
>
>**参数**：
>
>**返回值**：
>
>无
>

### 4、f_read

>**描述：**
>
>**函数原型：**
>
>```
>FRESULT f_read (FIL* fp, void* buff, UINT btr, UINT* br)
>```
>
>**参数：**
>
>**返回值：**
>
>无
>


### 5、f_write

>**描述：**
>
>**函数原型：**
>
>```
>FRESULT f_write (FIL* fp, const void* buff, UINT btw, UINT* bw)
>```
>
>**参数：**
>
>**返回值：**
>
>无
>


### 6、f_lseek

>**描述：**
>
>**函数原型：**
>
>```
>FRESULT f_lseek (FIL* fp, FSIZE_t ofs)
>```
>
>**参数：**
>
>**返回值：**
>
>无
>


### 7、f_sync

>**描述：**
>
>**函数原型：**
>
>```
>FRESULT f_sync (FIL* fp)
>```
>
>**参数：**
>
>**返回值：**
>
>无
>


### 8、f_opendir

>**描述：**
>
>**函数原型：**
>
>```
>FRESULT f_opendir (DIR* dp, const TCHAR* path)
>```
>
>**参数：**
>
>**返回值：**
>
>无
>

### 9、f_closedir

>**描述：**
>
>**函数原型：**
>
>```
>FRESULT f_closedir (DIR* dp)
>```
>
>**参数：**
>
>**返回值：**
>
>无
>


### 10、f_readdir

>**描述：**
>
>**函数原型：**
>
>```
>FRESULT f_readdir (DIR* dp, FILINFO* fno)
>     ```
>     
>     **参数：**
>     
>**返回值：**
>
>无
>

### 11、f_findfirst

>**描述**：
>
>**函数原型：**
>
>```
>FRESULT f_findfirst (DIR* dp, FILINFO* fno, const TCHAR* path, const TCHAR* pattern)
>```
>
>**参数**：
>
>**返回值：**
>
>无

### 12、f_findnext

>**描述**：
>
>**函数原型：**
>
>```
>FRESULT f_findnext (DIR* dp, FILINFO* fno)
>```
>
>**参数**：
>
>**返回值：**
>
>无

### 13、f_unlink

>**描述**：
>
>**函数原型：**
>
>```
>FRESULT f_unlink (const TCHAR* path)
>```
>
>**参数**：
>
>**返回值**：
>
>无

### 14、f_rename

>**描述**：
>
>**函数原型：**
>
>```
>FRESULT f_rename (const TCHAR* path_old, const TCHAR* path_new)
>```
>
>**参数**：
>
>**返回值**：
>
>无
>
### 15、f_stat

>**描述**：
>
>**函数原型：**
>
>```
>FRESULT f_stat (const TCHAR* path, FILINFO* fno)
>```
>
>**参数**：
>
>**返回值**：
>
>无
>
### 16、f_chmod

>**描述**：
>
>**函数原型：**
>
>```
>FRESULT f_chmod (const TCHAR* path, BYTE attr, BYTE mask)
>```
>
>**参数**：
>
>**返回值**：
>
>无
>
## 数据类型

## 参考例程

​		参考/src/fs