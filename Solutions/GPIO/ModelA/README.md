# i.MX8MP GPIO 使用说明



## 📦 工具介绍

`libgpiod` 是 Linux GPIO 的新用户空间接口（代替传统 `/sys/class/gpio`），主要工具包括：

| 命令         | 功能说明                         |
| ------------ | -------------------------------- |
| `gpiodetect` | 列出系统中的 GPIO 控制器         |
| `gpioinfo`   | 显示某个 GPIO 控制器下的引脚信息 |
| `gpioget`    | 读取 GPIO 引脚电平               |
| `gpioset`    | 设置 GPIO 引脚电平               |
| `gpiomon`    | 监听 GPIO 边沿中断               |



📍 查看 GPIO 控制器

```shell
root@imx8mp-debix:~# gpiodetect 
gpiochip0 [30200000.gpio] (32 lines)
gpiochip1 [30210000.gpio] (32 lines)
gpiochip2 [30220000.gpio] (32 lines)
gpiochip3 [30230000.gpio] (32 lines)
gpiochip4 [30240000.gpio] (32 lines)
gpiochip5 [3-0020] (16 lines)
gpiochip6 [3-0023] (16 lines)

```

注意:这里需要在设备树或者手册中找到对应的地址，才能知道是哪个`gpiochipx`



设置IO高低电平

```shell
gpioset -c gpiochip0 22=1 高电平
gpioset -c gpiochip0 22=0 低电平
```



读取 GPIO 输入电平

```shell
gpioget gpiochip0 22
```

