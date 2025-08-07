# i.MX8MP GPIO Usage Guide

## 📦 Tool Introduction

`libgpiod` is the new user-space interface for GPIO in Linux, replacing the traditional `/sys/class/gpio`. The main tools include:

| Command      | Description                               |
| ------------ | ----------------------------------------- |
| `gpiodetect` | Lists the GPIO controllers in the system  |
| `gpioinfo`   | Displays pin information for a controller |
| `gpioget`    | Reads the logic level of a GPIO pin       |
| `gpioset`    | Sets the logic level of a GPIO pin        |
| `gpiomon`    | Monitors GPIO edge interrupts             |

---

📍 **Check GPIO Controllers**

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

*Note:* To identify which `gpiochipx` corresponds to a specific pin, refer to the device tree or hardware manual based on the GPIO base address.

---

### Set GPIO Output Level

```shell
gpioset -c gpiochip0 22=1   # Set high level
gpioset -c gpiochip0 22=0   # Set low level
```

---

### Read GPIO Input Level

```shell
gpioget gpiochip0 22
```
