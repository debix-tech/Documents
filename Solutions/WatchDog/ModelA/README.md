# 🐶 Watchdog 使用说明 - i.MX8M Plus 平台



📌 简介

i.MX8M Plus 内建的 Watchdog 模块（WDOG）用于监控系统运行状况。若系统在设定时间内未喂狗，Watchdog 将触发复位或中断，保障系统在异常状态下恢复。



📦 硬件资源

- **模块名**：`WDOG1`, `WDOG2`, `WDOG3`
- **IP 类型**：NXP Secure Watchdog（也叫 WDOGv4）
- **特性**：
  - 可配置超时时间
  - 可选择复位或中断响应
  - 支持 `Nowayout` 模式（不可关闭）
  - 支持低功耗模式



📁 驱动信息

```shell
drivers/watchdog/imx2_wdt.c
```

内核默认启用 `imx2_wdt` 驱动支持：

```makefile
CONFIG_IMX2_WDT=y
```





📂 设备节点

```shell
root@imx8mp-debix:/sys/class# ls /dev/watchdog
/dev/watchdog

```





⚙️ 基本用法（用户态）

直接执行提供的C文件之后，CTRL + C打断喂狗，10秒后系统重启：

```shell
root@imx8mp-debix:~# ./watchdogd 9 1
watchdogd started (interval 9 , margin 1
^C[  534.513846] watchdog: watchdog0: watchdog did not stop!

root@imx8mp-debix:~# 
U-Boot SPL 2023.04-00018-gcbcba604-dirty (Aug 09 2024 - 10:08:03 +0000)
DDRINFO: start DRAM init

```

