# 📘 README — Using PWM on i.MX8MP

## 📌 Introduction

This document explains how to enable and use **PWM (Pulse Width Modulation)** on platforms based on the **NXP i.MX8M Plus (imx8mp)** SoC, such as the DEBIX Model A.

## 1️⃣ Hardware Information

* SoC: NXP i.MX8M Plus
* Commonly used PWM controllers: `PWM1`, `PWM2`, `PWM3`, `PWM4`
* For specific pin multiplexing, please refer to the device tree documentation.

### 📋 DEBIX i.MX8MP PWM Device Tree Overlay Files (Sorted by PWM Controller)

| PWM Controller | Overlay File Name              | Pin Name    |
| -------------- | ------------------------------ | ----------- |
| **PWM1**       | `imx8mp-debix-pin23-PWM1.dtso` | I2C4\_SDA   |
| **PWM2**       | `imx8mp-debix-pin21-PWM2.dtso` | I2C4\_SCL   |
|                | `imx8mp-debix-pin29-PWM2.dtso` | GPIO1\_IO11 |
|                | `imx8mp-debix-pin32-PWM2.dtso` | GPIO1\_IO13 |
|                | `imx8mp-debix-pin36-PWM2.dtso` | SPDIF\_RX   |
|                | `imx8mp-debix-pin38-PWM2.dtso` | SAI5\_RXD0  |
| **PWM3**       | `imx8mp-debix-pin27-PWM3.dtso` | SAI5\_RXC   |
|                | `imx8mp-debix-pin34-PWM3.dtso` | SPDIF\_TX   |
| **PWM4**       | `imx8mp-debix-pin25-PWM4.dtso` | SAI5\_RXFS  |

## 2️⃣ User-Space Control

Take `pwm0` under `pwmchip0` as an example:

```shell
# Export the PWM channel
echo 0 | sudo tee /sys/class/pwm/pwmchip0/export

# Set the period (unit: nanoseconds), e.g., 20ms = 20000000ns
echo 20000000 | sudo tee /sys/class/pwm/pwmchip0/pwm0/period

# Set the duty cycle (e.g., 50% = 10000000ns)
echo 10000000 | sudo tee /sys/class/pwm/pwmchip0/pwm0/duty_cycle

# Enable PWM output
echo 1 | sudo tee /sys/class/pwm/pwmchip0/pwm0/enable
```

---
