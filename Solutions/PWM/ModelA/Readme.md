# 📘 README — 使用 i.MX8MP 上的 PWM 功能

## 📌 简介

本文档介绍如何在基于 **NXP i.MX8M Plus (imx8mp)** 的平台（如 DEBIX Model A）上启用并使用 **PWM（Pulse Width Modulation）**



## 1️⃣ 硬件说明

- SoC：NXP i.MX8M Plus
- 常用 PWM 控制器：`PWM1`, `PWM2`, `PWM3`, `PWM4`
- 具体复用请参考文档中的设备树



### 📋 DEBIX i.MX8MP PWM 设备树覆盖文件列表（按 PWM 控制器排序）

| PWM 控制器 | 覆盖文件名                     | 引脚名称   |
| ---------- | ------------------------------ | ---------- |
| **PWM1**   | `imx8mp-debix-pin23-PWM1.dtso` | I2C4_SDA   |
| **PWM2**   | `imx8mp-debix-pin21-PWM2.dtso` | I2C4_SCL   |
|            | `imx8mp-debix-pin29-PWM2.dtso` | GPIO1_IO11 |
|            | `imx8mp-debix-pin32-PWM2.dtso` | GPIO1_IO13 |
|            | `imx8mp-debix-pin36-PWM2.dtso` | SPDIF_RX   |
|            | `imx8mp-debix-pin38-PWM2.dtso` | SAI5_RXD0  |
| **PWM3**   | `imx8mp-debix-pin27-PWM3.dtso` | SAI5_RXC   |
|            | `imx8mp-debix-pin34-PWM3.dtso` | SPDIF_TX   |
| **PWM4**   | `imx8mp-debix-pin25-PWM4.dtso` | SAI5_RXFS  |





## 2️⃣ 用户空间控制

以 `pwmchip0` 的 `pwm0` 为例：

```shell
# 导出 PWM 通道
echo 0 | sudo tee /sys/class/pwm/pwmchip0/export

# 设置周期（单位：纳秒），如 20ms = 20000000ns
echo 20000000 | sudo tee /sys/class/pwm/pwmchip0/pwm0/period

# 设置占空比（如 50% = 10000000ns）
echo 10000000 | sudo tee /sys/class/pwm/pwmchip0/pwm0/duty_cycle

# 启动 PWM 输出
echo 1 | sudo tee /sys/class/pwm/pwmchip0/pwm0/enable

```

