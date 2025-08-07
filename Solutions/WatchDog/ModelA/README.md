# 🐶 Watchdog User Guide – i.MX8M Plus Platform

📌 **Overview**

The built-in Watchdog module (WDOG) in the i.MX8M Plus is used to monitor system health. If the system fails to "feed" the watchdog within a specified timeout, the watchdog will trigger a reset or interrupt to help the system recover from abnormal conditions.

---

📦 **Hardware Resources**

* **Module Names**: `WDOG1`, `WDOG2`, `WDOG3`
* **IP Type**: NXP Secure Watchdog (also called WDOGv4)
* **Features**:

  * Configurable timeout
  * Selectable response: reset or interrupt
  * Supports `Nowayout` mode (cannot be disabled)
  * Supports low power mode

---

📁 **Driver Information**

```shell
drivers/watchdog/imx2_wdt.c
```

The kernel enables the `imx2_wdt` driver by default:

```makefile
CONFIG_IMX2_WDT=y
```

---

📂 **Device Node**

```shell
root@imx8mp-debix:/sys/class# ls /dev/watchdog
/dev/watchdog
```

---

⚙️ **Basic Usage (User Space)**

After executing the provided C file, press CTRL + C to interrupt the feeding process. The system will reboot after 10 seconds:

```shell
root@imx8mp-debix:~# ./watchdogd 9 1
watchdogd started (interval 9 , margin 1)
^C[  534.513846] watchdog: watchdog0: watchdog did not stop!

root@imx8mp-debix:~# 
U-Boot SPL 2023.04-00018-gcbcba604-dirty (Aug 09 2024 - 10:08:03 +0000)
DDRINFO: start DRAM init
```
