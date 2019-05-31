# 通用输入/输出 (GPIO）

## 功能说明

系统支持8个通用GPIO ，均支持FPOTA方式将外设管脚映射到GPIO上。

- 可配置上下拉驱动模式
- 可配置输入输出信号
- 支持FPOTA映射功能

要使用GPIO功能，首先要FPOTA方式映射GPIO口，比如映射IO13（物理外设管脚）作为普通FUNC_GPIO0普通GPIO口，可以

```
fpioa_set_function(13, FUNC_GPIO0);
```

##API说明

### gpio_init

> 初始化 GPIO。

### gpio_deinit

> 释放GPIO资源。

##交流与答疑

欢迎交流,请访问`官网<[http://www.ai-alloy.com](http://www.ai-alloy.com/)>`_