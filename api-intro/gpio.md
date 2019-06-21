# 通用GPIO

## 功能说明

系统支持8个通用GPIO ，均支持FPOTA方式将外设管脚映射到GPIO上。

* 可配置上下拉驱动模式
* 可配置输入输出信号
* 支持FPOTA映射功能

要使用GPIO功能，首先要FPOTA方式映射GPIO口，比如映射IO13（物理外设管脚）作为普通FUNC\_GPIO0普通GPIO口，可以

```text
fpioa_set_function(13, FUNC_GPIO0);
```

## API说明

### gpio\_init

> **描述**：初始化 GPIO
>
> **函数原型**： int gpio_init(void)
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

