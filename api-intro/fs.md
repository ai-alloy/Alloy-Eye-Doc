---
description:  Fat文件系统
---

## 功能描述

使用文件系统，可以方便的操作flash或外置TF卡，需要做持久化的信息或配置信息，将其保存为文件写入flash或TF卡即可。调用文件系统的api，把数据发送到文件系统，文件系统会决定擦除哪个分区以及存储到哪个分区。

文件系统操作flash时，注意可操作的空间大小（目前使用的16Mflash，后8M可用来供用户操作文件系统，前8M为系统使用）。

有兴趣了解更多可以参考：http://elm-chan.org/fsw/ff/00index_e.html

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
> **参数**：将文件系统对象注册/取消注册到FatFs模块
>
> fs： 指向要注册和清除的文件系统对象的指针。空指针取消注册已注册的文件系统对象
>
> path：  指向以null结尾的字符串的指针，该字符串指定逻辑驱动器。没有驱动器号的字符串表示默认驱动器
>
> opt：  安装选项。0：现在不安装（安装在第一次访问卷上），1：强制安装卷以检查它是否准备好工作
>
> **返回值**：
>
> FRESULT：返回状态
>


### 2、f_open

>**描述**：打开/创建文件
>
>**函数原型**：
>
>```
>FRESULT f_open (FIL* fp, const TCHAR* path, BYTE mode);
>```
>
>**参数**：
>
>fp：指向空白文件对象结构的指针
>
>path：指向以null结尾的字符串的指针，该字符串指定要打开或创建的[文件名]
>
>mode：模式标志，指定文件的访问类型和打开方法，它由以下标志的组合指定
>
>| 模式             | 含义                                                         |
>| ---------------- | ------------------------------------------------------------ |
>| FA_READ          | 指定对象的读访问权限。可以从文件中读取数据。                 |
>| FA_WRITE         | 指定对象的写访问权。数据可以写入文件。与`FA_READ`结合用于读写访问。 |
>| FA_OPEN_EXISTING | 打开文件。如果文件不存在，则函数将失败。（默认）             |
>| FA_CREATE_NEW    | 创建一个新文件。如果文件存在，则函数将失败并显示`FR_EXIST`。 |
>| FA_CREATE_ALWAYS | 创建一个新文件。如果文件存在，则会被截断并覆盖。             |
>| FA_OPEN_ALWAYS   | 如果文件存在，则打开该文件。如果没有，将创建一个新文件。     |
>| FA_OPEN_APPEND   | 与`FA_OPEN_ALWAYS`相同，但读/写指针设置为文件末尾。          |
>
>**返回值**：
>
>FRESULT：返回状态
>


### 3、f_close

>**描述**：关闭一个打开的文件
>
>**函数原型**：
>
>```
>FRESULT f_close (FIL* fp)
>```
>
>**参数**：
>
>fp：指向要关闭的打开文件对象结构的指针
>
>**返回值**：
>
>FRESULT：返回状态
>

### 4、f_read

>**描述：**从文件中读取数据
>
>**函数原型：**
>
>```
>FRESULT f_read (FIL* fp, void* buff, UINT btr, UINT* br)
>```
>
>**参数：**
>
>fp：指向打开文件对象的指针
>
>buff：指向缓冲区的指针，用于存储读取的数据
>
>btr：`UINT`类型范围内要读取的字节数
>
>br：指向接收读取的字节数的`UINT`变量的指针。无论函数返回代码如何，该值在函数调用后始终有效
>
>**返回值：**
>
>FRESULT：返回状态
>


### 5、f_write

>**描述：**将数据写入文件
>
>**函数原型：**
>
>```
>FRESULT f_write (FIL* fp, const void* buff, UINT btw, UINT* bw)
>```
>
>**参数：**
>
>fp：指向打开文件对象结构的指针
>
>buff：指向要写入的数据的指针
>
>btr：`指定要在`UINT类型范围内写入的字节数
>
>br：指向`UINT`变量的指针，该变量接收写入的字节数。无论函数返回代码如何，该值在函数调用后始终有效
>
>**返回值：**
>
>FRESULT：返回状态
>


### 6、f_lseek

>**描述：**移动打开文件对象的文件读/写指针
>
>**函数原型：**
>
>```
>FRESULT f_lseek (FIL* fp, FSIZE_t ofs)
>```
>
>**参数：**
>
>fp：指向打开文件对象的指针
>
>ofs：从文件顶部偏移字节以设置读/写指针。数据类型`FSIZE_t`是`DWORD`（32位）或`QWORD`（64位）的别名取决于配置选项`FF_FS_EXFAT`。
>
>**返回值：**
>
>FRESULT：返回状态
>


### 7、f_sync

>**描述：**函数刷新写入文件的缓存信息
>
>**函数原型：**
>
>```
>FRESULT f_sync (FIL* fp)
>```
>
>**参数：**
>
>fp：指向要刷新的打开文件对象的指针
>
>**返回值：**
>
>FRESULT：返回状态
>


### 8、f_opendir

>**描述：**打开一个目录
>
>**函数原型：**
>
>```
>FRESULT f_opendir (DIR* dp, const TCHAR* path)
>```
>
>**参数：**
>
>dp：指向空白目录对象的指针以创建新目录
>
>path：指向以null结尾的字符串的指针，该字符串指定要打开的[目录名称]
>
>**返回值：**
>
>FRESULT：返回状态
>

### 9、f_closedir

>**描述：**关闭一个打开的目录
>
>**函数原型：**
>
>```
>FRESULT f_closedir (DIR* dp)
>```
>
>**参数：**
>
>dp：指向要关闭的打开目录对象结构的指针
>
>**返回值：**
>
>FRESULT：返回状态
>


### 10、f_readdir

>**描述：**读取目录项
>
>**函数原型：**
>
>```
>FRESULT f_readdir (DIR* dp, FILINFO* fno)
>```
>
>**参数：**
>
>dp：指向打开目录对象的指针
>
>fno：指向文件信息结构的指针，用于存储有关读取项的信息。空指针会重新读取目录的读取索引
>
>**返回值：**
>
>FRESULT：返回状态
>

### 11、f_findfirst

>**描述**：打开一个目录并读取匹配的第一个项目
>
>**函数原型：**
>
>```
>FRESULT f_findfirst (DIR* dp, FILINFO* fno, const TCHAR* path, const TCHAR* pattern)
>```
>
>**参数**：
>
>dp：指向空白目录对象的指针
>
>fno：指向文件信息结构的指针，用于存储有关找到的项目的信息
>
>path：指向以null结尾的字符串的指针，该字符串指定要打开的目录名称
>
>pattern：指向以空字符结尾的字符串的指针，该字符串指定要搜索的名称匹配模式
>
>**返回值：**
>
>FRESULT：返回状态

### 12、f_findnext

>**描述**：读取下一个匹配的项目
>
>**函数原型：**
>
>```
>FRESULT f_findnext (DIR* dp, FILINFO* fno)
>```
>
>**参数**：
>
>dp：指向由`f_findfirst`函数创建的有效目录对象的指针
>
>fno：指向文件信息结构的指针，用于存储有关找到的目录项的信息
>
>**返回值：**
>
>FRESULT：返回状态

### 13、f_unlink

>**描述**：删除文件或子目录
>
>**函数原型：**
>
>```
>FRESULT f_unlink (const TCHAR* path)
>```
>
>**参数**：
>
>path：指向以null结尾的字符串的指针，该字符串指定要删除的文件或子目录
>
>**返回值**：
>
>FRESULT：返回状态

### 14、f_rename

>**描述**：重命名/移动文件或子目录
>
>**函数原型：**
>
>```
>FRESULT f_rename (const TCHAR* path_old, const TCHAR* path_new)
>```
>
>**参数**：
>
>path_old：指向以null结尾的字符串的指针，该字符串指定要重命名的现有文件或子目录
>
>path_new：指向以null结尾的字符串的指针，该字符串指定新的对象名称
>
>返回值：
>
>FRESULT：返回状态
>

### 15、f_stat

>**描述**：检查文件或子目录的存在
>
>**函数原型：**
>
>```
>FRESULT f_stat (const TCHAR* path, FILINFO* fno)
>```
>
>**参数**：
>
>path：指向以null结尾的字符串的指针，该字符串指定要获取其信息的对象。该对象不能是root direcotry。
>
>fno：指向空白`FILINFO`结构的指针，用于存储对象的信息。如果不需要，则设置空指针
>
>**返回值**：
>
>FRESULT：返回状态
>

### 16、f_chmod

>**描述**：更改文件或子目录的属性
>
>**函数原型：**
>
>```
>FRESULT f_chmod (const TCHAR* path, BYTE attr, BYTE mask)
>```
>
>**参数**：
>
>path：指向以null结尾的字符串的指针，该字符串指定要更改的对象
>
>attr：要在以下标志的一个或多个组合中设置的属性标志。指定的标志已设置，其他标志已清除，如下图标识
>
>| 属性   | 描述 |
>| ------ | ---- |
>| AM_RDO | 只读 |
>| AM_ARC | 档案 |
>| AM_SYS | 系统 |
>| AM_HID | 隐   |
>
>mask：属性掩码，指定要更改的属性。指定的属性已设置或清除，其他属性保持不变
>
>**返回值**：
>
>FRESULT：返回状态
>
## 数据类型

### 1、FRESULT

​	描述：返回状态

​	类型：

	FR_OK = 0,				/* (0) Succeeded */
	FR_DISK_ERR,			/* (1) A hard error occurred in the low level disk I/O layer */
	FR_INT_ERR,				/* (2) Assertion failed */
	FR_NOT_READY,			/* (3) The physical drive cannot work */
	FR_NO_FILE,				/* (4) Could not find the file */
	FR_NO_PATH,				/* (5) Could not find the path */
	FR_INVALID_NAME,		/* (6) The path name format is invalid */
	FR_DENIED,				/* (7) Access denied due to prohibited access or directory full */
	FR_EXIST,				/* (8) Access denied due to prohibited access */
	FR_INVALID_OBJECT,		/* (9) The file/directory object is invalid */
	FR_WRITE_PROTECTED,		/* (10) The physical drive is write protected */
	FR_INVALID_DRIVE,		/* (11) The logical drive number is invalid */
	FR_NOT_ENABLED,			/* (12) The volume has no work area */
	FR_NO_FILESYSTEM,		/* (13) There is no valid FAT volume */
	FR_MKFS_ABORTED,		/* (14) The f_mkfs() aborted due to any problem */
	FR_TIMEOUT,				/* (15) Could not get a grant to access the volume within defined period */
	FR_LOCKED,				/* (16) The operation is rejected according to the file sharing policy */
	FR_NOT_ENOUGH_CORE,		/* (17) LFN working buffer could not be allocated */
	FR_TOO_MANY_OPEN_FILES,	/* (18) Number of open files > _FS_LOCK */
	FR_INVALID_PARAMETER	/* (19) Given parameter is invalid */
## 参考例程

​		参考/src/fs